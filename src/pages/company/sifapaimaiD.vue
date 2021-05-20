<template>
    <view class="page u-border-top">
        <view class="item">
            <view class="gray">公告名称</view>
            <view>{{con.aname}}</view>
        </view>
        <view class="item">
            <view class="gray">拍卖标的</view>
            <view>{{con.salename ? con.salename : '-'}}</view>
        </view>
        <view class="flex">
            <view class="item">
                <text class="gray">起拍价</text>
                <view>{{con.stgpe ? con.stgpe : '-'}}</view>
            </view>
            <view class="item u-border-left u-padding-left-20">
                <text class="gray">评估价</text>
                <view>{{con.stock ? con.stock : '-'}}</view>
            </view>
        </view>
        <view class="flex">
            <view class="item">
                <text class="gray">拍卖阶段</text>
                <view>{{con.saleall ? con.saleall : '-'}}</view>
            </view>
            <view class="item u-border-left u-padding-left-20">
                <text class="gray">委托法院</text>
                <view>{{con.emtct ? con.emtct : '-'}}</view>
            </view>
        </view>
        <view class="item">
            <view class="gray">拍卖时间</view>
            <view>{{con.saledate ? con.saledate : '-'}}</view>
        </view>
        <u-gap height="20" bg-color="#f7f7f7"></u-gap>
        <view class="item u-border-bottom">竞买公告</view>
        <view class="item">{{con.saleidtn ? con.saleidtn : '-'}}</view>
        <u-gap height="20" bg-color="#f7f7f7"></u-gap>
        <view class="item">竞买须知</view>
        <view class="item">{{con.arfkay ? con.arfkay : '-'}}</view>
        <u-gap height="20" bg-color="#f7f7f7"></u-gap>
        <view class="item u-border-bottom">
            <view class="item2">标的物介绍</view>
        </view>
        <view class="item">
            <view class="gray item2">标的物详情</view>
            <view class="item2">{{con.wrrtstn ? con.wrrtstn : '-'}}</view>
        </view>
        <view class="item">
            <view class="gray item2">标的物位置</view>
            <view class="item2">{{con.pdmtn ? con.pdmtn : '-'}}</view>
        </view>
        <view class="item">
            <view class="gray item2">标的物图片
            </view>
            <view class="item2">{{con.saleidtn ? con.saleidtn : '-'}}</view>
        </view>
        <view class="item">
            <view class="gray item2">相关附件（仅支持pdf预览，电脑端可查看全部文件）
            </view>
            <view class="item2">{{con.lopad ? con.lopad : '-'}}</view>
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
                    url: 'applets/auctionsave',
                })
                console.log(res)
                this.con=res
            },
        }
    }
</script>

<style lang="scss" scoped>
.gray{
    color:#959595;
}
.item{
    padding:25rpx;
}
.item2{
    padding:10rpx 0;
}
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
</style>