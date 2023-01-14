<template>
    <div class="main">
        <uni-section title="化验单选择" type="line"></uni-section>
        <div class="pic-chose">

            <view class="box1">
                <uni-file-picker limit="1" @select="select" :image-styles="imageStyles"></uni-file-picker>
            </view>

        </div>

        <uni-section title="指标选择" type="line"></uni-section>
        <div class="choseplace">
            <checkbox-group @change="change">
                <div class="small_item" v-for="(item) in select_group_items" :key="item.name">
                    <label>
                        <checkbox :value="item.value" :checked="select_list.indexOf(item.value) != -1" />{{ item.name }}
                    </label>
                </div>
            </checkbox-group>
        </div>

        <uni-section title="特征填写" type="line"></uni-section>
        <div class="formlist">
            <div class="item" v-for="(item, index) of select_list" :key="index">
                <div class="brief_content" @click="handle_show(item)">
                    <div class="content">
                        {{ select_group_items[parseInt(item)].name }}
                    </div>
                    <div class="icon">
                        <uni-icons type="bottom" size="20"></uni-icons>
                    </div>
                </div>

                <div class="detail_content" v-if="select_group_items[item].show">
                    <div class="item2" v-for="(item2, index) of select_group_items[item].child" :key="index">
                        <div class="item2-label">{{ item2.name }}</div>
                        <div class="item2-input"><input v-model="item2.value" type="text"
                                style="padding:0.25vh;font-size:2vh"></div>
                    </div>
                </div>
            </div>
        </div>
        <div class="btn-area">
            <button @click="submit">提交</button>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { Ref } from 'vue';
let select_list: Ref<string[]> = ref([])
let select_group_items = reactive([
    {
        name: "血常规",
        value: "0",
        child: [
            {
                name: '红细胞计数',
                value: ''
            },
            {
                name: '血红蛋白',
                value: ''
            },
            {
                name: '白细胞',
                value: ''
            },
            {
                name: '白细胞分类计数',
                value: ''
            },
            {
                name: '血小板',
                value: ''
            }
        ],
        show: false
    },
    {
        name: "肝功能",
        value: "1",
        child: [
            {
                name: '谷丙转氨酶',
                value: ''
            },
            {
                name: '谷丙转氨酶',
                value: ''
            },
            {
                name: '谷氨酰转移酶',
                value: ''
            },
            {
                name: '碱性磷酸酶',
                value: ''
            },
            {
                name: '总胆红素',
                value: ''
            },
            {
                name: '直接胆红素',
                value: ''
            },
            {
                name: '间接胆红素',
                value: ''
            },
            {
                name: '乳酸脱氢酶',
                value: ''
            },
            {
                name: '白蛋白',
                value: ''
            }
        ],
        show: false
    },
    {
        name: "血糖",
        value: "2",
        child: [
            {
                name: '血糖',
                value: ''
            }
        ],
        show: false
    },
    {
        name: "血脂",
        value: "3",
        child: [
            {
                name: '血脂',
                value: ''
            }
        ],
        show: false
    }
])

let imageStyles = {
    width: 128,
    height: 128,
    border: {
        color: "#5473f6",
        width: 2,
        style: 'solid',
        radius: '20px'
    }
}

const select = () => {

    uni.showLoading({
        title: '信息提取中',
        mask: true
    })
    setTimeout(() => {
        select_list.value = ["0", "1"]
        select_group_items[0].child = [
            {
                name: '红细胞计数',
                value: '24'
            },
            {
                name: '血红蛋白',
                value: '420'
            },
            {
                name: '白细胞',
                value: '420'
            },
            {
                name: '白细胞分类计数',
                value: '24'
            },
            {
                name: '血小板',
                value: '564'
            }
        ]
        select_group_items[1].child = [
            {
                name: '谷丙转氨酶',
                value: '420'
            },
            {
                name: '谷丙转氨酶',
                value: '240'
            },
            {
                name: '谷氨酰转移酶',
                value: '420'
            },
            {
                name: '碱性磷酸酶',
                value: '504'
            },
            {
                name: '总胆红素',
                value: '24'
            },
            {
                name: '直接胆红素',
                value: '20'
            },
            {
                name: '间接胆红素',
                value: '50'
            },
            {
                name: '乳酸脱氢酶',
                value: '40'
            },
            {
                name: '白蛋白',
                value: '30'
            }
        ]
        uni.hideLoading()
        uni.showToast({
            title: '提取成功'
        })
    }, 3000)
}






type Detail = {
    detail: { value: string[] }
}

const change = ({ detail }: Detail) => {
    select_list.value = detail.value
    console.log(detail.value);
}

const handle_show = (item: string) => {
    select_group_items[parseInt(item)].show = !select_group_items[parseInt(item)].show
}

const submit = () => {
    uni.navigateTo({
        url: '/pages/judge/index'
    })
}
</script>

<style lang="less" scoped>
.main {
    height: 100vh;
    overflow-y: scroll;
    background-color: #fafafa;
    padding: 15rpx;

    .mb-10 {
        font-size: 60rpx;
    }

    .pic-chose {
        background-color: #fff;
        height: 30vh;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 20rpx;
        margin-bottom: 5vh;

        .box1 {
            height: 20vh;
            font-weight: 600;
        }
    }

    .choseplace {
        background-color: #fff;
        border-radius: 20rpx;
        margin-bottom: 5vh;
    }

    .formlist {
        background-color: #fff;
        border-radius: 20rpx;

        .item {
            margin: 2vh auto;
            margin-top: 0;

            .brief_content {
                height: 4vh;
                width: 80vw;
                border: 0.5px solid #000;
                border-radius: 20rpx;
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding: 0 5vw;
            }

            .item2 {
                display: flex;
                height: 3.5vh;
                justify-content: space-around;
                align-items: center;
                margin-bottom: 10rpx;

                .item2-label {
                    height: 2.5vh;
                    width: 30vw;
                }

                .item2-input {

                    height: 2.5vh;
                    width: 30vw;
                    border: 1rpx solid #bbb;
                    border-radius: 10rpx;
                }
            }
        }
    }

    .btn-area {
        height: 10vh;
        display: flex;
        justify-content: center;
        align-items: center;

        button {
            height: 6vh;
            width: 100%;
            background-color: #71c1e7;
        }
    }
}

.items-enter-active {
    animation: come_out 1s;
}

.items-leave-active {
    animation: come_out 1s reverse;
}

@keyframes come_out {
    from {
        transform: translateX(-100%);
    }

    to {
        transform: translateX(0);
    }
}
</style>