<template>
    <div class="main">
        <div class="item" v-for="(item) in list" @click="handle_predict">{{ item }}</div>
    </div>
</template>

<script lang="ts" setup>

let list = ['肝脏科', '肾脏科', '神经科', '血液疾病']
const handle_predict = () => {
    uni.switchTab({ url: '/pages/service/index' })
}
</script>

<style lang="less" scoped>
.main {
    background-color: #fafafa;
    height: 100vh;
    padding: 20rpx;

    .item {
        height: 5vh;
        background-color: #fff;
        padding: 0.5vh 6vw;
        font-size: 30rpx;
        font-weight: 600;
    }
}
</style>