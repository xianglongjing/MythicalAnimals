<template>
    <view class="page u-border-top">
        <view>
            <view class="info">
                <view class="flex">
                    <view class="item">
                        <text class="gray">宗地标识</text>
                        <view>{{con.parcelid ? con.parcelid : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">宗地编号</text>
                        <view>{{con.parcelnumber ? con.parcelnumber : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">所在行政区</text>
                        <view>{{con.district ? con.district : '-'}}</view>
                    </view>
                    <view v-if="con.dtrpm" class="item u-border-left u-padding-left-20">
                        <text class="gray">土地面积</text>
                        <view>{{con.area ? con.area : '-'}}</view>
                    </view>
                </view>
                <view>
                    <text class="gray">宗地坐落</text>
                    <view>{{con.located ? con.located : '-'}}</view>
                </view>
                <view>
                    <text class="gray">土地他项权利人证号</text>
                    <view>{{con.cnotorhotl ? con.cnotorhotl : '-'}}</view>
                </view>
                <view>
                    <text class="gray">土地使用权证号</text>
                    <view>{{con.lurcn ? con.lurcn : '-'}}</view>
                </view>
                <view>
                    <text class="gray">土地抵押人名称</text>
                    <view>{{con.nolm ? con.nolm : '-'}}</view>
                </view>
                <view>
                    <text class="gray">土地抵押人性质</text>
                    <view>{{con.nature ? con.nature : '-'}}</view>
                </view>
                <view v-if="con.result">
                    <text class="gray">土地抵押权人</text>
                    <view>{{con.mortgagee ? con.mortgagee : '-'}}</view>
                </view>
                <view v-if="con.result">
                    <text class="gray">抵押土地用途</text>
                    <view>{{con.use ? con.use : '-'}}</view>
                </view>
                <view v-if="con.result">
                    <text class="gray">抵押土地权属性质与使用权类型</text>
                    <view>{{con.molratour ? con.molratour : '-'}}</view>
                </view>
                <view v-if="con.result">
                    <text class="gray">抵押面积</text>
                    <view>{{con.ma ? con.ma : '-'}}</view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">评估金额</text>
                        <view>{{con.amount ? con.amount : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">抵押金额</text>
                        <view>{{con.mat ? con.mat : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">土地抵押登记起始时间</text>
                        <view>{{con.lmrst ? con.lmrst : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">土地抵押结束时间</text>
                        <view>{{con.lmet ? con.lmet : '-'}}</view>
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
                con:[],
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
                    url: 'applets/landmortgagesave',
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
                justify-content: center;
                text-align: center;
            }
            .item{
                width:50%;
                align-items: center;
                margin:20rpx 0;
                justify-content: space-between;
            }
        }
    }
</style>