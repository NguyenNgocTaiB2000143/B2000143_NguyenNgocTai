<template>
   <div class="wrapper">
     <div class="header">
       <div class="nav-menu">
         <NavMenu />
       </div>
     </div>
     <div class="container">
       <div class="row contact">
         <div class="col-sm-6">
           <div class="contact-info">
             <p>
               <a>.</a>
             </p>
             <p>
               <a>.</a>
               
             </p>
             <p>
               <a>.</a>
               
             </p>
             <p>
               <i class="fas fa-school"></i>
               Trường Công Nghệ Thông Tin
             </p>
             <p>
               <i class="fas fa-envelope icon-email"></i>
               <a href="mailto:taib2000143@student.ctu.edu.vn" style="color: #000; text-decoration: none;">
                 taib2000143@student.ctu.edu.vn
               </a>
             </p>
             <p>
               <i class="fas fa-phone icon-phone"></i>
               <a href="tel:+860948771821" style="color: #000; text-decoration: none;">
                 +86 0948771821
               </a>
             </p>
           </div>
         </div>
         <div class="col-sm-6">
           <div class="map-container">
             <iframe
               class="map"
               src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d15715.309578979477!2d105.76044688128938!3d10.031098185838209!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x31a0883d2192b0f1%3A0x4c90a391d232ccce!2zVHLGsOG7nW5nIEPDtG5nIE5naOG7hyBUaMO0bmcgVGluIHbDoCBUcnV54buBbiBUaMO0bmcgKENUVSk!5e0!3m2!1svi!2s!4v1680923439730!5m2!1svi!2s"
               width="600"
               height="450"
               style="border:0;"
               allowfullscreen=""
               loading="lazy"
               referrerpolicy="no-referrer-when-downgrade"
             ></iframe>
           </div>
         </div>
       </div>
 
       <div class="BaseFooter">
         <BaseFooter />
       </div>
     </div>
   </div>
 </template>

<script>
import NavMenu from "../components/NavMenu.vue";
import BaseFooter from "../components/BaseFooter.vue";

export default {
   components: {
      NavMenu,
      BaseFooter,
   },
   methods: {
      feedback() {
         alert("Cảm ơn bạn đã đóng góp ý kiến!!");
      },
   },
};
</script>

<style scoped>
.wrapper {
  max-width: 100%;
  background-color: #fff;
  font-family: "Open Sans", sans-serif;
  padding-bottom: 20px;
  padding-top: 10px;
  box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.header {
  background-color: #8B4513;
  color: #fff;
  padding: 10px;
}

.container {
  text-align: left;
  margin-top: 10px;
  color: #333;
}

.form-group {
  margin: 10px 0;
  padding-left: 15px;
}

.map {
  padding: 0 15px;
  width: 100%;
  margin-top: 10px;
}

.contact-info p {
  margin-bottom: 5px;
}

.contact {
  margin-top: 10px;
  padding-left: 15px;
}

.BaseFooter {
  margin-top: 20px;
}

.footer {
  background-color: #8B4513;
  color: #fff;
  padding: 10px;
}

/* Thêm các kiểu tùy chỉnh khác nếu cần */
</style>

