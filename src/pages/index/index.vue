<template>
  <!-- title -->
  <div class="title">拍医拍智慧医疗平台</div>
  <div class="top">
    <img class="bg1" src="/static/bg1.png">
    <img class="bg1-2" src="/static/frame.png">
    <div class="discribe">精准模型在线识别</div>
  </div>
  <!-- 医疗咨询、化验单智能分析 -->
  <div class="middle1">
    <div class="item" style="background:#c9f4eb ;" @click="handle_predict">
      <div class="discribe">智能识别</div>
      <div class="word">化验单识别</div>
      <img class="bg" src="/static/middle1-1.png" alt="">
    </div>
    <div class="item" style="background:#ffc64b;" @click="goto('/pages/consult/index')">
      <div class="discribe">医疗问诊</div>
      <div class="word">化验单上传</div>
      <img class="bg" src="/static/middle1-2.png" alt="">
    </div>
  </div>
  <!-- 疾病预测 -->
  <div class="middle2">
    <div class="title2">疾病预测</div>
    <div class="more" @click="goto('/pages/more/index')">查看更多></div>
    <div class="line2">
      <div class="item2" v-for="(item, index) in list" :key="index" :style="{ background: item.bg }"
        @click="handle_predict">
        <img class="img2" :src="item.src">
        <div class="describe2">{{ item.describe }}</div>
      </div>
    </div>
  </div>
  <!-- 疾病自测 -->
  <div class="middle3">
    <div class="title3">健康自测</div>
    <div class="box3">
      <div class="item3" @click="goto('/pages/test/index')" :style="{ width: (index % 3) == 0 ? '85vw' : '40vw' }"
        v-for="(item, index) in list2" :key="index">
        <div class="head">{{ item.describe }}</div>
        <div class="describe3">
          <div>{{ item.person }}</div>
          <div style="color:#bbb">人测过</div>
        </div>
        <img :src="item.src" class="img3">
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
let { height, top } = uni.getMenuButtonBoundingClientRect()
let height_1 = height + 'px';
let top_1 = top + 'px';

interface ItemList {
  src: string
  describe: string
  bg: string
}

interface ItemList2 {
  src: string
  describe: string
  person: number
}
let list: ItemList[] = [
  { src: '/static/list1.png', describe: '肝脏科', bg: '#d6e1fd' },
  { src: '/static/list2.png', describe: '肾脏科', bg: '#fef4e8' },
  { src: '/static/list3.png', describe: '神经科', bg: '#d0f1de' },
  { src: '/static/list4.png', describe: '血液疾病', bg: '#fad297' },
]
let list2: ItemList2[] = [
  { src: '/static/list2-1.png', describe: '抑郁测评专业版', person: 25 },
  { src: '/static/list2-2.png', describe: '失眠程度测评', person: 25 },
  { src: '/static/list2-3.png', describe: '自闭症测评', person: 25 },
]

const goto = (path: string) => {
  uni.navigateTo({ url: path })
}
const handle_predict = () => {
  uni.switchTab({ url: '/pages/service/index' })
}
</script>

<style lang="less" scoped>
.top {
  height: 30vh;
  width: 100vw;
  position: relative;

  .bg1 {
    height: 30vh;
    width: 100vw;
  }

  .bg1-2 {
    height: 15vh;
    width: 50vw;
    position: absolute;
    bottom: -15rpx;
    right: 20rpx;
  }

  .discribe {
    position: absolute;

    top: 15vh;
    font-size: 45rpx;
    font-weight: 600;
    color: #fff;
    left: 5vw;
  }
}

.title {
  position: fixed;
  z-index: 10;
  top: v-bind(top_1);
  height: v-bind(height_1);
  left: 5vw;
  line-height: v-bind(height_1);
  color: #fff;
  font-weight: 600;
}

.middle1 {
  height: 13vh;
  width: 100vw;
  display: flex;
  justify-content: space-around;
  margin-top: 5vh;

  .item {
    width: 45vw;
    height: 13vh;
    border-radius: 15rpx;
    position: relative;

    .discribe {
      font-size: 35rpx;
      position: absolute;
      color: #fff;
      font-weight: 600;
      top: 3vh;
      left: 2vw;
      z-index: 11;
    }

    .word {
      position: absolute;
      color: #fff;
      font-weight: 600;
      top: 7vh;
      left: 2vw;
      z-index: 11;
    }

    .bg {
      margin-left: 25vw;
      margin-top: 5vh;
      height: 8vh;
      width: 20vw;
    }
  }
}

.middle2 {
  width: 100vw;
  margin-top: 5vh;
  position: relative;

  .more {
    font-size: 35rpx;
    font-weight: 600;
    position: absolute;
    right: 20rpx;
    top: 5rpx;
  }

  .title2 {
    font-size: 40rpx;
    font-weight: 600;
    margin-left: 5vw;
    margin-bottom: 2vh;
  }

  .line2 {
    width: 90vw;
    margin: 0 auto;
    display: flex;
    justify-content: space-around;

    .item2 {
      height: 12vh;
      width: 20vw;
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: center;
      border-radius: 10rpx;
      box-shadow: 5rpx 5rpx 5rpx #bbb;

      .img2 {
        height: 6vh;
        width: 15vw;
      }

      .discribe2 {
        height: 3vh;

      }
    }
  }
}

.middle3 {
  margin-top: 5vh;

  .title3 {
    font-size: 40rpx;
    font-weight: 600;
    margin-left: 5vw;
    margin-bottom: 2vh;
  }

  .box3 {
    width: 90vw;
    margin: 0 auto;
    display: flex;
    justify-content: space-around;
    flex-flow: wrap;

    .item3 {
      height: 15vh;
      position: relative;
      box-shadow: 5rpx 5rpx 5rpx #bbb;
      border-radius: 15rpx;
      margin-bottom: 15rpx;

      .describe3 {
        display: flex;
        margin-top: 25rpx;
      }

      .head {
        margin-top: 2vh;
        font-size: 35rpx;
      }

      .img3 {
        position: absolute;
        z-index: -1;
        bottom: 0;
        right: 0;
        height: 80%;
        width: 50%;
      }
    }

  }

}
</style>