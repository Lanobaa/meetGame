<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { videoPlay } from 'vue3-video-play';
import 'vue3-video-play/dist/style.css'
import { useThrottleFn } from '@vueuse/core';
import * as echarts from 'echarts/core';
import { LineChart } from 'echarts/charts';
import meetVideo from '../assets/6_1677240394.mp4';
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
import Header from './Header.vue';
import Menu from './Menu.vue';
import Right from './Right.vue';

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


import crossImg from '@/assets/x.png';
const options = reactive({
  width: '100vw', //播放器高度
  height: '100vh', //播放器高度
  color: "#409eff", //主题色
  title: '', //视频名称
  src: meetVideo, //视频源
  muted: false, //静音
  webFullScreen: false,
  speedRate: ["0.75", "1.0", "1.25", "1.5", "2.0"], //播放倍速
  autoPlay: true, //自动播放
  loop: false, //循环播放
  mirror: false, //镜像画面
  ligthOff: false,  //关灯模式
  volume: 0.3, //默认音量大小
  control: true, //是否显示控制
  controlBtns:['audioTrack', 'quality', 'speedRate', 'volume', 'setting', 'pip'] //显示所有按钮,
})

const nxx = ref(0);
const nyy = ref(0);

const spiritEffect = (fo, nx, ny) => {
  if (fo == 'top') {
    nyy.value = ny;
  }
  if (fo == "bottom") {
    nyy.value = -ny;
  }
  if (fo == 'left') {
   nxx.value = nx;
  }
  if (fo == "right") {
    nxx.value = -nx;
  }
}
onMounted(() => {
  const w = document.body.clientWidth;
  const h = document.body.clientHeight;
  const dirName = ['top', 'right', 'bottom', 'left'];
  document.addEventListener('mousemove', useThrottleFn((e) => {
    let x = (e.pageX - (w / 2)) * (w > h ? (h / w) : 1);
    let y = (e.pageY - (h / 2)) * (h > w ? (w / h) : 1);
    let direction = Math.round((((Math.atan2(y, x) * (180 / Math.PI)) + 180) / 90) + 3) % 4;
    let dirText = dirName[direction];
    let nx = x / 22;
    let ny = y / 22;
    spiritEffect(dirText, Math.abs(nx), Math.abs(ny));
  }, 100));
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
        animationEasing: 'cubicIn',
        animationDuration: 1800,
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
        animationEasing: 'cubicIn',
        animationDuration: 1800,
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
        animationEasing: 'cubicIn',
        animationDuration: 1800,
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
        animationEasing: 'cubicIn',
        animationDuration: 1800,
        data: [500, 3200, 2500, 4200, 2600, 5000, 400]
      },
    ]
  });
});
</script>

<template>
  <div class="home">
    <div class="videos">
      <videoPlay v-bind="options" />
    </div>
    <Header />
    <div class="main flex flex-nowrap flex-row">
      <Menu />
      <div class="body flex flex-row flex-nowrap flex-1">
        <div class="bodyLeft flex-">
          <div class="cover flex flex-row justify-between items-center">
            <div class="title" :style="{ 'transform': `translate(${nxx}px, ${nyy}px)` }">
             <div class="t_wrap">
               <span>成为爆款游戏</span>
               <p>无论是个人开发者还是成熟团队，<br/>MeetGames助您成功出海！</p>
             </div>
            </div>
            <div class="layout">
              <div class="c_circle" :style="{ 'transform': `translate(${nxx}px, ${nyy}px)` }"></div>
              <div class="c_shank" :style="{ 'transform': `translate(${-nxx}px, ${-nyy}px)` }"></div>
            </div>
          </div>
          <div class="pivotal flex justify-between items-end animateBottomToTop1">
            <div class="p_con">
              <div class="title flex flex-row justify-between items-center">
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
          <div class="myEcharts animateBottomToTop2">
            <div class="target"><img src="../assets/target.png" alt=""></div>
            <div id="myEcharts" :style="{ width: '100%', height: '300px' }"></div>
          </div>
          <div class="e_two flex flex-row justify-between items-center animateBottomToTop3">
            <div class="channel"><img src="../assets/channel.png" alt=""></div>
            <div class="flex-1">
              <div id="myEchartsOne" :style="{ width: '100%', height: '300px' }"></div>
            </div>
            <div class="flex-1">
              <div id="myEchartsTwo" :style="{ width: '100%', height: '300px' }"></div>
            </div>
          </div>
        </div>
        <div class="bodyRight flex-1">
          <Right />
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="less">

