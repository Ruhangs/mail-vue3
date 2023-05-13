<template>
  <div class="homepage">
    <HomeSwipper :banner="data.banner"></HomeSwipper>
    <div class="live">
      <h1>乐享生活100+</h1>
      <div class="live-list" v-if="data.sports.length != 0">
        <div class="live-item" v-for="index in 10"  :key="index">
          <div class="live-btn">
            <img :src="data.sports[index].menuThumbnail" :alt="data.sports[index].displayName">
            <h3>{{ data.sports[index].displayName }}</h3>
          </div>
        </div>
      </div>
      <a-button type="primary" size="large" @click="router.push('/product')">立即享受生活</a-button>
    </div>
  </div>
</template>

<script setup lang="ts">
import HomeSwipper from './Home/HomeSwipper.vue';
import { useRouter } from 'vue-router';
import { getHomepage } from '../api/index'
import { reactive } from 'vue';
const router = useRouter()
let res: any = await getHomepage('')
console.log('xxx',res);
const data = reactive({
  banner: res.banner,
  sports: res.sports
})
console.log(data.banner);
</script>


<style lang="less" scoped>
.homepage {
  padding-top: 46px;
  height: 375px;
  position: relative;
  
}

.live {
  width: 1200px;
  margin:  40px auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding-bottom: 40px;
  h1 {
    font-size: 30px;
  }
  .live-list{
    display: flex;
    flex-wrap: wrap;
    .live-item {
      width: 240px;
    }
    .live-btn {
      display: flex;
      height: 73px;
      width: 200px;
      background-color: #fff;
      border-radius: 8px 8px 25px 8px;
      margin-bottom: 30px;
      box-shadow: 5px 5px 5px #ccc;
      align-items: center;
      justify-content: center;
      position: relative;
      img {
        position: absolute;
        width: 80px;
        height: 80px;
        left: -15px;
        top: -15px;
      }
      h3{
        font-size: 15px;
        font-weight: 900;
      }
    }
  }
}
</style>