<template>
    <view class="page">
        <view class="change">
        <u-tabs :list="list" bar-width="100" bg-color="#f8f8f8" :is-scroll="false" :current="current" @change="change" active-color="#fd5123">
        </u-tabs>
        </view>
        <view v-if="current===0">
        <view class="law-body" v-for="(item,index) in law" :key="index">
           <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/lan.png" border-radius="10rpx" width="200" height="160"></u-image>
        <view class="law-desc">
            <view class="name">{{item.name}}</view>
            <text class="text-gray u-font-25">{{item.name }}，{{item.bid}}</text>
            <view class="u-line-1 better">擅长:{{item.gat}}</view>
            <view class="text-gray u-font-25">帮助人数: <text class="num">12345</text>人</view>
            <view class="phone"><u-icon name="phone"></u-icon>
                {{item.phone}}</view>
            <u-button :customStyle="call" shape="circle" style="float:right">立即咨询</u-button>
        </view>
        </view>
        </view>
        <view v-if="current===1">
            <view class="law-body" v-for="(item,index) in lawer" :key="index">
                <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/luo.png" border-radius="10rpx" width="170" height="160"></u-image>
                <view class="law-desc">
                    <view class="name">{{item.bid}}</view>
                    <view class="text-grey u-font-25">{{item.name}} <text class="shu">|</text> 团队规模: <text class="num">
                        {{item.team}}</text>人</view>
                    <view class="address"><u-icon name="map"></u-icon>
                        {{item.address}}</view>
                    <u-button :customStyle="calls" shape="circle">立即咨询</u-button>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                law:[],
                lawer:[],
                list:[{
                    name:'律师服务'
                },
                    {
                        name:'律所服务'
                    },
                ],
                current:0,
                call:{
                    width:'160rpx',
                    height:'45rpx',
                    position:'absolute',
                    left:'260rpx',
                    bottom:'20rpx',
                    color:'white',
                    background:'#E2261A'
                },
                calls:{
                    width:'160rpx',
                    height:'45rpx',
                    position:'absolute',
                    right:'-205rpx',
                    bottom:'35rpx',
                    color:'white',
                    background:'#E2261A'
                }
            }
        },
        onLoad () {
            this.lawList()
            this.lawfirm()
            // this.shopList = shop
        },
        methods: {
            change(index) {
                this.current = index;
            },
            async lawList () {
                const { data: res } = await this.$request({
                    method: 'GET',
                    url: '/attorney',
                })
                console.log(res)
                this.law=res.data
            },
            async lawfirm () {
                const { data: res } = await this.$request({
                    method: 'GET',
                    url: '/lawfirm',
                })
                console.log(res)
                this.lawer=res.data
            },
        }
    }
</script>
<style lang="scss">
    page {
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
.change{
    width:400rpx;
}
    .law-body{
        width:90%;
        border-radius: 15rpx;
        padding:30rpx 20rpx;
        margin:20rpx auto;
        background: white;
        display: flex;
        flex-direction: row;
        .law-desc{
            position: relative;
            margin-left:20rpx;
            .name{
                font-size: 30rpx;
                font-weight: 800;
            }
            .better{
                padding:10rpx 0;
            }
            .num{
                color:#E2261A;
            }
            .phone{
                padding:20rpx 0 0;
            }
            .address{
                color:gray;
                font-size: 25rpx;
                padding:45rpx 0;
            }
            .shu{
                padding:0 10rpx;
            }
        }
    }
</style>