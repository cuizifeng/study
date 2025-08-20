<template>
  <Swiper
    ref="swiperRef"
    @swiper="swiperHandler"
    :modules="modules"
    class="pages"
    direction="vertical"
    :touchRatio="2"
    :shortSwipes="true"
    :longSwipesMs="50000"
    effect="creative"
    @slideChange="slideNextHander"
  >
    <!-- :creativeEffect="creativeEffectData" -->
    <SwiperSlide>
      <div id="aa" class="page" style="background-color: #fff">1111</div>
    </SwiperSlide>
    <SwiperSlide>
      <div id="bb" class="page" style="background-color: bisque">2222</div>
    </SwiperSlide>
    <SwiperSlide>
      <div id="cc" class="page" style="background-color: aqua">3333</div>
    </SwiperSlide>
    <SwiperSlide>
      <div class="page" style="background-color: cadetblue">44444</div>
    </SwiperSlide>
    <SwiperSlide>
      <div class="page" style="background-color: darkgoldenrod">55555</div>
    </SwiperSlide>
  </Swiper>
</template>
<script setup>
import { ref, onMounted } from "vue";
import "swiper/css";
import { Swiper, SwiperSlide } from "swiper/vue";
import { EffectCreative, Autoplay } from "swiper/modules";

const modules = ref([EffectCreative, Autoplay]);
const swiperRef = ref();
const creativeEffectData = ref({
  prev: {
    scale: 1,
    translate: [0, "0%", -1, "100%"], //上下滑动
  },
  next: {
    scale: 1,
    translate: [0, "100%", 1, "-100%"], //上下滑动
  },
});

const slideNextHander = (e) => {
  console.log("111222222", e);
};
const swiperHandler = (e) => {
  console.log("eee======", e);
};
onMounted(() => {});
</script>
<style lang="less" scoped>
.pages {
  height: 100vh;
}
.page {
  width: 100vw;
  height: 100vh;
}
.swiper-container {
  width: 100%;
  height: 100%;
}
</style>
