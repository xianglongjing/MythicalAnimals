<template>
  <view class="home-page">
<!--    <view class="search-box">-->
<!--      <view class="inline-block" style="padding-top: 6rpx">-->
<!--        <u-icon name="scan" color="#fd5123" size="38"></u-icon>-->
<!--      </view>-->
<!--      <view class="inline-block" style="width: 260rpx">-->
<!--        <u-search-->
<!--                :action-style="search_btn"-->
<!--                :animation="true"-->
<!--                @custom="goSearch"-->
<!--                @search="goSearch"-->
<!--                bg-color="#f8f8f8"-->
<!--                input-align="left"-->
<!--                placeholder="搜索"-->
<!--                v-model="keyword"-->
<!--        ></u-search>-->
<!--      </view>-->
<!--    </view>-->
    <view class="sp-header">
      <view class="header-main">
        <view class="sp-icon">
          <image :src="shopDetail.img" mode="aspectFill" />
        </view>
        <view class="sp-info">
          <view class="sp-name u-line-1">
            {{shopDetail.corporateName}}
            <text class="tags">{{shopDetail.typeName}}</text>
          </view>
          <view>
            <view class="sp-num">临沂</view>
            <view class="sp-num">|</view>
            <view class="sp-num">粉丝数<text class="u-margin-left-10">{{shopDetail.followNum}}</text></view>
          </view>
          <view class="u-margin-top-8"><text class="bao">保</text><text class="qiye">企业</text></view>
        </view>
        <view class="sp-btn">
<!--          <u-button-->
<!--            shape="circle"-->
<!--            size="mini"-->
<!--            :custom-style="customStyle"-->
<!--            @click="followHandle(shopDetail.id)"-->
<!--          >{{shopDetail.follow === 1 ? '已关注' : '+ 关注'}}</u-button>-->
        </view>
      </view>
      <view class="header-other">
      </view>
      <view class="shop-detail">
        <view class="shop-detail-items">
          <text class="detail-num">111.00万</text>
          <text class="detail-desc">成交额</text>
        </view>
        <view class="text-gray"></view>
        <view class="shop-detail-items">
          <text>4.98</text>
          <text class="detail-desc">综合评分</text>
        </view>
        <view class="text-gray"></view>
        <view class="shop-detail-items">
          <text><text class="detail-num">100%</text></text>
          <text class="detail-desc">项目完成率 </text>
        </view>
        <view class="text-gray"></view>
        <view class="shop-detail-items">
          <text><text class="detail-num">778</text></text>
          <text class="detail-desc">服务雇主数</text>
        </view>
      </view>
      <view class="sp-guide">
        <u-read-more
          :toggle="true"
          show-height="120"
          ref="uReadMore"
          :shadow-style="shadowStyle"
          color="#ffffff"
          close-text="查看全部"
        >
          <rich-text :nodes="shopDetail.c_profile" style="color: #ffffff;font-size: 24rpx"></rich-text>
        </u-read-more>
      </view>
    </view>
    <u-tabs
      active-color="#FD5123"
      :list="tabs"
      :is-scroll="false"
      :current="current"
      @change="tabChange"
    ></u-tabs>
    <view v-if="current === 0">
      <view class="sp-goods">
        <view
          class="sp-goods-item"
          v-for="item1 in goodsList"
          :key="item1.id"
          @click="goGoodDetail(item1.id)"
        >
          <view class="goods-warter">
            <view class="goods-img-wrap">
              <image class="goods-image" :src="item1.headimg" mode="aspectFill" />
            </view>
            <view class="goods-title u-line-2">{{item1.name}}</view>
<!--            <view class="goods-shop u-line-1">{{shopDetail.corporateName}}</view>-->
            <view class="goods-shop u-line-1">
              <text class="text-bold text-red">￥1200</text>
              <text>销520</text>
            </view>
          </view>
        </view>
      </view>
      <u-loadmore
        color="#999999"
        font-size="24"
        margin-bottom="50"
        margin-top="50"
        bg-color="#f8f8f8"
        :status="loadStatus"
        v-if="goodsList.length !== 0"
      ></u-loadmore>
