<template>
   <div class="login-container">
     <div class="d-flex justify-content-center align-items-center">
       <div class="card shadow p-3 mb-5 bg-body rounded">
         <div class="card-body">
           <h3 class="card-title text-center mb-4"><b>Đăng nhập Admin</b></h3>
           <form @submit.prevent="login()" class="needs-validation">
             <div class="mb-3">
               <label for="email" class="form-label">Email</label>
               <div class="input-group">
                 <span class="input-group-text"><i class="fa-solid fa-envelope"></i></span>
                 <input
                   type="email"
                   class="form-control"
                   id="email"
                   placeholder="Nhập địa chỉ email"
                   v-model="user.email"
                   @blur="validate()"
                   :class="{ 'is-invalid': errors.email }"
                   required
                 />
                 <div class="invalid-feedback" v-if="errors.email">
                   {{ errors.email }}
                 </div>
               </div>
             </div>
             <div class="mb-3">
               <label for="password" class="form-label">Mật khẩu</label>
               <div class="input-group">
                 <span class="input-group-text"><i class="fas fa-key"></i></span>
                 <input
                   type="password"
                   class="form-control"
                   id="password"
                   placeholder="Nhập mật khẩu"
                   v-model="user.password"
                   @blur="validate()"
                   :class="{ 'is-invalid': errors.password }"
                   required
                 />
                 <div class="invalid-feedback" v-if="errors.password">
                   {{ errors.password }}
                 </div>
               </div>
             </div>
             <div class="d-grid">
               <button type="submit" class="btn btn-success">Đăng nhập</button>
             </div>
           </form>
         </div>
         <div class="card-footer text-center">
           <p class="mb-0">
             Nếu bạn chưa có tài khoản!
             <router-link to="/register"><b>Đăng ký</b></router-link>
           </p>
         </div>
       </div>
     </div>
   </div>
 </template>
 
 <script>
 import UserService from "../services/user.service";
 
 export default {
   data() {
     return {
       errors: {
         email: "",
         password: "",
       },
       user: {
         email: "",
         password: "",
       },
     };
   },
   methods: {
     validate() {
       let isValid = true;
 
       this.errors = {
         email: "",
         password: "",
       };
 
       if (!this.user.email) {
         this.errors.email = "Email là bắt buộc";
         isValid = false;
       }
 
       if (!this.user.password) {
         this.errors.password = "Mật khẩu là bắt buộc";
         isValid = false;
       }
       return isValid;
     },
     async login() {
       if (this.validate()) {
         const userLogin = await UserService.login(this.user);
         const localUserLogin = JSON.stringify(userLogin);
         localStorage.setItem("localUserLogin", localUserLogin);
 
         if (userLogin.role === "admin") {
           this.$router.push({ name: "admin" });
         } else {
           alert("Xin lỗi! Bạn không phải là admin");
         }
       }
     },
   },
 };
 </script>
 
 <style scoped>
 .login-container {
   display: flex;
   justify-content: center;
   align-items: center;
   height: 100vh;
   background-image: url('https://img.freepik.com/premium-vector/guitar-doodle-style-paper-background-vector-illustration_8043-1715.jpg?w=740');
   background-size: cover;
   background-position: center;
   background-repeat: no-repeat;
 }
 
 .card {
   width: 350px;
   border-radius: 10px;
   box-shadow: 0 0 20px rgba(188, 91, 16, 0.1);
 }
 
 .card-body {
   padding: 20px;
 }
 
 .form-label {
   color: #8B4513;
 }
 
 .input-group-text {
   background-color: #8B4513;
   color: white;
 }
 
 .btn-success {
   background-color: #8B4513;
   border: none;
 }
 
 .btn-success:hover {
   background-color: #8B4513;
 }
 
 .card-footer {
   background-color: #f8f9fa;
   padding: 10px;
 }
 </style>
 