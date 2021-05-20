<template>
    <view class="page u-border-top">
        <view class="con u-border-bottom" v-for="item in con" :key="item.id" @click="detail(item.id)">
            <view class="left">
                <view>
                    <text class="gray">案号：</text>
                    <text>{{item.case ? item.case : '-'}}</text>
                </view>
                <view>
                    <text class="gray">被执行人：</text>
                    <text>{{item.notptbe ? item.notptbe : '-'}}</text>
                </view>
                <view>
                    <text class="gray">执行标的：</text>
                    <text>{{item.subject ? item.subject : '-'}}</text>
                </view>
                <view>
                    <text class="gray">未履行金额：</text>
                    <text>{{item.amount ? item.amount : '-'}}</text>
                </view>
                <view>
                    <text class="gray">执行法院：</text>
                    <text>{{item.court ? item.court : '-'}}</text>
                </view>
                <view>
                    <text class="gray">立案日期：</text>
                    <text>{{item.filing ? item.filing : '-'}}</text>
                </view>
                <view>
                    <text class="gray">终本日期：</text>
                    <text>{{item.date ? item.date : '-'}}</text>
                </view>
            </view>
            <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
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
        onLoad(options){
            this.list(options.id)
        },
        methods:{
            async list (id) {
                const { data: res } = await this.$request({
                    method: 'GET',
                    data:{
                        id:id
                    },
                    url: 'applets/cases',
                })
                console.log(res)
                this.con=res
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/zhongbenajD?id='+id
                })
            }
        }

    }
</script>

<style lang="scss" scoped>
    .gray{
        color:#959595;
    }
.con{
    padding:25rpx;
    display: flex;
    justify-content: space-between;
    line-height: 50rpx;
}
</style>