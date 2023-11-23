<template>
   <div class="container">
     <div class="product-list">
       <div class="row mb-3">
         <div class="col-md-4">
           <button type="button" class="btn btn-info">
             <router-link to="/adminpage" class="button-add">
               <i class="fas fa-arrow-left"></i>
               Quay lại
             </router-link>
           </button>
         </div>
         <div class="col-md-4">
           <form class="form-inline my-2 my-lg-0">
             <input
               class="form-control mr-sm-2"
               type="search"
               placeholder="Tìm kiếm..."
               aria-label="Search"
               v-model="searchText"
             />
             <button class="btn btn-outline-success my-2 my-sm-0" type="submit">
               <i class="fas fa-search"></i>
             </button>
           </form>
         </div>
         <div class="col-md-4 text-right">
           <button
             type="button"
             class="btn btn-danger"
             @click="removeAllUsers"
           >
             <i class="fas fa-trash"></i>
             Xóa tất cả
           </button>
         </div>
       </div>
       <div class="table-responsive">
         <table class="table table-bordered table-striped">
           <thead class="thead-dark">
             <tr class="text-center">
               <th scope="col">Vai trò</th>
               <th scope="col">Tên</th>
               <th scope="col">Email</th>
               <th scope="col">Ngày tạo</th>
               <th scope="col">Xử lý</th>
             </tr>
           </thead>
           <tbody class="text-center">
             <tr :key="index" v-for="(user, index) in filteredUsers">
               <td>{{ user.role }}</td>
               <td>{{ user.name }}</td>
               <td>{{ user.email }}</td>
               <td>{{ time(user.createdAt) }}</td>
               <td>
                 <button
                   type="button"
                   class="btn btn-danger"
                   @click="deleteUser(user._id)"
                 >
                   Xóa
                 </button>
               </td>
             </tr>
           </tbody>
         </table>
       </div>
       <p class="text-center non-user" v-if="filteredUsersCount === 0">
         Không có tài khoản nào
       </p>
     </div>
   </div>
 </template>
 
 <script>
 import UserService from "../../services/user.service";
 
 export default {
   data() {
     return {
       users: [],
       searchText: "",
     };
   },
   computed: {
     userStrings() {
       return this.users.map((user) => {
         const { email } = user;
         return [email].join("");
       });
     },
     filteredUsers() {
       if (!this.searchText) return this.users;
       return this.users.filter((_user, index) =>
         this.userStrings[index].includes(this.searchText)
       );
     },
     filteredUsersCount() {
       return this.filteredUsers.length;
     },
   },
   methods: {
     async getAllUser() {
       try {
         this.users = await UserService.getAll();
       } catch (error) {
         console.log(error);
       }
     },
     async deleteUser(UserId) {
       if (confirm("Bạn muốn xóa Tài khoản này?")) {
         try {
           await UserService.delete(UserId);
           this.$router.push({ name: "user.list" });
           this.getAllUser();
         } catch (error) {
           console.log(error);
         }
       }
     },
     async removeAllUsers() {
       if (confirm("Bạn muốn xóa tất cả Tài khoản?")) {
         try {
           await UserService.deleteAll();
           this.$router.push({ name: "user.list" });
           this.getAllUser();
         } catch (error) {
           console.log(error);
         }
       }
     },
     time(timestamp) {
       const date = new Date(timestamp);
       return date.toLocaleString();
     },
   },
   created() {
     this.getAllUser();
   },
 };
 </script>
 
 <style scoped>
 .container {
   padding: 20px;
   background-color: #f8f9fa;
   border: 2px solid #ced4da;
   border-radius: 10px;
   margin-top: 20px;
 }
 
 .product-list {
   margin-top: 20px;
 }
 
 .btn-info,
 .btn-danger {
   background-color: #8B4513;
   border-color: #8B4513;
 }
 
 .btn-info:hover,
 .btn-danger:hover {
   background-color: #693e23;
   border-color: #693e23;
 }
 
 .button-add {
   color: #fff;
 }
 
 .form-inline {
   display: flex;
   align-items: center;
 }
 
 .form-control {
   margin-right: 10px;
 }
 
 .table thead {
   background-color: #8B4513;
   color: #fff;
 }
 
 .table th,
 .table td {
   text-align: center;
 }
 
 .table-responsive {
   overflow-x: auto;
 }
 
 .non-user {
   margin-top: 20px;
   color: #777;
 }
 
 </style>
 