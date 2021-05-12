<template>

    <view class="page">
        <view class="success">
            <image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/dui.png"></image>
            <view class="yu">您的预约请求已发送</view>
        </view>
        <view class="form">
            <view class="content">
                <text>预约城市</text>
                <text>临沂兰山</text>
            </view>
            <view class="content">
                <text>预约日期</text>
                <text>2021-03-10</text>
            </view>
        </view>
        <u-button :custom-style="back" @click="backs">返回</u-button>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                back:{
                    width:'90%',
                    margin:'100rpx auto',
                    height:'70rpx'
                }
            }
        },
        methods:{
            backs(){
            uni.navigateTo({
                url:'/pages/visit/visitDetail'
            })
        }
        }

    }
</script>
<style lang="scss">
    page {
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
.success{
    background: white;
    margin-top: 20rpx;
    padding:80rpx 0;
    width:100%;
    text-align: center;
    image{
        width:150rpx;
        height:150rpx;
    }
    .yu{
        font-size: 35rpx;
        margin-top: 30rpx;
        font-weight: 600;
    }
}
    .form{
        width:100%;
        background:white;
        margin:20rpx 0;
        .content{
            padding:0 20rpx;
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            line-height: 100rpx;
        }
    }
</style>