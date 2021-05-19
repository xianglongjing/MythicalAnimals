<template>
    <view class="page u-border-top">
        <view class="con">
            <view>
                <view class="gray">决定书文号</view>
                <view>{{con.dnumber ? con.dnumber : '-'}}</view>
            </view>
            <view>
                <view class="gray">处罚事由</view>
                <view>{{con.penalties ? con.penalties : '-'}}</view>
            </view>
            <view>
                <view class="gray">违反法律</view>
                <view>{{con.vtl ? con.vtl : '-'}}</view>
            </view>
            <view>
                <view class="gray">处罚依据</view>
                <view>{{con.bfp ? con.bfp : '-'}}</view>
            </view>
            <view>
                <view class="gray">处罚结果</view>
                <view>{{con.penalty ? con.penalty : '-'}}</view>
            </view>
            <view>
                <view class="gray">处罚日期</view>
                <view>{{con.date ? con.date : '-'}}</view>
            </view>
            <view>
                <view class="gray">处罚单位</view>
                <view>{{con.unit ? con.unit : '-'}}</view>
            </view>
            <view>
                <view class="gray">执行情况</view>
                <view>{{con.implementation ? con.implementation : '-'}}</view>
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
        onLoad(options){
            this.getSearchList(options.id)
        },
        methods:{
            async getSearchList (id) {
                const {data:res}  = await this.$request({
                    method:'GET',
                    url: 'applets/protectionsave',
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
    line-height: 55rpx;
}
</style>