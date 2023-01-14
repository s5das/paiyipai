<template>
    <div class="main">
        <div class="head">健康测试</div>
        <uni-section class="mb-10" title="问题" type="line"></uni-section>
        <div class="question">
            1、请问你是否有夜间睡觉手心出汗的症状？
        </div>
        <div class="foot">
            <button>是</button>
            <button>否</button>
        </div>
    </div>
</template>

<script lang="ts" setup>

</script>

<style lang="less" scoped>
.main {
    background-color: #fafafa;
    height: 100vh;
    padding: 20rpx;

    .head {
        height: 25vh;
        background-color: #5077f7;
        border-radius: 0 0 30% 20%;
        font-weight: 600;
        font-size: 50rpx;
        color: #fff;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 10vh;
    }

    .question {
        height: 30vh;
        background-color: #fff;
        padding: 50rpx;
        font-size: 30rpx;
        font-weight: 600;
    }

    .foot {
        margin-top: 10vh;
        height: 10vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #fff;

        button {
            height: 5vh;
            width: 30vw;
            text-align: center;
            line-height: 5vh;
        }
    }
}
</style>