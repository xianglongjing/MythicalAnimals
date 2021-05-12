<template>
    <view class="page">
        <view style="height:670rpx">
            <view class="bg" :style="bg">
                <view class="title">
                    <view>尊敬的用户</view>
                    <view>本次申请需要您完成实名认证</view>
                </view>
            </view>
            <view class="form">
                <view class="title">工商营业执照</view>
                <view class="card">
                    <image :src="image.business || 'https://yiqiwang360.com/images/yiqiguanjia/cardbusi.png'" class="fu"></image>
                    <u-button :customStyle="push" shape="circle" @click="upload">
                        <u-icon name="camera"></u-icon>
                        上传三证合一营业执照
                    </u-button>
                </view>
                <view class="desc u-margin-left-30 u-line-1">1.证件需清晰完整并在有效期内，复印件需加盖公章</view>
                <view class="desc u-margin-left-30 u-line-1">2.图片大小不超过10M</view>
            </view>
        </view>
        <view class="idcard">
            <view class="title">身份证正反面</view>
            <view class="images">
                <u-image mode="aspectFit" :src="image.side || 'https://yiqiwang360.com/images/yiqiguanjia/cardhui2.png'" width="350" height="200" class="u-margin-right-20" border-radius="15" @click="sides"></u-image>
                <u-image mode="aspectFit" :src="image.front || 'https://yiqiwang360.com/images/yiqiguanjia/cardhui1.png'" width="350" height="200" border-radius="15" @click="fronts"></u-image>
            </view>
            <view class="desc u-line-1">1.证件需清晰完整并在有效期内</view>
            <view class="desc u-line-1">2.图片大小不超过10M</view>
        </view>
        <view class="footer">
            <view class="u-line-1">我是上述企业的法定代表人，同意 <text class="agree">《声明》</text>及<text class="agree">《企业服务协议》</text></view>
            <u-button :customStyle="add" shape="circle" @click="uploadCards">提交并开始认证</u-button>
        </view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                bankCardBase64:null,
                frontbase:null,
                sidebase:null,
                uploadList:[],
                uploadLists:[],
                image:{
                    business:'',
                    side:'',
                    front:'',
                },
                paidImgUrl:'https://yiqiwang360.com/images/yiqiguanjia/cardbusi.png',
                bg: {
                    // backgroundImage: "url(" + require("https://yiqiwang360.com/images/yiqiguanjia/redbg.png") + ")",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 340rpx",
                    margin: '0rpx auto',
                    borderRadius: "10rpx"
                },
                add: {
                    width: '85%',
                    marginTop: '50rpx',
                    color: 'white',
                    fontSize: '34rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
                push: {
                    width: '300rpx',
                    height: '50rpx',
                    position: 'absolute',
                    fontSize: '23rpx',
                    top: '200rpx',
                    left: '200rpx',
                    background: '#ACACAC',
                    color: 'white'
                },
                card: {
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/cardbusi.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "420rpx 250rpx",
                }
            }

        },
        methods: {
            upload : function() {
                uni.chooseImage({
                    count:1,
                    success:(res)=>{
                        this.image.business = res.tempFilePaths;
                        this.uploadList.push(res.tempFilePaths);
                    }
                })
            },
            sides : function() {
                uni.chooseImage({
                    count:1,
                    success:(res)=>{
                        this.image.side = res.tempFilePaths;
                        this.uploadList.push(res.tempFilePaths);
                    }

                })
            },
            fronts : function() {
                uni.chooseImage({
                    count:1,
                    success:(res)=>{
                        this.image.front = res.tempFilePaths;
                        // let img = {name:'front',uri:[res.tempFilePaths]};
                        // this.uploadLists.push(res.tempFilePaths);
                        this.uploadList.push(res.tempFilePaths);
                        /*//将图片url转换为base64
                        this.$pathToBase64(res.tempFilePaths[0]).then(base64=>{
                            this.frontbase=base64
                        }).catch(error=>{
                            console.log(error)
                        })*/

                    }

                })

            },
            uploadCards : function(){
               if(this.image.business == 'https://yiqiwang360.com/images/yiqiguanjia/cardbusi.png'){
                    uni.showToast({title:"请选择营业执照", icon:"none"});
                    return;

                }
                /* uni.showLoading({title:"上传中"});
                var param={
                    type:2,
                    images:[
                        {
                            business:"business",
                            front:'front',
                            side:'side',
                            image: {bankCardBase64:this.bankCardBase64,frontbase:this.frontbase,sidebase:this.sidebase},
                            orderNum:1
                        }
                    ]
                }*/
                for (var i = 0;i < this.uploadList.length;i++) {
                    uni.uploadFile({
                        url: 'http://192.168.8.39:8081/certificate',
                        fileType: "image",
                        filePath: this.uploadList[i][0],
                        name: 'file',
                        formData: {
                            token:uni.getStorageSync('token'),
                            name:i
                        },
                        header: {
                            'content-type': 'multipart/form-data'
                        },
                        success: (res) => {
                            console.log(res)
                            uni.navigateTo({
                                url:'/pages/confirm/shopconfirm'
                            })
                        },
                    });
                }
                console.log(this.uploadList)
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
    .form {
        background: white;
        width: 92%;
        padding: 30rpx 30rpx;
        position: absolute;
        left: 30rpx;
        top: 170rpx;
        border-radius: 14rpx;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
        }
        .card{
            width:420rpx;
            height:250rpx;
            margin:20rpx auto;

            .fu{
                width:420rpx;
                height:230rpx;
                position: relative;
            }
        }
        .desc{
            font-size: 25rpx;
            line-height:45rpx ;
            color:#989898;
        }
    }
    .idcard{
        background: white;
        width: 92%;
        padding: 30rpx 30rpx;
        margin:20rpx 30rpx;
        border-radius: 15rpx;
        .title{
            font-size: 35rpx;
            font-weight: 1000;
        }
        .images{
            margin:10rpx 0 20rpx;
            display: flex;
            flex-direction: row;
        }
        .desc{
            font-size: 25rpx;
            line-height:40rpx ;
            color:#989898;
        }
    }
    .footer{
        font-size: 23rpx;
        background:white;
        margin-top:150rpx;
        padding:30rpx;
        .agree{
            color:#E74B46;
        }
    }
</style>