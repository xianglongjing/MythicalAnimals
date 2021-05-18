<template>
    <view class="page">
        <view class="tou u-border-bottom">
            <u-image src="http://images.yiqiwang360.com/yiqicha/renwu.png" width="60" height="60"></u-image>
            <text class="u-margin-left-20">贾跃亭</text>
        </view>
        <view class="u-margin-top-20 u-border-bottom">
            <u-tabs :list="list" font-size="26"
                    :is-scroll="false" :current="current" bar-height="4" bar-width="50" :bold="false"
                    @change="change" active-color="#FF4E21" inactive-color="#474747"></u-tabs>
        </view>
        <view v-if="current==0">
            <!--        下拉-->
            <view class="content">
                <sl-filter :themeColor="themeColor" :menuList="menuList" @result="result"></sl-filter>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.opencourt" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">开庭公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/kaiting?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">{{item.corporate.cpyname}}</text>
                       <text class="blue">{{item.status}}</text>
                    的开庭公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.proceedings" :key="'a-'+item.cid">
                <view class="item u-border-bottom">
                    <text class="title">法律诉讼</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lawsus?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">

                            {{item.corporate.cpyname}}

                        </text>
                        <text class="blue">{{item.cause}}</text> 的法律诉讼
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.court" :key="'b-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">法院公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lawgongg?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text class="blue">{{item.status}}</text>的法院公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.consumption" :key="'c-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">限制消费令</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/xianzhixiaofeiling?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                     有限制消费令信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.cases" :key="'d-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">终本案件</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/zhongbenanjian?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有终本案件信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.dishonest" :key="'e-'+item.id">
                    <view class="item u-border-bottom">
                        <text class="title">失信被执行人</text>
                        <text class="warn">警示信息</text>
                    </view>
                    <view class="item2 u-border-bottom" @click="go('company/shixinbeizhixingren?id='+item.id+'&type=' + item.corporate.id)">
                        <text class="one">该老板在
                            <text class="red">{{item.corporate.cpyname}}</text>
                            有失信被执行人信息</text>
                        <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                    </view>
                </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.debtor" :key="'f-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">被执行人</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/beiman?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有被执行人信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.auction" :key="'g-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">司法拍卖</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/sifapaimai?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有司法拍卖信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.ruling" :key="'h-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">送达公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/songdagongg?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text class="blue">{{item.status}}</text>的送达公告
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.register" :key="'i-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">立案信息</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/lianxinxi?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text>{{item.status}}</text>的立案信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.bankruptcy" :key="'j-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">破产重整</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/pochanchongzheng?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有破产重整信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.Inquiry" :key="'k-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">询价评估</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/xunjiapinggu?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有询价评估信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.business" :key="'l-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">经营异常</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/jingyingyichang?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有经营异常信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.penalties" :key="'m-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">行政处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/xingzchufa?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text>{{item.status}}</text>的行政处罚
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.seriouslyillegal" :key="'e-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">严重违法</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/yanzhongweifa?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有严重违法信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.pledge" :key="'n-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">股权出质</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/guquanchuzhi?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有股权出质信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.equity" :key="'o-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">股权质押</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/guquanzhiya?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有股权质押信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.protection" :key="'p-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">环保处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/protect?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有环保处罚信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.arrears" :key="'q-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">欠税公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/qianshuigonggao?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有欠税公告信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.mortgage" :key="'r-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">动产抵押</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/dongchandiya?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有动产抵押信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in mycon.notice" :key="'s-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">公示催告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/gongshicuigao?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有公示催告信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
        </view>
        <view v-if="current==1">
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.opencourt" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">开庭公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/kaiting?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">{{item.corporate.cpyname}}</text>
                        <text class="blue">{{item.status}}</text>
                        的开庭公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.proceedings" :key="'a-'+item.cid">
                <view class="item u-border-bottom">
                    <text class="title">法律诉讼</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lawsus?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">

                            {{item.corporate.cpyname}}

                        </text>
                        <text class="blue">{{item.cause}}</text> 的法律诉讼
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.court" :key="'b-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">法院公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lawgongg?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text class="blue">{{item.status}}</text>的法院公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.consumption" :key="'c-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">限制消费令</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/xianzhixiaofeiling?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有限制消费令信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.cases" :key="'d-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">终本案件</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/zhongbenanjian?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有终本案件信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.dishonest" :key="'e-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">失信被执行人</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/shixinbeizhixingren?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有失信被执行人信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.debtor" :key="'f-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">被执行人</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/beiman?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有被执行人信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.auction" :key="'g-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">司法拍卖</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/sifapaimai?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有司法拍卖信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.ruling" :key="'h-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">送达公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/songdagongg?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text class="blue">{{item.status}}</text>的送达公告
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.register" :key="'i-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">立案信息</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/lianxinxi?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text>{{item.status}}</text>的立案信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.bankruptcy" :key="'j-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">破产重整</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/pochanchongzheng?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有破产重整信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.Inquiry" :key="'k-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">询价评估</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/xunjiapinggu?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有询价评估信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.business" :key="'l-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">经营异常</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/jingyingyichang?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有经营异常信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.penalties" :key="'m-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">行政处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/xingzchufa?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        <text>{{item.status}}</text>的行政处罚
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.seriouslyillegal" :key="'e-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">严重违法</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/yanzhongweifa?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有严重违法信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.pledge" :key="'n-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">股权出质</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/guquanchuzhi?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有股权出质信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.equity" :key="'o-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">股权质押</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/guquanzhiya?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有股权质押信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.protection" :key="'p-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">环保处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/protect?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有环保处罚信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.arrears" :key="'q-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">欠税公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/qianshuigonggao?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有欠税公告信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.mortgage" :key="'r-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">动产抵押</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/dongchandiya?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有动产抵押信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in nearcon.notice" :key="'s-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">公示催告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"
                      @click="go('company/gongshicuigao?id='+item.id+'&type=' + item.corporate.id)">
                    <text class="one">该老板在
                        <text class="red">{{item.corporate.cpyname}}</text>
                        有公示催告信息
                    </text>
                    <text class="gray">共{{item.quantity}}条
                        <u-icon name="arrow-right" size="26"></u-icon>
                    </text>
                </view>
            </view>
        </view>
        <view v-if="current==2">
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in ass.change" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">自身变更</text>
                    <text class="warn">提示信息</text>
                </view>
                <view class="item2 u-border-bottom">
                    <text>该公司
                        <text class="red">{{item.type ? item.type : '-'}}</text>
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in warncon.business" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">经营异常</text>
                    <text class="warn">提示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/jingyingyichang?id='+company.id)">
                    <text>该公司
                        <text class="red">{{item.ildtr ? item.ildtr : '-'}}</text>
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    import slFilter from '@/components/sl-filter/sl-filter.vue';
    export default {
        components: {
            slFilter
        },
        data(){
            return {
                mycon:{},
                nearcon:{},
                warncon:{},
                ass:{},
                list: [{
                    name: '自身风险'
                }, {
                    name: '周边风险'
                }, {
                    name: '预警提醒'
                }],
                current: 2,
                themeColor: '#E8544A',
                filterResult: '',
                menuList: [{
                    'title': '全部风险类型',
                    'detailTitle': '',
                    'isMutiple': true,
                    'key': 'jobType',
                    'detailList': [{
                        'title': '司法风险',
                        'value': ''
                    },
                        {
                            'title': '全部司法风险',
                            'value': 'uni-app'
                        },
                        {
                            'title': '强制清算',
                            'value': 'java'
                        },
                        {
                            'title': '涉金融黑黑名单',
                            'value': 'web'
                        },
                        {
                            'title': '失信被执行人',
                            'value': 'Android'
                        },
                        {
                            'title': '限制消费令',
                            'value': 'iOS'
                        }
                    ]
                },
                    {
                        'title': '全部风险级别',
                        'detailTitle': '',
                        'isMutiple': true,
                        'key': 'jobType',
                        'detailList': [{
                            'title': '',
                            'value': ''
                        },
                            {
                                'title': '全部风险级别',
                                'value': 'uni-app'
                            },
                            {
                                'title': '高风险',
                                'value': 'java'
                            },
                            {
                                'title': '警示',
                                'value': 'web'
                            }
                        ]
                    },
                ]
            }
        },
        onLoad(options){
            this.myself(options.id)
            this.near(options.id)
            this.warn(options.id)
        },
        methods:{
            async myself (id) {
                // this.pageNum++
                const { data: res } = await this.$request({
                    method: 'GET',
                    url: 'applets/grriskdetails',
                    data: {
                        id:id
                    }
                })
                // console.log(res)
                this.mycon=res
            },
            async near (id) {
                // this.pageNum++
                const { data: res } = await this.$request({
                    method: 'GET',
                    url: 'applets/surroundings',
                    data: {
                        id:id
                    }
                })
                // console.log(res)
                this.nearcon=res
            },
            async warn (id) {
                // this.pageNum++
                const { data: res } = await this.$request({
                    method: 'GET',
                    url: 'applets/reminder',
                    data: {
                        id:id
                    }
                })
                this.warncon=res
                this.ass=res.associate
                console.log(res)
            },
            //立案信息
            registerD(id,type){
                console.log(id,type)
                uni.navigateTo({
                    url:'/pages/company/lianxinxi?id='+id+'&type=' + type,
                })
            },
            // 询价评估
            InquiryD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/xunjiapinggu?id='+id,
                })
            },
            // 经营异常
            busD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/jingyingyichang?id='+id,
                })
            },
            // 破产重整
            bankD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/pochanchongzheng?id='+id,
                })
            },
            //行政处罚
            penaltiesD(id,type){
                console.log(id,type)
                uni.navigateTo({
                    url:'/pages/company/xingzchufa?id='+id+'&type=' + type,
                })
            },
            //限制消费令
            consumD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/xianzhixiaofeiling?id='+id,
                })
            },
            //终本案件
            casesD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/zhongbenanjian?id='+id,
                })
            },
            //失信被执行人
            dishonestD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/shixinbeizhixingren?id='+id,
                })
            },
            //被执行人
            debtorD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/beiman?id='+id,
                })
            },
            //司法拍卖
            auctionD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/sifapaimai?id='+id,
                })
            },
            //严重违法
            seriousD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/yanzhongweifa?id='+id,
                })
            },
            //股权出质
            pledgeD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/guquanchuzhi?id='+id,
                })
            },
            //股权质押
            equityD(id){
                console.log(id)
                uni.navigateTo({
                    url:'/pages/company/guquanzhiya?id='+id,
                })
            },
            go (path) {
                let name = path
                let nameArr = name.split('=')
                uni.navigateTo(
                    { url: '/pages/' + path }
                )
            },
            change(index) {
                this.current = index;
            },
            result(val) {
                console.log('filter_result:' + JSON.stringify(val));
                this.filterResult = JSON.stringify(val, null, 2)
            }
        }
    }
</script>
<style>
    page{
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    .gray{
        color:#A9A9A9;
    }
    .red{
        color:#E75D54;
    }
    .blue{
        color:#1283E1;
    }
.tou{
    display: flex;
    align-items: center;
    background: white;
    height:90rpx;
    padding:25rpx 25rpx 40rpx;
}
    .con{
        background: white;
        .item{
            padding:30rpx;
            .warn{
                background: #FDF5EE;
                /*border:1rpx solid #EFCF7E;*/
                color:#EFCF7E;
                padding:7rpx 12rpx;
                font-size: 24rpx;
                margin-left:10rpx;
                border-radius: 10rpx;
            }
        }
        .item2{
            padding:30rpx;
            display: flex;
            justify-content: space-between;
            .one{
                flex:1;
            }
        }
    }
</style>