<!--      <view class="bg">-->
<!--        <image src="/static/image/shophome-bg.png"></image>-->
<!--      </view>-->
<!--      <view class="note" :style ="note"></view>-->
      <view class="need-zong" :style ="note">
      <view class="need-form">
        <view class="need-form-input">
          <u-field
                  :border-bottom="false" label="我需要"
                  v-model="need" :field-style="needInput"
          >
          </u-field>
        </view>
        <view class="need-form-input">
          <u-field type="number"
                  label="手机号"
                  placeholder="请输入手机号便于服务商联系您"
                  v-model="phone" :border-bottom="false" placeholder-style="font-size:24rpx"
          ></u-field>
        </view>
      </view>
        <u-button shape="square" size="default" :ripple="true" :custom-style="customStyle" ripple-bg-color="#f54c33"
                       @click="login">马上找TA获取方案和报价</u-button>
      </view>

    </view>
    <view v-if="current === 1">
      <view class="need-hot">
        <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
          <view id="demo1" class="scroll-view-item_H">全部</view>
          <view id="demo2" class="scroll-view-item_H">电商定制设计</view>
          <view id="demo3" class="scroll-view-item_H">包装设计</view>
          <view id="demo1" class="scroll-view-item_H">包月</view>
          <view id="demo2" class="scroll-view-item_H">VI设计</view>
          <view id="demo3" class="scroll-view-item_H">抖音视频</view>
        </scroll-view>
      </view>
<!--      <u-empty text="暂无动态" mode="list" :show="emptyShow"></u-empty>-->
      <view class="service">
        <image mode="aspectFill" src="https://yiqiwang360.com/images/app/logo.png"></image>
        <view class="ser-con">
          <text>品牌文案设计品牌文案设计品牌文案设计品牌文案设计</text>
          <view class="ser-bot">
            <text class="ser-price">￥1200/起/项</text>
            <text class="ser-r"> <text class="u-border-right u-line">成交1</text>评分5.00 </text>
          </view>
        </view>
      </view>
      <view class="service">
        <image mode="aspectFill" src="https://yiqiwang360.com/images/app/logo.png"></image>
        <view class="ser-con">
          <text>品牌文案设计品牌文案设计品牌文案设计品牌文案设计</text>
          <view class="ser-bot">
            <text class="ser-price">￥1200/起/项</text>
            <text class="ser-r"> <text class="u-border-right u-line">成交1</text>评分5.00 </text>
          </view>
        </view>
      </view>

    </view>
    <view v-if="current === 2">
      <view class="need-hot">
        <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
          <view id="demo1" class="scroll-view-item_H">全部</view>
          <view id="demo2" class="scroll-view-item_H">电商定制设计</view>
          <view id="demo3" class="scroll-view-item_H">包装设计</view>
          <view id="demo1" class="scroll-view-item_H">包月</view>
          <view id="demo2" class="scroll-view-item_H">VI设计</view>
          <view id="demo3" class="scroll-view-item_H">抖音视频</view>
        </scroll-view>
      </view>
      <view class="sp-goods">
        <view
                class="sp-goods-item"
                v-for="item1 in goodsList"
                :key="item1.id"
                @click="goGoodDetail(item1.id)"
        >
          <view class="goods-warter">
            <view class="goods-img-wrap">
              <image class="goods-image" :src="item1.headimg" mode="aspectFill"/>
            </view>
            <view class="goods-title u-line-2">{{item1.name}}</view>
            <view class="case-btn">
              <text>原创LOGO</text>
              <text>品牌LOGO</text>
            </view>
            <!--            <view class="goods-shop u-line-1">{{shopDetail.corporateName}}</view>-->
            <view class="case u-line-1">
              <text class="u-margin-right-30">
                <text class="cuIcon-attention"></text>
                144
              </text>
              <text>
                <text class="cuIcon-appreciate"></text>
                1
              </text>
            </view>
          </view>
        </view>
      </view>
      <u-loadmore
              color="#999999"
              font-size="24"
              margin-bottom="50"
              margin-top="50"
              bg-color="#f8f8f8"
              :status="loadStatus"
              v-if="goodsList.length !== 0"
      ></u-loadmore>
    </view>
