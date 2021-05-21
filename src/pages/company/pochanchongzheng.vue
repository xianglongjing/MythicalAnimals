<template>
    <view class="page u-border-top">
        <view class="con" v-for="item in con" :key="item.id" @click="detail(item.id)">
            <view>
                <view>
                    <text class="gray">案号：</text>
                    <text>{{item.case ? item.case : '-'}}</text>
                </view>
                <view>
                    <text class="gray">案件类型：</text>
                    <text>{{item.type ? item.type : '-'}}</text>
                </view>
                <view>
                    <text class="gray">被申请人：</text>
                    <text>{{item.effective ? item.effective : '-'}}</text>
                </view>
                <view>
                    <text class="gray">申请人：</text>
                    <text>{{item.applicant ? item.applicant : '-'}}</text>
                </view>
                <view>
                    <text class="gray">经办法院：</text>
                    <text>{{item.tioe ? item.tioe : '-'}}</text>
                </view>
                <view>
                    <text class="gray">公告日期：</text>
                    <text>{{item.date ? item.date : '-'}}</text>
                </view>
            </view>
            <u-icon name="arrow-right" size="32" color="#959595"></u-icon>
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
                    url: 'applets/bankruptcy',
                })
                console.log(res)
                this.con=res
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/pochanczD?id='+id
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
    .con{
        background: white;
        padding:30rpx 25rpx;
        line-height: 50rpx;
        display: flex;
        justify-content: space-between;
    }
</style>