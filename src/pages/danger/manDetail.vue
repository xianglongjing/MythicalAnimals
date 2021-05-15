<template>
    <view class="page">
        <view class="tou u-border-bottom">
            <u-image src="http://images.yiqiwang360.com/yiqicha/renwu.png" width="60" height="60"></u-image>
            <text class="u-margin-left-20">贾跃亭</text>
        </view>
        <view class="u-margin-top-20 u-border-bottom">
            <u-tabs :list="list" font-size="26"
                    :is-scroll="false" :current="current" bar-height="4" bar-width="50" :bold="false"
                    @change="change" active-color="#FF4E21" inactive-color="#474747"></u-tabs>
        </view>
        <view v-if="current==0">
            <!--        下拉-->
            <view class="content">
                <sl-filter :themeColor="themeColor" :menuList="menuList" @result="result"></sl-filter>
            </view>
            <view class="con u-margin-top-30">
                <view class="item u-border-bottom">
                    <text class="title">法律诉讼</text>
                    <text class="warn">高风险</text>
                </view>
                <view class="item2 u-border-bottom">
                    <view @click="go">
                        <text>该老板在成都锤子科技集团有限公司(有限合作)</text>
                        <view class="red">有股权冻结信息</view>
                    </view>
                    <text class="gray">共2条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
                <view class="item2 u-border-bottom">
                    <view @click="go">
                        <text>该老板在成都锤子科技集团有限公司(有限合作)</text>
                        <view class="red">有股权冻结信息</view>
                    </view>
                    <view class="gray">共2条 <u-icon name="arrow-right" size="26"></u-icon></view>
                </view>
                <view class="item2 u-border-bottom">
                    <view>
                        <text>该老板在成都锤子科技集团有限公司(有限合作)</text>
                        <view class="red">有股权冻结信息</view>
                    </view>
                    <view class="gray">共2条 <u-icon name="arrow-right" size="26"></u-icon></view>
                </view>
            </view>
        </view>

    </view>
</template>

<script>
    import slFilter from '@/components/sl-filter/sl-filter.vue';
    export default {
        components: {
            slFilter
        },
        data(){
            return {
                list: [{
                    name: '自身风险'
                }, {
                    name: '周边风险'
                }, {
                    name: '预警提醒'
                }],
                current: 0,
                themeColor: '#E8544A',
                filterResult: '',
                menuList: [{
                    'title': '全部风险类型',
                    'detailTitle': '',
                    'isMutiple': true,
                    'key': 'jobType',
                    'detailList': [{
                        'title': '司法风险',
                        'value': ''
                    },
                        {
                            'title': '全部司法风险',
                            'value': 'uni-app'
                        },
                        {
                            'title': '强制清算',
                            'value': 'java'
                        },
                        {
                            'title': '涉金融黑黑名单',
                            'value': 'web'
                        },
                        {
                            'title': '失信被执行人',
                            'value': 'Android'
                        },
                        {
                            'title': '限制消费令',
                            'value': 'iOS'
                        }
                    ]
                },
                    {
                        'title': '全部风险级别',
                        'detailTitle': '',
                        'isMutiple': true,
                        'key': 'jobType',
                        'detailList': [{
                            'title': '',
                            'value': ''
                        },
                            {
                                'title': '全部风险级别',
                                'value': 'uni-app'
                            },
                            {
                                'title': '高风险',
                                'value': 'java'
                            },
                            {
                                'title': '警示',
                                'value': 'web'
                            }
                        ]
                    },
                ]
            }
        },
        methods:{
            go(){
                uni.navigateTo({
                    url:'/pages/danger/freeze'
                })
            },
            change(index) {
                this.current = index;
            },
            result(val) {
                console.log('filter_result:' + JSON.stringify(val));
                this.filterResult = JSON.stringify(val, null, 2)
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
        color:#A9A9A9;
    }
    .red{
        color:#E75D54;
    }
.tou{
    display: flex;
    align-items: center;
    background: white;
    height:90rpx;
    padding:25rpx 25rpx 40rpx;
}
    .con{
        background: white;
        .item{
            padding:25rpx 30rpx;
            .warn{
                border:1rpx solid #E75D54;
                color:#E75D54;
                padding:2rpx 9rpx;
                font-size: 24rpx;
                margin-left:10rpx;
                border-radius: 10rpx;
            }
        }
        .item2{
            font-size: 26rpx;
            line-height: 45rpx;
            padding:25rpx 30rpx;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
    }
</style>