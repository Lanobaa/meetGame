<script lang="ts" setup>
import {ref} from 'vue';
import one from '../assets/a_1.png';
import two from '../assets/a_2.png';
import three from '../assets/a_3.png';
import four from '../assets/a_4.png';
import five from '../assets/a_5.png';
import six from '../assets/a_6.png';
import seven from '../assets/a_7.png';

const data = ref([
  {
    id: '1',
    label: '日本卡牌测试测试',
    price: '201,100.00',
    icon: one,
  },
  {
    id: '2',
    label: '女士手表测试',
    price: '201,100.00',
    icon: two,
  },
  {
    id: '3',
    label: '皮肤护理测试',
    price: '201,100.00',
    icon: three,
  },
  {
    id: '4',
    label: '球类运动',
    price: '201,100.00',
    icon: four,
  },
  {
    id: '5',
    label: '日本卡牌测试测试',
    price: '201,100.00',
    icon: five,
  },
  {
    id: '6',
    label: '日本卡牌测试测试',
    price: '201,100.00',
    icon: six,
  },
  {
    id: '7',
    label: '球类运动',
    price: '201,100.00',
    icon: seven,
  },
]);
const current = ref(0);
const mouseEnterFn = (index: number) => {
  current.value = index;
};
const mouseLeaveFn = () => {
  current.value = 0;
}
</script>

<template>
  <div class="advertise card animateBottomToTop6">
    <div class="title">投放花费排行</div>
    <ul class="list">
      <li
          v-for="(item, index) in data"
          :key="index"
          @mouseenter="() => mouseEnterFn(index)"
          @mouseleave="mouseLeaveFn"
          :class="[
            'flex',
            'flex-row',
            'justify-start',
            'items-center',
            ((current - 1) === index ? 'animateScale': ''),
          ]"
      >
        <div><img :src="item.icon" alt=""></div>
        <div>
          <span>{{ item.label }}</span>
          <p>$ {{ item.price }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<style lang="less" scoped>
.advertise {
  width: 100%;
  background: white;
  padding: 30px;

  .title {
    font-size: 16px;
    font-weight: bold;
    margin-bottom: 10px;
    color: #1D2129;
  }

  .img {
    width: 100%;
    height: auto;
    margin-bottom: 20px;
  }

  .list {
    padding: 0 20px;
    li:hover {
      transition: all 300ms;
      cursor: pointer;
      transform: scale(1.2);
      transform-origin: center right;
      font-size: 17px;
      & + li {
        font-size: 15px;
        transform: scale(1.1);
        transform-origin: center right;
        & > div > img {
          filter: drop-shadow(10px 0 5px rgba(0,0,0,0.05));
        }
      }
      & > div {
        img {
          filter: drop-shadow(10px 0 5px rgba(0,0,0,0.15));
        }
        span, p { text-shadow: 2px 2px 1px rgba(0,0,0,0.1) };
      }
    }

    li {
      &.animateScale {
        font-size: 15px;
        transform: scale(1.1);
        transform-origin: center right;
        & > div > img {
          filter: drop-shadow(10px 0 5px rgba(0,0,0,0.05));
        }
      }
      padding: 10px 0;
      transition: all 300ms;
      div:first-child {
        margin-right: 10px;

        img {
          display: block;
          width: 39px;
          height: 45px;
        }
      }

      div:last-child {
        span {
          display: block;
          margin-bottom: 4px;
          font-size: 14px;
          color: #4E5969;
        }

        p {
          padding: 0;
          margin: 0;
          font-size: 12px;
          color: #4E5969;
        }
      }
    }
  }
}
</style>
