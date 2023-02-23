<script setup lang="ts">
import { ref, onMounted } from 'vue';
import * as echarts from 'echarts/core';
import { LineChart } from 'echarts/charts';
import {
  LegendComponent,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  ToolboxComponent,
} from 'echarts/components';
// 标签自动布局、全局过渡动画等特性
import { LabelLayout, UniversalTransition } from 'echarts/features';
// 引入 Canvas 渲染器，注意引入 CanvasRenderer 或者 SVGRenderer 是必须的一步
import { CanvasRenderer } from 'echarts/renderers';

// 注册必须的组件
echarts.use([
  ToolboxComponent,
  LegendComponent,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LineChart,
  LabelLayout,
  UniversalTransition,
  CanvasRenderer
]);
import logo from '@/assets/logo.png';
import photo from '@/assets/photo.png';
import bell from '@/assets/bell.png';
import home from '@/assets/home.png';
import media from '@/assets/media.png';
import creativity from '@/assets/creativity.png'
import advertise from '@/assets/advertise.png';
import sdk from '@/assets/sdk.png';
import game from '@/assets/game.png';
import manage from '@/assets/manage.png';
import crossImg from '@/assets/x.png';
// useRoute, useHead, and HelloWorld are automatically imported. See vite.config.ts for details.
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

onMounted(() => {
  const myChart = echarts.init(document.getElementById('myEcharts'));
  myChart.setOption({
    color: ['#8656F4', '#00DDFF', '#37A2FF', '#FF0087', '#FFBF00'],
    title: {
      text: '投放数据',
      top: 0,
      left: 10
    },
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross',
        label: {
          backgroundColor: '#6a7985'
        }
      }
    },
    legend: {
      type: 'plain',
      left: 10,
      top: 30,
      itemWidth: 8,
      itemHeight: 8,
      data: [{
        width: 5,
        icon: 'roundRect',
        name: '指标A',
      }]
    },
    grid: {
      top: '25%',
      left: '1%',
      right: '2%',
      bottom: '3%',
      containLabel: true
    },
    xAxis: [
      {
        type: 'category',
        boundaryGap: false,
        axisPointer: {
          z: 1,
          value: '2022-07-04',
          snap: true,
          lineStyle: {
            color: '#8656F4',
            width: 2
          },
          handle: {
            show: true,
            color: '#7581BD'
          }
        },
        data: ['2022-07-01', '2022-07-02', '2022-07-03', '2022-07-04', '2022-07-05', '2022-07-06', '2022-07-07']
      }
    ],
    yAxis: [
      {
        type: 'value'
      }
    ],
    series: [
      {
        name: '指标A',
        type: 'line',
        stack: 'Total',
        smooth: true,
        lineStyle: {
          width: 2,
          color: 'rgb(134,85,243)',
        },
        symbol: `image://${crossImg}`,
        showSymbol: false,
        symbolSize: [18, 18],
        areaStyle: {
          opacity: 0.8,
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 0,
              color: 'rgba(93, 0, 255, .12)'
            },
            {
              offset: 1,
              color: 'rgba(93, 0, 255, 0)'
            }
          ])
        },
        emphasis: {
          focus: 'series'
        },
        data: [500, 3200, 2500, 4200, 2600, 5000, 400]
      },
    ]
  });
  const myChartOne = echarts.init(document.getElementById('myEchartsOne'));
  myChartOne.setOption({
    color: ['#8656F4', '#FFBD48', '#37A2FF', '#FF0087', '#FFBF00'],
    title: {
      text: '模拟人生',
      top: 0,
      left: 10
    },
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross',
        label: {
          backgroundColor: '#6a7985'
        }
      }
    },
    legend: {
      type: 'plain',
      left: 10,
      top: 30,
      itemWidth: 8,
      itemHeight: 8,
      data: [
        {
          width: 5,
          icon: 'roundRect',
          name: 'ARPU',
        },
        {
          width: 5,
          icon: 'roundRect',
          name: 'ARPPU',
        }
      ]
    },
    grid: {
      top: '25%',
      left: '1%',
      right: '2%',
      bottom: '3%',
      containLabel: true
    },
    xAxis: [
      {
        type: 'category',
        boundaryGap: false,
        axisPointer: {
          z: 1,
          value: '2022-07-04',
          snap: true,
          lineStyle: {
            color: '#8656F4',
            width: 2
          },
          handle: {
            show: true,
            color: '#7581BD'
          }
        },
        data: ['2022-07-01', '2022-07-02', '2022-07-03', '2022-07-04', '2022-07-05', '2022-07-06', '2022-07-07']
      }
    ],
    yAxis: [
      {
        type: 'value'
      }
    ],
    series: [
      {
        name: 'ARPU',
        type: 'line',
        stack: 'Total',
        smooth: true,
        lineStyle: {
          width: 2,
          color: 'rgb(134,85,243)',
        },
        symbol: `image://${crossImg}`,
        showSymbol: false,
        symbolSize: [18, 18],
        areaStyle: {
          opacity: 0.8,
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 0,
              color: 'rgba(93, 0, 255, .12)'
            },
            {
              offset: 1,
              color: 'rgba(93, 0, 255, 0)'
            }
          ])
        },
        emphasis: {
          focus: 'series'
        },
        data: [500, 3200, 2500, 4200, 2600, 5000, 400]
      },
      {
        name: 'ARPPU',
        type: 'line',
        stack: 'Total',
        smooth: true,
        lineStyle: {
          width: 2,
          color: '#FFBD48',
        },
        symbol: `image://${crossImg}`,
        showSymbol: false,
        symbolSize: [18, 18],
        areaStyle: {
          opacity: 0.8,
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 0,
              color: 'rgba(255, 215, 100, .2)'
            },
            {
              offset: 1,
              color: 'rgba(255, 215, 100, 0)'
            }
          ])
        },
        emphasis: {
          focus: 'series'
        },
        data: [2000, 100, 5000, 2900, 2600, 1000, 600]
      },
    ]
  });
  const myChartTwo = echarts.init(document.getElementById('myEchartsTwo'));
  myChartTwo.setOption({
    color: ['#FFBD48', '#00DDFF', '#37A2FF', '#FF0087', '#FFBF00'],
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross',
        label: {
          backgroundColor: '#FFBD48'
        }
      }
    },
    legend: {
      type: 'plain',
      left: 10,
      top: 30,
      itemWidth: 8,
      itemHeight: 8,
      data: [{
        width: 5,
        icon: 'roundRect',
        name: '付费率',
      }]
    },
    grid: {
      top: '25%',
      left: '1%',
      right: '2%',
      bottom: '3%',
      containLabel: true
    },
    xAxis: [
      {
        type: 'category',
        boundaryGap: false,
        axisPointer: {
          z: 1,
          value: '2022-07-04',
          snap: true,
          lineStyle: {
            color: '#8656F4',
            width: 2
          },
          handle: {
            show: true,
            color: '#7581BD'
          }
        },
        data: ['2022-07-01', '2022-07-02', '2022-07-03', '2022-07-04', '2022-07-05', '2022-07-06', '2022-07-07']
      }
    ],
    yAxis: [
      {
        type: 'value'
      }
    ],
    series: [
      {
        name: '付费率',
        type: 'line',
        stack: 'Total',
        smooth: true,
        lineStyle: {
          width: 2,
          color: 'rgb(134,85,243)',
        },
        symbol: `image://${crossImg}`,
        showSymbol: false,
        symbolSize: [18, 18],
        areaStyle: {
          opacity: 0.8,
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 0,
              color: 'rgba(93, 0, 255, .12)'
            },
            {
              offset: 1,
              color: 'rgba(93, 0, 255, 0)'
            }
          ])
        },
        emphasis: {
          focus: 'series'
        },
        data: [500, 3200, 2500, 4200, 2600, 5000, 400]
      },
    ]
  });
});
</script>

