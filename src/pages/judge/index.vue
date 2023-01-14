<template>
    <div class="main">
        <div class="head">
            结果分析
        </div>

        <div class="body">
            时间回到 1999 年，接入因特网不久的中国政府有意使用 Linux，可 Linux 重要贡献者、开源运动旗手 Eric Raymond
            对此公开表达了消极甚至反对的态度，他因刚发表的新书《大教堂与集市》而名声大噪。此时，自由软件信徒崔宝秋正在纽约州立大学石溪分校念博士，他发邮件与 Eric Raymond
            争论，指出开源应无国界，并认为中国政府能够采用 Linux
            的话，会大大推动 Linux 的发展，为社区带来大量的开发者。这封邮件上了 Linux 每周新闻（Linux Weekly News）网站，参与讨论的还有 Richard Stallman——自由软件的精神领袖和
            GNU
            系统、自由软件基金会的创立者。
        </div>
    </div>
</template>

<script lang="ts" setup>

</script>

<style lang="less" scoped>
.main {
    height: 100vh;
    background-color: #fafafa;
    padding: 15rpx;

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
    }

    .body {
        margin-top: 10vh;
        padding: 50rpx;
        background-color: #fff;
        font-size: 35rpx;
        font-weight: 600;
    }
}
</style>