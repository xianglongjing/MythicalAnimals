<template>
    <view class="page u-border-top">
        <view>
            <view class="title u-border-bottom">动产抵押登记信息</view>
            <view class="info">
                <view class="flex">
                    <view class="item">
                        <text class="gray">登记编号</text>
                        <view>{{con.number ? con.number : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">登记日期</text>
                        <view>{{con.date ? con.date : '-'}}</view>
                    </view>
                </view>
                <view>
                    <text class="gray">登记机关</text>
                    <view>{{con.organ ? con.organ : '-'}}</view>
                </view>
            </view>
        </view>
        <u-gap height="20" bg-color="#f8f8f8"></u-gap>
        <view>
            <view class="title u-border-bottom">抵押权人信息</view>
            <view class="info">
                <view>
                    <text class="gray">抵押权人名称</text>
                    <view>{{con.pawnname ? con.pawnname : '-'}}</view>
                </view>
                <view>
                    <text class="gray">抵押权人证件类型</text>
                    <view>{{con.license ? con.license : '-'}}</view>
                </view>
                <view>
                    <text class="gray">证件号码</text>
                    <view>{{con.licensenumber ? con.licensenumber : '-'}}</view>
                </view>
            </view>
        </view>
        <u-gap height="20" bg-color="#f8f8f8"></u-gap>
        <view>
            <view class="title u-border-bottom">被担保主债券信息</view>
            <view class="info">
                <view class="flex">
                    <view class="item">
                        <text class="gray">种类</text>
                        <view>{{con.stamp ? con.stamp : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">数额</text>
                        <view>{{con.amount ? con.amount : '-'}}</view>
                    </view>
                </view>
                <view>
                    <text class="gray">债务人履行债务的期限</text>
                    <view>{{con.fulfilmentdate ? con.fulfilmentdate : '-'}}</view>
                </view>
                <view>
                    <text class="gray">担保的范围</text>
                    <view>{{con.range ? con.range : '-'}}</view>
                </view>
                <view>
                    <text class="gray">备注</text>
                    <view>{{con.gremarks ? con.gremarks : '-'}}</view>
                </view>
            </view>
        </view>
        <u-gap height="20" bg-color="#f8f8f8"></u-gap>
        <view>
            <view class="title u-border-bottom">抵押物信息</view>
            <view class="info">
                <view class="flex">
                    <view class="item">
                        <text class="gray">名称</text>
                        <view>{{guaranty.name ? guaranty.name : '-'}}</view>
                    </view>
                    <view class="item u-border-left u-padding-left-20">
                        <text class="gray">所有权归属</text>
                        <view>{{guaranty.ownership ? guaranty.ownership : '-'}}</view>
                    </view>
                </view>
                <view>
                    <text class="gray">数量、质量、状况、所在地等情况</text>
                    <view>{{guaranty.situation ? guaranty.situation : '-'}}</view>
                </view>
                <view>
                    <text class="gray">备注</text>
                    <view>{{guaranty.remarks ? guaranty.remarks : '-'}}</view>
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
                corporatse:[],
                guaranty:[]
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
                    url: 'applets/mortgagesave',
                })
                console.log(res)
                this.con=res
                this.guaranty=res.guaranty
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
                margin:10rpx 0;
                align-items: center;
                justify-content: space-between;
            }
        }
    }
</style>