<template>
    <view class="page">
        <view class="u-border-bottom" style="background: white">
            <u-tabs
                    :list="List"
                    :current="current"
                    @change="Change" gutter="95"
                    bar-width="90" font-size="30"
                    active-color="#E2291D" bg-color="none" inactive-color="#666666"
            ></u-tabs>
        </view>
        <view v-if="current==0">
            <view class="item" v-for="item in goodsList" :key="item.id">
                <view class="item-t u-border-bottom">
                    <view class="item-l">
                        <u-image mode="aspectFit" src="http://images.yiqiwang360.com/yiqicha/vip.png" width="40" height="40"></u-image>
                        <text class="vip">VIP会员</text>
                    </view>
                    <text class="red">订单已完成</text>
                </view>
                <view class="item-b">
                    <view>
                        <text class="title">{{item.name}}</text>
                        <text class="gray u-margin-left-10">已完成支付</text>
                    </view>
                    <view class="gray">{{item.expiry}}到期
<!--                        （使用中）-->
                    </view>
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
            <view class="item" v-for="item in goodsList2" :key="item.id">
                <view class="item-t u-border-bottom">
                    <view class="item-l">
                        <u-image mode="aspectFit" src="http://images.yiqiwang360.com/yiqicha/vip.png" width="40" height="40"></u-image>
                        <text class="vip">VIP会员</text>
                    </view>
                    <text class="red">订单未完成</text>
                </view>
                <view class="item-b u-border-bottom u-padding-bottom-30">
                    <view>
                        <text class="title">{{item.name}}</text>
                    </view>
                    <view class="gray">剩余支付时间：
                        <u-count-down :timestamp="timestamp"></u-count-down>
                    </view>
                </view>
                <view class="flex">
                   <view class="flex-l">
                       <text class="gray">支付金额：</text>
                       <text class="red u-font-32">{{item.pay_total}}</text>
                   </view>
                    <u-button :customStyle="pay" @click="show">去支付</u-button>
                </view>
            </view>
            <u-loadmore
                    color="#999999"
                    font-size="24"
                    margin-bottom="50"
                    margin-top="50"
                    :status="loadStatus"
                    @loadmore="getList2"
            ></u-loadmore>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                List: [{
                    name: '已完成订单'
                }, {
                    name: '待支付订单'
                }],
                current:0,
                page:1,
                goodsList:{},
                goodsList2:{},
                loadStatus: 'more',
                pageNum:1,
                pay:{
                    width:'120rpx',
                    height:'45rpx',
                    background:'#E2261A',
                    color:'white'
                },
                timestamp: 3600,
            }
        },
        // 到底部
        onReachBottom () {
            if (this.goodsList.length < this.pageNum * 10) return this.loadStatus = 'nomore'
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
        onLoad(){
          this.getList()
          this.getList2()
        },
        methods: {
            happenTimeFun(num) {//时间戳数据处理
                let date = new Date(num * 1000);
                //时间戳为10位需*1000，时间戳为13位的话不需乘1000
                let y = date.getFullYear();
                let MM = date.getMonth() + 1;
                MM = MM < 10 ? ('0' + MM) : MM;//月补0
                let d = date.getDate();
                d = d < 10 ? ('0' + d) : d;//天补0
                let h = date.getHours();
                h = h < 10 ? ('0' + h) : h;//小时补0
                let m = date.getMinutes();
                m = m < 10 ? ('0' + m) : m;//分钟补0
                let s = date.getSeconds();
                s = s < 10 ? ('0' + s) : s;//秒补0
                return y + '-' + MM + '-' + d; //年月日
                //return y + '-' + MM + '-' + d + ' ' + h + ':' + m+ ':' + s; //年月日时分秒
            },
            async getList() {
                const token = uni.getStorageSync('token')
                const {data: res} = await this.$request({
                    url: 'applets/myorder',
                    method: 'POST',
                    data: {
                        token: uni.getStorageSync('token'),
                        page: this.pageNum
                    }
                })
                // console.log(res)
                this.goodsList = res
                this.goodsList.forEach(item => {
                    item.expiry = this.happenTimeFun(item.expiry)
                })
            },
            async getList2() {
                const token = uni.getStorageSync('token')
                const {data: res} = await this.$request({
                    url: 'applets/myordersave',
                    method: 'POST',
                    data: {
                        token: uni.getStorageSync('token'),
                        page: this.pageNum
                    }
                })
                console.log(res)
                this.goodsList2 = res
            },
            Change(index) {
                this.current = index;
            },
            show(){

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
.red{
    color:#EC7A74;
}
.gray{
     font-size: 25rpx;
     color:#969696;
 }
.item{
    background: white;
    margin:30rpx;
    .red{
    font-weight: 670;
}
    .item-t{
    display: flex;
    justify-content: space-between;
    padding:20rpx;


    .item-l{
        display: flex;
        align-items: center;
        .vip{
            font-size: 30rpx;
            margin-left:10rpx;
        }
    }
}
    .item-b{
        padding:20rpx;
        .title{
            font-weight: 650;
        }

    }
    .flex{
        line-height: 100rpx;
        padding:0 20rpx;
        justify-content: space-between;
        align-items: center;
        .flex-l{
            flex:1;
        }
    }
}

</style>