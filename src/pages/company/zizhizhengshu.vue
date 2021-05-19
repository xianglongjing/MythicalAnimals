<template>
    <view class="page u-border-top">
        <u-dropdown class="u-border-bottom">
            <u-dropdown-item v-model="value1" title="全部证书类型" :options="options1"></u-dropdown-item>
        </u-dropdown>
        <view class="con u-border-bottom" v-for="item in goodsList" :key="item.id" @click="detail(item.id)">
            <view>
                <view class="name">软件证书</view>
                <view>
                    <text class="gray">证书编号：</text>
                    <text>{{item.cnumber ? item.cnumber : '-'}}</text>
                </view>
                <view>
                    <text class="gray">发证日期：</text>
                    <text>{{item.issue ? item.cnumber : '-'}}</text>
                </view>
                <view>
                    <text class="gray">截止日期：</text>
                    <text>{{item.cnumber ? item.cnumber : '-'}}</text>
                </view>
            </view>
            <u-icon name="arrow-right" color="#777777" size="40"></u-icon>
        </view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                value1:'',
                goodsList:{},
                page:1,
                pageNum:1,
                options1: [{
                    label: '默认排序',
                    value: 1,
                },
                    {
                        label: '距离优先',
                        value: 2,
                    },
                    {
                        label: '价格优先',
                        value: 3,
                    }
                ],
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
        methods: {
            change(index) {
                this.current = index;
            },
            async getList (id) {
                const { data: res } = await this.$request({
                    url: 'applets/certifications',
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
                    url:'/pages/company/zizhizhengshuDe?id='+id
                })
            }
        }
    }
</script>
<style lang="scss" scoped>
    .gray {
        color: #959595;
    }
    .con{
        display: flex;
        justify-content: space-between;
        padding:30rpx 25rpx;
        background:white;
        line-height: 50rpx;
        .name{
            font-size: 39rpx;
            margin-bottom:20rpx;
        }
    }
</style>
