<template>
   <div class="login-container">
      <div class="login-card">
         <div class="card-background"></div>
         <div class="card-header text-center">
            <h3><b>Đăng nhập</b></h3>
         </div>
         <div class="card-body">
            <form @submit.prevent="login()">
               <div class="input-group form-group">
                  <div class="input-group-prepend">
                     <span class="input-group-text">
                        <i class="fa-solid fa-envelope"></i>
                     </span>
                  </div>
                  <input
                     type="email"
                     class="form-control"
                     placeholder="Email"
                     @blur="validate()"
                     v-model="user.email"
                     :class="{ 'is-invalid': errors.email }"
                  />
                  <div class="invalid-feedback" v-if="errors.email">
                     {{ errors.email }}
                  </div>
               </div>
               <div class="input-group form-group">
                  <div class="input-group-prepend">
                     <span class="input-group-text"
                        ><i class="fas fa-key"></i
                     ></span>
                  </div>
                  <input
                     type="password"
                     class="form-control"
                     placeholder="Mật khẩu"
                     @blur="validate()"
                     v-model="user.password"
                     :class="{ 'is-invalid': errors.password }"
                  />
                  <div class="invalid-feedback" v-if="errors.password">
                     {{ errors.password }}
                  </div>
               </div>
               <div class="form-group">
                  <input
                     type="submit"
                     value="Đăng nhập"
                     class="btn login-btn"
                  />
               </div>
            </form>
         </div>
         <div class="card-footer">
            <div class="d-flex justify-content-center links">
               <p>
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

      async checkout() {
         // Kiểm tra hợp lệ trước khi thanh toán
         if (!this.validate()) {
            // Nếu dữ liệu không hợp lệ, bạn có thể thực hiện các hành động phù hợp, ví dụ: hiển thị thông báo lỗi
            return;
         }

         // Thực hiện các bước thanh toán ở đây
         // Ví dụ:
         // Gửi dữ liệu đơn hàng và thông tin thanh toán lên máy chủ
         // Xóa các sản phẩm trong giỏ hàng sau khi đã thanh toán thành công
         // Chuyển người dùng đến trang xác nhận đơn hàng hoặc trang thành công

         // Sau khi thanh toán thành công, bạn có thể làm như sau để xóa giỏ hàng:
         this.products = [];
         localStorage.removeItem("localProductCart");

         // Hoặc nếu bạn muốn đưa người dùng đến trang xác nhận đơn hàng, bạn có thể chuyển hướng bằng cách sử dụng router Vue:
         // this.$router.push('/xac-nhan-don-hang');
      },

      async login() {
         if (this.validate()) {
            try {
               const userLogin = await UserService.login(this.user);
               const localUserLogin = JSON.stringify(userLogin);
               localStorage.setItem("localUserLogin", localUserLogin);
               localStorage.setItem("userName", userLogin.name);
               if (userLogin.role === "user") {
                  this.$router.push({ name: "home" });
               } else if (userLogin.role === "admin") {
                  this.$router.push({ name: "admin" });
               } else {
                  alert("Xin lỗi! Bạn đã nhập sai email hoặc mật khẩu!");
               }
            } catch (error) {
               alert("Đã xảy ra lỗi trong quá trình đăng nhập!");
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

.login-card {
   width: 400px;
   background-color: rgba(255, 255, 255, 0.9);
   border-radius: 10px;
   overflow: hidden;
   box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.card-background {
   height: 150px;
   background-color: #8B4513;
}

.card-header {
   text-align: center;
   color: #8B4513;
}

.card-body {
   padding: 20px;
}

.login-btn {
   color: #fff;
   background-color: #8B4513;
   border: none;
   border-radius: 5px;
   padding: 10px;
   cursor: pointer;
}

.login-btn:hover {
   background-color: #5c2d0e;
}

.card-footer {
   background-color: rgba(255, 255, 255, 0.9);
   padding: 10px;
}

.links {
   color: #8B4513;
}

.links a {
   margin-left: 4px;
   text-decoration: none;
   color: #8B4513;
}
</style>