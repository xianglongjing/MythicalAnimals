<template>
    <view class="page">
        <view class="con">
            <u-field
                    v-model="name"
                    label="预约城市" style="font-weight: 700;font-size: 32rpx"
                    placeholder="临沂兰山" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="shui"
                    label="预约社区" style="font-weight: 1000;font-size: 32rpx"
                    placeholder="中关村社区" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="address"
                    label="姓名" style="font-weight: 1000;font-size: 32rpx"
                    placeholder="韩梅梅"  placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="phone"
                    label="电话" style="font-weight: 1000;font-size: 32rpx"
                    placeholder="13337887272" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="hang"
                    label="预约日期" style="font-weight: 1000;font-size: 32rpx"
                    placeholder="2021-03-10"  placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="zhang"
                    label="公司" style="font-weight: 1000;font-size: 32rpx"
                    placeholder="0123123456789" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="zhang"
                    label="备注" style="font-weight: 1000;font-size: 32rpx"
                    placeholder="0123123456789" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
        </view>
        <u-button :customStyle="add" shape="circle" @click="post">提交预约</u-button>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                name:'',
                shui:'',
                phone:'',
                address:'',
                hang:'',
                zhang:'',
                disabled:true,
                add:{
                    width:'81%',
                    marginTop:'400rpx',
                    color:'white',
                    fontSize:'34rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
            }
        },
        methods:{
            post(){
                uni.navigateTo({
                    url:'/pages/visit/success'
                })
            },
        }
    }
</script>
<style lang="scss">
    page {
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    .con{
        margin:20rpx;
        background: white;
    }
    .right{
        text-align: right;
    }
</style>