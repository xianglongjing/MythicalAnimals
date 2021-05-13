<template>
    <view class="pages">
      <view class="bg" :style="bg">
      </view>
        <view style="height: 200rpx">
        <view class="content">
        <u-image mode="aspectFille" src="https://yiqiwang360.com/images/yiqiguanjia/cardm.png" width="170" height="160"></u-image>
        <view class="con-r">
            <view class="title">医企管家官方挪车码</view>
            <text class="text-gray">优惠价格 仅享一次</text>
<!--            <view class="price">￥ <text class="big">1.00</text></view>-->
            <view class="price">￥ <text class="big">1.00</text></view>
            <u-button :customStyle="buy">立即购买</u-button>
        </view>
        </view>
        </view>
        <view class="up">
            <u-icon name="arrow-up" size="60" color="#666666"></u-icon>
        </view>
        <view class="show">
            <u-divider half-width="50" style="font-weight: bolder;padding:100rpx 0;" color="#000000">解决停车困扰</u-divider>
           <view class="show-con u-margin-top-30">
            <view class="show-item">
             <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/car1.png" width="300rpx" height="200rpx" border-radius="20rpx"></u-image>
                <view>打开医企管家[扫一扫]</view>
                <text>使用医企管家扫码绑定</text>
            </view>
            <view class="show-item">
                <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/car2.png" width="300rpx" height="200rpx" border-radius="20rpx"></u-image>
                <view>确认手机号和车牌号</view>
                <text>确定绑定人的车辆信息</text>
            </view>
               <view class="show-item">
                   <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/car3.png" width="300rpx" height="200rpx" border-radius="20rpx"></u-image>
                   <view>完成车主信息认证</view>
                   <text>车主信息认证成功</text>
               </view>
               <view class="show-item">
                   <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/car4.png" width="300rpx" height="200rpx" border-radius="20rpx"></u-image>
                   <view>张贴使用挪车码</view>
                   <text>虚拟号码联系车主</text>
               </view>
           </view>
        </view>
        <view class="stop">
            <u-divider half-width="50" style="font-weight: bolder;padding:30rpx 0" color="#000000">使用说明</u-divider>
            <view class="stop-item">
                <u-image src="https://yiqiwang360.com/images/yiqiguanjia/stop1.png" width="100%" height="300"></u-image>
                <view>电话通知，随时挪车</view>
            </view>
            <view class="stop-item u-margin-top-50">
                <u-image src="https://yiqiwang360.com/images/yiqiguanjia/stop2.png" width="100%" height="300"></u-image>
                <view>保护隐私，拒绝骚扰</view>
            </view>
        </view>
        <view class="question">
            <u-divider half-width="50" style="font-weight: bolder;padding:30rpx 0" color="#000000">常见问题</u-divider>
            <view class="ques">
                使用医企管家挪车码会产生额外费用吗？
            </view>
            <view class="answer">
                医企管家挪车码是在挪车场中为保护用户车主隐私的产品，除了购买挪车码的费用及在拨叫过程中产生正常的通话资费，没有额外费用。
            </view>
            <view class="ques u-margin-top-60">
                如何使用挪车码？
            </view>
            <view class="answer">
                通过车主服务小程序购买到货后，撕开【挪车码】正面贴纸，贴在静面反光面上，撕开静电贴纸黏在车挡风玻璃上，扫码按照页面提示绑定车牌号、手机号，被妨碍人扫描挪车码可呼叫车主，双方联系方皆为虚拟号码。
            </view>
            <view class="more u-margin-top-50">查看更多问题</view>
        </view>
        <view class="footer">
        <view class="help u-margin-bottom-50">客服帮助</view>
            <u-divider half-width="50" fontSize="35" style="font-weight: bolder;padding:30rpx 0" color="#000000" bg-color="#f8f8f8">挪车服务</u-divider>
        <text class="text-gray">本服务由医企管家提供</text>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                bg: {
                    // backgroundImage: "url(" + require("https://yiqiwang360.com/images/yiqiguanjia/carbg.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 1200rpx",
                    margin:'0rpx auto',
                    borderRadius:"10rpx"
                },
                buy:{
                    background:'#E2261A',
                    color:'white',
                    width:'150rpx',
                    height:'52rpx',
                    fontSize:'25rpx',
                    margin:'0'
                }
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
    background-image: url("https://yiqiwang360.com/images/yiqiguanjia/carbg.png");
    background-size: 750rpx 1200rpx;
    width:100%;
    height: 1200rpx;
}
    .content{
        padding:20rpx 40rpx;
        background: white;
        width:90%;
        height: 240rpx;
        border-radius: 15rpx;
        position: absolute;
        left:40rpx;
        top:1100rpx;
        display: flex;
        flex-direction: row;
        align-items: center;
        .con-r{
            margin-left:60rpx;
            .title{
                font-size: 29rpx;
                color:#000000;
            }
            .price{
                margin-bottom: 10rpx;
                color:#E2261A;
                .big{
                    font-weight: 1000;
                    font-size: 32rpx;
                }
            }
        }
    }
    .up{
        text-align: center;
    }
    .show{
        background:white;
        width:90%;
        margin:20rpx;
        padding:30rpx 0;
        .show-con{
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            .show-item{
                padding:0 18rpx;
                margin:0 0 40rpx;
                text{
                    color:#AFAFAF;
                    font-size: 26rpx;
                }
            }
        }

    }
    .stop{
        background:white;
        width:90%;
        margin:20rpx;
        padding:0 20rpx;
        .stop-item{
            text-align: center;
            color:#727272;
            line-height: 80rpx;
        }
    }
    .question{
        background:white;
        width:90%;
        margin:20rpx;
        padding:0 20rpx;
        .ques{
            font-weight: 700;
        }
        .answer{
            color:#676767;
            font-size: 25rpx;
        }
        .more{
            text-align: center;
            line-height: 80rpx;
        }
    }
    .footer{
        text-align: center;
        padding:30rpx 0;
        .help{
            color:#E2261A;
        }
    }
</style>