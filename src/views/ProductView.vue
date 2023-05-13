<template>
  <div class="loading" v-show="data.isLoading">
    <Loading></Loading>
  </div>
  <div class="product" v-show="!data.isLoading">
    <div class="prod-list">
      <h1><SketchOutlined/>产品推荐</h1>
    </div>
    <div class="scene-list">
      <h3><RadarChartOutlined/>切换使用场景</h3>
    </div>
  </div>
</template>

<script setup lang="ts">
import Loading from '@/components/Loading.vue';
import { useFullscreen } from "@/stores/counter" 
import { SketchOutlined, RadarChartOutlined } from '@ant-design/icons-vue'
import { useRoute } from 'vue-router';
import { onMounted, reactive } from 'vue';
import { getProducts } from '@/api';
const route = useRoute()
const fullScreen = useFullscreen()
console.log(fullScreen.isFullscreen);
const data = reactive({
  products:[],
  isLoading: true
})

onMounted(async () => {
  let res = await getProducts()
  console.log(res);
  data.isLoading = false
})

window.addEventListener('wheel',(e) => {
  console.log(e);
  if (e.deltaY > 0){
    fullScreen.setFullscreen(true)
  }
  if (e.deltaY < 0){
    fullScreen.setFullscreen(false)
  }
  
})
</script>

<style lang="less" scoped>
.prod-list {
  width: 300px;
  height: 100vh;
  padding: 60px 0 0;
  position: fixed;
  z-index: 999;
  transition: all 0.5;
  background-color: pink;
  // background-color: rgba(255, 255, 255, 0.8);
  left: 0;
  top: 0;
}
.scene-list {
  width: 300px;
  height: 100vh;
  padding: 60px 0 0;
  position: fixed;
  z-index: 999;
  transition: all 0.5;
  background-color: pink;
  // background-color: rgba(255, 255, 255, 0.8);
  right: 0;
  top: 0;
}
</style>