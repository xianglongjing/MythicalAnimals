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
            <view v-if="!this.keyword" class="search-history">
                <view class="se-title">
                    <view class="title-text">历史搜索</view>
                    <view class="clear-btn" @click="clearHistory">
                        <u-icon name="trash" color="#888888" label-color="#888888"
                                label-size="26" label="清空" size="26"></u-icon>
                    </view>
                </view>
                <view class="se-items">
                    <view class="se-item u-border-bottom" v-for="(item,k) in his" :key="k">
                        <u-icon name="clock" color="#333333" label-color="#333333"
                                label-size="28" :label="item" margin-left="10" size="36"></u-icon>
                    </view>
                </view>

            </view>

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
                goodsList:{}
            }
        },
        onNavigationBarSearchInputChanged(e){
            this.keyword = e.text
            //发起请求
            this.pageNum = 0
            this.goSearch()

        },
        onNavigationBarSearchInputConfirmed(e){
            this.keyword = e.text
            //写历史搜索
            this.setHistory()
            //发起请求
            this.pageNum = 0
            this.goSearch()
        },
        onNavigationBarButtonTap(e){
            //写历史搜索
            this.setHistory()
            //发起请求
            this.pageNum = 0
            this.goSearch()

        },
        onLoad (options) {
            //读取历史搜索
            this.his = uni.getStorageSync('searchHistory')
        },
        methods:{
            //写历史搜索
            setHistory(){
                let keyw = [this.keyword]
                let sh = [...uni.getStorageSync('searchHistory'),...keyw]
                uni.setStorageSync('searchHistory',sh)
                this.his = sh
            },
            //清空历史记录
            clearHistory(){
                uni.clearStorageSync('searchHistory')
                this.his = {}
            },
            goSearch(){
                this.getSearchList()
            },
            // onPullDownRefresh() {
            //     this.page = 1
            //     this.goSearch()
            // },
            async getSearchList () {
                const { data: res } = await this.$request({
                    method:'POST',
                    url: 'applets/risk',
                    data: {
                        keyword: this.keyword,
                        page:this.pageNum,
                        type:false
                    }
                })
                console.log(res)
                this.goodsList = res
                if (this.goodsList.length < res.total) {
                    this.loadStatus = 'loadmore'
                }
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
                if(this.type==true){
                    uni.navigateTo({
                        url:'/pages/danger/shopDetail?type=' + type
                    })
                }else{
                    uni.navigateTo({
                        url:'/pages/ll/manDetail?type=' + type
                    })
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