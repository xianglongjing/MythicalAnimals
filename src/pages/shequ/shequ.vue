<template>
    <view class="page">
<!--        <uni-nav-bar :status-bar="true" left-icon="back" :fixed="true" :border="false" :shadow="false" @clickLeft="goBack">-->
<!--            <view class="inline-block u-border-bottom" style="width:100%;padding:20rpx">-->
<!--            </view>-->
<!--        </uni-nav-bar>-->
        <view class="bg" :style="bg">
           <view class="bg-con">
               <view class="big u-margin-bottom-20">合作园区</view>
               <text class="title">合作园区·一个有生意的社区</text>
<!--               <view class="more">-->
<!--                   <text>了解更多</text>-->
<!--                   <text class="cuIcon-right"></text>-->
<!--               </view>-->
           </view>
        </view>
        <view class="slide">
            <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
                <view id="demo1" class="scroll-view-item_H" :style="lan">
                    <view class="title">兰山</view>
                    <text>共1个社区</text>
                </view>
                <view id="demo2" class="scroll-view-item_H" :style="luo">
                    <view class="title">罗庄</view>
                    <text>共2个社区</text>
                </view>
                <view id="demo3" class="scroll-view-item_H" :style="he">
                    <view class="title">河东</view>
                    <text>共3个社区</text>
                </view>
                <view id="demo1" class="scroll-view-item_H" :style="ling">
                    <view class="title">兰陵</view>
                    <text>共1个社区</text>
                </view>
            </scroll-view>
        </view>
        <view class="content u-margin-top-40 u-padding-top-20">
            <u-tabs :list="list" :is-scroll="false" :current="current" @change="change" active-color="#fd5123">
            </u-tabs>
            <view v-if="current === 0">
                <view class="con-item" @click="detail">
                <u-image mode="aspectFill" src="../../static/image/yigao.png" border-radius="10" width="100%"
                         height="400"></u-image>
                <view class="desc">
                    <view class="title">兰山颐高上海街</view>
                    <view class="text-gray">临沂市兰山区颐高上海街A座</view>
                    <view class="num">77剩余工位
                        <text class="u-padding-left-20">|</text>
                        <text class="u-padding-left-20">18入驻企业</text>
                    </view>
                    <view class="price">￥
                        <text class="u-font-30">1888</text>
                        /月起
                    </view>
                    <u-button :customStyle="see" shape="square">预约参观</u-button>
                </view>
                </view>
                <view class="con-item">
                    <u-image mode="aspectFill" src="../../static/image/yigao.png" border-radius="10" width="100%"
                             height="400"></u-image>
                    <view class="desc">
                        <view class="title">兰山颐高上海街</view>
                        <view class="text-gray">临沂市兰山区颐高上海街A座</view>
                        <view class="num">77剩余工位
                            <text class="u-padding-left-20">|</text>
                            <text class="u-padding-left-20">18入驻企业</text>
                        </view>
                        <view class="price">￥
                            <text class="u-font-30">1888</text>
                            /月起
                        </view>
                        <u-button :customStyle="see" shape="square">预约参观</u-button>
                    </view>
                </view>
            </view>

        </view>

    </view>
</template>

<script>
    export default {
        data(){
            return {
                see:{
                    background:'#fd5123',
                    width:'160rpx',
                    height:'55rpx',
                    color:'white',
                    fontSize:'26rpx',
                    position:'absolute',
                    bottom:'10rpx',
                    right:'60rpx'
                },
                bg: {
                    backgroundImage: "url(" + require("../../static/image/shequbg.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 450rpx",
                    margin:'0rpx auto',
                    borderRadius:"10rpx"
                },
                lan: {
                    backgroundImage: "url(" + require("../../static/image/lan.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "200rpx auto",
                    borderRadius:"10rpx"
                },
                luo: {
                    backgroundImage: "url(" + require("../../static/image/luo.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "200rpx auto",
                    borderRadius:"10rpx"
                },
                he: {
                    backgroundImage: "url(" + require("../../static/image/hedong.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "200rpx auto",
                    borderRadius:"10rpx"
                },
                ling: {
                    backgroundImage: "url(" + require("../../static/image/lanling.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "200rpx auto",
                    borderRadius:"10rpx"
                },
                list: [{
                    name: '全部'
                }, {
                    name: '兰山'
                }, {
                    name: '罗庄'
                },{
                    name: '河东'
                }, {
                    name: '兰陵'
                }, {
                    name: '沂南'
                },{
                    name: '沂水'
                },  ],
                current: 0
            }
            },

        methods:{
            change(index) {
                this.current = index;
            },
            detail(){
                uni.navigateTo({
                    url:'/pages/shequ/shequDetail'
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
    width:100%;
    height:500rpx;
    .bg-con{
        color:white;
        padding:20rpx 40rpx;
        .big{
            font-size: 45rpx;
            text-align: center;
        }
        .title{
            font-size: 30rpx;
            line-height: 60rpx;
        }
        .more{
            margin-top: 60rpx;
            width:130rpx;
            border:1rpx solid white;
            padding:3rpx 0;
            text-align: center;
            font-size: 22rpx;
        }
    }
}
    .slide{
        display: flex;
        align-items: center;
        justify-content: center;
        background: white;
        box-shadow: 0px 2rpx 5px #888888;
        width:100%;
        height:200rpx;
        border-radius: 12rpx;
        position: absolute;
        top:340rpx;
        left:30rpx;
        .scroll-view_H {
            flex: 1;
            white-space: nowrap;
            padding-right: 100rpx;
        }
        .scroll-view-item {
            text-align: center;
            font-size: 36rpx;
        }
        .scroll-view-item_H {
            display: inline-block;
            line-height: 41rpx;
            height: 140rpx;
            background-color: #fcefe6;
            border-radius: 20rpx;
            font-size: 24rpx;
            color: white;
            padding: 50rpx 20rpx;
            margin:0 20rpx;
            vertical-align: middle;
            .title{
                font-size: 30rpx;
            }
            text{
                font-size: 26rpx;
            }
        }
    }
    .content{
        height:auto;
        .con-item{
            padding:0 0 20rpx;
            border-radius: 10rpx;
            width:92%;
            background: white;
            margin:30rpx auto;
            .desc{
                position: relative;
                padding:10rpx 30rpx 0;
                .title{
                    line-height: 50rpx;
                    font-size: 30rpx;
                    font-weight: 1000;
                }
                .num{
                    color:#A2A2A2;
                    line-height: 50rpx;
                }
                .price{
                    color:#fd5123;
                    line-height: 60rpx;
                }
            }
        }
    }
</style>