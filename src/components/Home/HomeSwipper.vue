<template>
  <div class="homeswiper" >
    <div class="swiperBg" :style="{ backgroundColor: data.bgColor }"></div>
    <a-carousel arrows autoplay :beforeChange="changeFn">
      <template #prevArrow>
        <div class="custom-slick-arrow" style="left: 10px; z-index: 1">
          <left-circle-outlined />
        </div>
      </template>
      <template #nextArrow>
        <div class="custom-slick-arrow" style="right: 10px">
          <right-circle-outlined />
        </div>
      </template>
      <div class="swiper-item" v-for="item in props.banner" v-bind:key="item">
        <div class="swiper-box">
          <div class="swiper-left">
            <h3 :style="{ color: item.text_color }">{{ item.desktop_sub_title || item.sub_title  }}</h3>
            <h1 :style="{ color: item.text_color }">{{ item.desktop_title || item.title}}</h1>
          </div>
          <div class="swiper-right">
            <img 
              :src="`https://pixl.decathlon.com.cn/${item.picture_desktop}/banner.jpg`" 
              :alt="item.title" 
              />
          </div>
        </div>
      </div>
    </a-carousel>

  </div>
</template>

<script setup lang="ts">
import { defineProps, reactive } from 'vue';
import { LeftCircleOutlined, RightCircleOutlined } from '@ant-design/icons-vue';
const props: any = defineProps({
  banner: Array
})
const data = reactive({
  bgColor: props.banner[0].bg_color
})
console.log(props.banner);
function changeFn(from: any, to: any) {
  data.bgColor = props.banner[to].bg_color;
}
</script>

<style lang="less" scoped>
.swiperBg {
  position: absolute;
  display: block;
  width: 100%;
  height: 575px;
  background-color: orangered;
  transform-origin: 0 0;
  transform: skew(0, -8deg);
  transition: all 0.5s;
}
.swiper-item {
  height: 575px;
  .swiper-box {
    display: flex;
    min-width: 1000px;
    justify-content: center;
    .swiper-left {
      width: 340px;
      padding-right: 100px;
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      margin-top: 100px;
      text-align: right;
    }
    h3 {
      font-size: 30px;
      font-weight: 900;
      margin: 0;
    }
    h1 {
      font-size: 60px;
      font-weight: 900;
      margin: 0;
      line-height: 70px;
    }

    .swiper-right {
      margin-top: 45px;
      transform-origin: 0 100%;
      transform: skew(0, -8deg);
      overflow: hidden;
      border-radius: 20px;
      border-bottom-right-radius: 80px;
      img {
        transform-origin: 0 100%;
        transform: skew(0, 8deg);
        border-radius: 20px;
      }
    }
  }
}
/* For demo */
.ant-carousel :deep(.slick-slide) {
  text-align: center;
  height: 575px;
  line-height: 160px;
  overflow: hidden;
}

.ant-carousel :deep(.slick-arrow.custom-slick-arrow) {
  width: 25px;
  height: 25px;
  font-size: 25px;
  color: #fff;
  background-color: rgba(31, 45, 61, 0.11);
  opacity: 0.3;
  z-index: 1;
}
.ant-carousel :deep(.custom-slick-arrow:before) {
  display: none;
}
.ant-carousel :deep(.custom-slick-arrow:hover) {
  opacity: 0.5;
}

.ant-carousel :deep(.slick-slide h3) {
  color: #fff;
}
</style>