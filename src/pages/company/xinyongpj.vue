<template>
    <view class="page u-border-top">
        <view class="flex u-border-bottom" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
            <view>
                <view>
                    <text class="gray">主体等级：</text>
                    <text>{{item.subject ? item.subject : '-'}}</text>
                </view>
                <view>
                    <text class="gray">债券信用等级：</text>
                    <text>{{item.bond ? item.bond : '-'}}</text>
                </view>
                <view>
                    <text class="gray">评级公司：</text>
                    <text>{{item.rating ? item.rating : '-'}}</text>
                </view>
                <view>
                    <text class="gray">评级日期：</text>
                    <text>{{item.ratingdate ? item.ratingdate : '-'}}</text>
                </view>
                <view>
                    <text class="gray">评级展望：</text>
                    <text>{{item.outlook ? item.outlook : '-'}}</text>
                </view>
            </view>
            <u-icon name="arrow-right" size="40" color="#777777"></u-icon>
        </view>
        <u-loadmore
                color="#999999"
                font-size="24"
                margin-bottom="50"
                margin-top="50"
                :status="loadStatus"
                @loadmore="list"
        ></u-loadmore>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                goodsList:{},
                page:1,
                pageNum:1
            }
        },
        // 到底部
        onReachBottom () {
            if (this.list.length < this.pageNum * 10) return this.loadStatus = 'more'
            this.pageNum++
            this.list()
        },
        // 下拉刷新
        onPullDownRefresh () {
            this.pageNum = 1
            // this.pageNum++
            this.list()
            let that = this
            setTimeout(function() {
                uni.stopPullDownRefresh();
            }, 1000);
            // this.getSearchList(() => {
            //     uni.stopPullDownRefresh()
            // })
        },
        onLoad(options){
            this.list(options.id)
        },
        methods: {
            async list(id) {
                const {data: res} = await this.$request({
                    method: 'GET',
                    url: 'applets/credit',
                    data: {
                        id:id,
                        page:this.pageNum
                    }
                })
                this.goodsList = {...this.goodsList, ...res}
                console.log(res)
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/xinyongpjD?id='+id
                })
            },
            change(index) {
                this.current = index;
            }
        }
    }
</script>
<style>
    page {
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    .gray {
        color: #959595;
    }
    .flex{
        justify-content: space-between;
        padding:30rpx 25rpx;
        background:white;
        line-height: 50rpx;
    }
</style>
