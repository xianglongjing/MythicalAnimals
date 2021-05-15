<template>
    <view class="page">
        <view class="white">
            <uni-nav-bar :status-bar="true" left-icon="back" :fixed="true" :border="false" :shadow="false" @clickLeft="goBack">
                <view class="inline-block u-border-bottom" style="width:100%;padding:20rpx">
                    <u-search
                            :action-style="search_btn"
                            :animation="true"
                            @custom="goSearch"
                            @search="goSearch"
                            bg-color="#f8f8f8"
                            input-align="left" style="width: 560rpx;height:30rpx; padding:30rpx 0;background: #f8f8f8"
                            placeholder="请输入公司名称/人名" shape="square"
                            v-model="keyword"
                    ></u-search>
                </view>
            </uni-nav-bar>
            <u-empty src="http://images.yiqiwang360.com/yiqicha/wujilu.png" class="u-margin-30" :show="emptyShow">
            </u-empty>
            <view class="list u-padding-top-30" v-if="keyword&&emptyShow==false">
                <view style="width:70%;margin:0 auto;text-align: center">
                    <u-tabs
                            :list="list"
                            :current="current"
                            @change="Change" gutter="70"
                            bar-width="50" font-size="30"
                            active-color="#E2291D" bg-color="none" inactive-color="#666666"
                    ></u-tabs>
                </view>
            </view>
<!--            <view v-if="!this.keyword" class="search-history">-->
<!--                <view class="se-title">-->
<!--                    <view class="title-text">历史搜索</view>-->
<!--                    <view class="clear-btn" @click="clearHistory">-->
<!--                        <u-icon name="trash" color="#888888" label-color="#888888"-->
<!--                                label-size="26" label="清空" size="26"></u-icon>-->
<!--                    </view>-->
<!--                </view>-->
<!--                <view class="se-items">-->
<!--                    <view class="se-item u-border-bottom" v-for="(item,k) in his" :key="k">-->
<!--                        <u-icon name="clock" color="#333333" label-color="#333333"-->
<!--                                label-size="28" :label="item" margin-left="10" size="36"></u-icon>-->
<!--                    </view>-->
<!--                </view>-->

<!--            </view>-->

<!--            <view class="sou u-margin-top-50">-->
<!--                <text>最近搜索</text>-->
<!--            </view>-->
<!--            <view class="shops">-->
<!--                <view class="shop" @click="shop">-->
<!--                    <u-image src="http://images.yiqiwang360.com/yiqicha/gongsiming.png" width="60" height="60"></u-image>-->
<!--                    <text>北京锤子数码科技有限公司</text>-->
<!--                </view>-->
<!--                <view class="shop u-margin-left-25" @click="man">-->
<!--                    <u-image src="http://images.yiqiwang360.com/yiqicha/renwu.png" width="60" height="60"></u-image>-->
<!--                    <text>贾跃亭</text>-->
<!--                </view>-->
<!--                <view class="shop" @click="shop">-->
<!--                    <u-image src="http://images.yiqiwang360.com/yiqicha/gongsiming.png" width="60" height="60"></u-image>-->
<!--                    <text>北京锤子数码科技有限公司</text>-->
<!--                </view>-->
<!--                <view class="shop u-margin-left-25" @click="man">-->
<!--                    <u-image src="http://images.yiqiwang360.com/yiqicha/renwu.png" width="60" height="60"></u-image>-->
<!--                    <text>贾跃亭</text>-->
<!--                </view>-->
<!--            </view>-->
        </view>
        <view v-if="current==0&&emptyShow==false">
            <view class="con" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
                <view class="flex">
                    <u-image border-radius="10" height="70" width="70" src="../../static/image/mao.png"></u-image>
                    <text class="u-margin-left-20">{{item.cpyname}}</text>
                </view>
                <view class="u-margin-top-20">
                    <text>风险总数：</text>
                    <text>0条</text>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                his:{},
                emptyShow:false,
                search_btn:{
                   color:'black'
                },
                keyword:'',
                pageNum: 1,
                goodsList:{},
                list: [{
                    name: '公司风险'
                }, {
                    name: '人员风险'
                }],
                current:0
            }
        },
        onLoad (options) {
        },
        methods:{
            detail(id){
                uni.navigateTo({
                    url:'/pages/danger/shopDetail?id='+id
                })
            },
            goSearch(){
                this.getSearchList()
            },
            Change(index) {
                this.current = index;
                // if (index===0){
                //     this.type=true
                // }
                // if (index===1){
                //     this.type=false
                // }
            },
            async getSearchList (id) {
                const { data: res } = await this.$request({
                    method:'POST',
                    url: 'applets/risk',
                    data: {
                        keyword: this.keyword,
                        page:this.pageNum,
                        type:true
                    }
                })
                console.log(res)
                this.goodsList = res
                // //判断全部为空的吸星大法
                let dataNum = res.length
                console.log(dataNum)
                if(this.keyword==''){
                    this.emptyShow = false
                }
                if (dataNum>=1){
                    this.emptyShow = false
                }else{
                    this.emptyShow = true
                }
                if(this.type=true){
                    this.current==0
                }else{
                    this.current==1
                }
            },
            goBack(){
                uni.navigateBack({
                    delta: 1
                });
            },
            shop(){
                uni.navigateTo({
                    url:'/pages/danger/shopDetail'
                })
            },
            man(){
                uni.navigateTo({
                    url:'/pages/danger/manDetail'
                })
            },
        }
    }
</script>
<style>
    page{
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    .white{
        background: white;
        padding:10rpx 30rpx;
        .sou{
            color:#ABABAB;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
    }
    .con{
        line-height: 55rpx;
        padding:30rpx;
        border-radius: 10rpx;
        background: white;
        margin:30rpx;
        .flex{
            align-items: center;
        }
    }
    .shops{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        .shop{
            display: flex;
            flex-direction: row;
            justify-content: center;
            align-items: center;
            border-radius: 5rpx;
            padding:10rpx 20rpx;
            margin:10rpx 0 10rpx 0;
            background-color: #F8F5F7;
            text{
                margin-left:10rpx;
            }
        }
    }
</style>