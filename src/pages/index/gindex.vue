
<template>
    <view class="page">
        <view class="bgred" :style ="bg">
            <view class="bg-top">
                <view class="u-margin-right-20">
                    <image class="navbar-icon" src="https://yiqiwang360.com/images/yiqiguanjia/icons/shou.png" style="width:50rpx;height:40rpx"></image>
                    <text class="navbar-text">医企管家</text>
                </view>
                <u-search
                        :action-style="search_btn"
                        :animation="true" shape="round"
                        @custom="goSearch"
                        @search="goSearch"
                        bg-color="#E36966"
                        input-align="left"
                        placeholder="搜索服务" color="white" placeholder-color="white"
                        v-model="keyword" height="50" style="opcity:0.3"
                ></u-search>
            </view>
        </view>
        <view class="page-section">
            <view class="section-item" @click="shop">
                <view>
                    <view class="title">企业认证</view>
                    <text>产品认证/体系认证</text>
                </view>
                <view>
                    <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/icons/qiye.png" width="50" height="50"></u-image>
                </view>
            </view>
            <view class="section-item" @click="fapiao">
                <view>
                    <view class="title">发票抬头</view>
                    <text>商业发票/海运提单</text>
                </view>
                <view>
                    <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/icons/piao.png" width="55" height="55"></u-image>
                </view>
            </view>
            <view class="section-item">
                <view>
                    <view class="title">扫名片</view>
                    <text>精准智能识别名片</text>
                </view>
                <view>
                    <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/icons/card.png" width="55" height="45"></u-image>
                </view>
            </view>
            <view class="section-item">
                <view>
                    <view class="title">我的客服</view>
                    <text>免费在线客服</text>
                </view>
                <view>
                    <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/icons/kefu.png" width="50" height="54"></u-image>
                </view>
            </view>
        </view>
        <view class="service">
            <view class="ser-title">
                <text class="cuIcon-titles text-red u-font-28"></text>
                <text class="u-font-28 red" style="font-weight: 1000">专享贴心服务</text>
            </view>
            <view class="ser-section">
                <view class="ser-item" @click="fuhua">
                    <u-image height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/fuhua.png" width="50"></u-image>
                    <text>孵化管家</text>
                </view>
                <view class="ser-item" @click="law">
                    <u-image height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/falv.png" width="50"></u-image>
                    <text>法律管家</text>
                </view>
                <view class="ser-item" @click="money">
                    <u-image height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/caishui.png" width="50"></u-image>
                    <text>财税管家</text>
                </view>
                <view class="ser-item">
                    <u-image height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/peixun.png" width="50"></u-image>
                    <text>培训管家</text>
                </view>
                <view class="ser-item">
                    <u-image height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/yingx.png" width="50"></u-image>
                    <text>营销管家</text>
                </view>
                <view class="ser-item">
                    <u-image height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/ruanj.png" width="50"></u-image>
                    <text>软件管家</text>
                </view>
                <view class="ser-item">
                    <u-image  mode="aspectFit" height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/jinr.png" width="50"></u-image>
                    <text>金融管家</text>
                </view>
                <view class="ser-item" @click="car">
                    <u-image mode="aspectFit" height="50" src="https://yiqiwang360.com/images/yiqiguanjia/icons/car.png" width="50"></u-image>
                    <text>挪车码</text>
                </view>
            </view>
        </view>
        <!--    <view v-for="(item,index) in shopList" :key="index">-->
        <!--      {{item.title}}-->
        <!--&lt;!&ndash;      <view v-for="(item1,index) in item.category" :key="index">{{item1.name}}</view>&ndash;&gt;-->
        <!--       </view>-->

        <view class="shop-status">
            <block>
                <view class="ser-title u-border-bottom">
                    <text class="cuIcon-titles text-red u-font-28"></text>
                    <text class="u-font-28 red" style="font-weight: 1000">企业动态</text>
                </view>
                <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/realshop.png" width="100%" height="300"></u-image>
                <view class="u-margin-top-20">
                    <view v-for="(item,index) in shopList" :key="index">{{item.body}}</view>
                    <view class="date text-gray u-border-bottom">人民日报 <text class="u-margin-left-10">2021-02-07</text></view>
                </view>
                <view class="u-padding-top-20 status-bo" @click="newdetail(item.id)" v-for="(item,index) in shopList" :key="index">
                    <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/realshop.png" width="200" height="139"></u-image>
                    <view class="u-margin-left-20">
                        <text class="u-line-2i">{{item.title}}</text>
                        <view class="date text-gray u-padding-top-20">{{item.category.name}} <text class="u-margin-left-10">{{item.created_at}}</text></view>
                    </view>
                </view>
                <!--      <view class="u-padding-top-20 status-bo">-->
                <!--        <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/realshop.png" width="200" height="139"></u-image>-->
                <!--        <view class="u-margin-left-20">-->
                <!--          <text class="u-line-2">企业动态企业动态企业动态企业动态</text>-->
                <!--          <view class="date text-gray u-padding-top-20">人民日报 <text class="u-margin-left-10">2021-02-07</text></view>-->
                <!--        </view>-->
                <!--      </view>-->
            </block>
        </view>
    </view>
