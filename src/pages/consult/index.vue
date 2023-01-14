<template>
    <div class="main">
        <div class="describe">
            <div class="title1">请详细描述您的症状</div>
            <div class="inputarea">
                <textarea class="textarea" v-model="txt" placeholder-style="color:#93dbd6;" style="width:100%"
                    placeholder="为了更好的获取医生帮助，请尽可能详细描述症状"></textarea>
            </div>
        </div>
        <div class="photo">
            <div class="title2">上传化验单照片</div>
            <div class="photoarea">
                <uni-section title="选择图片" type="line">
                    <view class="example-body">
                        <uni-file-picker limit="9" title="最多选择9张图片" @select="select"></uni-file-picker>
                    </view>
                </uni-section>
            </div>
        </div>
        <div class="user">
            <div class="title3">就诊用户</div>
            <div class="info" v-if="userinfo">
                <img class="avatar" :src="userinfo.avatarUrl">
                <div class="nickname">
                    {{ userinfo.nickName }}
                </div>
            </div>
            <div class="buttonarea" v-if="!userinfo">
                <button @click="getinfo">点击登录</button>
            </div>
        </div>
    </div>
    <div class="command">
        <button class="cancel" @click="cancel">取消</button>
        <button class="submit" @click="submit">提交</button>
    </div>
    <uni-popup ref="popup" background-color="#fff" @change="change">
        <div
            style="display: flex;justify-content: center;height: 8vh;align-items: center;font-weight: 600;font-size: 40rpx;">
            上传成功
        </div>
    </uni-popup>
</template>

<script lang="ts" setup>
import { Ref } from 'vue'

interface UserInfo {
    avatarUrl: string
    nickName: string
}
let userinfo: Ref<UserInfo | undefined> = ref(undefined)

if (uni.getStorageSync('userinfo')) {
    userinfo.value = JSON.parse(uni.getStorageSync('userinfo'))
}

let txt = ref("")

const select = (event: any) => {
    console.log(event);
}

const getinfo = () => {
    uni.getUserProfile({
        desc: "safdsdaf",
        success: (res) => {
            uni.setStorageSync('userinfo', JSON.stringify({ avatarUrl: res.userInfo.avatarUrl, nickName: res.userInfo.nickName }))
            userinfo.value = JSON.parse(uni.getStorageSync('userinfo'))
            console.log(userinfo.value);

        }
    })
}

const cancel = () => {
    uni.switchTab({ url: '/pages/index/index' })
}


let popup: any = ref()

const submit = () => {
    popup.value.open('top')
}

interface ChangeEvent {
    show: true | false
    type: string
}
const change = (event: ChangeEvent) => {
    if (event.show == false) {
        uni.switchTab({ url: '/pages/index/index' })
    }

} 
</script>

<style lang="less" scoped>
.main {
    background-color: #fafafa;
    height: 100vh;
    padding: 20rpx;
}

.describe {
    padding: 20rpx;
    background-color: #fff;
    border-radius: 20rpx;

    .title1 {
        font-size: 40rpx;
        font-weight: 600;
        margin-bottom: 15rpx;
    }

    .inputarea {}
}

.photo {
    padding: 20rpx;
    background-color: #fff;
    border-radius: 20rpx;
    margin-top: 5vh;

    .title2 {
        font-size: 40rpx;
        font-weight: 600;
        margin-bottom: 15rpx;

        .phtotarea {}
    }
}

.user {
    padding: 20rpx;
    background-color: #fff;
    border-radius: 20rpx;
    margin-top: 5vh;

    .title3 {
        font-size: 40rpx;
        font-weight: 600;
        margin-bottom: 15rpx;
    }

    .info {
        display: flex;
        justify-content: space-around;
        align-items: center;
        height: 10vh;

        .avatar {
            height: 100rpx;
            width: 100rpx;
            border-radius: 50rpx;
        }

        .nickname {
            height: 50rpx;
            width: 50rpx;
            font-weight: 600;
            font-size: 40rpx;
        }
    }

    .buttonarea {
        button {
            background-color: #9ededa;
        }
    }
}

.command {
    height: 10vh;
    width: 100%;
    position: fixed;
    bottom: 0;
    display: flex;
    justify-content: space-around;
    align-items: center;
    background-color: #fff;

    .cancel {
        width: 35vw;
        height: 6vh;
        background-color: #e8f2fc;
        color: #6a7ff0;
    }

    .submit {
        width: 35vw;
        height: 6vh;
        background-color: #3c76f1;
        color: #ffffff;
    }
}
</style>