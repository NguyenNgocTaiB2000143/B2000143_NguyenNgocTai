<template>
   <div class="slider-box">
      <div class="slider-content">
         <Splide :options="options" aria-label="My Favorite Images">
            <SplideSlide>
               <img src="https://guitardongtam.com/Upload/2021/8/13/guitardongtam-79e9.jpg" alt="Sample 1" />
            </SplideSlide>
            <SplideSlide>
               <img src="https://vn.yamaha.com/vi/files/gstore_26ca39665c4728893fd6951220083954.jpg?impolicy=resize&imwid=1200&imhei=480" alt="Sample 2" />
            </SplideSlide>
         </Splide>
      </div>
      <div class="centered-text">
         <h1 class="title"><b>Mang đến sự tươi mới dành cho khách hàng</b></h1>
      </div>
   </div>
</template>

<style>
.centered-text {
   text-align: center;
   margin-top: 20px; /* Duyệt động để điều chỉnh khoảng cách từ slider đến tiêu đề */
}
</style>

<script>
import { Splide, SplideSlide } from "@splidejs/vue-splide";
import { defineComponent } from "vue";

export default defineComponent({
   components: {
      Splide,
      SplideSlide,
   },

   setup() {
      const options = {
         rewind: true,
         gap: "1rem",
         autoplay: true,
      };

      return { options };
   },
});
</script>

<style scoped>
.splide__slide img {
   width: 100%;
   height: 300px;
   object-fit: cover; /* Bao phủ toàn bộ khung hình */
   display: block;
}
.content {
   margin-top: 5px;
   position: absolute; /* Để đưa nội dung vào trong khung ảnh */
   right: 10px;
   bottom: 20px;
   width: 400px;
   text-align: justify;
   background-color: #333;
   padding: 7px 7px 12px;
   border-radius: 3px;
   opacity: 0.85;
}
.content a {
   text-decoration: none;
   color: white;
   display: inline-block;
   line-height: 24px;
   text-transform: uppercase;
}
</style>
