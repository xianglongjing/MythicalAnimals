<template>
  <view class="page">
    <view class="back">
      <view class="yellow">
        <view class="title">一企查VIP会员</view>
        <view>开通VIP会员，享众多超值权益</view>
      </view>
    </view>
    <view class="vip">
      <u-tabs :list="list" font-size="32" active-color="#fd5123" :is-scroll="false" :current="current" @change="change"></u-tabs>
      <view v-if="current==0">
        <view class="flex">
          <a class="product" v-for="item in con" :key="item.id" @click="choseprofrom(item.id)"
             :class="{'selected':flag==item.id}">
            <view class="name">{{item.name}}</view>
            <view class="price">￥{{item.price}}/年</view>
          </a>
        </view>
        <view class="tips">
          <view>活动说明:</view>
          <view>
            1.活动期间，购买3年一企查VIP套餐随机加送10-15个月一企查VIP，具体加送时长以页面显示为准。
          </view>
          <view>
            2.购买成功后赠送的一企查VIP将会自动充值到购买账户中。
          </view>
        </view>
        <view class="wx u-border-bottom">
          <view class="flex">
            <u-image width="50" height="50" src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan9.png"></u-image>
            <text class="u-margin-left-20">微信支付</text>
          </view>
          <label class="radio">
            <radio value="1" :checked="xuanzhong==='1'" @click="radio('1')"/>
          </label>
        </view>
        <view class="wx">
          <view class="flex">
            <u-image width="50" height="50" src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan10.png"></u-image>
            <text class="u-margin-left-20">支付宝支付</text>
          </view>
          <label class="radio">
            <radio value="2" :checked="xuanzhong==='2'" @click="radio('2')"/>
          </label>
        </view>
        <view class="special u-margin-top-30">
          <view class="weight">VIP特权</view>
          <view class="icons">
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan3.png"></u-image>
              <text>股东高管</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan4.png"></u-image>
              <text>股权结构</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan8.png"></u-image>
              <text>数据导出</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan2.png"></u-image>
              <text>一企查风险</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan1.png"></u-image>
              <text>企业动态</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan7.png"></u-image>
              <text>受益所有人</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan6.png"></u-image>
              <text>精准筛选</text>
            </view>
            <view class="items">
              <u-image mode="aspectFit" width="70" height="70"
                       src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan5.png"></u-image>
              <text>疑似关系</text>
            </view>
          </view>
        </view>
        <view class="dian">
          <ul>
            <li>完成支付后可在已完成订单中申请开票</li>
            <li>VIP会员自支付完成之时起5分钟内生效</li>
            <li>收款方为临沂市铭远企业管理服务有限公司</li>
          </ul>
        </view>
        <u-button :hair-line="false" :customStyle="kai" @click="pay">
          <view class="total">支付{{tprice}}开通VIP</view>
          <view class="day">活动倒计时：22天</view>
        </u-button>
        <view>
        </view>
      </view>
      <view v-if="current==1">
        <view class="flex">
          <a class="product" v-for="item in con" :key="item.id" @click="choseprofrom(item.id)"
             :class="{'selected':flag==item.id}">
            <view class="name">{{item.name}}</view>
            <view class="price">￥{{item.price}}/年</view>
          </a>
        </view>
        <view class="person u-border-bottom">
          <text>套餐人数</text>
          <view>
            <u-number-box :min="10" :step="10" v-model="num" @change="valChange"></u-number-box>
          </view>
        </view>
        <view class="person u-border-bottom">
          <text>实付金额</text>
          <view>
            {{nprice}}*{{num}}= <text style="font-weight: 600;font-size: 32rpx">100</text>元
          </view>
        </view>
        <view class="wx u-border-bottom">
          <view class="flex">
            <u-image width="50" height="50" src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan9.png"></u-image>
            <text class="u-margin-left-20">微信支付</text>
          </view>
          <label class="radio">
            <radio value="1" :checked="xuanzhong==='1'" @click="radio('1')"/>
          </label>
        </view>
        <view class="wx">
          <view class="flex">
            <u-image width="50" height="50" src="http://images.yiqiwang360.com/yiqicha/huiyuan/huiyuan10.png"></u-image>
            <text class="u-margin-left-20">支付宝支付</text>
          </view>
          <label class="radio">
            <radio value="2" :checked="xuanzhong==='2'" @click="radio('2')"/>
          </label>
        </view>
        <u-button :hair-line="false" :customStyle="kai" @click="pay">
          <view class="total">支付{{tprice}}开通VIP</view>
          <view class="day">活动倒计时：22天</view>
        </u-button>
      </view>
    </view>
  </view>
