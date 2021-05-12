

<template>
    <view class="page">
        <view class="uni-tab-bar">
            <view scroll-x class="uni-swiper-tab" autoplay="false">
                <block v-for="(tabBar,index) in tabBars" :key="index" class="flex">
                    <view class="swiper-tab-list" :class="{'active': tabIndex==index}" @tap="toggleTab(index)">
                       <u-image v-if="tabIndex==index" :src="tabBar.src2" width="50" height="50"></u-image>
                        <u-image v-else :src="tabBar.src" width="50" height="50"></u-image>
                        {{tabBar.name}}
                        <view class="swiper-tab-line">
                        </view>
                    </view>
                </block>
            </view>
        </view>
        <!--内容区-->
        <view class="uni-tab-bar" style="height:1000rpx">
            <swiper :current="tabIndex" @change="tabChange" style="height:1000rpx">
                <swiper-item v-for="(item,id) in contentList" :key="item.id">
                    <view class="top">
                    <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/yigao.png" width="200" height="160" border-radius="15"></u-image>
                    <view class="top-r">
                       <view class="title">固定工位</view>
                        <view class="hui">创业公司及小型团队发展</view>
                        <view class="hui">{{item.price}}元/月起</view>
                    </view>
                    </view>
                    <view class="footer">
                        <image src="https://yiqiwang360.com/images/yiqiguanjia/yigao.png"></image>
                        <view class="desc">
                            <view class="flex">{{item.name}}
                                <text class="price">￥
                                    <text class="u-font-35">{{item.price}}</text>
                                    /月起
                                </text>
                            </view>
                            <view>{{item.add}}</view>
                            <view>{{item.seats}}剩余工位
                                <text class="u-margin-left-20">|</text>
                                <text class="u-margin-left-20">18入驻企业</text>
                            </view>
                            <u-button :custom-style="see" @click="go(item.id)">预约参观</u-button>
                        </view>
                    </view>
                </swiper-item>
            </swiper>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                tabIndex: 0,	//选中标签栏的序列
                contentList: [],
                see:{
                    width:'95%',
                    height:'60rpx',
                    color:'white',
                    marginTop:'40rpx',
                    background:'#E71E14'
                },
                huilist:[
                    {   id:1,

                    },
                    {   id:2,

                    },
                    {   id:3,

                    },
                    {   id:4,

                    },
                ],

                tabBars:[
                    {
                        name: '固定工位',
                        id: 'guanzhu',
                        src:'https://yiqiwang360.com/images/yiqiguanjia/icons/hui1.png',
                        src2:'https://yiqiwang360.com/images/yiqiguanjia/icons/red1.png'
                    },
                    {
                        name: '专属办公室',
                        id: 'tuijian',
                        src:'https://yiqiwang360.com/images/yiqiguanjia/icons/hui2.png',
                        src2:'https://yiqiwang360.com/images/yiqiguanjia/icons/red2.png'
                    },
                    {
                        name: '会议室',
                        id: 'redian',
                        src:'https://yiqiwang360.com/images/yiqiguanjia/icons/hui3.png',
                        src2:'https://yiqiwang360.com/images/yiqiguanjia/icons/red3.png'
                    },
                    {
                        name: '场地',
                        id: 'redian',
                        src:'https://yiqiwang360.com/images/yiqiguanjia/icons/hui4.png',
                        src2:'https://yiqiwang360.com/images/yiqiguanjia/icons/red4.png'
                    },
                ],
                swiperHeight: 0

            }

        },
        onLoad(options){
            this.space(options.id);
        },
        methods:{
            toggleTab(index){
                console.log(index)
                this.tabIndex = index
            },
            //滑动切换swiper
            tabChange(e){
                console.log(e.detail)
                const tabIndex = e.detail.current
                this.tabIndex = tabIndex
            },
            // go (id) {
            //
            //     uni.navigateTo({
            //         url: '/pages/visit/success?id=' + id
            //     })
            // },
            async go (id) {
                const { data: res } = await this.$request({
                    method: 'POST',
                    url: '/now',
                    data:{id:id}
                })
                console.log(res)
                uni.navigateTo({
                                url: '/pages/visit/success?id=' + id
                             })
            },
            async space (id,space) {
                const { data: res } = await this.$request({
                    method: 'POST',
                    url: '/space',
                    data:{id:id,space:1}
                })
                console.log(res)
                this.contentList = res.data
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
    .page{
       position: relative;
    }
     .swiper-tab-list{
         display: flex;
         flex-direction: column;
         align-items: center;
       float:left;
         text-align: center;
        margin:30rpx 40rpx;
        color: #969696;
        font-weight: bold;
    }
    .uni-tab-bar .active{
        color: #E02118;
    }

    .active .swiper-tab-line{
        border-bottom: 6upx solid #E02118;
        width: 70upx;
        margin: auto;
        border-radius: 20upx;
    }
    .uni-swiper-tab{
        margin:20rpx 0;
        background: white;
        border-bottom: 1upx solid #eeeeee;
    }
    .top{
        display: flex;
        flex-direction: row;
        align-items: center;
        padding:20rpx;
        width:95%;
        background: white;
        margin:0 auto;
        .top-r{
            padding-left: 20rpx;
            border-left: 5rpx solid #D6D6D6;
            margin-left:20rpx;
            .title{
                font-size: 33rpx;
                font-weight: 550;
                padding:10rpx 0;
            }
            .hui{
                padding:5rpx 0;
            }
        }
    }

    .footer {
        margin:30rpx auto;
        padding-left:30rpx;
        image {
            border-radius: 15rpx;
            width: 95%;
            height: 400rpx;
        }
        .desc{
            padding:30rpx 30rpx 100rpx;
            background: white;
            .flex{
                padding-bottom: 10rpx;
                font-size: 30rpx;
                font-weight: 550;
                display: flex;
                flex-direction: row;
                justify-content: space-between;
                .price{
                    color:#E71E14;
                }
            }
        }
    }
</style>