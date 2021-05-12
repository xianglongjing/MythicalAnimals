<template>
  <view class="page">
     <view class="bgred" :style="bg">
       <view class="set">
         <u-image mode="aspectFill" src="../../static/icons/mine/set.png" width="50" height="50"></u-image>
       </view>
     </view>
    <view class="content">
    <view class="con-top">
      <u-image src="../../static/icons/mine.png" width="100" height="100" style="border-radius: 50%"></u-image>
      <view>
        <view class="title">上午好，韩梅梅</view>
        <text class="shop">临沂市铭远企业管理服务有限公司</text>
      </view>
    </view>
      <view class="con-bo">
        <view class="bo-item u-border-right">
          <u-image mode="aspectFill" src="../../static/icons/mine/card.png" width="70" height="50"></u-image>
          <text>我的名片</text>
        </view>
        <view class="bo-item u-border-right">
          <u-image mode="aspectFill" src="../../static/icons/mine/my.png" width="50" height="50"></u-image>
          <text>我的关注</text>
        </view>
        <view class="bo-item">
          <u-image mode="aspectFill" src="../../static/icons/mine/city.png" width="50" height="50"></u-image>
          <text>我的认证</text>
        </view>
      </view>
    </view>
    <view class="shop">
      <view class="ser-title">
        <text class="cuIcon-titles text-red u-font-28"></text>
        <text class="u-font-28 red" style="font-weight: 1000">我的企业</text>
      </view>
      <view class="shop-con">
        <u-image mode="aspectFill" width="70" height="70" src="../../static/image/qiye.png"></u-image>
        <view class="con-r">
          <text class="name">临沂市铭远企业管理服务有限公司</text>
          <view class="u-margin-top-10 u-margin-bottom-10">
            <text class="red">在业</text>
            <text class="lv">商务服务业</text>
          </view>
          <text class="u-line-1 u-font-23" style="color:#B8B8B8;line-height: 40rpx">公司经营范围包括：商务信息咨询；财务信息咨询</text>
          <view class="shop-bo">
            <view class="bo-item u-border-right" style="margin-left:-40rpx">
              <text class="title">法人代表</text>
              <text>代表名称</text>
            </view>
            <view class="bo-item u-border-right">
              <text class="title">注册资金</text>
              <text>500万人民币</text>
            </view>
            <view class="bo-item">
              <text class="title u-margin-bottom-10">成立时间</text>
              <text>2019-05-09</text>
            </view>
          </view>
        </view>
      </view>
      <view class="shop-con">
        <u-image mode="aspectFill" width="70" height="70" src="../../static/image/qiye.png"></u-image>
        <view class="con-r">
          <text class="name">临沂市铭远企业管理服务有限公司</text>
          <view class="u-margin-top-10 u-margin-bottom-10">
            <text class="red">在业</text>
            <text class="lv">商务服务业</text>
          </view>
          <text class="u-line-1 u-font-23" style="color:#B8B8B8;line-height: 40rpx">公司经营范围包括：商务信息咨询；财务信息咨询</text>
          <view class="shop-bo">
            <view class="bo-item u-border-right" style="margin-left:-40rpx">
              <text class="title">法人代表</text>
              <text>代表名称</text>
            </view>
            <view class="bo-item u-border-right">
              <text class="title">注册资金</text>
              <text>500万人民币</text>
            </view>
            <view class="bo-item">
              <text class="title u-margin-bottom-10">成立时间</text>
              <text>2019-05-09</text>
            </view>
          </view>
        </view>
      </view>
    </view>
    <u-button :customStyle="add" shape="circle">添加我的企业信息</u-button>
  </view>
</template>

