<template>
    <view class="page">
        <view class="fp-body" @click="detail">
            <view class="name">临沂市铭远企业管理服务有限公司</view>
            <view class="num">企业税号:0123456789</view>
        </view>
        <view class="fp-body" @click="detail">
            <view class="name">临沂市铭远企业管理服务有限公司</view>
            <view class="num">企业税号:0123456789</view>
        </view>
        <view class="line">我是有底线的</view>
        <u-button :customStyle="add" shape="circle">添加抬头</u-button>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                add:{
                    width:'81%',
                    marginTop:'400rpx',
                    color:'white',
                    fontSize:'34rpx',
                    backgroundImage: "url(" + require("../../static/image/redbg.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
            }
        },
        methods:{
            detail(){
                uni.navigateTo({
                    url:'/pages/shequ/fpDetail'
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
.fp-body{
    background: white;
    border-radius: 10rpx;
    margin:30rpx;
    padding:40rpx;
    .name{
        padding:10rpx 0;
        font-size: 37rpx;
        font-weight: 1000;
    }
    .num{
     color:grey;
    }
}
    .line{
        color:grey;
        margin-top:90rpx;
        text-align: center;
    }
</style>