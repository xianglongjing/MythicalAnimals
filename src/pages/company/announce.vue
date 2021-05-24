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
        <view class="white" v-for="item in con" :key="item.id">
            <view class="info">
                <view class="info-l">
                    <u-image mode="aspectFill" width="80" height="80"
                             :src="item.image || 'https://seopic.699pic.com/photo/50139/5280.jpg_wh1200.jpg'"></u-image>
                    <text class="red u-margin-left-30">{{item.name}}</text>
                </view>
                <view>
                    <text>任职{{item.registernumber ? item.registernumber : '-'}}家企业</text>
                </view>
            </view>
            <view class="u-margin-top-20">
                <text class="gray">持股比例</text>
                <view>{{item.ratio ? item.ratio : '-'}}</view>
            </view>
            <view class="flex">
                <view>
                    <text class="gray">认缴出资额</text>
                    <view>{{item.scc ? item.scc : '-'}}</view>
                </view>
                <view class="u-border-left u-padding-left-20">
                    <text class="gray">实缴出资额</text>
                    <view>{{item.capital ? item.capital : '-'}}</view>
                </view>
            </view>
            <view class="flex">
                <view>
                    <text class="gray">认缴出资日期</text>
                    <view>{{item.sccd ? item.sccd : '-'}}</view>
                </view>
                <view class="u-border-left u-padding-left-20">
                    <text class="gray">实缴出资日期</text>
                    <view>{{item.payment ? item.payment : '-'}}</view>
                </view>
            </view>
            <view class="flex">
                <view>
                    <text class="gray">认缴公示日期</text>
                    <view>{{item.spad ? item.spad : '-'}}</view>
                </view>
                <view class="u-border-left u-padding-left-20">
                    <text class="gray">实缴公示日期</text>
                    <view>{{item.padoap ? item.padoap : '-'}}</view>
                </view>
            </view>
            <view class="flex">
                <view>
                    <text class="gray">认缴出资方式</text>
                    <view>{{item.sttccm ? item.sttccm : '-'}}</view>
                </view>
                <view class="u-border-left u-padding-left-20">
                    <text class="gray">实缴出资方式</text>
                    <view>{{item.mopc ? item.mopc : '-'}}</view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                List: [{
                    name: '股东及出资信息1'
                }, {
                    name: '股东变更信息0'
                }],
                current:0,
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
                    url: 'applets/trademarksave',
                })
                console.log(res)
                this.con=res
            },
            Change(index) {
                this.current = index;
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
        color:#777777;
    }
    .red{
        color:#E12216;
    }
    .tab{
        background:white;
    }
.white{
    background:white;
    padding:25rpx;
    .info{
        display: flex;
        align-items: center;
        justify-content: space-between;
        .info-l{
            align-items: center;
            display: flex;
        }
    }
    .flex{
        margin:20rpx 0;
        line-height: 50rpx;
        justify-content: space-between;
        view{
            flex:1;
        }
    }
}
</style>