.animateBottomToTop1 {
  animation: commonMovie 500ms;
  animation-delay: 6500ms;
  animation-fill-mode: forwards;
  opacity: 0;
}
.animateBottomToTop2 {
  animation: commonMovie 500ms;
  animation-delay: 6800ms;
  animation-fill-mode: forwards;
  opacity: 0;
}
.animateBottomToTop3 {
  animation: commonMovie 500ms;
  animation-delay: 7100ms;
  animation-fill-mode: forwards;
  opacity: 0;
}
.animateBottomToTop4 {
  animation: commonMovie 500ms;
  animation-delay: 7400ms;
  animation-fill-mode: forwards;
  opacity: 0;
}
.animateBottomToTop5 {
  animation: commonMovie 500ms;
  animation-delay: 7900ms;
  animation-fill-mode: forwards;
  opacity: 0;
}
.animateBottomToTop6 {
  animation: commonMovie 500ms;
  animation-delay: 8200ms;
  animation-fill-mode: forwards;
  opacity: 0;
}
@keyframes commonMovie {
  0% {
    opacity: 0;
    transform: translateY(100px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
}
</style>

<style lang="less" scoped>
.home {
  width: 100vw;
  height: 100vh;
  .videos {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    margin: auto;
    z-index: 100;
    width: 100vw;
    height: 100vh;
    background: pink;
    animation: sixHide 6s;
    opacity: 0;
    @keyframes sixHide {
      0% {
        opacity: 1;
      }
      98% {
        opacity: 1;
      }
      100% {
        opacity: 0;
      }
    }
  }
  .main {
    width: 100vw;
    height: calc(100vh - 60px);
    overflow: hidden;
    .body {
      max-height: 100%;
      background: #f8f8f8;
      .bodyLeft {
        flex: 4;
        padding: 0 30px;
        position: relative;
        .cover {
          width: 60%;
          position: absolute;
          top: 40px;
          left: 0;
          right: 0;
          margin: auto;
          z-index: 1;
          transition: all 500ms;
          .title {
            transition: all 1000ms;
            .t_wrap {
              transition: all 1000ms;
              &:hover {
                transform: scale(1.1);;
                cursor: pointer;
              }

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

          }
          .layout {
            width: 408px;
            position: relative;
            transform: scale(1.2);
            top: 20px;
            //animation: shankMovie 800ms ease-in-out;
            //@keyframes shankMovie {
            //  0% {
            //    transform: translateY(100px) scale(0.1);
            //  }
            //  70% {
            //    transform: scale(1.5);
            //  }
            //  100% {
            //    transform: scale(1.2);
            //  }
            //}
            .c_shank {
              transition: all 600ms;
              width: 190px;
              height: 154px;
              position: absolute;
              transform: scale(1);
              top: -50px;
              left: 120px;
              background: url('../assets/handShank.png');
              background-size: 100% 100%;
              animation: changeSmall 500ms;
              animation-delay: 6s;
              @keyframes changeSmall {
                0% {
                  top: 34rem;
                  left: -17rem;
                  transform: scale(5) rotate(2deg);
                }
                100% {
                  top: -50px;
                  left: 120px;
                  transform: scale(1) rotate(0deg);
                }
              }
            }
            .c_circle {
              transition: all 1000ms;
              width: 408px;
              height: 97px;
              position: absolute;
              transform: scale(1.2);
              top: -30px;
              left: 0;
              background: url('../assets/circleball.png');
              background-size: 100% 100%;
            }
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
              margin-left: 20px;
              margin-bottom: 26px;
              position: relative;
              a {
                position: absolute;
                top: 20px;
                right: 10px;
                font-size: 14px;
                color: rgba(255,255,255, 0.5);
              }
            }
            .category {
              width: inherit;
              .c_item {
                border-right: 1px solid rgba(255,255,255, 0.2);
                text-align: center;
                &:last-child {
                  border-right: none;
                }
                & > span {
                  font-size: 14px;
                  color: rgba(255,255,255, .8);
                }
                p {
                  margin-bottom: 10px;
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
        padding-right: 30px;
        min-width: 300px;
      }
    }
  }
}
</style>
