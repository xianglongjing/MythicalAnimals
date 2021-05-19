<template>
    <view class="page u-border-top">
        <view class="tab u-border-bottom">
            <u-tabs
                    :list="List"
                    :current="current"
                    @change="Change" gutter="90"
                    bar-width="50" font-size="30"
                    active-color="#E12216" bg-color="none" inactive-color="#000000"
            ></u-tabs>
        </view>
        <view v-if="current==0">
            <view class="zong u-border-bottom" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
                <view class="title">{{item.name}}</view>
                <view class="con">
                    <view class="left">
                        <view>
                            <text class="blue">发布提及</text>
                            <text class="gray">{{item.date ? item.date : '-'}}</text>
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
        <view v-if="current==1">
            <u-empty text="暂无信息" mode="list" src="http://images.yiqiwang360.com/yiqicha/wujilu.png" class="u-margin-30" :show="emptyShow">
            </u-empty>
        </view>

    </view>
</template>

<script>
    export default {
        data(){
            return {
                List: [{
                    name: '相关公告'
                }, {
                    name: '企业研报'
                }],
                current:0,
                page:1,
                pageNum:1,
                loadStatus: 'more',
                goodsList:{},
                emptyShow:true
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
            Change(index) {
                this.current = index;
            },
            async getList (id) {
                const { data: res } = await this.$request({
                    url: 'applets/report',
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
            // detail(id){
            //     uni.navigateTo({
            //         url:'/pages/company/zhaiquanxinxiD?id='+id
            //     })
            // }
        }
    }
</script>
<style>
    page{
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
.tab{
    text-align: center;
    background: white;
}
.gray{
    color:#959595;
}
.blue{
    color:#3C7295;
    background: #E6F6FC;
    padding:10rpx;
    letter-spacing: 2rpx;
    margin-right:15rpx;
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