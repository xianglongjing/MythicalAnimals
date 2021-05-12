<template>
    <view class="page">
        <view class="form">
            <u-form :model="form" ref="uForm">
                <u-form-item label="企业名称" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.name" required prop="name"/></u-form-item>
                <u-form-item label="企业地址" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.add" required prop="add"/></u-form-item>
                <u-form-item label="企业电话" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.phone" required prop="phone"/></u-form-item>
                <u-form-item label="企业邮箱" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.email" /></u-form-item>
                <u-form-item label="企业网址" label-width="150" right-icon="edit-pen" :right-icon-style="edit"><u-input v-model="form.url" /></u-form-item>
            </u-form>
        </view>
<!--        <view class="service">-->
<!--            <view class="title">产品/服务</view>-->
<!--            <view class="ser-desc">临沂市铭远企业管理服务有限公司经营范围包括:商务信息咨询;财务信息咨询</view>-->
<!--            <u-icon name="edit-pen" size="40" color="gray" class="right"></u-icon>-->
<!--        </view>-->
<!--        <view class="service">-->
<!--            <view class="title">企业公告</view>-->
<!--            <view class="ser-desc">临沂市铭远企业管理服务有限公司经营范围包括:商务信息咨询;财务信息咨询</view>-->
<!--            <u-icon name="edit-pen" size="40" color="gray" class="right"></u-icon>-->
<!--        </view>-->
        <view class="post">
            <view class="title">资质提交</view>
            <view class="card">
                <image src="https://yiqiwang360.com/images/yiqiguanjia/cardbusi.png" class="fu"></image>
             <u-button :customStyle="push" shape="circle">
                 <u-icon name="camera"></u-icon>
                 上传三证合一营业执照
             </u-button>
            </view>
        </view>
        <u-button :customStyle="post" shape="circle">提交审核</u-button>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                form: {
                    name: '',
                    add: '',
                    phone: '',
                    email:'',
                    url:''
                },
                rules: {
                    name: [{
                        required: true,
                        message: '请输入名称',
                        trigger: 'blur'
                    }],
                    add: [{
                        required: true,
                        message: '请输入详细地址',
                        trigger: 'blur'
                    }],
                    phone: [
                        {
                            required: true,
                            message: '请输入手机号码',
                            trigger: 'blur'
                        },
                        {
                            validator: (rule, value, callback) => {
                                return this.$u.test.mobile(value)
                            },
                            message: '手机号码不正确',
                            trigger: 'blur',
                        }
                    ]
                },
                post:{
                    width:'80%',
                    height:'90rpx',
                    fontSize:'32rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                    margin:'50rpx auto',
                    color:'white'
                },
                edit:{
                    fontSize:'40rpx'
                },
                push:{
                    width:'300rpx',
                    height:'50rpx',
                    position:'absolute',
                    fontSize:'23rpx',
                    top:'100rpx',
                    left:'60rpx',
                    background:'#ACACAC',
                    color:'white'
                },
            //     card:{
            //         backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/cardbusi.png)",
            //         backgroundRepeat: "no-repeat",
            //         backgroundSize: "420rpx 250rpx",
            // }
            }
        },
        onReady () {
            this.$refs.uForm.setRules(this.rules)
        },
        methods:{
            submitAddress () {
                this.$refs.uForm.validate(async valid => {
                    if (valid) {
                        if (this.form.name === '' ||
                            this.form.phone === '' ||
                            this.form.add === ''
                        ) return uni.showToast({
                            title: '请完整填写内容',
                            icon: 'none'
                        })
                        const { data: res } = await this.$request({
                            url: '/enterprise/store',
                            data: Object.assign(
                                {},
                                // {
                                //     uid: this.storage.uid,
                                //     token: this.storage.token,
                                //     status: this.status
                                // },
                                this.form
                            )
                        })
                        this.$refs.uForm.resetFields()
                        uni.showToast({
                            title: '添加企业成功',
                            icon: 'none',
                            success: () => {
                                if (this.id === 'undefined') {
                                    uni.redirectTo({
                                        url: '/pages/mine/mine'
                                    })
                                }
                            }
                        })
                    } else {
                        return uni.showToast({
                            title: '请正确填写或填写完整',
                            icon: 'none'
                        })
                    }
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
.form{
    background:white;
    margin:50rpx 30rpx;
    padding:0 20rpx;
    border-radius: 15rpx;
}
    .service{
        background:white;
        padding:20rpx 20rpx 40rpx;
        margin:0 30rpx 20rpx;
        border-radius: 13rpx;
        position: relative;
        .title{
            padding:0 0 15rpx;
        }
        .ser-desc{
            font-size: 21rpx;
            line-height: 40rpx;
        }
        .right{
            position: absolute;
            right:20rpx;
            bottom: 10rpx;
        }
    }
    .post{
        background: white;
        border-radius: 13rpx;
        padding:20rpx 20rpx;
        margin:0 30rpx 20rpx;
        .card{
            width:420rpx;
            height:400rpx;
            margin:20rpx auto;
            position: relative;
            .fu{
                width:420rpx;
                height:230rpx;
                position: relative;
            }
        }
    }
</style>