<!--    动态-->
    <view v-if="current === 3">
      <view class="moving">
       <image mode="aspectFill" src="https://api.yiqiwang360.com/images/app/banner/img_banner.png"></image>
        <view>
          商家发布动态商家发布动态商家发布动态商家发布动态商家发布动态商家发布动态
        </view>
        <view class="mov-date">
          <view>
          <text>2021-01-23</text>
          <text class="u-margin-left-10">17:36:31</text>
          </view>
          <text>阅读： 566</text>
        </view>
      </view>
      <view class="moving">
        <image mode="aspectFill" src="https://api.yiqiwang360.com/images/app/banner/img_banner.png"></image>
        <view>
          商家发布动态商家发布动态商家发布动态商家发布动态商家发布动态商家发布动态
        </view>
        <view class="mov-date">
          <text>2021-01-23</text>
          <text class="u-margin-left-10">17:36:31</text>
        </view>
      </view>
    </view>
    <view v-if="current === 4" class="page">
      <view class="ass-top">
        <view class="u-margin-left-10"> 综合评分 <text class="score">4.97分</text></view>
        <view class="ass-type">
          <view class="type-item">
            <u-circle-progress :percent="100" active-color="#E81C14" width="130" border-width="6">
              <view class="u-progress-content">
                <view class="u-progress-dot ass-star">5.00</view>
                <text class='u-progress-info text-xs'>完成质量</text>
              </view>
            </u-circle-progress>
            <text class="text-xs">与同行相比</text>
            <text class="text-xs">-持平-</text>
          </view>
          <view class="type-item">
            <u-circle-progress :percent="100" active-color="#E81C14" width="130" border-width="6">
              <view class="u-progress-content">
                <view class="u-progress-dot ass-star">5.00</view>
                <text class='u-progress-info text-xs'>工作态度</text>
              </view>
            </u-circle-progress>
            <text class="text-xs">与同行相比</text>
            <text class="text-xs">-持平-</text>
          </view>
          <view class="type-item">
            <u-circle-progress :percent="100" active-color="#E81C14" width="130" border-width="6">
              <view class="u-progress-content">
                <view class="u-progress-dot ass-star">5.00</view>
                <text class='u-progress-info text-xs'>服务态度</text>
              </view>
            </u-circle-progress>
            <text class="text-xs">与同行相比</text>
            <text class="text-xs">-持平-</text>
          </view>
        </view>
      </view>
      <view class="ass-cus">
        <text>客户评价 <text class="text-gray">(105)</text></text>
        <view class="cus-con">

            <text>好评率100%</text>
            <text>好评100%</text>
            <text>不错(214)</text>
            <text>专业水平高(89)</text>

          <text>沟通顺畅(70)</text>
          <text>严谨认真(58)</text>
          <text>有创意(40)</text>
        </view>
        <view class="down">
          <u-icon name="arrow-down"></u-icon>
        </view>
      </view>
      <view class="ass-body">
        <view class="tab-change u-border-bottom" >
          <u-tabs
                  :list="tabList"
                  :is-scroll="false"
                  :current="currents"
                  inactive-color="#666666"
                  active-color="#fd5123"
                  @change="tabChanges" style="width:60%"
          >
          </u-tabs>
        </view>
        <view class="ass-con" v-if="currents === 0">
          <view class="con-item u-border-bottom">
            <view class="item-top">
              <view class="person">
                <image src="http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg"
                       mode="aspectFill" class="header"></image>
                <text>昵称</text>
                <text class="text-gray text-xs u-margin-left-10">2020-12-22 17::57:10</text>
              </view>
            </view>
            <view class="ass-dec">
              专业，店铺运营的好，流量提升多，销量好。我也有很多利润。找到满意的运营团队真的很欣慰！

            </view>
          </view>
          <view class="con-item u-border-bottom">
            <view class="item-top">
              <view class="person">
                <image src="http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg"
                       mode="aspectFill" class="header"></image>
                <text>昵称</text>
                <text class="text-gray text-xs u-margin-left-10">2020-12-22 17::57:10</text>
              </view>
            </view>
            <view class="ass-dec">
              专业，店铺运营的好，流量提升多，销量好。我也有很多利润。找到满意的运营团队真的很欣慰！
            </view>
          </view>
        </view>
      </view>

    </view>
    <view v-if="current === 5" class="means">
     <view class="means-top">
      <view class="yiqibaos">
        <view class="bao-items">
          <view class="item">
            <image mode="aspectFit" src="/static/image/g-bao.png"></image>
            <text>资金安全</text>
          </view>
          <view class="item">
            <image mode="aspectFit" src="/static/image/g-zheng.png"></image>
            <text>商家实名</text>
          </view>
          <view class="item">
            <image mode="aspectFit" src="/static/image/g-guan.png"></image>
            <text>全程监管</text>
          </view>
        </view>
      </view>
      <view class="u-line-1 text-xs">服务商已缴纳保证金￥10000，承诺交易出现问题先行赔付</view>
     </view>
      <view class="about">
        <view class="text-bold u-margin-bottom-30">
          关于我们
        </view>
        <view class="about-con">
          中国文化建站与艺术设计的领先者，中国高端文创品牌设计先锋品牌，以文化建站与艺术设计闻名全网，坚持高端个性设计，以卓越之美纵横市场，对粗制滥造不屑一顾。
        </view>
      </view>
      <view class="skilled">
        <view class="text-bold">
          擅长技能
        </view>
        <view class="ski-con">
          <text>品牌策划</text>
          <text>包装设计</text>
          <text>营销策划</text>
          <text>LOGO设计</text>
          <text>美工/文案外包</text>
          <text>VI设计</text>
          <text>活动策划</text>
        </view>
      </view>
      <view class="record">
          <view class="text-bold u-margin-bottom-15">经营数据</view>

       <view class="record-con">
          <view class="record-item">
            <text>122.19万</text>
            <text>成交额</text>
          </view>
         <view class="record-item">
           <text>221</text>
           <text>服务雇主数</text>
         </view>
         <view class="record-item">
           <text>2015-12-18</text>
           <text>开店时间</text>
         </view>
       </view>
        <view class="record-con">
         <view class="record-item">
           <text>100%</text>
           <text>项目完成率</text>
         </view>
         <view class="record-item">
           <text>221</text>
           <text>好评率</text>
         </view>
         <view class="record-item">
           <text>4.97</text>
           <text>综合评分</text>
         </view>
        </view>
      </view>
      <view class="manage">
        <view class="text-bold u-padding-bottom-30">经营资质</view>
        <image mode="aspectFill" src="/static/image/shangbiao.png"></image>
      </view>
    </view>
    <!-- 电话咨询列表 -->
    <u-action-sheet
      :list="phonesList"
      v-model="phonesShow"
      safe-area-inset-bottom
      :tips="tips"
      @click="callPhone"
    ></u-action-sheet>
    <!-- 地址列表 -->
    <u-action-sheet
      :list="addressList"
      v-model="addressShow"
      safe-area-inset-bottom
      @click="goAddress"
      :tips="addressTips"
    ></u-action-sheet>
    <!-- 删除确认框 -->
    <u-modal v-model="deleteShow" content="您确定删除吗？" show-cancel-button @confirm="deleteDynamic"></u-modal>
    <view class="cu-bar bg-white tabbar border shop goods-footer u-border-top">
      <view></view>
      <view class="action shop">
        <text class="cuIcon-favor"></text>关注
      </view>
      <view class="action shop" @click="showPhones">
        <view class="cuIcon-dianhua"></view>电话咨询
      </view>
      <view class="btn-group">
        <u-button shape="circle"
                  class="cu-btn shadow-blur line-con bg-gradual-orange"
                  style="color:#ffffff;"
        >
          <text class="u-padding-right-10">在线咨询</text>

        </u-button>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      storage: {
        token: '',
        uid: 0,
        info: {}
      },
      phone:'',
      need:'',
      needInput: {},
      checked:false,
      count:5,
      star:5,
      note: {
        backgroundImage: "url(" + require("../../static/image/shophome-bg.png") + ")",
        backgroundRepeat: "no-repeat",
        backgroundSize: "750rpx auto",
        margin:'0 20rpx',
        borderRadius:"10rpx"
      },
      customStyle: {
        width: '84%',
        color: '#ffffff',
        backgroundColor: '#FF2E0F',
        border: "none"
      },
      emptyShow: false,
      // customStyle: {
      //   color: '#ffffff',
      //   background: 'none'
      // },
      tabs: [{
        name: '首页'
      }, {
        name: '服务'
      },
        {
          name: '案例'
        },
        {
          name: '动态'
        },{
          name: '评价'
        },
        {
          name: '资料'
        }],
      tabList: [
        {
          name: '全部'
        }, {
          name: '雇主推荐'
        },],
      current: 0,
      currents: 0,
      shopDetail: {},
      goodsList: [],
      shopRate: '',
      shopId: 0,
      // 电话咨询
      phonesShow: false,
      phonesList: [],
      tips: {
        text: '点击号码直接拨打',
        color: '#909399',
        fontSize: 26
      },
      addressTips: {
        text: '点击地址查看地图',
        color: '#909399',
        fontSize: 26
      },
      // 地址
      addressList: [],
      addressShow: false,
      // 动态
      dynamicList: [],
      deleteShow: false,
      //more
      shadowStyle: {
        backgroundImage: "none",
        paddingTop: "0",
        marginTop: "20rpx",
        color: "#ffffff"
      },
      // 动态翻页
      pageNum: 1,
      loadStatus: 'nomore',
      dynamicId: 0,
      // 服务翻页
      goodsNum: 1,
      goodsLoadStatus: 'nomore'
    }
  },
  onLoad (options) {
    this.shopId = options.id
    this.getStorage()
    if (options.current) { this.current = 1 }
    this.getShopDetail(options.id)
    this.getGoodsList(options.id)
    this.getPhonesList()
    this.getAddressList()
  },
  // 到底部
  onReachBottom () {
    if (this.current === 1) {
      if (this.dynamicList.length < this.pageNum * 10) return this.loadStatus = 'nomore'
      this.pageNum++
      this.getDynamicList()
    } else if (this.current === 0) {
      if (this.goodsList.length < this.goodsNum * 10) return this.goodsLoadStatus = 'nomore'
      this.goodsNum++
      this.getGoodsList(this.shopId)
    }
  },
  watch: {
    current: function () {
      if (this.current === 1) {
        this.pageNum = 1
        this.dynamicList = []
        this.getDynamicList()
      }
    }
  },
  methods: {
    // 获取本地存储
    getStorage () {
      this.storage.token = uni.getStorageSync('token')
      this.storage.uid = uni.getStorageSync('uid')
      this.storage.info = uni.getStorageSync('info')
    },
    tabChange (index) {
      this.current = index;
    },
    tabChanges (index) {
      this.currents = index;
    },
    // 服务商详情
    async getShopDetail (id) {
      const { data: res } = await this.$request({
        url: 'merchant/merchantinfo',
        data: {
          uid: this.storage.uid,
          id: id
        }
      })
      this.shopDetail = res.list
      if (this.shopDetail.score.toString().length === 1) {
        this.shopRate = this.shopDetail.score + '.0'
      } else {
        this.shopRate = this.shopDetail.score
      }
      this.$nextTick(() => {
        this.$refs.uReadMore.init();
      })
    },
    // 服务商服务列表
    async getGoodsList (id) {
      const { data: res } = await this.$request({
        url: 'merchant/serviceProduct',
        data: {
          // 普通用户和服务商区分，uid需要为0
          uid: 0,
          id: id,
          pageNum: this.goodsNum
        }
      })
      this.goodsList = [...this.goodsList, ...res.data.data]
      if (this.goodsList.length < res.data.total) {
        this.goodsLoadStatus = 'loadmore'
      }
    },
    // 关注服务商操作
    async followHandle (spid) {
      if (this.storage.token === '') {
        uni.redirectTo({
          url: '/pages/mine/login'
        })
        return uni.showToast({
          title: '未登录，请先登录',
          icon: 'none',
          duration: 2000
        })
      }
      const { data: res } = await this.$request({
        url: 'myhome/addconcern',
        data: {
          token: this.storage.token,
          uid: this.storage.uid,
          spid: spid
        }
      })
      this.getShopDetail(spid)
    },
    // 跳转到服务详情
    goGoodDetail (id) {
      uni.navigateTo({
        url: '/pages/shops/goodDetail?id=' + id
      })
    },
    // 电话
    async getPhonesList () {
      const { data: res } = await this.$request({
        url: 'phoneslist',
        data: {
          token: this.storage.token,
          uid: this.shopId
        }
      })
      if (res.data.length !== 0) {
        this.phonesList = res.data.map((item) => { return Object.assign({}, item, { text: item.name + '：' + item.phone }) })
      } else {
        this.phonesList = [{ text: '暂无联系电话' }]
      }
    },
    showPhones () {
      if (this.storage.token === '') {
        uni.redirectTo({
          url: '/pages/mine/login'
        })
        return uni.showToast({
          title: '未登录，请登录',
          icon: 'none',
          duration: 2000
        })
      }
      this.phonesShow = true
    },
    // 拨打电话
    callPhone (index) {
      if (this.phonesList[0].text !== '暂无联系电话') {
        uni.makePhoneCall({
          phoneNumber: this.phonesList[index].phone
        })
      }
    },
    // 地址
    showAddress () {
      if (this.storage.token === '') {
        uni.redirectTo({
          url: '/pages/mine/login'
        })
        return uni.showToast({
          title: '未登录，请登录',
          icon: 'none',
          duration: 2000
        })
      }
      this.addressShow = true
    },
    async getAddressList () {
      const { data: res } = await this.$request({
        url: 'sitelist',
        data: {
          uid: this.shopId,
          token: this.storage.token
        }
      })
      if (res.data.length !== 0) {
        this.addressList = res.data.map((item) => { return Object.assign({}, item, { text: item.address }) })
      } else {
        this.addressList = [{ text: '暂无联系地址' }]
      }
    },
    goAddress (index) {
      if (this.addressList[0].text !== '暂无联系地址') {
        let latitude = this.addressList[index].latitude
        let longitude = this.addressList[index].longitude
        let address = this.addressList[index].address
        uni.navigateTo({
          url: '/pages/merchant/mAddressDetail?latitude=' + latitude + '&longitude=' + longitude + '&address=' + address
        })
      }
    },
    // 动态列表
    async getDynamicList () {
      const { data: res } = await this.$request({
        url: 'merchant/listDynamic',
        data: {
          spid: this.shopId,
          pageNum: this.pageNum
        }
      })
      if (res.data.length === 0) return this.emptyShow = true
      this.dynamicList = [...this.dynamicList, ...res.data.data]
      if (this.dynamicList.length < res.data.total) {
        this.loadStatus = 'loadmore'
      }
    },
    // 删除动态
    showDelete (id) {
      this.deleteShow = true
      this.dynamicId = id
    },
    async deleteDynamic () {
      const { data: res } = await this.$request({
        url: 'merchant/deDynamic',
        data: {
          id: this.dynamicId,
          uid: this.storage.uid,
          token: this.storage.token
        }
      })
      uni.showToast({
        title: '删除成功',
        icon: 'none'
      })
      this.pageNum = 1
      this.dynamicList = []
      this.getDynamicList()
    },
    showBig (index, index1) {
      uni.previewImage({
        current: index1,
        urls: this.dynamicList[index].img,
        indicator: 'default',
        loop: true
      })
    }
  }
}

