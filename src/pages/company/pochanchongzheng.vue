<template>
    <view class="page u-border-top">
        <view class="white">
            <view>
                <view class="gray">案号</view>
                <view>{{details.case ? details.case : '-'}}</view>
            </view>
            <view>
                <view class="gray">案件类型</view>
                <view>{{details.type ? details.type : '-'}}</view>
            </view>
            <view>
                <view class="gray">被申请人</view>
                <view>{{details.respondent ? details.respondent : '-'}}</view>
            </view>
            <view>
                <view class="gray">申请人</view>
                <view>{{details.applicant ? details.applicant : '-'}}</view>
            </view>
            <view>
                <view class="gray">经办法院</view>
                <view>{{details.tioe ? details.tioe : '-'}}</view>
            </view>
            <view>
                <view class="gray">管理人机构</view>
                <view>{{details.manager ? details.manager : '-'}}</view>
            </view>
            <view>
                <view class="gray">管理人主要负责人</view>
                <view>{{details.tmpicotm ? details.tmpicotm : '-'}}</view>
            </view>
            <view>
                <view class="gray">公开日期</view>
                <view>{{details.date ? details.date : '-'}}</view>
            </view>
        </view>
        <u-gap height="20" bg-color="#f7f7f7"></u-gap>
        <view class="tab u-border-bottom">
            <u-tabs
                    :list="List"
                    :current="current"
                    @change="Change" gutter="140"
                    bar-width="50" font-size="30"
                    active-color="#E12216" bg-color="none" inactive-color="#000000"
            ></u-tabs>
        </view>
        <view v-if="current==0">
            <view class="flex">
                <view></view>
                <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                con:[],
                details:[],
                List: [{
                    name: '公告'
                }, {
                    name: '文书'
                }],
                current:0,
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
                    url: 'applets/bankruptcysave',
                })
                console.log(res)
                this.con=res
                this.details=res.details
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/dianxinxukeD?id='+id
                })
            },
            Change(index) {
                this.current = index;
            },
        }
    }
</script>

<style lang="scss" scoped>
    .gray{
        color:#959595;
    }
.white{
    padding:25rpx;
    line-height: 50rpx;
}
    .tab{
        text-align: center;
    }
    .flex{
        padding:20rpx 30rpx;
        justify-content: space-between;
    }
</style>