</template>

<script>
    import uniNavBar from "@/static/components/uni-nav-bar/uni-nav-bar.vue"
    export default {
        components: {uniNavBar},
        data () {
            return {
                bg: {
                    // backgroundImage: "url(https://yiqiwang360.com/images/yiqiguanjia/redbg.png)",
                    backgroundRepeat: "no-repeat",
                    backgroundSize: "750rpx 300rpx",
                    margin:'0rpx auto',
                    borderRadius:"10rpx"
                },
                need: '工商注册',
                phone: '',
                customStyle: {
                    width: '80%',
                    top: '10rpx',
                    color: '#ffffff',
                    backgroundColor: '#FF2E0F',
                    marginBottom: '50rpx',
                    border: "none"
                },
                needInput: {},
                //位置
                district: '临沂市',
                //搜索
                keyword: '',
                search_btn: {

                },
                //轮播图
                swiper: [],
                // 导航列表
                navList: [],
                loadStatus: 'loadmore',
                //新闻
                orderList: [
                    '寒雨连江夜入吴',
                    '平明送客楚山孤',
                    '洛阳亲友如相问',
                    '一片冰心在玉壶'
                ],
                newsList: [],
                starFix: 5,
                //服务商数量
                merNum: 1000,
                //热门楼层
                classIfy: [],
                // 产品列表
                shopList: [],
                pageNum: 1,
                //返回顶部
                scrollTop: 0,
                scrollTopStyle: {
                    color: '#ffffff',
                },
                scrollTopBg: {
                    background: 'rgba(253, 81, 35, 0.2)',
                },
                menuNum: 3,
                shelf: {
                    weixin: true
                },
            }
        },
        onLoad () {
            this.getNavList()

            // this.shopList = shop
        },
        onShow () {
        },
        // 下拉刷新
        onPullDownRefresh () {
        },
        methods: {
            // 获取本地存储

            //企业动态详情
            newdetail(category_id){
                uni.navigateTo({
                    url:'/pages/shop/shopaction?category_id=' + category_id
                })
            },
            async getNavList () {
                await this.$request({
                    method: 'GET',
                    url: '/news?page=3',
                    data:{
                        user_id:1
                    }
                }).then(res=>{
                    console.log(res.data.data.news.data)
                    this.shopList = res.data.data.news.data
                })
                /*console.log(11)
                console.log(res)
                this.shopList = res*/
                // this.menuNum = 12 / res.data.length
            },

            //企业认证详情
            shop(){
                uni.navigateTo({
                    url:'/pages/confirm/shopconfirm'
                })
            },
            //孵化详情
            fuhua(){
                uni.navigateTo({
                    url:'/pages/shequ/shequ'
                })
            },
            //法律详情
            law(){
                uni.navigateTo({
                    url:'/pages/index/law'
                })
            },
            //财税管家详情
            money(){
                uni.navigateTo({
                    url:'/pages/index/money'
                })
            },
            //发票详情
            fapiao(){
                uni.navigateTo({
                    url:'/pages/shequ/fapiao'
                })
            },
            //挪车码详情
            car(){
                uni.navigateTo({
                    url:'/pages/index/ncar'
                })
            },

            // 菜单点击跳转
            goNav (id) {
                if (id === 22) {
                    //钱来旺
                    uni.navigateTo({
                        url: '/pages/index/qlw'
                    })
                } else if (id === 25) {
                    //快速服务
                    uni.switchTab({
                        url: '/pages/serve/serve'
                    });
                    // uni.navigateTo({
                    //   url: '/pages/serve/fast'
                    // })
                } else if (id === 27) {
                    //联系我们
                    uni.navigateTo({
                        url: '/pages/common/contact'
                    })
                } else if (id === 28) {
                    uni.navigateTo({
                        url: '/pages/index/chairman'
                    })
                } else if (id === 32) {
                    uni.navigateTo({
                        url: '/pages/index/culture'
                    })
                } else {
                    uni.navigateTo(
                        { url: '/pages/shops/goodsSecondList?id=' + id }
                    )
                }
            },
            // 搜索
            goSearch () {
                if (this.keyword === '') return uni.showToast({
                    title: '请输入关键词再搜索',
                    icon: 'none',
                    duration: 2000
                })
                uni.navigateTo({
                    url: '/pages/index/search?query=' + this.keyword
                })
                this.keyword = ''
            },

            // 点击跳转
            go (path) {
                let name = path
                let nameArr = name.split('=')
                if (nameArr[1]==='全部分类'){
                    uni.switchTab({
                        url: '/pages/serve/serve'
                    })
                    return false
                }
                uni.navigateTo(
                    { url: '/pages/' + path }
                )
            },
            goTab (path) {
                uni.switchTab(
                    { url: '/pages/' + path }
                )
            },
        },
        //返回顶部
        onPageScroll (e) {
            this.scrollTop = e.scrollTop;
        }
    }
