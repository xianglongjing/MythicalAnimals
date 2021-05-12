<template>
    <view>
        <view class="form">
            <u-form :model="form" ref="uForm">
                <u-form-item label="企业名称" required label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.cname" required prop="cname" placeholder="请输入营业执照上的企业名称"/></u-form-item>
                <u-form-item label="企业税号" required label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.cnumber" required prop="cnumber" placeholder="请输入营业执照上的企业税号"/></u-form-item>
                <u-form-item label="企业地址" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.cadd" placeholder="请输入营业执照上的企业地址"/></u-form-item>
                <u-form-item label="企业电话" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.cphone" placeholder="请输入电话"/></u-form-item>
                <u-form-item label="开户银行" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.baccount" placeholder="请输入开户银行"/></u-form-item>
                <u-form-item label="银行账户" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.bank" placeholder="请输入开户银行账户"/></u-form-item>
            </u-form>
        </view>
        <u-button :customStyle="add" shape="circle" @click="sumbit">确认添加</u-button>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                form: {
                    cname: '',
                    cnumber: '',
                    cadd:'',
                    cphone: '',
                    bank:'',
                    baccount:''
                },
                edit:{
                    fontSize:'40rpx'
                },
                add:{
                    width:'85%',
                    marginTop:'350rpx',
                    color:'white',
                    fontSize:'34rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
                rules: {
                    cname: [{
                        required: true,
                        message: '请输入名称',
                        trigger: 'blur'
                    }],
                    cnumber: [{
                        required: true,
                        message: '请输入企业税号',
                        trigger: 'blur'
                    }],
                },
            }
        },
        onReady() {
            this.$refs.uForm.setRules(this.rules);
        },
        methods:{
            sumbit(){
                if(this.form.cname==''){
                    uni.showToast({
                        title: '请输入企业名称', //提示文字
                        duration: 1000, //显示时长
                        mask: true, //是否显示透明蒙层，防止触摸穿透，默认：false
                        icon: 'none'//图标，支持"success"、"loading"
                    })
                }else if(this.form.cnumber==''){
                    uni.showToast({
                        title: '请输入企业税号', //提示文字
                        duration: 1000, //显示时长
                        mask: true, //是否显示透明蒙层，防止触摸穿透，默认：false
                        icon: 'none'//图标，支持"success"、"loading"
                    })
                }else{
                     this.addfp()
                }
            },
            async addfp () {
                const { res } = await this.$request({
                    method: 'POST',
                    url: '/invoice',
                    data:this.form
                }).then(res=>{
                    console.log(res)
                    uni.navigateTo({
                        url:'/pages/shequ/fapiao'
                    })
                }).catch((err)=>{
                    console.log(err)
                });
                // console.log(res)
                // this.shopList = res.data
                // this.menuNum = 12 / res.data.length
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
    .form{
        background:white;
        margin:40rpx 20rpx;
        padding:0 20rpx;
        border-radius: 15rpx;
    }
</style>