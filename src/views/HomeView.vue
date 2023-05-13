<script setup lang="ts">
import Loading from '@/components/Loading.vue';
import { defineAsyncComponent, onMounted } from 'vue';
import * as api from '@/api/index'
onMounted(async () => {
  let res = await api.getHomepage('')
  console.log('xxx1',res);
})
const HomeCom = defineAsyncComponent(() => import('../components/HomeCom.vue'))
</script>

<template>
  <div>
    <suspense>
      <template #fallback>
        <Loading></Loading>
      </template>
      <template #default>
        <HomeCom></HomeCom>
      </template>
    </suspense>
  </div>
</template>

<style>
.homepage{
  padding-top: 46px;
}
</style>
