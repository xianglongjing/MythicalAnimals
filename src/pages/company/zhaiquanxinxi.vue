<template>
    <view class="page u-border-top">
        <view class="zong u-border-bottom" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
            <view class="title">{{item.name}}</view>
            <view class="con">
                <view class="left">
                    <view>
                        <text class="gray">债券代码：</text>
                        <text>{{item.bondcode ? item.bondcode : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">债券类型：</text>
                        <text>{{item.bondtype ? item.bondtype : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">债券发布日期：</text>
                        <text>{{item.issuedate ? item.issuedate : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">上市交易日期：</text>
                        <text>{{item.tradingday ? item.tradingday : '-'}}</text>
                    </view>
                </view>
                <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
            </view>
        </view>
        <u-loadmore
                color="#999999"
                font-size="24"
                margin-bottom="50"
                margin-top="50"
                :status="loadStatus"
                @loadmore="getList"
        ></u-loadmore>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                goodsList:{},
                pageNum:1,
                page:1,
                loadStatus: 'more'
            }
        },
        // 到底部
        onReachBottom () {
            if (this.goodsList.length < this.pageNum * 10) return this.loadStatus = 'more'
            this.pageNum++
            this.getList()
        },
        // 下拉刷新
        onPullDownRefresh () {
            this.pageNum = 1
            // this.pageNum++
            this.getList()
            let that = this
            setTimeout(function() {
                uni.stopPullDownRefresh();
            }, 1000);
            // this.getSearchList(() => {
            //     uni.stopPullDownRefresh()
            // })
        },
        onLoad(options){
            this.getList(options.id)
        },
        methods:{
            async getList (id) {
                const { data: res } = await this.$request({
                    url: 'applets/bond',
                    data: {
                        id:id,
                        page:this.pageNum
                    }
                })

                this.goodsList = {...this.goodsList, ...res}
                console.log(res)
                if (this.goodsList.length < res.total) {
                    this.loadStatus = 'loading'
                } else {
                    this.loadStatus = 'nomore'
                }
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/zhaiquanxinxiD?id='+id
                })
            }
        }
    }
</script>
<style>
    page{
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    .gray{
        color:#959595;
    }
    .zong{
        padding:25rpx;
        background: white;
        .title{
            font-size: 36rpx;
            padding:10rpx 0;
        }
        .con{
            line-height: 50rpx;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
    }

</style>