</script>
<style lang="scss">
    page {
        background: #f8f8f8;
    }

</style>
<style lang="scss">
    .page {
        background: #f8f8f8;
    }
    .ser-title{
        font-size: 25rpx;
        line-height: 80rpx;
    }
    .red{
        color:#C91A1C;
    }
    /*.search-box {*/
    /*  width:200rpx;*/
    /*  background: #f8f8f8;*/
    /*  padding: 0 30rpx;*/
    /*  height: 40rpx;*/
    /*  line-height: 70rpx;*/
    /*  border-radius: 50rpx;*/
    /*  display: flex;*/
    /*  .inline-block{*/
    /*    align-self:center*/
    /*  }*/
    /*}*/
    .bgred{
        background-size: 750rpx 300rpx;
        background: url("https://yiqiwang360.com/images/yiqiguanjia/redbg.png") no-repeat;
        color:white;
        padding:30rpx 20rpx;
        height:450rpx;
        width:100%;
        .bg-top{
            line-height: 50rpx;
            align-items: center;
            display: flex;
            flex-direction: row;
        }
    }
    .page-section{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        padding:20rpx;
        background:#F8F9FB;
        border-radius: 8rpx;
        width:95%;
        height:300rpx;
        position: absolute;
        top:130rpx;
        left:10px;
        .section-item{
            padding:0 20rpx;
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            align-items: center;
            width:47%;
            border-radius: 5rpx;
            margin:0 10rpx 20rpx;
            height:130rpx;
            background: white;
            .title{
                font-size: 26rpx;
                font-weight: 520;
            }
            text{
                line-height: 50rpx;
                font-weight: normal;
                font-size: 20rpx;
                color:grey;
            }
        }
    }
    .service{
        border-radius: 5rpx;
        background: white;
        width:96%;
        margin:0 auto;

        .ser-section{
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: row;
            flex-wrap: wrap;
            .ser-item{
                padding:20rpx 0;
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
                width:25%;
                height:130rpx;
                font-size: 23rpx;
                text{
                    line-height: 50rpx;
                }
            }
        }

    }
    .shop-status{
        padding:20rpx;
        border-radius: 5rpx;
        background: white;
        width:96%;
        margin:20rpx auto;
        .date{
            font-size: 22rpx;
            line-height: 60rpx;
        }
        .status-bo{
            line-height: 80rpx;
            display: flex;
            flex-direction: row;
        }
    }
</style>