<script>
export default {
  data () {
    return {
      add:{
        width:'85%',
        marginTop:'50rpx',
        color:'white',
        fontSize:'34rpx',
        backgroundImage: "url(" + require("../../static/image/redbg.png") + ")",
        backgroundRepeat: "no-repeat",
        backgroundSize: "750rpx 300rpx",
      },
      bg: {
        backgroundImage: "url(" + require("../../static/image/redbg.png") + ")",
        backgroundRepeat: "no-repeat",
        backgroundSize: "750rpx 300rpx",
        margin:'0rpx auto',
        borderRadius:"10rpx"
      },
      storage: {
        token: '',
        uid: 0,
        info: {}
      },
      // // 修改昵称对话框隐藏或显示
      // editNickNameShow: false,
      // newNickName: '',
      logoutShow: false,
      // 待评价
      commentsNum: 0,
      // 商家待接单
      ordersNum: 0,
      // 商家待接需求
      demandsNum: 0
    }
  },
  onLoad () {
    this.getStorage()
  },
  onShow () {
    this.getStorage()
    this.getBasicInfo()
  },
  onPullDownRefresh () {
    this.getBasicInfo(() => { uni.stopPullDownRefresh() })
  },
  methods: {
    // 获取本地存储
    getStorage () {
      this.storage.token = uni.getStorageSync('token')
      this.storage.uid = uni.getStorageSync('uid')
      this.storage.info = uni.getStorageSync('info')
    },
    // 跳转登录
    goLogin () {
      uni.navigateTo(
        { url: '/pages/mine/login' }
      )
    },
    // 昵称
    // setNickName () {
    //   this.editNickNameShow = true
    // },
    // async submitNickName () {
    //   const { data: res } = await this.$request({
    //     method: 'POST',
    //     url: 'myhome/editnickname',
    //     data: {
    //       token: this.storage.token,
    //       uid: this.storage.uid,
    //       nackname: this.newNickName
    //     }
    //   })
    //   this.newNickName = ''
    //   this.getBasicInfo()
    // },
    // cancelNickName () {
    //   this.newNickName = ''
    // },
    // 获取基本信息
    async getBasicInfo (callBack) {
      if (this.storage.token === '') return
      const { data: res } = await this.$request({
        method: 'POST',
        url: 'myhome',
        data: {
          token: this.storage.token,
          uid: this.storage.uid
        }
      })
      uni.setStorageSync('info', res.infor)
      this.getStorage()
      this.commentsNum = res.infor.khEvaNum
      this.ordersNum = res.infor.spOrderNum
      this.demandsNum = res.infor.spNeedsNum
      callBack && callBack()
    },
    // 点击跳转
    go (path) {
      if (this.storage.token === '') {
        return uni.showToast({
          title: '未登录，请登录',
          icon: 'none',
          duration: 1500
        })
      }
      uni.navigateTo(
        { url: '/pages/' + path }
      )
    },
    goto (path) {
      uni.navigateTo(
        { url: '/pages/' + path }
      )
    },
    // 拨打客服电话
    callPhone () {
      uni.makePhoneCall({
        phoneNumber: '4000361717'
      })
    },
    // 退出登录
    logoutDialogShow () {
      if (this.storage.token === '') {
        return uni.showToast({
          title: '未登录，请登录',
          icon: 'none',
          duration: 1500
        })
      }
      this.logoutShow = true
    },
    logout () {
      const { data: res } = this.$request({
        url: 'login/deToken',
        data: {
          token: this.storage.token,
          uid: this.storage.uid
        }
      })
      uni.showToast({
        title: '退出成功',
        icon: 'none',
        duration: 1500
      })
      uni.clearStorageSync()
      uni.navigateTo(
        { url: '/pages/mine/login' }
      )
    },
    goMyOrders (val) {
      if (this.storage.token === '') {
        return uni.showToast({
          title: '未登录，请登录',
          icon: 'none',
          duration: 1500
        })
      }
      uni.navigateTo({
        url: '/pages/orders/myOrders?state=' + val
      })
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
  .red{
    color:#C91A1C;
  }
  .bgred{
    position: relative;
    color:white;
    padding:30rpx 20rpx;
    height:410rpx;
    width:100%;
    .set{
      position: absolute;
      right:20rpx;
    }
    .bg-top{
      line-height: 50rpx;
      align-items: center;
      display: flex;
      flex-direction: row;

    }
  }
  .content{
    padding:20rpx;
    width:95%;
    height:270rpx;
    background: white;
    border-radius: 20rpx;
    position: absolute;
    top:100rpx;
    left:20rpx;
    .con-top{
      align-items: center;
      display: flex;
      flex-direction: row;
      .title{
        font-size: 32rpx;
      }
      .shop{
        padding:0;
        line-height: 50rpx;
        font-size: 25rpx;
      }
    }
    .con-bo{
      margin-top:20rpx;
      text-align: center;
      padding:20rpx 0;
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      .bo-item{
        height:100rpx;
        font-size: 26rpx;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        line-height: 60rpx;
        width:33%;
      }
    }
  }
  .shop{
    padding:0 20rpx;
    .shop-con{
      margin:20rpx 0;
      border-radius: 10rpx;
      background: white;
      padding:30rpx;
      display: flex;
      flex-direction: row;
      .con-r{
        margin-left:40rpx;
        .red{
          border-radius: 5rpx;
          background: #FAE9E7;
          padding:5rpx;
          font-size: 20rpx;
        }
        .lv{
          border-radius: 5rpx;
          margin-left:10rpx;
          color:#23AB7B;
          background: #DFF8F2;
          padding:5rpx;
          font-size: 20rpx;
        }
        .name{
          font-weight: 1000;
        }
      }
      .shop-bo{
        margin-top:20rpx;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap;
        .title{
          height:50rpx;
          color:#B8B8B8;
        }
        .bo-item{
          font-size: 25rpx;
          flex:1;
          display: flex;
          align-items: center;
          justify-content: center;
          flex-direction: column;
          text-align: center;
        }
      }
    }

  }
</style>
