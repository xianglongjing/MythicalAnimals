<template>
    <view class="page u-border-top">
        <view class="con u-border-bottom" v-for="item in con" :key=item.id>
            <view>
                <view class="gray">检查事项</view>
                <view>{{item.checkname ? item.checkname : '-'}}</view>
            </view>
            <view>
                <view class="gray">检查结果</view>
                <view>{{item.result ? item.result : '-'}}</view>
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
            async list(id) {
                const {data: res} = await this.$request({
                    method: 'GET',
                    url: 'applets/stochasticread',
                    data: {
                        id:id
                    }
                })
                this.con = res
                console.log(res)
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
    .con{
        background: white;
        padding:25rpx;
        line-height: 50rpx;
    }
</style>