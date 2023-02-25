<script setup lang="ts">
import logo from '@/assets/logo.png';
import photo from '@/assets/photo.png';
import bell from '@/assets/bell.png';
</script>

<template>
  <div class="header flex justify-between items-center">
    <div class="logo pl-4"><img :src="logo" alt=""></div>
    <div class="user flex justify-end items-center pr-5">
      <a class="ml-5 text-sm">文档中心</a>
      <a class="ml-5 text-sm">工单</a>
      <div class="vertical ml-6"></div>
      <a class="bell ml-6"><img :src="bell" alt=""></a>
      <div class="photo ml-6"><img :src="photo" alt=""></div>
    </div>
  </div>
</template>

<style lang="less" scoped>
.header {
  width: 100vw;
  height: 60px;
  background: white;
  .user {
    a {
      color: #767B84;
    }
    .vertical {
      height: 16px;
      border-left: 1px solid #c9cdd4;
    }
  }
}
</style>
