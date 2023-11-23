<template>
   <div class="row">
      <!-- Hình ảnh thứ nhất -->
      <div class="product-grid col">
         <div class="thumb">
            <div class="image">
               <img
                  src="https://kenhz.net/wp-content/uploads/2021/01/cua-hang-guitar-ba-don-tphcm.jpg"
                  alt="https://kenhz.net/wp-content/uploads/2021/01/cua-hang-guitar-ba-don-tphcm.jpg"
                  style="width: 86%; height: auto;">
            </div>
         </div>
      </div>

      <!-- Hình ảnh thứ hai -->
      <div class="product-grid col">
         <div class="thumb">
            <div class="image">
               <img
                  src="https://amnhacvietthanh.vn/wp-content/uploads/2021/03/phan-biet-cac-loai-dan-guitar-acoustic.jpg"
                  alt="https://amnhacvietthanh.vn/wp-content/uploads/2021/03/phan-biet-cac-loai-dan-guitar-acoustic.jpg"
                  style="width: 102%; height: auto;">
            </div>
         </div>
      </div>

      <!-- Hình ảnh thứ ba -->
      <div class="product-grid col">
         <div class="thumb">
            <div class="image">
               <img
                  src="https://top10tphcm.com/wp-content/uploads/2021/07/mua-ban-dan-Guitar-cu-moi-TPHCM.jpg"
                  alt="https://top10tphcm.com/wp-content/uploads/2021/07/mua-ban-dan-Guitar-cu-moi-TPHCM.jpg"
                  style="width: 96%; height: auto;">
            </div>
         </div>
      </div>
   </div>
</template>





<script>
import ProductService from "../services/product.service";

export default {
   data() {
      return {
         products: [],
         searchText: "",
      };
   },

   computed: {
      productStrings() {
         return this.products.map((product) => {
            const { name, description } = product;
            return [name, description].join("");
         });
      },
      filteredProducts() {
         if (!this.searchText) return this.products;
         return this.products.filter((_product, index) =>
            this.productStrings[index].includes(this.searchText)
         );
      },
      filteredProductsCount() {
         return this.filteredProducts.length;
      },
   },
   methods: {
      async getAllProduct() {
         try {
            this.products = await ProductService.getAll();
         } catch (error) {
            console.log(error);
         }
      },
      async addProductToCart(index) {
         const saveLocalCart = JSON.parse(
            localStorage.getItem("localProductCart") ?? "[]"
         );
         for (const item of saveLocalCart) {
            if (item.id === this.products[index]._id) {
               item.amount++;
               const localProductCart = JSON.stringify(saveLocalCart);
               localStorage.setItem("localProductCart", localProductCart);
               alert(
                  `Số lượng sản phẩm ${this.products[index].name} đã được cập nhật`
               );
               return;
            }
         }
         const temp = {
            id: this.products[index]._id,
            name: this.products[index].name,
            imgUrl: this.products[index].imgUrl,
            price: this.products[index].price,
            description: this.products[index].description,
            amount: 1,
         };
         saveLocalCart.push(temp);
         const localProductCart = JSON.stringify(saveLocalCart);
         localStorage.setItem("localProductCart", localProductCart);
         alert(
            `Sản phẩm ${this.products[index].name} vừa được thêm vào giỏ hàng`
         );
      },
   },

   created() {
      this.getAllProduct();
   },
};
</script>

<style scoped>
.row {

  
  padding :30px 0px 0px 0px;
  max-width: 100%;

}


#content {
   min-height: 400x;
}

.product-category {
   padding-top: 0px;
}

.product-name p {
   color: red;
}

.header-content {
   display: flex;
   border-bottom: 3px solid #eee;
   font-weight: normal;
   font-size: 22px;
}

.search-btn {
   margin-left: 550px;
   padding-bottom: 5px;
}

.non-product {
   margin-left: 450px;
   margin-top: 15px;
   font-size: 20px;
   font-weight: bold;
   color: blue;
}

.product-grid {
   height: 180px;
   position: relative;
   text-align: center;
   vertical-align: top;
   padding: 7px;
   margin-bottom: 15px;
   border: 3px solid transparent;
}

.product-grid .thumb img {
   object-fit: cover;
   height: 150px;
   box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.product-grid .thumb .caption h4 a {
   font-size: 13px;
   line-height: 22px;
   text-decoration: none;
   padding: 5px;
   color: #333;
   margin: 0 auto;
   width: 100%;
   overflow: hidden;
   text-overflow: ellipsis;
   -webkit-line-clamp: 2;
   display: -webkit-box;
   -webkit-box-orient: vertical;
}

.product-grid:hover {
   transform: scale(1.2);
}

.price {
   color: #ff0000;
   font-weight: bold;
}

.btn-primary {
   background-color: #3e7cb4;
}

.botton-cart {
   position: absolute;
   bottom: 0;
   left: calc(50% - 55px);
}

.btn-cart {
   background-color: #3e7cb4;
   color: #fff;
   border-radius: 3px;
}

.btn-cart:hover {
   background-color: #1760a0;
}</style>
