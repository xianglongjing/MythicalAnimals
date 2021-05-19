<template>
    <view class="page u-border-top">
        <view class="first" v-for="item in law" :key="item.id">
            <view>
                <text class="gray">抽查计划编号</text>
                <view>{{item.plannumber ? item.plannumber : '-'}}</view>
            </view>
            <view>
                <text class="gray">抽查计划名称</text>
                <view>{{item.planname ? item.planname : '-'}}</view>
            </view>
            <view>
                <text class="gray">抽查任务名称</text>
                <view>{{item.taskname ? item.taskname : '-'}}</view>
            </view>
            <view class="flex u-margin-top-20 u-padding-bottom-30">
                <view class="item">
                    <text class="gray">抽查类型</text>
                    <view>{{item.type ? item.type : ''}}</view>
                </view>
                <view class="item u-border-left u-padding-left-20">
                    <text class="gray">抽查机关</text>
                    <view>{{item.organ ? item.organ : ''}}</view>
                </view>
            </view>
            <view class="items">
                <text class="gray">抽查完成日期</text>
                <view class="red">{{item.date ? item.date : ''}}</view>
            </view>
            <view class="items">
                <text class="gray">检查情况</text>
                <view @click="qk(item.id)" class="red">查看详情</view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                law:{}
            }
        },
        onLoad (options) {
            this.list(options.id)
        },
        methods:{
            async list(id) {
                const {data: res} = await this.$request({
                    method: 'GET',
                    url: 'applets/stochasticsave',
                    data: {
                        id:id
                    }
                })
                this.law = res
                console.log(res)
            },
            qk(id){
                uni.navigateTo({
                    url:'/pages/company/jianchaqk?id='+id
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
    .red{
        color:#fd5123;
    }
    .first{
        line-height: 50rpx;
        background: white;
        padding:25rpx;
        .flex{
            justify-content: space-between;
            align-items: center;
            .item{
                width:50%;
            }

        }
        .items{
            padding:20rpx 0;
        }
    }
</style>