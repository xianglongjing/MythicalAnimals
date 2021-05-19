<template>
    <view class="page u-border-top">
        <view>
            <view class="info">
                <view>
                    <text class="gray">案号</text>
                    <view>{{con.case ? con.case : '-'}}</view>
                </view>
                <view>
                    <text class="gray">法院名称</text>
                    <view>{{con.court ? con.court : '-'}}</view>
                </view>
                <view>
                    <text class="gray">被执行人姓名</text>
                    <view>{{con.pname ? con.pname : '-'}}</view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">标的物名称</text>
                        <view>{{con.sname ? con.sname : '-'}}</view>
                    </view>
                    <view v-if="con.dtrpm" class="item u-border-left u-padding-left-20">
                        <text class="gray">确定参考价方式</text>
                        <view>{{con.dtrpm ? con.dtrpm : '-'}}</view>
                    </view>
                </view>
                <view class="flex">
                    <view class="item">
                        <text class="gray">财产类型</text>
                        <view>{{con.type ? con.type : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">发布日期</text>
                        <view>{{con.lottery ? con.lottery : '-'}}</view>
                    </view>
                </view>
                <view>
                    <text class="gray">关联对象</text>
                    <view>{{con.sea ? con.sea : '-'}}</view>
                </view>
                <view v-if="con.result">
                    <text class="gray">询价结果</text>
                    <view>{{con.result ? con.result : '-'}}</view>
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
                con:[]
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
                    url: 'applets/inquirysave',
                })
                console.log(res)
                this.con=res
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/dianxinxukeD?id='+id
                })
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