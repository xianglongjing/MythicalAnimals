<template>
    <view class="page u-border-top">
        <view class="tab u-border-bottom">
            <u-tabs
                    :list="List"
                    :current="current"
                    @change="Change" gutter="70"
                    bar-width="50" font-size="30"
                    active-color="#E2291D" bg-color="none" inactive-color="#666666"
            ></u-tabs>
        </view>
        <view class="con u-border-bottom" v-for="item in con" :key="item.id" @click="detail(item.id)">
            <view class="left">
                <view>
                    <text class="gray">案号：</text>
                    <text>{{item.case ? item.case : '-'}}</text>
                </view>
                <view>
                    <text class="gray">标的物名称：</text>
                    <text>{{item.sname ? item.sname : '-'}}</text>
                </view>
                <view>
                    <text class="gray">财产类型：</text>
                    <text>{{item.type ? item.type : '-'}}</text>
                </view>
                <view>
                    <text class="gray">发布日期：</text>
                    <text>{{item.lottery ? item.lottery : '-'}}</text>
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
                List: [{
                    name: '询价评估结果'
                }, {
                    name: '选定评估机构'
                }],
                current:0,
                con:{}
            }
        },
        onLoad(options){
            this.getSearchList(options.id)
        },
        methods:{
            Change(index) {
                this.current = index;
            },
            async getSearchList (id) {
                const {data:res}  = await this.$request({
                    method:'GET',
                    url: 'applets/inquiry',
                    data: {
                        id:id
                    }
                })
                console.log(res)
                this.con = res
            },
            detail(id){
                uni.navigateTo({
                    url:'/pages/company/xunjiapingguD?id='+id
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
.tab{
    text-align: center;
    background: white;
}
    .con{
        padding:25rpx;
        background: white;
        display: flex;
        justify-content: space-between;
        align-items: center;
        line-height: 50rpx;
    }
</style>