<template>
  <div class="home">
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
    <div class="main flex flex-nowrap flex-row">
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
      <div class="body flex flex-row flex-nowrap flex-1">

        <div class="bodyLeft flex-">
          <div class="cover">
            <div class="title">
              <span>成为爆款游戏</span>
              <p>无论是个人开发者还是成熟团队，<br/>MeetGames助您成功出海！</p>
            </div>
            <div class="c_img"></div>
          </div>
          <div class="pivotal flex justify-between items-end">
            <div class="p_con">
              <div class="title">
                <span>关键数据</span>
                <a>2022-12-31</a>
              </div>
              <div class="category flex flex-row justify-between items-center">
                <div class="c_item flex-1">
                  <p>US$ 999.00</p>
                  <span>游戏充值金额</span>
                </div>
                <div class="c_item flex-1">
                  <p>999.00</p>
                  <span>游戏活跃用户数</span>
                </div>
                <div class="c_item flex-1">
                  <p>999.00</p>
                  <span>游戏注册用户数</span>
                </div>
                <div class="c_item flex-1">
                  <p>US$ 999.00</p>
                  <span>投放花费</span>
                </div>
              </div>
            </div>
            <div class="p_bg bg_one"></div>
            <div class="p_bg bg_two"></div>
          </div>
          <div class="myEcharts">
            <div class="target"><img src="../assets/target.png" alt=""></div>
            <div id="myEcharts" :style="{ width: '100%', height: '300px' }"></div>
          </div>
          <div class="e_two flex flex-row justify-between items-center">
            <div class="channel"><img src="../assets/channel.png" alt=""></div>
            <div class="flex-1">
              <div id="myEchartsOne" :style="{ width: '100%', height: '300px' }"></div>
            </div>
            <div class="flex-1">
              <div id="myEchartsTwo" :style="{ width: '100%', height: '300px' }"></div>
            </div>
          </div>
        </div>
        <div class="bodyRight flex-1"></div>
      </div>
    </div>
  </div>
