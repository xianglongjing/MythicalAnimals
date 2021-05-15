<template>
    <view class="page">
<!--        <view class="screen">-->
<!--&lt;!&ndash;            <u-dropdown>&ndash;&gt;-->
<!--&lt;!&ndash;                <u-dropdown-item v-model="value1" title="全部行业" :options="options1"></u-dropdown-item>&ndash;&gt;-->
<!--&lt;!&ndash;                <u-dropdown-item v-model="value2" title="默认距离" :options="options2"></u-dropdown-item>&ndash;&gt;-->
<!--&lt;!&ndash;            </u-dropdown>&ndash;&gt;-->
<!--            <text class="u-margin-right-50">更多筛选</text>-->
<!--        </view>-->
        <view class="find">
<!--            为你找到-->
<!--            <text class="red">123456</text>-->
<!--            家公司-->
            <view class="shop" v-for="item in con" :key="item.id">
                <view class="shop-top">
                <u-image mode="aspectFill" src="http://images.yiqiwang360.com/yiqicha/gongsiming.png" width="50" height="50"></u-image>
                    <view class="shop-r">
                        <view class="name">{{item.cpyname}}</view>
                    </view>
                    <view>
                        <text class="red status">在营(开业)企业</text>
                    </view>
                </view>
                <view class="info">
                    <view class="item u-border-right">
                        <view>法定代表人</view>
                        <view>{{item.partner.name}}</view>
                    </view>
                    <view class="item u-border-right">
                        <view>注册资本</view>
                        <view>{{item.rtdcapital ? item.rtdcapital : '-'}}{{item.rtdcapital ? '万' : ''}}</view>
                    </view>
                    <view class="item">
                        <view>成立日期</view>
                        <view>{{item.ebhtdate ? item.ebhtdate : '-'}}</view>
                    </view>
                </view>
                <view class="phones u-padding-left-20 u-margin-top-20 u-margin-left-50">
                    <text>电话：</text>
                    <text class="phone">{{item.phone ? item.phone : '-'}}</text>
                </view>
                <view class="position">
                    <view class="daohang">
                    <u-image src="http://images.yiqiwang360.com/yiqicha/daohang.png" width="25" height="25"></u-image>
                    <text class="u-margin-left-20">
<!--                        距您35米| -->
                        {{item.address ? item.address : '-'}}</text>
                    </view>
                    <view class="red">导航</view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                con:{},
                // key: '35d32d635e17746f7054c71c8539a377',
                value1: '',
                value2: '',
                options1: [{
                    label: '默认排序',
                    value: 1,
                },
                    {
                        label: '距离优先',
                        value: 2,
                    },
                    {
                        label: '价格优先',
                        value: 3,
                    }
                ],
                options2: [{
                    label: '去冰',
                    value: 1,
                },
                    {
                        label: '加冰',
                        value: 2,
                    },
                ],
            }
        },

        onLoad(){
            this.location()
            this.getLocation()
        },
        methods:{
            async location () {
                this.pageNum++
                const { data: res } = await this.$request({
                    method: 'POST',
                    url: 'applets/nearby',
                    data: {
                        longitude: 118.350432,
                        latitude: 35.10283,
                        page:1
                    }
                })
                this.con=res
               console.log(res)
                // uni.navigateTo({
                //     url: '/pages/ll/searchDetail?keyword=' + this.keyword
                // })
            },
            //定位信息
            getLocation(){
                uni.getLocation({
                    type: 'wgs84',
                    success: function (res) {
                        console.log(res)
                        if (res.address){
                            this.district = res.address.district
                        }
                    }
                })
            },
            // location(){
            //     uni.chooseLocation({
            //         success: function(res) {
            //             console.log(res)
            //             console.log('位置名称：' + res.name);
            //             console.log('详细地址：' + res.address);
            //             console.log('纬度：' + res.latitude);
            //             console.log('经度：' + res.longitude);
            //             let latitude = res.latitude; //纬度
            //             let longitude = res.longitude; //经度
            //         }
            //     });
            // },
            lo(){
                uni.getLocation({
                    type: 'gcj02', //返回可以用于uni.openLocation的经纬度
                    success:(res)=>{
                        let that=this
                        const latitude = res.latitude;
                        const longitude = res.longitude;
                        console.log(res)
                        uni.request({
                            header:{
                                "Content-Type": "application/text"
                            },
                            //注意:这里的key值需要高德地图的 web服务生成的key  只有web服务才有逆地理编码
                            url:'https://restapi.amap.com/v3/geocode/regeo?output=JSON&location='+res.longitude+','+res.latitude+'&key=280802ed0116fef931dbcf5e7e9278d7&radius=1000&extensions=all',
                            success(re) {
                                console.log(re)
                                if(re.statusCode===200){
                                    that.citydata=re.data.regeocode.addressComponent.city
                                    console.log("获取中文街道地理位置成功",that.citydata)

                                }else{
                                    console.log("获取信息失败，请重试！")
                                }
                            }
                        });
                    }
                })
            },
        }
    }
</script>

<style lang="scss" scoped>
    .red{
        color:#E75D54;
    }
    page{
        background: #f8f8f8;
    }
.screen{
    display: flex;
    flex-direction: row;
    align-items: center;
    background: white;
}
    .find{
        padding:20rpx 30rpx;
        .shop{
            margin:20rpx 0;
            padding:20rpx;
            background: white;
            .shop-top{
                justify-content: center;
                display: flex;
                flex-direction: row;
                padding:10rpx 0 30rpx;
                .shop-r{
                    flex:1;
                    margin-left:30rpx;
                    .name{
                      font-size: 30rpx;
                        font-weight: 650;
                        padding:0rpx 0 10rpx;
                    }

                }
                .status{
                    border:1rpx solid #B4B5B5;
                    padding:5rpx;
                    font-size: 22rpx;
                    border-radius: 5rpx;
                }
            }
            .info{
                display: flex;
                align-items: center;
                justify-content: center;
                text-align: center;
                .item{
                    flex-grow: 1;
                    line-height: 50rpx;
                }
            }
            .phones{
                background:#f8f8f8;
                padding:15rpx 10rpx;
                .phone{
                    color:#fd5123;
                }
            }
            .position{
                display: flex;
                flex-direction: row;
                justify-content: space-between;
                padding:20rpx 0 0 25rpx;
                .daohang{
                    display: flex;
                    flex-direction: row;
                    align-items: center;
                }
            }
        }
    }
</style>