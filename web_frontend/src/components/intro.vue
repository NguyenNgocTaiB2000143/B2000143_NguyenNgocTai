<template>
    <div class="wrapper">
       <div class="header">
          <div class="nav-menu">
             <NavMenu />
          </div>
       </div>
       <div class="container">
          <div class="row intro">
             <div class="col-sm-6">
                <p>
                   <i class="fa-solid fa-location-dot"></i>
                   <a href="https://ctu.edu.vn">
                      
                   </a>
                </p>
                <p>
                   <i class="fa-solid fa-school"></i>
                   
                </p>
                <p>
                  <div class="intro">
            <h1><b>..................</b></h1>
            <h1><b>Harmony Guitars</b></h1>
            <p>
               Chào mừng bạn đến với Harmony Guitars - điểm đến lý tưởng cho những người yêu thích âm nhạc và đam mê đàn guitar. 
               Chúng tôi tự hào là một cửa hàng chuyên nghiệp cung cấp đàn guitar chất lượng cao và dịch vụ tận tâm để đáp ứng mọi nhu cầu của khách hàng Tại Harmony Guitars
               , chúng tôi tin rằng mỗi người chơi guitar đều đặc biệt và có những mong muốn riêng. 
               Sứ mệnh của chúng tôi là mang đến sự hài lòng tuyệt đối cho khách hàng bằng cách cung cấp một bộ sưu tập đa dạng với các thương hiệu nổi tiếng và một mức giá phải chăng.
               Hãy đến Harmony Guitars để trải nghiệm không gian mua sắm âm nhạc chuyên nghiệp và thân thiện ngay hôm nay!
            </p>
        </div>
 
                </p>
                <p>
                   <i class="fa-solid fa-phone icon-phone"></i>
                   <a style="color: #000;text-decoration: none;" href="tel:+86 0948771821">+86 0948771821</a>
                </p>
             </div>
             <div class="col-sm-6">
               <img class="map"
                  src="https://vietthuongshop.vn/upload/content/images/Tuvan/2019/1-2019/noi-ban-dan-guitar-gia-re-uy-tin-o-tp-hcm-1.jpg"  
                  alt="Map Image"
                  width="600"
                  height="450"
                  style="border: 0; display: block; margin: 0 auto;" />
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
    padding-bottom: 50px;
    padding-top: 5px;
    box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
 }
 
 .header {
    width: 100%;
    height: auto;
 }
 
 .container {
    text-align: left;
    margin-top: 5px;
    color: #333;
 
 }
 
 .form-group {
    padding-left: 15px;
 }
 
 .map {
    padding: 0 15px;
    width: 100%;
 }
 
 .contact {
    margin-top: 10px;
    padding-left: 15px;
 }
 </style>
 