<template>
    <view class="page">
        <view class="money-con">
            <u-image mode="aspectFill" border-radius="10rpx" src="https://yiqiwang360.com/images/yiqiguanjia/luo.png" width="300"
                     height="180"></u-image>
            <view class="money-desc">
                <view class="title">企业所得税</view>
                <text class="gray">您的需求，我们来服务</text>
                <u-button :customStyle="call" shape="circle" class="u-margin-top-40">立即咨询</u-button>
            </view>
        </view>
        <view class="money-con">
            <u-image mode="aspectFill" border-radius="10rpx" src="https://yiqiwang360.com/images/yiqiguanjia/lan.png" width="300"
                     height="180"></u-image>
            <view class="money-desc">
                <view class="title">个体工商户</view>
                <text class="gray">您的需求，我们来服务</text>
                <u-button :customStyle="call" shape="circle" class="u-margin-top-40">立即咨询</u-button>
            </view>
        </view>
        <view class="money-con">
            <u-image mode="aspectFill" border-radius="10rpx" src="https://yiqiwang360.com/images/yiqiguanjia/luo.png" width="300"
                     height="180"></u-image>
            <view class="money-desc">
                <view class="title">中小微企业</view>
                <text class="gray">您的需求，我们来服务</text>
                <u-button :customStyle="call" shape="circle" class="u-margin-top-40">立即咨询</u-button>
            </view>
        </view>
        <view class="money-con">
            <u-image mode="aspectFill" border-radius="10rpx" src="https://yiqiwang360.com/images/yiqiguanjia/luo.png" width="300"
                     height="180"></u-image>
            <view class="money-desc">
                <view class="title">智能申报</view>
                <text class="gray">您的需求，我们来服务</text>
                <u-button :customStyle="call" shape="circle" class="u-margin-top-40">立即咨询</u-button>
            </view>
        </view>
        <view class="money-con">
            <u-image mode="aspectFill" border-radius="10rpx" src="https://yiqiwang360.com/images/yiqiguanjia/luo.png" width="300"
                     height="180"></u-image>
            <view class="money-desc">
                <view class="title">纳税筹划服务</view>
                <text class="gray">您的需求，我们来服务</text>
                <u-button :customStyle="call" shape="circle" class="u-margin-top-40">立即咨询</u-button>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                call:{
                    width:'160rpx',
                    height:'45rpx',
                    color:'white',
                    marginTop:'50rpx',
                    background:'#E2261A'
                },

            }
        },
        //下拉刷新
        onPullDownRefresh() {
            setTimeout(function () {
                uni.stopPullDownRefresh();
            }, 1000);
        },
    }
</script>
<style lang="scss">
    page {
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
.money-con{
    background:white;
    border-radius: 10rpx;
    width:90%;
    height: 200rpx;
    padding:20rpx;
    margin:30rpx auto;
    display: flex;
    flex-direction: row;
    .money-desc{
        margin-left: 30rpx;
        .title{
            font-size: 32rpx;
            font-weight: 700;
        }
        .gray{
            color:#525252;
        }
    }
}
</style>