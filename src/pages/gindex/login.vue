<template>

    <view>
        <u-button open-type="getUserInfo" :customStyle="login" lang="zh_CN" @getuserinfo="onGotUserInfo">获取用户信息</u-button>
        </view>

</template>

<script>
    export default {
        data() {
            return {
                indata: {},
                login: {
                    width: '85%',
                    margin: '50rpx auto',
                    color: 'white',
                    fontSize: '34rpx',
                    backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                },
                userInfo: [],
                storage: []
            }
        },
        onLoad() {
            // 执行查看授权选项
            this.getSettingMes();
        },
        methods: {
            getlist() {
                uni.login({
                    provider: 'weixin',
                    success: function (res) {
                        console.log(res)
                        let appid = ''
                        let secret = ''
                        let url = ' http://192.168.8.39:8081/login?appid=' + appid + '&secret=' + secret + '&js_code=' +
                            res.code + '&grant_type=authorization_code';
                        uni.request({
                            url: 'http://192.168.8.39:8081/login',
                            methods: 'POST',// 请求路径
                            success: result => {
                                console.info("result.data==>", result.data);
                                let openId = result.data.openid;
                                console.info("openId==>", openId);
                                uni.switchTab({
                                    url: '/pages/mine/mine'
                                })
                            },
                        });
                    }
                })
            },

            // 查看已授权选项
            getSettingMes() {
                let _this = this;
                uni.getSetting({
                    success(res) {
                        if (res.authSetting['scope.userInfo']) {
                            // 用户信息已授权，获取用户信息
                            uni.getUserInfo({
                                success(res) {
                                    console.log(res);
                                },
                                fail() {
                                    console.log("获取用户信息失败")
                                }
                            })
                        } else if (!res.authSetting['scope.userInfo']) {
                            console.log("需要点击按钮手动授权")
                        }
                    },
                    fail() {
                        console.log("获取已授权选项失败")
                    }
                })
            },
            // 手动授权方法
            onGotUserInfo(e) {
                let that = this
                uni.login({
                    success(res) {
                        let code = res.code
                        uni.getUserInfo({
                            // 获取信息成功
                            success(ress) {
                                console.log(code)
                                that.getOpenId(code, ress.userInfo)
                            },
                            fail() {
                                console.log("获取用户信息失败");
                            }
                        })

                    }
                })
                // 获取用户信息

            },
            async getOpenId(code, userInfo) {
                let datas = userInfo
                datas['code'] = code
                const {data: res} = await this.$request({
                    method: 'POST',
                    url: '/login',
                    data: datas
                })
                console.log(111111)
                console.log(res.data)
                console.log(res.data.info)
                console.log(11111)
                uni.setStorageSync('token', res.data.token)
                uni.setStorageSync('avatarUrl', res.data.avatarUrl)
                uni.setStorageSync('nickName', res.data.nickName)
                uni.setStorageSync('id', res.data.id)
                uni.switchTab({
                    url: '/pages/mine/mine'
                })
                this.userinfo(res.data.token)
                // this.care = res.data
                // this.menuNum = 12 / res.data.length
            },
        }
    }
</script>

<style scoped>

</style>