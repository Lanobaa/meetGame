<script setup lang="ts">
import { onMounted } from 'vue';
import Advertise from './Advertise.vue';
import * as echarts from 'echarts/core';
import {GaugeChart} from 'echarts/charts';
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
echarts.use([
  GaugeChart,
  ToolboxComponent,
  LegendComponent,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LabelLayout,
  UniversalTransition,
  CanvasRenderer
]);

onMounted(() => {
  const gaugeData = [
    {
      value: 8000,
      name: '总可用余额',
      title: {
        offsetCenter: ['0%', '-20%'],
        color: '#86909C',
      },
      detail: {
        valueAnimation: true,
        color: '#1D2129',
        fontSize: 24,
        fontWeight: 'bold',
        offsetCenter: ['0%', '12%']
      }
    },
  ];
  const gaugeEcharts = echarts.init(document.getElementById('gaugeEcharts'));
  gaugeEcharts.setOption({
    series: [
      {
        type: 'gauge',
        z: 100,
        startAngle: 90,
        endAngle: -270,
        min: 0,
        max: 12000,
        pointer: {
          show: true,
          showAbove: true,
          width: 10,
          length: '50%',
          icon: 'circle',
          offsetCenter: [0, '-60'],
          itemStyle: {
            color: '#ffffff',
          },
        },
        progress: {
          show: false,
        },
        axisLine: {
          show: false,
        },
        splitLine: {
          show: false,
        },
        axisTick: {
          show: false
        },
        axisLabel: {
          show: false,
        },
        data: gaugeData,
        title: {
          show: false,
          fontSize: 14
        },
        detail: {
          show: false,
        },
        animationDelay: 7900,
      },
      {
        type: 'gauge',
        startAngle: 90,
        endAngle: -270,
        min: 0,
        max: 12000,
        pointer: {
          show: false,
        },
        animationDelay: 7900,
        progress: {
          show: true,
          overlap: false,
          width: 30,
          roundCap: true,
          clip: false,
          itemStyle: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              {
                offset: 0,
                color: 'rgb(145, 62, 223)'
              },
              {
                offset: 1,
                color: 'rgb(114, 49, 205)'
              }
            ]),
            shadowColor: 'rgba(114, 49, 205, 0.5)',
            shadowBlur: 20,
            shadowOffsetY: 0,
            shadowOffsetX: 10,
          }
        },
        axisLine: {
          lineStyle: {
            width: 20,
            color: [[1, '#F0E9FF']]
          }
        },
        splitLine: {
          show: false,
          distance: 0,
          length: 10
        },
        axisTick: {
          show: false
        },
        axisLabel: {
          show: false,
          distance: 50
        },
        data: gaugeData,
        title: {
          fontSize: 14
        },
        detail: {
          width: 90,
          height: 14,
          fontSize: 20,
          color: 'inherit',
          formatter: '$ {value}.00'
        }
      },
    ]
  });
});
</script>

<template>
  <div class="right">
    <div class="company card animateBottomToTop4">
      <div class="title flex flex-row justify-start items-center">
        <span>上海无与伦比科技有限公司</span>
        <a>管理员</a>
      </div>
      <div class="con">
        <p>姓名：王二蛋 <b>已实名认证</b></p>
        <p>账号：1016353</p>
      </div>
    </div>
    <div class="property card animateBottomToTop5">
      <div class="title flex flex-row justify-start items-center">
        <span>我的资产</span>
        <a href=""><img src="../assets/refresh.png" alt=""></a>
      </div>
      <div id="gaugeEcharts" style="margin-top: -25px; width: 250px; height: 250px; margin-left: auto; margin-right: auto;"></div>
      <div class="detail">
        <ul>
          <li class="flex flex-row justify-between items-center">
            <div class="name flex flex-row justify-start items-center">
              <img src="../assets/facebook.png" alt="">
              <span>Facebook</span>
            </div>
            <div class="price">$ 4000.00</div>
          </li>
          <li class="flex flex-row justify-between items-center">
            <div class="name flex flex-row justify-start items-center">
              <img src="../assets/google.png" alt="">
              <span>Google</span>
            </div>
            <div class="price">$ 2000.00</div>
          </li>
        </ul>
        <div class="btn flex flex-row justify-between items-center">
          <a class="pay">充值</a>
          <a class="record">充值记录</a>
        </div>
      </div>
    </div>
    <Advertise />
  </div>
</template>

<style>
.card {
  padding: 30px;
  border-radius: 10px;
  background: white;
  margin-bottom: 30px;
}
</style>
<style lang="less" scoped>
.right {
  padding: 30px 0;
  .company {
    background: url("../assets/bg_bg.png") #fff no-repeat;
    background-size: 100% auto;
    background-position: top right;
    .title {
      white-space: nowrap;
      span {
        font-size: 16px;
        color: #1D2129;
        font-weight: bold;
      }
      a {
        display: block;
        margin-left: 10px;
        border-radius: 5px;
        background: #8633ff;
        background: -moz-linear-gradient(top,  #8633ff 0%, #6c30cb 100%);
        background: -webkit-linear-gradient(top,  #8633ff 0%,#6c30cb 100%);
        background: linear-gradient(to bottom,  #8633ff 0%,#6c30cb 100%);
        color: white;
        font-size: 12px;
        padding: 2px 4px;
      }
    }
    .con {
      margin-top: 20px;
      color: #4E5969;
      font-size: 14px;
      line-height: 26px;
       p b {
         margin-left: 10px;
         color: #00A709;
       }
    }
  }
  .property {
    .title {
      span {
        font-size: 16px;
        color: #1D2129;
        margin-right: 10px;
        font-weight: bold;
      }
    }
    .detail {
      ul {
        li {
          margin-bottom: 10px;
          .name {
            line-height: 24px;
            font-size: 14px;
            span {
              margin-left: 6px;
              color: #4E5969;
            }
          }
          .price { color: #242428; }
        }
      }
      .btn {
        a {
          display: block;
          width: 46%;
          height: 32px;
          line-height: 32px;
          border-radius: 8px;
          text-align: center;
          font-size: 14px;
        }
        .pay {
          background: #FEB22D;
          color: white;
        }
        .record {
          border: 1px solid #6b7280;
        }
      }
    }
  }
}
</style>
