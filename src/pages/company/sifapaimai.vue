<template>
    <view class="page u-border-top">
        <view class="zong u-border-bottom" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
            <view class="title">{{item.aname}}</view>
            <view class="con">
                <view class="left">
                    <view>
                        <text class="gray">拍卖标的：</text>
                        <text>{{item.salename ? item.salename : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">起拍价：</text>
                        <text>{{item.stgpe ? item.stgpe : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">评估价：</text>
                        <text>{{item.arlpe ? item.arlpe : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">拍卖阶段：</text>
                        <text>{{item.saleall ? item.saleall : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">委托法院：</text>
                        <text>{{item.emtct ? item.emtct : '-'}}</text>
                    </view>
                    <view>
                        <text class="gray">拍卖时间：</text>
                        <text>{{item.saledate ? item.saledate : '-'}}</text>
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
                goodsList:{}
            }
        },
        // 下拉刷新
        onPullDownRefresh () {
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
                    url: 'applets/auction',
                    data: {
                        id:id
                    }
                })

                this.goodsList = res
                console.log(res)
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/sifapaimaiD?id='+id
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