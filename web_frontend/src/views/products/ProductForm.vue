<template>
   <div class="container">
     <div class="product-info">
       <div class="pricing-header px-3 py-3 pr-3 mx-auto text-center">
         <router-link to="/adminpage" class="btn btn-info button-add">
           <i class="fa-solid fa-circle-left"></i> Quay lại
         </router-link>
       </div>
 
       <div class="container">
         <form @submit.prevent="save()" class="needs-validation" novalidate>
           <div class="form-group row">
             <label for="productName" class="col-sm-3 col-form-label"><b>Tên sản phẩm</b></label>
             <div class="col-sm-9">
               <input
                 type="text"
                 class="form-control"
                 id="productName"
                 v-model="product.name"
                 :class="{ 'is-invalid': errors.name }"
                 required
               />
               <div class="invalid-feedback" v-if="errors.name">
                 {{ errors.name }}
               </div>
             </div>
           </div>
 
           <div class="form-group row">
             <label for="productImgUrl" class="col-sm-3 col-form-label"><b>Hình ảnh</b></label>
             <div class="col-sm-9">
               <input
                 type="text"
                 class="form-control"
                 id="productImgUrl"
                 v-model="product.imgUrl"
                 :class="{ 'is-invalid': errors.imgUrl }"
                 required
               />
               <div class="invalid-feedback" v-if="errors.imgUrl">
                 {{ errors.imgUrl }}
               </div>
             </div>
           </div>
 
           <div class="form-group row">
             <label for="productPrice" class="col-sm-3 col-form-label"><b>Giá sản phẩm</b></label>
             <div class="col-sm-9">
               <input
                 type="text"
                 class="form-control"
                 id="productPrice"
                 v-model="product.price"
                 :class="{ 'is-invalid': errors.price }"
                 required
               />
               <div class="invalid-feedback" v-if="errors.price">
                 {{ errors.price }}
               </div>
             </div>
           </div>
 
           <div class="form-group row">
             <label for="productDescription" class="col-sm-3 col-form-label"><b>Mô tả sản phẩm</b></label>
             <div class="col-sm-9">
               <textarea
                 class="form-control"
                 id="productDescription"
                 rows="3"
                 v-model="product.description"
                 :class="{ 'is-invalid': errors.description }"
                 required
               ></textarea>
               <div class="invalid-feedback" v-if="errors.description">
                 {{ errors.description }}
               </div>
             </div>
           </div>
 
           <div class="form-group row">
             <label class="col-sm-3 col-form-label"></label>
             <div class="col-sm-9">
               <button type="submit" class="btn btn-primary">Lưu</button>
               <button type="reset" class="btn btn-danger">Xoá</button>
             </div>
           </div>
         </form>
       </div>
     </div>
   </div>
 </template>
 
 <script>
 import ProductService from "../../services/product.service";
 
 export default {
   data() {
     return {
       errors: {
         name: "",
         imgUrl: "",
         price: "",
         description: "",
       },
       product: {
         name: "",
         imgUrl: "",
         price: "",
         description: "",
       },
     };
   },
   methods: {
     validate() {
       this.errors = {
         name: "",
         imgUrl: "",
         price: "",
         description: "",
       };
 
       let isValid = true;
 
       if (!this.product.name) {
         this.errors.name = "Tên sản phẩm là bắt buộc";
         isValid = false;
       }
 
       if (!this.product.imgUrl) {
         this.errors.imgUrl = "Hình ảnh sản phẩm là bắt buộc";
         isValid = false;
       }
 
       if (!this.product.price) {
         this.errors.price = "Giá sản phẩm là bắt buộc";
         isValid = false;
       } else if (!this.isNumber(this.product.price)) {
         this.errors.price = "Giá sản phẩm phải là số";
         isValid = false;
       }
 
       if (!this.product.description) {
         this.errors.description = "Mô tả sản phẩm là bắt buộc";
         isValid = false;
       }
 
       return isValid;
     },
     isNumber(value) {
       return /^\d*$/.test(value);
     },
     async save() {
       if (this.validate()) {
         try {
           if (this.$route.params.id) {
             await ProductService.update(this.$route.params.id, this.product);
             this.$router.push({ name: "admin" });
           } else {
             await ProductService.create(this.product);
             this.$router.push({ name: "admin" });
           }
         } catch (error) {
           console.log(error);
         }
       }
     },
     async getProduct(productId) {
       try {
         this.product = await ProductService.get(productId);
       } catch (error) {
         console.log(error);
       }
     },
   },
   created() {
     let productId = this.$route.params.id;
     if (productId) {
       this.getProduct(productId);
     }
   },
 };
 </script>

 <style scoped>
 .container {
   background-color: #1272d1;
   background-image: url('https://static.vecteezy.com/system/resources/thumbnails/002/007/957/original/white-music-note-background-free-video.jpg'); /* Đặt đường dẫn đến hình nền của bạn */
   background-size: cover;
   background-position: center;
   padding-bottom: 50px;
   margin-top: 20px;
   border: 2px solid #030202; /* Thêm viền cho container */
   border-radius: 10px; /* Bo tròn góc cho container */
 }
 
 .button-add {
   color: #fff;
 }
 
 .form-group {
   margin-bottom: 20px;
 }
 
 .invalid-feedback {
   color: #dc3545;
 }
 
 .btn-primary {
   background-color: #00ff15;
   border-color: #00ff37;
 }
 
 .btn-primary:hover {
   background-color: #0056b3;
   border-color: #0056b3;
 }
 
 .btn-danger {
   background-color: #dc3545;
   border-color: #dc3545;
 }
 
 .btn-danger:hover {
   background-color: #bd2130;
   border-color: #bd2130;
 }
 </style>