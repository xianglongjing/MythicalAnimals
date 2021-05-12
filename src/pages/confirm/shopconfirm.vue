<template>
    <view class="page">
        <view style="height:400rpx">
        <view class="bgred" :style="bg">
            <view class="title">
                <view>尊敬的用户</view>
                <view>本次申请需要您完成实名认证</view>
            </view>
        </view>
        <view class="card" @click="news">
            <view class="card-l">
                <u-image src="https://yiqiwang360.com/images/yiqiguanjia/icons/moneycard.png" width="80" height="80"></u-image>
                <view class="card-desc">
                    <view class="title">信息验证</view>
                    <view class="gray">只需1步1秒完成</view>
                </view>
            </view>
            <view class="confirm">已认证</view>
        </view>
        </view>
        <view class="paper" @click="card">
            <view class="card-l">
                <u-image src="https://yiqiwang360.com/images/yiqiguanjia/icons/cardpush.png" width="80" height="80"></u-image>
                <view class="card-desc">
                    <view class="title">证件认证</view>
                    <view class="gray">验证个人证件信息</view>
                </view>
            </view>
            <view class="confirm">已认证</view>
        </view>
    </view>
</template>
<script>
    export default {
        data(){
            return {
                bg: {
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 340rpx",
                    margin:'0rpx auto',
                    borderRadius:"10rpx"
                },
                add:{
                    width:'80%',
                    height:'90rpx',
                    marginTop:'200rpx',
                    color:'white',
                    fontSize:'34rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
            }
        },
        methods:{
            news(){
                uni.navigateTo({
                    url:'/pages/confirm/confirm'
                })
            },
            card(){
                uni.navigateTo({
                    url:'/pages/confirm/cardconfirm'
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
.bgred{
    background-size: 750rpx 340rpx;
    background: url("https://yiqiwang360.com/images/yiqiguanjia/redbg.png") no-repeat;
    width:100%;
    height: 300rpx;
    padding:30rpx;
    .title{
        color:white;
        font-size: 35rpx;
    }
}
    .card{
        padding:0 30rpx;
        background: white;
        position: absolute;
        width:90%;
        height: 200rpx;
        border-radius: 10rpx;
        left:30rpx;
        top:200rpx;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        .card-l{
            display: flex;
            flex-direction: row;
            justify-content: center;
            align-items: center;
            .card-desc{
                margin-left:40rpx;
                .title{
                    font-weight: 1000;
                    font-size: 36rpx;
                    padding:10rpx 0 15rpx;
                }
                .gray{
                    color:#9E9E9E;
                }
            }
        }
        .confirm{
            color:#4C4C4C;
            font-size: 35rpx;
        }
    }
.paper{
    margin:30rpx;
    padding:0 30rpx;
    background: white;
    width:90%;
    height: 200rpx;
    border-radius: 10rpx;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    .card-l{
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        .card-desc{
            margin-left:40rpx;
            .title{
                font-weight: 1000;
                font-size: 35rpx;
                padding:10rpx 0 15rpx;
            }
            .gray{
                color:#9E9E9E;
            }
        }
    }
    .confirm{
        color:#4C4C4C;
        font-size: 35rpx;
    }
}
</style>