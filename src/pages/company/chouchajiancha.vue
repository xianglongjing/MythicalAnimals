<template>
    <view class="page u-border-top">
        <view class="tab u-border-bottom">
            <u-tabs
                    :list="List"
                    :current="current"
                    @change="Change"
                    bar-width="50" font-size="30"
                    active-color="#E12216" bg-color="none" inactive-color="#000000"
            ></u-tabs>
        </view>
        <view v-if="current==0">
            <view class="con" v-for="item in con" :key="item.id">
                <view>
                    <text class="gray">检查实施机关：</text>
                    <text>{{item.organ ? item.organ : '-'}}</text>
                </view>
                <view>
                    <text class="gray">类型：</text>
                    <text>{{item.type ? item.type : '-'}}</text>
                </view>
                <view>
                    <text class="gray">结果：</text>
                    <text>{{item.result ? item.result : '-'}}</text>
                </view>
                <view>
                    <text class="gray">日期：</text>
                    <text>{{item.date ? item.date : '-'}}</text>
                </view>
            </view>
        </view>
       <view v-if="current==1">
           <u-empty text="暂无相关信息" mode="list" class="u-margin-30" :show="emptyShow">
           </u-empty>
       </view>
        <view v-if="current==2">
            <u-empty text="暂无相关信息" mode="list" class="u-margin-30" :show="emptyShow">
            </u-empty>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                List: [{
                    name: '市场监管'
                }, {
                    name: '产品质量监督'
                },
                    {
                        name: '认证监督司'
                    }],
                current:0,
                con:{},
                emptyShow:true
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
                    url: 'applets/survey',
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
        color:#959595;
    }
    .tab{
        background: white;
        text-align: center;
    }
    .con{
        background: white;
        line-height: 50rpx;
        padding:25rpx 20rpx;
    }
</style>