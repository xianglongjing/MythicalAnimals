<template>
    <view class="page">
       <view class="bg" :style="bg">
       </view>
        <view style="height:270rpx">
        <view class="shop-body">
            <image src="https://yiqiwang360.com/images/yiqiguanjia/icons/yiqi.png" mode="aspectFit" style="width:250rpx;height:100rpx;margin-right:10rpx"></image>
            <view class="body-r">
                <view class="name u-line-1">临沂市铭远企业管理服务有限公司</view>
                <view class="desc">
                    <view class="desc-l">简介:</view>
                    <text>临沂市铭远企业管理服务有限公司公司经营范围包括:商务信息咨询；财务信息咨询等</text>
                </view>
                <view class="phone">
                    <u-icon name="phone" class="u-margin-right-20" size="30"></u-icon>123456789
                </view>
                <view class="gray">
                    <image src="https://yiqiwang360.com/images/yiqiguanjia/icons/wifi.png"></image>
                    www.mingyuanjituan.com
                </view>
                <view class="gray u-margin-top-30">
                   <u-icon name="email" size="30" class="u-margin-right-20"></u-icon>
                    123456789@163.com
                </view>
                <view class="gray">
                    <u-icon name="map" size="30" class="u-margin-right-20"></u-icon>
                    <view class="phone u-line-1">山东省临沂市兰山区金玉山大厦</view>
                </view>
                <view class="gray u-margin-top-40">
                    <view class="u-margin-right-20"></view>
                    <view class="u-line-1">信息由认证企业编辑，<text class="confirm" @click="confirm">去认证 <text class="cuIcon-right"></text></text></view>
                </view>
            </view>

        </view></view>
        <view class="service">
          <view class="ser-top">
              <view class="title">产品/服务</view>
              <view class="edit">编辑该模块信息 <text class="cuIcon-right"></text></view>
          </view>
            <view class="content">
                暂无产品服务信息
            </view>
        </view>
        <view class="service u-margin-top-30">
            <view class="ser-top">
                <view class="title">企业公告</view>
                <view class="edit">编辑该模块信息 <text class="cuIcon-right"></text></view>
            </view>
            <view class="content">
                暂无产品服务信息
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                bg: {
                    // backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 550rpx",
                    margin:'0rpx auto',
                    borderRadius:"10rpx"
                },

            }
        },
        methods:{
            confirm(){
                uni.navigateTo({
                    url:'/pages/confirm/shopconfirm'
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
.bg{
    background-size: 750rpx 550rpx;
    background: url("https://yiqiwang360.com/images/yiqiguanjia/redbg.png") no-repeat;
    width:100%;
    height:400rpx;
    position: relative;
}
    .shop-body{
        background: white;
        border-radius: 20rpx;
        position: absolute;
        top:60rpx;
        left:35rpx;
        width:92%;
        padding:30rpx 10rpx;
        display: flex;
        flex-direction: row;
        .body-r{
            margin-left:10rpx;
            .name{
                font-size: 30rpx;
                font-weight: 700;
            }
            .desc{
                display: flex;
                flex-direction: row;
                padding:10rpx 0;
                .desc-l{
                    width:170rpx;
                    color:gray;
                }
            }
            .phone{
                color:#E64440;
                padding:20rpx 0;
            }
            .gray{
                color:gray;
                display: flex;
                flex-direction: row;
                align-items: center;
                image{
                    width:30rpx;
                    height:30rpx;
                    margin-right: 20rpx;
                }
            }
            .confirm{
                color:#E64440;
            }
        }
    }
    .service{
        background: white;
        width:92%;
        border-radius: 10rpx;
        margin:0 35rpx;
        padding:30rpx 20rpx;
        .ser-top{
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            padding:10rpx 0 30rpx;
            .title{



                font-size: 30rpx;
                font-weight: 800;
            }
            .edit{
                color:#E64440;
            }
        }
        .content{
            background:#F8F9FB;
            border-radius: 5rpx;
            padding:40rpx 0;
            text-align: center;
        }
    }
</style>