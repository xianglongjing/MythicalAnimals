<template>
    <view class="page u-border-top">
        <u-empty text="暂无相关内容" mode="list" src="http://images.yiqiwang360.com/yiqicha/wujilu.png" class="u-margin-30" :show="emptyShow">
        </u-empty>
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
            <view class="con">
                <view class="left" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
                    <view>
                        <text class="gray">被担保债权类型：</text>
                        <text>{{item.stamp ? item.stamp : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">被担保债权数额：</text>
                        <text>{{item.amount ? item.amount : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">抵押权人：</text>
                        <text>{{item.pawnname ? item.pawnname : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">登记编号：</text>
                        <text>{{item.number ? item.number : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">登记日期：</text>
                        <text>{{item.date ? item.date : '-'}}</text>
                    </view>
                </view>
                <u-icon name="arrow-right" color="#959595" size="34"></u-icon>
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
      <view v-if="current==1">
          <u-empty text="暂无相关内容" mode="list" src="http://images.yiqiwang360.com/yiqicha/wujilu.png" class="u-margin-30" :show="emptyShows">
          </u-empty>
      </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                List: [{
                    name: '动产抵押'
                }, {
                    name: '历史动产抵押'
                }],
                current:0,
                pageNum:1,
                page:1,
                goodsList:[],
                loadStatus: 'more',
                emptyShow:false,
                emptyShows:true
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
        onLoad (options) {
            this.getList(options.id)
        },
        methods:{
            Change(index) {
                this.current = index;
            },
            async getList (id) {
                const { data: res } = await this.$request({
                    method: 'GET',
                    data:{
                        id:id,
                        page:this.pageNum
                    },
                    url: 'applets/mortgage',
                })
                console.log(res)
                this.goodsList = {...this.goodsList, ...res}
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
                    url:'/pages/company/dongchandiyaD?id='+id
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
        background: white;
        padding:25rpx;
        display: flex;
        justify-content: space-between;
        align-items: center;
        line-height: 50rpx;
    }
</style>