<template>
    <view class="page">
        <view class="con">
            <u-field
                    v-model="name"
                    label="企业名称" style="font-weight: 1000"
                    placeholder="临沂市铭远企业管理服务有限公司" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="shui"
                    label="企业税号" style="font-weight: 1000"
                    placeholder="123456789" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="address"
                    label="企业地址" style="font-weight: 1000"
                    placeholder="山东省临沂市" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="phone"
                    label="就业电话" style="font-weight: 1000"
                    placeholder="13337887272" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="hang"
                    label="开户银行" style="font-weight: 1000"
                    placeholder="中国银行" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
            <u-field
                    v-model="zhang"
                    label="银行账户" style="font-weight: 1000"
                    placeholder="0123123456789" placeholder-style="text-align:right;font-weight:normal"
            >
            </u-field>
        </view>
        <u-button :customStyle="add" shape="circle">编辑</u-button>
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
                add:{
                    width:'81%',
                    marginTop:'400rpx',
                    color:'white',
                    fontSize:'34rpx',
                    backgroundImage: "url(" + require("../../static/image/redbg.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
            }
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