</script>
<style lang="scss">
  page{
    padding-bottom: 100rpx;
    background: #f8f8f8;
  }
.u-action-sheet-item {
  padding: 30rpx !important;
}
</style>
<style lang="scss" scoped>
.custom-style {
  color: #606266;
  background: #4cd964;
}
.home-page {
  .sp-header {
    padding: 140rpx 20rpx 0;
    background: #231c45
      url("https://yiqiwang360.com/images/app/sjbj.png") no-repeat fixed
      0% 0%/100% auto;

    color: #ffffff;
    .header-main {
      display: flex;
      .sp-icon {
        background: white;
        border-radius: 10rpx;
        width: 110rpx;
        height: 110rpx;
        margin-bottom: 20rpx;
        margin-right: 20rpx;
        image {
          border-radius: 10rpx;
          width: 110rpx;
          height: 110rpx;
        }
      }
      .sp-info {
        flex: 1;
        .bao{
          padding:2rpx 8rpx;
          position: relative;
          margin:10rpx 15rpx 10rpx 0;
          font-size: 20rpx;
          border-radius: 5rpx;
          color:#fd5123;
          background: rgba(230, 18, 7, 0.2);
          &:after{
            content: ' ';
            position: absolute;
            left: 0;
            top: 0;
            pointer-events: none;
            box-sizing: border-box;
            -webkit-transform-origin: 0 0;
            transform-origin: 0 0;
            width: 199.8%;
            height: 199.7%;
            -webkit-transform: scale(0.5, 0.5);
            transform: scale(0.5, 0.5);
            border: 0 solid #E61207;
            z-index: 2;
            border-width: 2rpx;
            border-radius: 8rpx;
          }
        }
        .qiye{
          padding:2rpx 8rpx;
          position: relative;
          margin:10rpx 15rpx 10rpx 0;
          font-size: 20rpx;
          &:after{
            content: ' ';
            position: absolute;
            left: 0;
            top: 0;
            pointer-events: none;
            box-sizing: border-box;
            -webkit-transform-origin: 0 0;
            transform-origin: 0 0;
            width: 199.8%;
            height: 199.7%;
            -webkit-transform: scale(0.5, 0.5);
            transform: scale(0.5, 0.5);
            border: 0 solid #ffffff;
            z-index: 2;
            border-width: 2rpx;
            border-radius: 8rpx;
          }
        }
        .sp-name {
          font-size: 30rpx;
          line-height: 32rpx;
          vertical-align: top;
          .tags {
            height: 30rpx;
            vertical-align: top;
            display:inline-block;
            background-color: #E61207;
            font-size: 20rpx;
            line-height: 26rpx;
            margin-left: 10rpx;
            padding: 2rpx 10rpx;
            border-radius: 4rpx;
          }
        }
        .sp-num {
          color:#cccccc;
          display: inline-block;
          margin-right: 20rpx;
          font-size: 22rpx;
          padding-top: 8rpx;
          height: 36rpx;
          line-height: 34rpx;
        }
      }
      .sp-btn {
        width: 120rpx;
        padding-top: 14rpx;
      }
    }
  }
  .header-other {
    width:100%;
    display: flex;
    font-size: 24rpx;


    .sp-score {
      flex: 1;
      font-size: 40rpx;
      line-height: 64rpx;
      vertical-align: middle;
      .num {
        margin-right: 20rpx;
      }
    }
    .adds {
      width: 200rpx;
      text-align: center;
      .icon {
        text-align: center;
      }
    }
    .others {
      width: 140rpx;
      text-align: center;
    }
  }
  .sp-guide {
    margin-top: 30rpx;
    color: #ffffff;
    view {
      color: #ffffff;
    }
  }
}
.sp-goods {
  margin:0 10rpx;
  box-sizing: border-box;
  padding-bottom: 20rpx;
}
.sp-goods-item {
  width: 50%;
  display: inline-block;
  padding: 20rpx 10rpx 0;
  box-sizing: border-box;
}
.goods-warter {
  border-radius: 8px;
  background-color: #ffffff;
  padding: 0px;
  overflow: hidden;
  width: 100%;
}
.goods-image {
  width: 100%;
  height: 260rpx;
  border-radius: 4px;
}
.goods-title {
  font-size: 30rpx;
  line-height: 40rpx;
  height: 80rpx;
  margin: 5px 8px 5px 8px;
  color: $u-main-color;
}
.goods-shop {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  font-size: 22rpx;
  color: $u-tips-color;
  padding: 0 8px 8px 8px;
}

