<template>
    <view class="page u-border-top">
        <view class="white">
            <view class="con">
                <view class="gray">案号</view>
                <view>{{con.case ?con.case : '-'}}</view>
            </view>
            <view class="con">
                <view class="gray">被执行人姓名/名称</view>
                {{con.notptbe ?con.notptbe : '-'}}</view>
            <view class="con">
                <view class="gray">身份证号码/组织机构代码</view>
                <view>{{con.icoc ?con.icoc : '-'}}</view>
            </view>
            <view class="con">
                <view class="gray">执行法院</view>
                <view>{{con.court ?con.court : '-'}}</view>
            </view>
            <view class="flex">
                <view class="con">
                    <text class="gray">立案日期</text>
                    <view>{{con.filing ? con.filing : '-'}}</view>
                </view>
                <view class="con u-border-left u-padding-left-20">
                    <text class="gray">终本日期</text>
                    <view>{{con.enddate ? con.enddate : '-'}}</view>
                </view>
            </view>
            <view class="flex">
                <view class="con">
                    <text class="gray">执行标的</text>
                    <view>{{con.subject ? con.subject : '-'}}</view>
                </view>
                <view class="con u-border-left u-padding-left-20">
                    <text class="gray">未履行金额</text>
                    <view>{{con.amount ? con.amount : '-'}}</view>
                </view>
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
        }
    }
</script>
<style>
    page{
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    .white{
        background: white;
        padding:25rpx;
        line-height: 50rpx;
    }
    .gray{
        color:#959595;
    }
    .flex{
        align-cons: center;
        .red{
            display: flex;
            justify-content: center;
            text-align: center;
        }
        .con{
            width:50%;
            align-cons: center;
            margin:20rpx 0;
            justify-content: space-between;
        }
    }
</style>