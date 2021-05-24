<template>
    <view class="page u-border-top">
        <view class="flex">
            <text>{{con.title}}</text>
            <text>{{con.date}}</text>
        </view>
        <view class="page u-margin-top-30">
            <u-parse :html="con.content"
                     :lazy-load="true"
                     :show-with-animation="true"
                     :tag-style="contentStyle"
                     domain="https://api.rosepo.com/"></u-parse>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                con:[],
                contentStyle: {
                    // 字符串的形式
                    h2: 'font-size:25rpx;line-height:48rpx;margin:20rpx 0;color:#000000;text-align:center;',
                    p: 'font-size:24rpx;line-height:50rpx;margin:20rpx 0;color:#333333',
                    img: 'border-radius:8rpx;',
                    ".get-item": "display:block;text-align: center;margin-bottom: 10rpx;"
                },
            }
        },
        onLoad(options){
            this.getSearchList(options.id)
        },
        methods:{
            async getSearchList (id) {
                const {data:res}  = await this.$request({
                    method:'GET',
                    url: 'applets/annualcontent',
                    data: {
                        id:id
                    }
                })
                console.log(res)
                this.con = res
            },
        }
    }
</script>

<style lang="scss" scoped>
    page{
        padding:25rpx 30rpx;
    }
.flex{
    /*padding:0 30rpx;*/
    justify-content: space-between;
}
</style>