.dynamic {
  background: #ffffff;
  padding: 15rpx;
  margin-top: 20rpx;
  .floor {
    display: flex;
    justify-content: space-between;
    margin: 10rpx 0;
    .date-md {
      font-size: 40rpx;
      letter-spacing: 2rpx;
    }
  }
  .dynamic-images {
    padding-bottom: 20rpx;
    .image-box {
      display: inline-block;
      box-sizing: border-box;
      width: 33%;
      padding: 10rpx;
    }
  }

}
.shop-detail{
  margin-top:20rpx;
  display: flex;
  flex-direction: row;
  .shop-detail-items{
    color:white;
    display: flex;
    flex:1;
    text-align: center;
    justify-content: center;
    flex-direction: column;
    .detail-num{
      height: 30rpx;
      line-height: 30rpx;
      font-size: 30rpx;
      font-weight: 500;
    }
    .detail-desc{
      color:gray;
      font-size: 24rpx;
    }
  }
  .line-right{
    height:50rpx;
    margin:30rpx 10rpx;
    line-height: 40rpx;
  }
}
/*<!--.bg{-->*/
/*<!--  width:100%;-->*/
/*<!--  height:100%;-->*/
/*<!--  z-index:-1;-->*/
/*<!--  position: absolute;-->*/
/*<!--  image{-->*/
/*<!--    top:10rpx;-->*/
/*<!--    width:100%;-->*/
/*<!--    height:500rpx;-->*/
/*<!--  }-->*/
/*<!--}-->*/
.need-zong{
  text-align: center;
  margin-top:30rpx;
  padding:180rpx 30rpx;
}
.need-form{
  display: flex;
  flex-direction: column;
  align-items: center;
  padding:0 20rpx;
  margin:60rpx 0 0;
  .need-form-input{
    width:90%;
    border-radius: 8rpx;
    background: white;
    margin-bottom:14rpx;
    .u-field{
      padding: 14rpx 30rpx;
    }
  }
}
.need-hot{
  color:#E08956;
  margin:20rpx 30rpx;
  display: flex;
  overflow: hidden;
  text{
    font-style: oblique;
    padding-top: 6rpx;
    color: #fd5123;
  }
  button{
    color:#E08956;
    margin:0 10rpx;
  }
}
.scroll-view_H {
  flex: 1;
  white-space: nowrap;
}
.scroll-view-item {
  text-align: center;
  font-size: 36rpx;
}
.scroll-view-item_H {
  display: inline-block;
  line-height: 48rpx;
  height: 50rpx;
  background-color:white;
  border-radius: 10rpx;
  font-size: 24rpx;
  color: grey;
  text-align: center;
  margin-left: 14rpx;
  padding: 0 20rpx;
  vertical-align: middle;
}
.goods-footer {
  z-index:99;
  position: fixed;
  bottom: -8rpx;
  left: 0;
  right: 0;
}
//服务
  .service{
    margin:20rpx;
    display: flex;
    flex-direction: row;
    padding:20rpx;
    background: white;
    image{
      margin-right:10rpx;
      width:170rpx;
      height: 170rpx;
    }
    .ser-con{
      padding:10rpx;
      .ser-bot{
        line-height: 80rpx;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        .ser-price{
          color:#C91A1C;
        }
        .ser-r{
          padding:10rpx;
          color:darkgrey;
          text{
            padding:0 6rpx;
          }
        }
      }
    }
  }
  //案例
