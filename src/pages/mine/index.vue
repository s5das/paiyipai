<template >
    <div class="main">
        <div class="head">
            <div class="info">
                <div class="userinfo" v-if="avatarUrl">
                    <div class="avatar">
                        <img :src="avatarUrl">
                    </div>
                    <div class="name">
                        {{ nickName }}
                    </div>
                </div>
                <div class="holdplace" v-if="!avatarUrl" @click="getinfo">
                    点击此处登录
                </div>
            </div>

        </div>


        <div class="list">
            <div class="item" v-for="(item, index) of list" @click="listhandle(index)">
                <div class="title">{{ item }}</div>
                <div class="arrow">></div>
            </div>
        </div>
    </div>

</template>
<script lang="ts" setup>
import { onShow } from '@dcloudio/uni-app';

let avatarUrl = ref("")
let nickName = ref("")
let list = [
    '咨询历史',
    '退出登录'
]

onShow(() => {

    interface UserInfo {
        avatarUrl: string
        nickName: string
    }

    let userInfo: UserInfo | undefined = JSON.parse(uni.getStorageSync('userinfo'))
    if (userInfo) {
        nickName.value = userInfo.nickName
        avatarUrl.value = userInfo.avatarUrl
    }

})
const listhandle = (index: number) => {
    if (index == 1) {
        uni.clearStorageSync()
        nickName.value = ""
        avatarUrl.value = ""
    }
}
const getinfo = () => {
    uni.getUserProfile({
        desc: "safdsdaf",
        success: (res) => {
            uni.setStorageSync('userinfo', JSON.stringify({ avatarUrl: res.userInfo.avatarUrl, nickName: res.userInfo.nickName }))
            nickName.value = res.userInfo.nickName
            avatarUrl.value = res.userInfo.avatarUrl

        }
    })
}
</script>
<style lang="less" scoped>
.main {
    background-color: #fafafa;
    height: 100vh;

    .head {
        height: 30vh;
        background-color: #5077f7;
        padding-top: 10vh;
        border-radius: 0 0 30rpx 40rpx;


        .info {
            height: 15vh;
            width: 30vw;
            margin: 0 auto;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;

            .userinfo {
                height: 15vh;
                width: 30vw;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;

                .avatar {
                    height: 120rpx;
                    width: 120rpx;
                    border-radius: 50%;

                    image {
                        height: 100%;
                        width: 100%;
                    }
                }

                .name {
                    height: 5vh;
                    font-size: 30rpx;
                    font-weight: 600;
                    color: #fff;
                }
            }

        }

        .holdplace {
            height: 5vh;
            font-size: 30rpx;
            font-weight: 600;
            color: #fff;

        }
    }



    .list {
        margin-top: 10vh;
        width: 100vw;

        .item {
            height: 6vh;
            display: flex;
            justify-content: space-around;
            align-items: center;
            background-color: #fff;
            border-bottom: 1rpx solid #bbb;

            .title {
                font-size: 30rpx;
            }

            .arrow {
                font-size: 30rpx;
                font-weight: 600;
            }
        }
    }
}
</style>