
<template>
    <view class="page">
        <view style="text-align: center;font-size: 35rpx;line-height: 60rpx">兰山颐高上海街社区</view>
        <view class="shop-body">
            <u-swiper :list="list" mode="number" height="400" indicator-pos="bottomRight"></u-swiper>
            <view class="shop-con">
                <view class="title">兰山颐高上海街</view>
<!--                <u-collapse>-->
<!--                    <u-collapse-item :title="item.head" v-for="(item, index) in itemList" :key="index" :open="item.open" :disabled="item.disabled">-->
<!--                        {{item.body}}-->
<!--                    </u-collapse-item>-->
<!--                </u-collapse>-->
                <view class="desc">临沂市兰山区颐高上海街临沂市兰山区颐高上海街临沂市兰山区颐高上海街临沂市兰山区颐高上海街</view>
                <view class="open u-border-bottom u-padding-bottom-40">展开简介 <u-icon name="arrow-down"></u-icon></view>
                <view class="phone u-border-bottom"><u-icon name="phone" color="#888888"></u-icon> <text class="u-padding-left-20">400 036 1717</text> <text class="u-padding-left-30">0539-8100385</text></view>
                <view class="phone u-border-bottom"><u-icon name="map" color="#888888"></u-icon><text class="u-padding-left-20">临沂市兰山区颐高上海街</text></view>
                <view class="page-section page-section-gap">
                    <map style="width: 100%; height: 160px;" :latitude="latitude" :longitude="longitude" :markers="covers">
                    </map>
                </view>
            </view>
        </view>
        <view class="space">
            <text class="title">空间</text>
            <view class="space-item u-border-bottom">
                <view>固定位置</view>
                <view>仅剩 <text class="num">16</text>个</view>
               <view><u-button :customStyle="see" shape="square">预约参观</u-button></view>
            </view>
            <view class="space-item u-border-bottom">
                <view>专属办公室</view>
                <view>仅剩 <text class="num">16</text>个</view>
                <view><u-button :customStyle="see" shape="square">预约参观</u-button></view>
            </view>
            <view class="space-item u-border-bottom">
                <view>会议室</view>
                <view>仅剩 <text class="num">16</text>个</view>
                <view><u-button :customStyle="see" shape="square">预约参观</u-button></view>
            </view>
            <view class="space-item u-border-bottom">
                <view>场地</view>
                <view>仅剩 <text class="num">16</text>个</view>
                <view><u-button :customStyle="see" shape="square">预约参观</u-button></view>
            </view>
        </view>
        <view class="service">
            <view class="title">设施及服务</view>
            <view class="service-con u-margin-top-30">
            <view>
                <u-icon name="checkbox-mark" color="#fd5123"></u-icon>
                交通便利
            </view>
                <view>
                    <u-icon name="checkbox-mark" color="#fd5123"></u-icon>
                    地段繁华
                </view>
                <view>
                    <u-icon name="checkbox-mark" color="#fd5123"></u-icon>
                    环境优美
                </view>
                <view>
                    <u-icon name="checkbox-mark" color="#fd5123"></u-icon>
                    生活便利
                </view>
                <view>
                    <u-icon name="checkbox-mark" color="#fd5123"></u-icon>
                    24小时安保
                </view>
            </view>
        </view>
        <view class="yuanqu">
            <view class="yuan-top">
                <view class="title">园区活动</view>
                <view class="text-gray">更多
                    <text class="cuIcon-right"></text>
                </view>
            </view>
            <view class="slide">
                <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
                    <view id="demo1" class="scroll-view-item_H">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="250" height="180" border-radius="10rpx"></u-image>
                        <view class="name">今日活动今日活动</view>
                        <text>2021/01/30</text>
                    </view>
                    <view id="demo2" class="scroll-view-item_H">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="250" height="180" border-radius="10rpx"></u-image>
                        <view class="name">今日活动今日活动</view>
                        <text>2021/01/30</text>
                    </view>
                    <view id="demo3" class="scroll-view-item_H">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="250" height="180" border-radius="10rpx"></u-image>
                        <view class="name">今日活动今日活动</view>
                        <text>2021/01/30</text>
                    </view>
                    <view id="demo1" class="scroll-view-item_H">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="250" height="180" border-radius="10rpx"></u-image>
                        <view class="name">今日活动今日活动</view>
                        <text>2021/01/30</text>
                    </view>
                </scroll-view>
            </view>
        </view>
        <view class="qiye">
            <view> <text class="title">已入驻企业</text> <text class="text-gray">(10)</text></view>
            <view class="qiye-con">
                <view style="width:200rpx;margin-left: -25rpx">
                    <u-tabs :list="qiye" :is-scroll="false" :current="current" @change="change" active-color="#fd5123">
                    </u-tabs>
                </view>
                <view v-if="current===0">
                    <view class="con-item u-margin-top-20">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="120" height="120"
                                 border-radius="5rpx"></u-image>
                        <view class="con-desc">
                            <view class="flex"><text class="name">公司名称公司名称公司名称</text> <text>兰山</text></view>
                            <view class="u-line-1 type">
                                <view class="u-border-right" style="padding-left: 0">服务雇主 <text class="num">1000家</text></view>
                                <view class="u-border-right">成交额 <text class="num">2000万</text></view>
                                <view>好评率 <text class="num">100%</text></view>
                            </view>
                            <view class="expert">
                                擅长:
                                <text class="u-border-right">LOGO</text>
                                <text class="u-border-right">包装设计</text>
                                <text class="u-border-right">VI设计</text>
                                <text>海报设计</text>
                            </view>
                        </view>
                    </view>
                    <view class="con-item u-margin-top-20">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="120" height="120"
                                 border-radius="5rpx"></u-image>
                        <view class="con-desc">
                            <view class="flex"><text class="name">公司名称公司名称公司名称</text> <text>兰山</text></view>
                            <view class="u-line-1 type">
                                <view class="u-border-right" style="padding-left: 0">服务雇主 <text class="num">1000家</text></view>
                                <view class="u-border-right">成交额 <text class="num">2000万</text></view>
                                <view>好评率 <text class="num">100%</text></view>
                            </view>
                            <view class="expert">
                                擅长:
                                <text class="u-border-right">LOGO</text>
                                <text class="u-border-right">包装设计</text>
                                <text class="u-border-right">VI设计</text>
                                <text>海报设计</text>
                            </view>
                        </view>
                    </view>
                    <view class="con-item u-margin-top-20">
                        <u-image mode="aspectFill" src="../../static/image/yigao.png" width="120" height="120"
                                 border-radius="5rpx"></u-image>
                        <view class="con-desc">
                            <view class="flex"><text class="name">公司名称公司名称公司名称</text> <text>兰山</text></view>
                            <view class="u-line-1 type">
                                <view class="u-border-right" style="padding-left: 0">服务雇主 <text class="num">1000家</text></view>
                                <view class="u-border-right">成交额 <text class="num">2000万</text></view>
                                <view>好评率 <text class="num">100%</text></view>
                            </view>
                            <view class="expert">
                                擅长:
                                <text class="u-border-right">LOGO</text>
                                <text class="u-border-right">包装设计</text>
                                <text class="u-border-right">VI设计</text>
                                <text>海报设计</text>
                            </view>
                        </view>
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
               title: 'map',
               latitude: 35.10474,
               longitude: 118.345154,
               markers: [{
                   width : 40,
                   height: 40,
                   latitude: 35.10474,
                   longitude: 118.345154,
                   iconPath: '../../static/icons/location.png'
               }],
               qiye:[{
                   name:'全部'
               },
                   {
                       name:'成交额'
                   }],
               current:0,
               list: [{
                   image: '../../static/image/yigao.png'
               },
                   {
                       image: 'https://cdn.uviewui.com/uview/swiper/2.jpg'
                   },
                   {
                       image: 'https://cdn.uviewui.com/uview/swiper/3.jpg'
                   }
               ],
               see:{
                   background:'#fd5123',
                   width:'160rpx',
                   height:'55rpx',
                   color:'white',
                   fontSize:'26rpx',
                   position:'absolute',
                   bottom:'30rpx',
                   right:'60rpx'
               },
               itemList: [{
                   head: "赏识在于角度的转换",
                   body: "只要我们正确择取一个合适的参照物乃至稍降一格去看待他人，值得赏识的东西便会扑面而来",
                   open: false,
                   disabled: false
               }],
           }
       },
        methods: {
            change(index) {
                this.current = index;
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
    .page {
        background: #f8f8f8;
    }
.shop-body{
    background: white;
    .shop-con{
        padding:30rpx;
        .title{
            line-height: 50rpx;
            font-size: 30rpx;
            font-weight: 1000;
        }
        .desc{
            color:#888888;
        }
        .open{
            color:#fd5123;
        }
        .phone{
            line-height: 90rpx;
        }
    }
}
    .space{
        background: white;
        margin:40rpx 0;
        padding:30rpx;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
        }
        .space-item{
            position: relative;
            display: flex;
            flex-direction: row;
            align-items: center;
            line-height: 120rpx;
            view{
                font-size: 28rpx;
                flex:1;
                .num{
                    color:#fd5123;
                }
            }
        }
    }
    .service{
        background: white;
        margin:40rpx 0;
        padding:30rpx 0;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
            padding:0 30rpx;
        }
        .service-con{
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            view{
                line-height: 60rpx;
                margin:0 20rpx;
            }
        }
    }
    .yuanqu{
        background: white;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
            padding:0 30rpx;
        }
        .yuan-top{
            display: flex;
            flex-direction: row;
            justify-content: space-between;
        }
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
            border-radius: 20rpx;
            font-size: 24rpx;
            padding: 20rpx 0;
            margin:0 20rpx;
            vertical-align: middle;
            .name{
                font-size: 26rpx;
                font-weight: 1000;
            }
            text{
                color:grey;
                font-size: 24rpx;
            }
        }
    }
    .qiye{
        margin:30rpx 0;
        background: white;
        padding:30rpx;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
        }
        .con-item{
            color:#929292;
            font-size: 23rpx;
            display:flex;
            flex-direction: row;
            padding:20rpx;
            border-radius:9rpx;
            border:1rpx solid whitesmoke;
            .con-desc{
                margin-left:20rpx;
                .flex{
                    display: flex;
                    flex-direction: row;
                    justify-content: space-between;
                }
                .name{
                    padding:0 0 10rpx;
                    color:#000;
                    font-size: 28rpx;
                    font-weight: 1000;
                }
                .type{
                    align-items: center;
                    line-height: 50rpx;
                    display: flex;
                    flex-direction: row;
                    view{
                        line-height:30rpx;
                        padding:0 15rpx;
                        flex:1;
                    }
                }
                .num{
                    color:#BAD5E8;
                }
                .expert{
                    text{
                        padding:0 10rpx;
                    }
                }
            }
        }
    }
</style>