<template>
    <view class="page">
        <view style="height:470rpx">
        <view class="bg" :style="bg">
            <view class="title">
                <view>尊敬的用户</view>
                <view>本次申请需要您完成实名认证</view>
            </view>
        </view>
        <view class="form">
            <view class="title">主体信息</view>
            <u-form :model="form" ref="uForm">
<!--                <u-form-item label="主体类型" :label-style="label" label-width="170" right-icon="question-circle"><u-input v-model="form.type" placeholder="企业"/></u-form-item>-->
                <view class="flex">
                    <text class="u-margin-right-40 u-font-31">主体类型</text>
                    <u-input v-model="text" :type="types" :border="borders" @click="show = true"/>
                </view>
               <view class="flex">
                <u-action-sheet :list="actionSheetList" v-model="show" @click="actionSheetCallback"></u-action-sheet>
<!--                <u-icon name="question-circle"></u-icon>-->
               </view>
                <u-form-item label="企业名称" :label-style="label" label-width="170" right-icon="arrow-right"><u-input v-model="form.cname" placeholder="请输入营业执照上的企业名称"/></u-form-item>
            </u-form>
        </view>
        </view>
        <view class="person">
            <view class="title">法定代表人信息</view>
            <view class="u-border-bottom" style="padding:0">
            <view class="u-line-1 push">需使用企业法定代表人的支付宝实名账号提交，您也可以</view>
            <view class="send u-border-bottom">转发给法定代表人</view>
                <u-field
                        v-model="form.lpname"
                        label="姓名"
                        placeholder="输入营业执照上法定代表人姓名" :border-bottom="border" style="margin:0"
                ></u-field>
            </view>
        </view>
        <view class="back" @click="back">
            返回认证首页 <text class="cuIcon-right"></text>
        </view>
        <view class="footer">
            <view>我是上述企业的法定代表人，同意 <text class="red">《声明》</text>及<text class="red">《芝麻信用企业服务协议》</text></view>
            <u-button :customStyle="add" shape="circle" @click="go">提交并开始认证</u-button>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return{
                text:'',
                borders:false,
                types: 'select',
                actionSheetList: [
                    {   id:1,
                        text: '企业'
                    },
                    {   id:2,
                        text: '个人工商户'
                    },
                    {   id:3,
                        text: '其他'
                    }
                ],
                show: false,
                form: {
                    type: '',
                    lpname: '',
                    cname:'',
                },
                list: [
                    {
                        value: '1',
                        label: '江'
                    },
                    {
                        value: '2',
                        label: '湖'
                    }
                ],

                label:{
                    fontSize:'32rpx'
                },
                border:false,
                add:{
                    width:'85%',
                    marginTop:'50rpx',
                    color:'white',
                    fontSize:'34rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
                bg: {
                    // backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 340rpx",
                    margin:'0rpx auto',
                    borderRadius:"10rpx"
                },
            }

        },
        methods:{
            actionSheetCallback(index) {
                this.text = this.actionSheetList[index].text;
                this.form.type = this.actionSheetList[index].id;
            },
            //返回认证首页
            back(){
                uni.navigateTo({
                    url:'/pages/confirm/shopconfirm'
                })
            },
            async go () {
                 await this.$request({
                    method: 'POST',
                    url: '/information',
                    data:this.form
                }).then(res=>{
                    console.log(res)
                     uni.navigateTo({
                         url:'/pages/confirm/shopconfirm'
                     })
                }).catch((err)=>{
                    console.log(err)
                });
                // console.log(res.data)
                console.log(this.form)
                // this.menuNum = 12 / res.data.length
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
    .flex{
        flex-direction: row;
        display: flex;
    }
.bg{
    background-size: 750rpx 340rpx;
    background: url("https://yiqiwang360.com/images/yiqiguanjia/redbg.png") no-repeat;
    padding:30rpx;
    width:100%;
    height:330rpx;
    position: relative;
    .title{
        color:white;
        font-size: 35rpx;
    }
}
    .form{
        background: white;
        width:92%;
        padding:30rpx 30rpx 0;
        position: absolute;
        left:30rpx;
        top:170rpx;
        border-radius: 14rpx;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
        }
        .flex{
            flex-direction: row;
            display: flex;
            align-items: center;
        }
        .flexs{
            width:100%;
            display: flex;
            flex-direction: row;
            justify-content: space-between;
        }
    }
    .person{
        background: white;
        width:92%;
        height: 270rpx;
        border-radius: 10rpx;
        margin:30rpx 30rpx;
        .title{
            padding:30rpx 30rpx 10rpx;
            font-size: 35rpx;
            font-weight: 1000;
        }
        .push{
            color:#777777;
            font-size: 25rpx;
            padding:0 30rpx;
        }
        .send{
            padding:6rpx 30rpx 20rpx;
            width:100%;
            color:#E01C14;
        }
    }
    .back{
        text-align: center;
        margin-top: 80rpx;
        color:#A2A2A2;
    }
    .footer{
        background: white;
        padding:20rpx 30rpx;
        margin-top:150rpx;
        .red{
            color:#E01C14;
        }
    }
</style>