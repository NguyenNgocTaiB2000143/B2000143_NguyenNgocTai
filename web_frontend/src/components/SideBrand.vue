<template>
      
         <h1 class="title"><b>CHÀO MỪNG QUÝ KHÁCH ĐÃ ĐẾN VỚI CỬA HÀNG</b></h1>
</template>

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
         perPage: 6,
         perMove: 1,
         gap: 2,
         height: 160,
         rewind: true,
         autoplay: true,
      };

      return { options };
   },
});
</script>

<style scoped>
.container {
  
  padding :0px;
  max-width: 100%;


}

.box-container {
   height: 150px;
   padding: 0 0;
}

.title {
   text-align: center;
   color: #091108;
   font-size: 26px;
   font-weight: normal;
   border-bottom: 3px solid #000000;
   margin-bottom: 30px;
   padding: 10px 0;
}

.splide__slide {
   height: 45px !important;
   text-align: center;
}
.product-grid {
   height: 180px;
   position: relative;
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
</style>
