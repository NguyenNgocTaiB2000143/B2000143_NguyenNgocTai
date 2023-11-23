<template>
   <div class="container">
     <nav class="navbar navbar-expand-lg navbar-light bg-light">
       <router-link to="/" class="navbar-brand">
         <i class="fas fa-home"></i> Trang chủ
       </router-link>
       <button
         class="navbar-toggler"
         type="button"
         data-toggle="collapse"
         data-target="#navbarNav"
         aria-controls="navbarNav"
         aria-expanded="false"
         aria-label="Toggle navigation"
       >
         <span class="navbar-toggler-icon"></span>
       </button>
       <div class="collapse navbar-collapse" id="navbarNav">
         <ul class="navbar-nav mr-auto">
           <li class="nav-item">
             <router-link to="/menu" class="nav-link">
               Menu
             </router-link>
           </li>
           <li class="nav-item">
             <router-link to="/contact" class="nav-link">
               Liên hệ
             </router-link>
           </li>
           <li class="nav-item">
             <router-link to="/intro" class="nav-link">
               Giới thiệu
             </router-link>
           </li>
         </ul>
         <ul class="navbar-nav ml-auto">
           <li class="nav-item">
             <router-link to="/cart" class="nav-link">
               Giỏ hàng <i class="fas fa-shopping-cart"></i>
               <span class="badge badge-danger">{{ localCarts.length }}</span>
             </router-link>
           </li>
           <li class="nav-item" v-if="localUser.role !== ''">
             <router-link to="/login" class="nav-link" @click="handleLogout">
               <b>{{ localUser.name }}</b>
               <button class="btn logout-btn">
                 <i class="fas fa-user"></i>
               </button>
             </router-link>
           </li>
           <li class="nav-item" v-if="localUser.role === 'admin'">
             <router-link to="/adminpage" class="nav-link">
               <button class="btn admin-btn">
                 <i class="fas fa-users-cog"></i>
               </button>
             </router-link>
           </li>
         </ul>
       </div>
     </nav>
   </div>
 </template>

<script>
export default {
   data() {
      return {
         localUser: {},
         localCarts: {},
      };
   },
   methods: {
      handleLogout() {
         localStorage.removeItem("localUserLogin");
      },
   },
   mounted() {
      const user = JSON.parse(localStorage.getItem("localUserLogin"));
      this.localUser = user;
      const localProductCart = JSON.parse(
         localStorage.getItem("localProductCart") ?? "[]"
      );
      this.localCarts = localProductCart;
   },
};
</script>

<style scoped>
.container {
   padding: 20px;
   max-width: 100%;
   z-index: 50;
   position: fixed;
   background-color: #fff;
   width: 100%;
}

.navbar {
   border-top: 1px solid #8B4513;
   border-bottom: 1px solid #8B4513;
   background-color: #8B4513;
}

.navbar .nav-item {
   color: #000000;
}

.navbar .nav-item a {
   font-family: "Open Sans", sans-serif;
   color: #070505 !important;
   text-align: left;
   font-size: 16px;
   padding: 15px;
   display: block;
}

.navbar .nav-item a:hover {
   background-color: rgba(255, 255, 255, 0.1);
   border-radius: 10px;
   box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.dropdown-menu {
   width: 100%;
}

.dropdown-menu ul {
   list-style: none;
   padding-left: 0;
}

.nav-item:hover .dropdown-menu {
   display: block;
}

.logout-btn,
.admin-btn {
   width: 30px;
   height: auto;
   margin-top: -5px;
   margin-left: 5px;
}

@media screen and (max-width: 1023px) {
   .admin-btn {
      visibility: hidden;
   }
}

i {
   color: #8B4513;
}

.box {
   height: 40px;
   width: 100%;
   margin-top: -30px;
   background-color: #090707;
}
</style>