.case-btn {
  text {
    font-size:20rpx;
    color: #C91A1C;
    border-radius: 6rpx;
    margin: 0 10rpx;
    border: 1rpx solid #C91A1C;
  }

}
  .case{
    font-size: 25rpx;
    padding:10rpx;
  }
  //动态
  .moving{
    padding:20rpx;
    margin:20rpx auto;
    width:95%;
    background: white;
    image{
      margin-bottom: 20rpx;
      height:200rpx;
      width:100%;
    }
    .mov-date{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      line-height: 60rpx;
      color:darkgrey;
    }
  }
.ass-star{
  color:$main-color;
}
.ass-top{
  background: white;
  padding:20rpx;
  .score{
    color:#E50200;
    margin-left:10rpx;
  }
  .ass-number{
    color:$main-color;
  }
  .ass-grade{
    text-align: center;
    display: flex;
    line-height: 40rpx;
    flex-direction: column;
    width:30%;
    justify-content: center;

    .ass-star{
      color:$main-color;
    }
  }
  .ass-type{
    text-align: center;
    display: flex;
    margin: 30rpx;
    flex-direction: row;
    .type-item{
      color:grey;
      flex: 1;
      display: flex;
      flex-direction: column;
      margin:0 40rpx;
      .u-progress-content{
        flex:1;
      }
      .item-con{
        width:120rpx;
        height: 120rpx;
        border-radius: 50%;
        border: 4rpx solid #C06C2D;
        margin-bottom:20rpx;
        justify-content: center;
        align-items: center;
        display: flex;
        flex-direction: column;
      }
      .smtex{
        letter-spacing:3rpx;
        font-size: 18rpx;
      }
    }
  }
}

