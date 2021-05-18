<template>
    <view class="page u-border-top">
        <view class="padding">
            <view>
                <view>股东名称</view>
                <view>{{con.pledger ? con.pledger : '-'}}</view>
            </view>
            <view class="flex2">
                <view class="item">
                    <view class="gray">质押股份数量</view>
                    <text>{{con.nops ? con.nops : '-'}}</text>
                </view>
                <view class="item2">
                    <text class="shu u-margin-right-20">|</text>
                    <view>
                        <view class="gray">质押股份市值</view>
                        <text>{{con.tmvops ? con.tmvops : '-'}}</text>
                    </view>
                </view>
            </view>
            <view class="flex2">
                <view class="item">
                    <view class="gray">占所持股份比例</view>
                    <text>{{con.pos ? con.pos : '-'}}</text>
                </view>
                <view class="item2">
                    <text class="shu u-margin-right-20">|</text>
                    <view>
                        <view class="gray">占总股份比例</view>
                        <text>{{con.tmvops ? con.tmvops : '-'}}</text>
                    </view>
                </view>
            </view>
            <view>
                <view class="gray">质押权人</view>
                <view>{{con.holder ? con.holder : '-'}}</view>
            </view>
            <view>
                <view class="gray">质押原因</view>
                <view>{{con.reason ? con.reason : '-'}}</view>
            </view>
            <view class="flex2">
                <view class="item">
                    <view class="gray">质押目的</view>
                    <text>{{con.purpose ? con.purpose : '-'}}</text>
                </view>
                <view class="item2">
                    <text class="shu u-margin-right-20">|</text>
                    <view>
                        <view class="gray">质押日收盘价</view>
                        <text>{{con.cpopd ? con.cpopd : '-'}}</text>
                    </view>
                </view>
            </view>
            <view class="flex2">
                <view class="item">
                    <view class="gray">预警线（估算）</view>
                    <text>{{con.ewle ? con.ewle : '-'}}</text>
                </view>
                <view class="item2">
                    <text class="shu u-margin-right-20">|</text>
                    <view>
                        <view class="gray">平仓线（估算）</view>
                        <text>{{con.cle ? con.cle : '-'}}</text>
                    </view>
                </view>
            </view>
            <view class="flex2">
                <view class="item">
                    <view class="gray">质押开始日期</view>
                    <text>{{con.psdate ? con.psdate : '-'}}</text>
                </view>
                <view class="item2">
                    <text class="shu u-margin-right-20">|</text>
                    <view>
                        <view class="gray">质押解除日期</view>
                        <text>{{con.prdate ? con.prdate : '-'}}</text>
                    </view>
                </view>
            </view>
            <view class="flex2">
                <view class="item">
                    <view class="gray">状态</view>
                    <text>{{con.status ? con.status : '-'}}</text>
                </view>
                <view class="item2">
                    <text class="shu u-margin-right-20">|</text>
                    <view>
                        <view class="gray">公告日期</view>
                        <text>{{con.adate ? con.adate : '-'}}</text>
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
                con:[]
            }
        },
        onLoad (options) {
            this.list(options.id)
        },
        methods: {
            async list (id) {
                const { data: res } = await this.$request({
                    method: 'GET',
                    data:{
                        id:id
                    },
                    url: 'applets/equitysave',
                })
                console.log(res)
                this.con=res
            },
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
    .title{
        font-weight: 600;
        padding:30rpx;
        background: white;
    }
    .padding{
        background: white;
    }
    .flex2{
        display: flex;
        background: white;
        justify-content: space-between;
        align-items: center;
        margin:20rpx 0;
        .item,.item2{
            flex:1;
        }
        .item2{
            line-height: 45rpx;
            align-items: center;
            display: flex;
            .shu{
                color:#f8f8f8;
                font-size:40rpx;
            }
        }
    }
    .info{
        background: white;
        margin:25rpx 0;
        padding:0 0rpx;
        display: flex;
        align-items: center;
        justify-content: space-between;
        .title{
            font-weight: 600;
        }
    }
</style>