</template>

<style lang="less">
.home {
  width: 100vw;
  height: 100vh;
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
  .main {
    width: 100vw;
    height: calc(100vh - 60px);
    overflow: hidden;
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
    .body {
      max-height: 100%;
      background: #f8f8f8;
      .bodyLeft {
        flex: 4;
        padding: 0 30px;
        position: relative;
        .cover {
          width: 100%;
          position: absolute;
          top: 0;
          left: 0;
          z-index: 1;
          .title {
            position: absolute;
            top: 40px;
            left: 15%;
            span {
              font-weight: bold;
              font-size: 24px;
              color: #232844;
            }
            p {
              white-space: nowrap;
              font-size: 14px;
              color: #797b82;
              margin-top: 8px;
            }
          }
          .c_img {
            width: 408px;
            height: 249px;
            position: absolute;
            transform: scale(1.2);
            top: 20px;
            left: 45%;
            background: url('../assets/handShank.png');
            background-size: 100% 100%;
          }
        }
        .pivotal {
          margin-top: 200px;
          position: relative;
          z-index: 10;
          &:before {
            content: "";
            position: absolute;
            top: -18px;
            right: 0;
            border-bottom: 18px solid #8633ff;
            border-right: 18px solid #f8f8f8;
            z-index: 2;
            width: 100%;
            height: 0;
          }
          &:after {
            content: '';
            position: absolute;
            left: 0;
            right: 0;
            bottom: -60px;
            top: 0;
            width: 80%;
            height: 80%;
            z-index: 1;
            margin: auto;
            box-shadow: 0 25px 50px rgba(0,0,0,.2);
          }
          .p_con {
            padding-right: 30px;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            z-index: 40;
            .title {
              font-size: 16px;
              color: white;
              margin-top: -20px;
              margin-left: 10px;
              margin-bottom: 26px;
            }
            .category {
              width: inherit;
              .c_item {
                padding-left: 30px;
                border-right: 1px solid rgba(255,255,255, 0.2);
                text-align: center;
                &:last-child {
                  border-right: none;
                }
                & > span {
                  font-size: 14px;
                  margin-bottom: 10px;
                  color: rgba(255,255,255, .8);
                }
                p {
                  white-space: nowrap;
                  font-size: 24px;
                  color: white;
                }
              }
            }
          }
          .bg_one {
            flex: 1;
            height: 130px;
            position: relative;
            z-index: 11;
            &:before {
              content: "";
              position: absolute;
              top: -36px;
              left: 0;
              border-bottom: 18px solid #8633ff;
              border-left: 18px solid #f8f8f8;
              border-right: 18px solid #f8f8f8;
              width: 100%;
              height: 0;
            }
            &:after {
              content: "";
              position: absolute;
              bottom: -18px;
              left: 0;
              border-top: 18px solid #6c30cb;
              border-left: 18px solid #f8f8f8;
              width: 100%;
              height: 0;
            }
          }
          .bg_two {
            flex: 3;
            position: relative;
            z-index: 12;
            height: 130px;
            &:after {
              content: "";
              position: absolute;
              bottom: -18px;
              left: 0;
              border-top: 18px solid #6c30cb;
              border-right: 18px solid #f8f8f8;
              width: 100%;
              height: 0;
            }
          }
          .p_bg {
            background: #8633ff;
            background: -moz-linear-gradient(top,  #8633ff 0%, #6c30cb 100%);
            background: -webkit-linear-gradient(top,  #8633ff 0%,#6c30cb 100%);
            background: linear-gradient(to bottom,  #8633ff 0%,#6c30cb 100%);
          }
        }
        .myEcharts {
          margin-top: 60px;
          padding: 20px;
          background: white;
          border-radius: 10px;
          position: relative;
          box-shadow: 0 5px 10px rgba(0,0,0,0.05);
          .target {
            position: absolute;
            right: 40px;
            top: 30px;
          }
        }
        .e_two {
          box-shadow: 0 5px 10px rgba(0,0,0,0.05);
          margin-top: 30px;
          padding: 20px;
          background: white;
          border-radius: 10px;
          position: relative;
          .channel {
            position: absolute;
            right: 40px;
            top: 30px;
          }
        }
      }
      .bodyRight {
        flex: 1;
        min-width: 300px;
        background: orange;
      }
    }
  }
}
</style>