.ass-cus {
  padding:20rpx;
  margin: 20rpx 0;
  background: white;
  .down{
    color:darkgrey;
    text-align: center;
  }
  .cus-con{
    padding:20rpx 10rpx;
    font-size: 20rpx;
    line-height: 70rpx;
    text{
      display: inline-block;
      line-height: 34rpx;
      font-size:25rpx;
      padding:4rpx 15rpx;
      margin:6rpx 5rpx;
      border-radius: 20rpx;
      color:#E50200;
      background: #FAE8E8;
    }
  }
}
.ass-body{
  background: white;
  .tab-change{
    display: flex;
    flex-direction: row;
  }
  .ass-con{
    .con-item{
      padding:20rpx 0;
      .item-top{
        justify-content: space-between;
        align-items: center;
        display: flex;
        flex-direction: row;
        padding:30rpx 20rpx;
        .item-r{
          padding:0 10rpx;
          color:$main-color;
          display: flex;
          align-items: center;
          flex-direction: row;
          .ass-star{
            margin:0 10rpx;
          }
        }
        .person{
          padding:0 10rpx;
          display: flex;
          flex-direction: row;
          align-items: center;
          .header{
            width:60rpx;
            height: 60rpx;
            border-radius: 50%;
            margin-right:20rpx;
          }
        }
      }
      .item-bo{
        padding:10rpx 0;
        text{
          padding:0 10rpx;
        }
        .em-re{
          border-radius: 10rpx;
          padding:7rpx;
          font-size: 22rpx;
        }

      }
      .ass-dec{
        margin:0 auto;
        width:80%;
      }
    }
  }
}
  .means{
    margin:20rpx;
    .means-top{
      padding:20rpx;
      border:1rpx solid #60B16B;
      background: #EEFAF0;
      color:#60B16B;
      .yiqibaos{
        height: 50rpx;
        margin-bottom: 10rpx;
        border-bottom: 1rpx dashed #60B16B;
        .bao-items{
          display: flex;
          .title-icon{
            width: 140rpx;
            padding-left: 20rpx;
            image{
              vertical-align: text-top;
              height: 30rpx;
              width: 100rpx;
              margin-right: 20rpx;
            }
          }
          .cuIcon-right{
            width: 40rpx;
            color: #fd5123;
          }
          .item{
            flex: 1;
            display:inline-block;
            text{
              font-size: 24rpx;
              line-height: 30rpx;
            }
            image{
              margin-right: 2rpx;
              vertical-align: bottom;
              width:38rpx;
              height:30rpx;
            }
          }
        }
      }
    }
    .about{
      margin:20rpx 0;
      background: white;
      padding:20rpx;
      .about-con{
        font-size: 23rpx;
      }
    }
    .skilled{
      padding:20rpx;
      background: white;
      .ski-con{
        line-height: 60rpx;
        padding:20rpx 0;
        text{
          display: inline-block;
          margin:10rpx 5rpx;
          line-height: 34rpx;
          font-size: 23rpx;
          color:#E50200;
          padding:6rpx 20rpx;
          background: #FAE8E8;
          border-radius: 35rpx;
        }
      }
    }

    .record {
      margin: 20rpx 0;
      padding: 20rpx;
      background: white;
      .record-con {
        display: flex;
        flex-direction: row;
        .record-item {
          flex:1;
          margin:20rpx 0;
          /*margin:20rpx 50rpx;*/
          display: flex;
          flex-direction: column;
          text:first-child{
            font-size: 30rpx;
            font-weight: 1500;
            height:30rpx;
            line-height: 30rpx;
          }
          text:last-child{
            color:darkgray;
            font-size: 23rpx;
          }
        }
      }
    }
    .manage{
      padding:20rpx;
      height: 400rpx;
      background: white;
      margin:20rpx 0;
      image{
        width:200rpx;
        height: 150rpx;
      }
    }

  }
</style>
