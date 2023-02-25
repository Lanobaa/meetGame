<script setup lang="ts">
import { ref } from 'vue';
import home from "@/assets/home.png";
import media from "@/assets/media.png";
import creativity from "@/assets/creativity.png";
import advertise from "@/assets/advertise.png";
import sdk from "@/assets/sdk.png";
import game from "@/assets/game.png";
import manage from "@/assets/manage.png";

const menus = ref([
  {
    title: '控制台',
    icon: home,
    children: [
      { title: '概览' },
    ]
  },
  {
    title: '媒体资产',
    icon: media,
    children: [
      { title: '媒体账户' },
      { title: '媒体充值' },
    ]
  },
  {
    title: '创意素材',
    icon: creativity,
    children: [
      { title: '素材管理' },
      { title: '素材成效' },
    ]
  },
  {
    title: '广告创编',
    icon: advertise,
    children: [
      { title: '广告工具' },
      { title: '授权管理' },
    ]
  },
  {
    title: 'TopSDK',
    icon: sdk,
    children: [
      { title: '我的游戏' },
      { title: 'SDK下载' },
    ]
  },
  {
    title: '游戏发行学院',
    icon: game,
    children: [
      { title: '学院首页' },
      { title: '学习中心' },
    ]
  },
  {
    title: '管理中心',
    icon: manage,
    children: [
      { title: '团队管理' },
      { title: '钱包' },
    ]
  },
]);
</script>

<template>
  <div class="menu">
    <ul
        class="menuItem"
        v-for="(item, index) in menus"
        :key="index"
    >
      <li class="subject flex flex-row items-center"><img :src="item.icon" alt=""><span>{{ item.title }}</span></li>
      <li v-for="(cur, key) in item.children" :key="key + index">{{ cur.title }}</li>
    </ul>
  </div>
</template>

<style lang="less" scoped>
.menu {
  width: 220px;
  padding: 10px;
  height: 100%;
  border-top: 4px solid #f8f8f8;
  background-image: url('../assets/menubg.png');
  background-repeat: no-repeat;
  background-position: left bottom;
  background-size: 100% auto;
  ul {
    .subject {
      img  {
        position: absolute;
        top: 0;
        left: 24px;
        bottom: 0;
        margin: auto;
      }
    }
    li:first-child {
      color: rgba(89, 91, 97, 1);
    }
    li {
      cursor: pointer;
      position: relative;
      z-index: 3;
      border-radius: 8px;
      padding: 0 10px;
      height: 40px;
      font-size: 14px;
      color: rgba(89, 91, 97, .6);
      line-height: 40px;
      text-indent: 40px;
      transition: all 300ms;
      &:hover {
        color: #fff;
        &:after {
          opacity: 1;
          //animation: gradientMovie 300ms;
          //animation-fill-mode: forwards;
        }
      }
      @keyframes gradientMovie {
        to { opacity: 0 }
        from { opacity: 1 }
      }
      &:after {
        content: '';
        transition: all 300ms;
        width: 100%;
        height: 100%;
        position: absolute;
        border-radius: 8px;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        margin: auto;
        z-index: -1;
        background: #8633ff;
        background: -moz-linear-gradient(top,  #8633ff 0%, #6c30cb 100%);
        background: -webkit-linear-gradient(top,  #8633ff 0%,#6c30cb 100%);
        background: linear-gradient(to bottom,  #8633ff 0%,#6c30cb 100%);
        opacity: 0;
      }
    }
  }
}
</style>
