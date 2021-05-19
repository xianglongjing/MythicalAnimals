<template>
    <view class="page u-border-top">
        <u-empty text="暂无相关内容" mode="list" src="http://images.yiqiwang360.com/yiqicha/wujilu.png" class="u-margin-30" :show="emptyShow">
        </u-empty>
        <view class="con u-border-bottom">
            <view class="left" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
                <view>
                    <text class="gray">决定书文号：</text>
                    <text>{{item.dnumber ? item.dnumber : '-'}}</text>
                </view>
                <view>
                    <text class="gray">处罚结果：</text>
                    <text>{{item.penalty ? item.penalty : '-'}}</text>
                </view>
                <view>
                    <text class="gray">处罚单位：</text>
                    <text>{{item.unit ? item.unit : '-'}}</text>
                </view>
                <view>
                    <text class="gray">处罚日期：</text>
                    <text>{{item.date ? item.date : '-'}}</text>
                </view>
            </view>
            <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
        </view>
        <u-loadmore
                color="#999999"
                font-size="24"
                margin-bottom="50"
                margin-top="50"
                :status="loadStatus"
                @loadmore="getList"
                v-if="!emptyShow"
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
                loadStatus: 'more',
                emptyShow:false
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
                    url: 'applets/protection',
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
                let dataNum = res.length
                console.log(dataNum)
                if (dataNum=0){
                    this.emptyShow = false
                }
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/protectD?id='+id
                })
            }
        }
    }
</script>

<style lang="scss" scoped>
    .gray{
        color:#959595;
    }
    .con{
        padding:25rpx;
        line-height: 50rpx;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>