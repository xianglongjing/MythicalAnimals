<template>
    <view class="page u-border-top">
        <view class="tab u-border-bottom">
            <u-tabs
                    :list="List"
                    :current="current"
                    @change="Change" gutter="70"
                    bar-width="50" font-size="30"
                    active-color="#E2291D" bg-color="none" inactive-color="#666666"
            ></u-tabs>
        </view>
        <view v-if="current==0">
            <view class="con u-border-bottom" v-for="item in con" :key="item.id" @click="detail(item.id)">
                <view class="left">
                    <view>
                        <text class="gray">土地坐落：</text>
                        <text>{{item.located ? item.located : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">所在行政区：</text>
                        <text>{{item.district ? item.district : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">抵押权人：</text>
                        <text>{{item.mortgagee ? item.mortgagee : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">抵押土地用途：</text>
                        <text>{{item.use ? item.use : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">抵押面积：</text>
                        <text>{{item.ma ? item.ma : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">抵押金额：</text>
                        <text>{{item.mat ? item.mat : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">起止时间：</text>
                        <text>{{item.lmrst ? item.lmrst : '-'}}至{{item.lmet ? item.lmet : '-'}}</text>
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
                    @loadmore="getSearchList"
            ></u-loadmore>
        </view>
        <view v-if="current==1">
            <u-empty text="暂无信息" mode="list" class="u-margin-30" :show="emptyShow">
            </u-empty>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                List: [{
                    name: '土地抵押'
                }, {
                    name: '历史土地抵押'
                }],
                current:0,
                con:{},
                page:1,
                pageNum:1,
                loadStatus:'more'
            }
        },
        // 到底部
        onReachBottom () {
            if (this.con.length < this.pageNum * 10) return this.loadStatus = 'more'
            this.pageNum++
            this.getSearchList()
        },
        // 下拉刷新
        onPullDownRefresh () {
            this.pageNum = 1
            // this.pageNum++
            this.getSearchList()
            let that = this
            setTimeout(function() {
                uni.stopPullDownRefresh();
            }, 1000);
            // this.getSearchList(() => {
            //     uni.stopPullDownRefresh()
            // })
        },
        onLoad(options){
            this.getSearchList(options.id)
        },
        methods:{
            Change(index) {
                this.current = index;
            },
            async getSearchList (id) {
                const {data:res}  = await this.$request({
                    method:'GET',
                    url: 'applets/landmortgage',
                    data: {
                        id:id,
                        page:this.pageNum
                    }
                })
                console.log(res)
                this.con = {...this.con, ...res}
                if (this.con.length < res.total) {
                    this.loadStatus = 'loading'
                } else {
                    this.loadStatus = 'nomore'
                }
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/tudidiyaD?id='+id
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
    .tab{
        text-align: center;
        background: white;
    }
    .con{
        padding:25rpx;
        background: white;
        display: flex;
        justify-content: space-between;
        align-items: center;
        line-height: 50rpx;
    }
</style>