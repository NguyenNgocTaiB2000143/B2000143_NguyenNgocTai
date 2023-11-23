<template>
   <div class="container">
      <div class="row justify-content-center align-items-center min-vh-100">
         <div class="col-md-6">
            <div class="card shadow-lg p-3 mb-5 bg-body rounded">
               <div class="card-header text-center">
                  <h3><b>Đăng Ký Tài Khoản</b></h3>
               </div>
               <div class="card-body">
                  <form @submit.prevent="register()">
                     <div class="form-group">
                        <label for="name">Họ và tên</label>
                        <div class="input-group">
                           <div class="input-group-prepend">
                              <span class="input-group-text">
                                 <i class="fa-solid fa-user"></i>
                              </span>
                           </div>
                           <input
                              type="text"
                              id="name"
                              class="form-control"
                              placeholder="Họ và tên"
                              @blur="validate()"
                              v-model="user.name"
                              :class="{ 'is-invalid': errors.name }"
                           />
                        </div>
                        <div class="invalid-feedback" v-if="errors.name">
                           {{ errors.name }}
                        </div>
                     </div>
                     <div class="form-group">
                        <label for="email">Email</label>
                        <div class="input-group">
                           <div class="input-group-prepend">
                              <span class="input-group-text">
                                 <i class="fa-solid fa-envelope"></i>
                              </span>
                           </div>
                           <input
                              type="email"
                              id="email"
                              class="form-control"
                              placeholder="Email"
                              @blur="validate()"
                              v-model="user.email"
                              :class="{ 'is-invalid': errors.email }"
                           />
                        </div>
                        <div class="invalid-feedback" v-if="errors.email">
                           {{ errors.email }}
                        </div>
                     </div>
                     <div class="form-group">
                        <label for="password">Mật khẩu</label>
                        <div class="input-group">
                           <div class="input-group-prepend">
                              <span class="input-group-text">
                                 <i class="fas fa-key"></i>
                              </span>
                           </div>
                           <input
                              type="password"
                              id="password"
                              class="form-control"
                              placeholder="Mật khẩu"
                              @blur="validate()"
                              v-model="user.password"
                              :class="{ 'is-invalid': errors.password }"
                           />
                        </div>
                        <div class="invalid-feedback" v-if="errors.password">
                           {{ errors.password }}
                        </div>
                     </div>
                     <div class="form-group">
                        <label for="repassword">Nhập lại mật khẩu</label>
                        <div class="input-group">
                           <div class="input-group-prepend">
                              <span class="input-group-text">
                                 <i class="fa-solid fa-shield"></i>
                              </span>
                           </div>
                           <input
                              type="password"
                              id="repassword"
                              class="form-control"
                              placeholder="Nhập lại mật khẩu"
                              @blur="validate()"
                              v-model="user.repassword"
                              :class="{ 'is-invalid': errors.repassword }"
                           />
                        </div>
                        <div class="invalid-feedback" v-if="errors.repassword">
                           {{ errors.repassword }}
                        </div>
                     </div>
                     <div class="form-group">
                        <button type="submit" class="btn btn-success btn-block">Đăng ký</button>
                     </div>
                  </form>
               </div>
               <div class="card-footer">
                  <div class="d-flex justify-content-center links">
                     <p>
                        Đã có tài khoản? 
                        <router-link to="/login"><b>Đăng nhập</b></router-link>
                     </p>
                  </div>
               </div>
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
            name: "",
            email: "",
            password: "",
            repassword: "",
         },
         user: {
            name: "",
            email: "",
            password: "",
            repassword: "",
         },
      };
   },
   methods: {
      validate() {
         let isValid = true;

         this.errors = {
            name: "",
            email: "",
            password: "",
            repassword: "",
         };

         if (!this.user.name) {
            this.errors.name = "Họ và tên là bắt buộc";
            isValid = false;
         }
         if (!this.user.email) {
            this.errors.email = "Email là bắt buộc";
            isValid = false;
         }
         if (!this.user.password) {
            this.errors.password = "Mật khẩu là bắt buộc";
            isValid = false;
         }
         if (this.user.repassword != this.user.password) {
            this.errors.repassword = "Mật khẩu chưa đúng";
            isValid = false;
         }
         return isValid;
      },
      async register() {
         if (this.validate()) {
            try {
               await UserService.create(this.user);
               alert(
                  `Chúc mừng ${this.user.name.toUpperCase()} !!! Bạn đã đăng ký tài khoản thành công!`
               );
               this.$router.push({ name: 'login' });
            } catch (error) {
               console.log(error);
            }
         }
      },
   },
};
</script>

<style scoped>

.container {
   padding-top: 80px;
   background-image: url('https://img.freepik.com/premium-vector/guitar-doodle-style-paper-background-vector-illustration_8043-1715.jpg?w=740'); /* Đường dẫn đến hình nền */
   background-size: cover;
   background-position: center;
}
.container {
   padding-top: 80px;
}

.card {
   border: none;
   border-radius: 15px;
}

.card-header {
   background-color: #8B4513;
   color: white;
   border-top-left-radius: 15px;
   border-top-right-radius: 15px;
}

.card-body {
   padding: 30px;
}

.form-group {
   margin-bottom: 20px;
}

.form-group label {
   font-weight: bold;
   color: #8B4513;
}

.input-group-prepend span {
   width: 40px;
   background-color: #8B4513;
   color: white;
   border: none;
}

.form-control {
   border-radius: 5px;
}

.btn-success {
   background-color: #8B4513;
   border: none;
}

.btn-success:hover {
   background-color: #8B4513;
}

.card-footer {
   background-color: white;
   border-bottom-left-radius: 15px;
   border-bottom-right-radius: 15px;
   padding: 20px;
}

.links {
   color: #8B4513;
}

.links a {
   text-decoration: none;
   color: #8B4513;
   font-weight: bold;
}

.links a:hover {
   text-decoration: underline;
}
</style>