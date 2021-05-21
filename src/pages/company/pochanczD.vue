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
            <view class="flex u-border-bottom" v-for="item in bull" :key="item.id" @click="gdetail(item.id)">
                <view>{{item.title ? item.title : '1'}}</view>
                <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
            </view>
            <u-empty text="暂无信息" mode="list" class="u-margin-30" :show="emptyShows">
            </u-empty>
        </view>
        <view v-if="current==1">
            <view class="flex u-border-bottom" v-for="item in inst" :key="item.id">
                <view>{{item.title ? item.title : '-'}}</view>
                <u-icon name="arrow-right" color="#959595" size="35"></u-icon>
            </view>
            <u-empty text="暂无信息" mode="list" class="u-margin-30" :show="emptyShow">
            </u-empty>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                con:[],
                details:[],
                inst:{},
                bull:{},
                List: [{
                    name: '公告'
                }, {
                    name: '文书'
                }],
                current:0,
                emptyShow:false,
                emptyShows:false,
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
                if (res.instrument.length === 0) return this.emptyShow = true
                if (res.bulletin.length === 0) return this.emptyShows = true
                this.con=res
                this.details=res.details
                this.inst=res.instrument
                this.bull=res.bulletin
            },
            gdetail(id){
                uni.navigateTo({
                    url:'/pages/company/gonggaoD?id='+id
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
        line-height: 52rpx;
        padding:20rpx 30rpx;
        justify-content: space-between;
    }
</style>