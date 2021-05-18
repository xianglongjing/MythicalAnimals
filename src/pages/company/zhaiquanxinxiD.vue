<template>
    <view class="page u-border-top">
        <view v-for="item in con" :key="item.id">
            <view class="title u-border-bottom">{{item.name}}</view>
            <view class="info">
                <view class="flex">
                    <view class="item">{{item.name}}
                        <text class="gray">债券代码</text>
                        <view>{{item.bondcode ? item.bondcode : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">发行人</text>
                        <view>{{item.Issuer ? item.Issuer : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">债券类型</text>
                        <view>{{item.bondtype ? item.bondtype : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">债券发行日</text>
                        <view>{{item.issuedate ? item.issuedate : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">债券到期日</text>
                        <view>{{item.maturitydate ? item.maturitydate : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">上市交易日</text>
                        <view>{{item.tradingday ? item.tradingday : '-'}}</view>
                    </view>
                </view>
                <view class="flex u-border-bottom">
                    <view class="item">
                        <text class="gray">债券摘牌日</text>
                        <view>{{item.delistingday ? item.delistingday : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-bottom-20 u-padding-left-20">
                        <text class="gray">债券起息日</text>
                        <view>{{item.valuedate ? item.valuedate : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">债券期限</text>
                        <view>{{item.maturity ? item.maturity : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">计息方式</text>
                        <view>{{item.method ? item.method : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">债券评级</text>
                        <view>{{item.rating ? item.rating : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">信用评级机构</text>
                        <view>{{item.agency ? item.agency : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">面值</text>
                        <view>{{item.face ? item.face : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">参考利率</text>
                        <view>{{item.interest ? item.interest : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">票面利率</text>
                        <view>{{item.coupon ? item.coupon : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">实际发行量</text>
                        <view>{{item.circulation ? item.circulation : '-'}}</view>
                    </view>
                </view>
                <view class="flex u-border-bottom">
                    <view class="item">
                        <text class="gray">计划发行量</text>
                        <view>{{item.planned ? item.planned : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">发行价格</text>
                        <view>{{item.price ? item.price : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">利差（BP）</text>
                        <view>{{item.spread ? item.spread : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">付息频率</text>
                        <view>{{item.payment ? item.payment : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">行权类型</text>
                        <view>{{item.exercise ? item.exercise : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">行权日期</text>
                        <view>{{item.exercisedate ? item.exercisedate : '-'}}</view>
                    </view>
                </view>
                <view class="flex u-border-bottom">
                    <view class="item">
                        <text class="gray">流通范围</text>
                        <view>{{item.range ? item.range : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">托管机构</text>
                        <view>{{item.custodian ? item.custodian : '-'}}</view>
                    </view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                con:{}
            }
        },
        onLoad (options) {
            this.list(options.id)
        },
        methods:{
            async list (id) {
                const { data: res } = await this.$request({
                    method: 'GET',
                    data:{
                        id:id
                    },
                    url: 'applets/bondsave',
                })
                console.log(res)
                this.con=res
            }
        }
    }
</script>

<style lang="scss" scoped>
    .gray{
        color:#959595;
    }
    .title{
        padding:30rpx;
        font-weight: 600;
    }
    .info{
        padding:30rpx;
        line-height: 50rpx;
        .flex{
            align-items: center;
            .red{
                display: flex;
                justify-itemtent: center;
                text-align: center;
            }
            .item{
                width:50%;
                margin:20rpx 0;
                align-items: center;
                justify-itemtent: space-between;
            }
        }
    }
</style>