</template>
<script>
  export default {
    data(){
      return {
        flag:-1,
        nprice:1,
        tprice:0.02,
        xuanzhong:'1',
        num:10,
        list: [{
          name: 'VIP会员'
        }, {
          name: '企业套餐'
        }],
        kai:{
          display:'flex',
          flexDirection:'column',
          background:'#F8DBAF',
          lineHeight:'35rpx',
          height:'100rpx',
          width:'95%'
        },
        con:{},
        current: 1,
        value:1,
        isSelect:false
      }
    },
    onLoad(){
      this.vip()
    },
    methods: {
      radio(e){
        //console.log(e,'---')
        this.xuanzhong=e  //把传过来的值赋给点击的按钮
        console.log(this.xuanzhong)
      },
      //套餐
      choseprofrom:function (id) {
        this.vip(id)
        this.flag = id;
        console.log(this.flag)
      },
      async vip () {
        const { data: res } = await this.$request({
          method: 'POST',
          data:{
            type:1
          },
          url: 'applets/produce',
        })
        // console.log(res)
        this.con=res
      },
      async pay () {
        const token=uni.getStorageSync('token')
        const { data: res } = await this.$request({
          method: 'POST',
          data:{
            token:token,
            pay_type:'wx',
            product_name:this.flag,
            recipient:1,
            trade_type:'APP',
            notify_url:'http://pay.yiqiwang360.com/api/pay/wxNotify',
            buyer_id:'oRvQ859xuQo-VXB9fcR_hfyoPgd8'
          },
          url: 'applets/pay',
        })
        console.log(res)

          // const data = res;
          let map= {
            "appid":res.appid,
            "appId":res.appid,
            "noncestr":res.noncestr,
            "nonceStr":res.noncestr,
            "package":res.package,
            "prepayid":res.prepayid,
            "prepayId":res.prepayid,
            "partnerid":res.partnerid,
            "timestamp":res.timestamp,
            "sign":res.sign,
            // notify_url:'http://pay.yiqiwang360.com/api/pay/wxNotify'
          }
        // let orderInfo = JSON.stringify(map)
        // console.log(map)
        uni.requestPayment({
            provider: "wxpay",
            orderInfo: map,
            success: function(res) {
              uni.showToast({
                title: '支付成功',
                icon: 'none'
              })

            },
            fail: function(err) {
              console.log('fail:' + JSON.stringify(err));
              this.flag_submit=true
              uni.showToast({
                title: '支付失败',
                icon: 'none'
              })
            }
          });
        // uni.getProvider({ //获取支付类型
        //   service: 'payment',
        //   success(reson) {
        //     payment(data).then(res => { //接口请求
        //       let result = res //接口返回数据
        //       uni.showLoading({}) //拉起支付加载提示
        //       if (res.statusCode == 200) {
        //         uni.hideLoading()
        //         uni.requestPayment({ //下面参数为必传
        //           "appid": result.appid,  // 微信开放平台 - 应用 - AppId，注意和微信小程序、公众号 AppId 可能不一致
        //           "noncestr": result.noncestr, // 随机字符串
        //           "package": 'result.package',       // 固定值
        //           "partnerid": result.partnerid,      // 微信支付商户号
        //           "prepayid": result.prepayid, // 统一下单订单号
        //           "timestamp": result.timestamp,        // 时间戳（单位：秒）
        //           "sign": result.sign, // 签名，这里用的 MD5 签名
        //           success(res) {
        //             showTips('支付成功')
        //             setTimeout(() => { //支付成功跳转
        //               callback()
        //             }, 1200)
        //           },
        //           fail(err) {
        //             showTips('支付失败')
        //             setTimeout(() => { //支付失败跳转
        //               callback()
        //             })
        //           }
        //         })
        //       }
        //     })
        //   }
        // })
      },
      change(index) {
        this.current = index;
      },
      valChange(e) {
        console.log('当前值为: ' + e.value)
      }
    }

  }
</script>
<style lang="scss" scoped>
  /deep/ uni-radio .uni-radio-input{
    width:40rpx;
    height:40rpx;
  }
  /deep/.u-primary-hover {
    background-color: #000000 !important;
  }

  /deep/.u-radio {
    display: flex;
    flex-direction: row-reverse;
    width:100%;
  }

  /deep/.u-radio-group {
    /*width: 100% !important;*/
  }

  /deep/.u-radio__label {
    width: 90%;
  }
  .selected {
    border:13rpx solid #A95633;
    background-color: #FFF0DD;
  }
.back{
  background: #000000;
  height:200rpx;
  .yellow{
    height:190rpx;
    width:70%;
    border-radius: 10rpx;
    margin:0 auto;
    text-align: center;
    line-height: 60rpx;
    background:#FDE9C7 ;
    .title{
      padding-top:30rpx;
      color:#46240D;
      font-weight: 600;
      font-size: 43rpx;
    }
  }
}
  .fu{
    position: relative;
  }
  .zi{
    position: absolute;
    top:300rpx;
    color:#000000;
  }
  .vip{
    margin-top:-30rpx;
    .flex{
      padding:30rpx 0;
      .product{
        flex-grow: 1;
        border-radius: 10rpx;
        margin:0 17rpx;
        padding:25rpx 30rpx;
        border:2rpx solid #DDDCD9;
        .name{
          font-weight: 600;
          font-size: 31rpx;
        }
        .price{
          color:#71241E;
          font-weight: 600;
        }
      }
    }
    .tips{
      width:95%;
      margin:30rpx auto;
      background: #FFF0DD;
      border-radius: 20rpx;
      padding:30rpx 24rpx;
      line-height: 50rpx;
    }
  }
  .wx{
    display: flex;
    padding:0 20rpx;
    align-items: center;
    justify-content: space-between;
    .flex{
      align-items: center;
    }
  }
  .special{
    padding:0 20rpx;
    .weight{
      font-weight: 600;
      font-size: 32rpx;
    }
    .icons{
      display: flex;
      margin:30rpx 0;
      align-items: center;
      text-align: center;
      justify-content: center;
      flex-wrap: wrap;
      .items{
        text-align: center;
        display: flex;
        width:25%;
        flex-wrap: wrap;
        flex-direction: column;
        align-items: center;
        margin:20rpx 0;
        text{
          margin-top:20rpx;
        }
      }
    }
  }
  .dian{
    background: #F2F2F2;
    line-height: 55rpx;
    color:#989898;
    padding:20rpx 0;
  }
  .total{
    color:#000000;
    font-weight: 600;
  }
  .day{
    color:#fd5123;
    margin-top: 10rpx;
  }
  .person{
    display: flex;
    justify-content: space-between;
    padding:20rpx 25rpx;
  }
</style>