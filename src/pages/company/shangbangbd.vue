<template>
    <view class="page u-border-top">
        <u-empty text="暂无相关内容" mode="list" src="http://images.yiqiwang360.com/yiqicha/wujilu.png" class="u-margin-30" :show="emptyShow">
        </u-empty>
        <view class="zong u-border-bottom" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
            <view class="title">{{item.name}}</view>
            <view class="con">
                <view class="left">
                    <view>
                        <text class="gray">榜单类型：</text>
                        <text>{{item.type ? item.type : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">榜内排名：</text>
                        <text>{{item.list ? item.list : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">榜内名称：</text>
                        <text>{{item.gname ? item.gname : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">发布日期：</text>
                        <text>{{item.date ? item.date : '-'}}</text>
                    </view>
                </view>
                <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
            </view>
        </view>
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
        // onReachBottom () {
        //     if (this.goodsList.length < this.pageNum * 10) return this.loadStatus = 'more'
        //     this.pageNum++
        //     this.getList()
        // },
        // 下拉刷新
        onPullDownRefresh () {
            setTimeout(function() {
                uni.stopPullDownRefresh();
            }, 1000);
        },
        onLoad(options){
            this.getList(options.id)
        },
        methods:{
            async getList (id) {
                const { data: res } = await this.$request({
                    url: 'applets/otlist',
                    data: {
                        id:id
                    }
                })

                this.goodsList = res
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
                    url:'/pages/company/guquanzhiyaD?id='+id
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