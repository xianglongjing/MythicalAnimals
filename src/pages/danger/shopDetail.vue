<template>
    <view class="page u-border-top">
       <view class="white flex u-border-bottom">
           <view class="shop-img">
               <u-image mode="aspectFill" src="http://images.yiqiwang360.com/yiqicha/gongsiming.png" width="60" height="60"></u-image>
               <text class="name">{{company.cpyname}}</text>
           </view>
           <view class="jiankong">
               <u-image mode="aspectFit" src="http://images.yiqiwang360.com/yiqicha/jiankong.png" width="30" height="30"></u-image>
           <text>监控</text>
           </view>
       </view>
<!--        <view class="tips">-->
<!--            <view>风险等级</view>-->
<!--            <view>风险总量</view>-->
<!--            <view>是否失信</view>-->
<!--        </view>-->

        <view class="u-margin-top-20 u-border-bottom">
            <u-tabs :list="list" font-size="26"
                    :is-scroll="false" :current="current" bar-height="4" bar-width="50" :bold="false"
                    @change="change" active-color="#FF4E21" inactive-color="#474747"></u-tabs>
        </view>
        <view v-if="current==0">
            <!--        下拉-->
<!--            <view class="content">-->
<!--                <sl-filter :themeColor="themeColor" :menuList="menuList" @result="result"></sl-filter>-->
<!--            </view>-->
<!--            <u-empty text="暂无数据" mode="con" v-if="this.risk"></u-empty>-->
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in opencourt" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">开庭公告</text>
                    <text class="warn">警示信息信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="opencourtD(company.id,item.id)">
                    <text>该公司 <text class="red">{{item.status}}</text>的开庭公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in law" :key="'a-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">法律诉讼</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="lawD(company.id,item.id)">
                    <text>该公司曾因<text class="red">{{item.cause}}</text>而被起诉</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in court" :key="'b-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">法院公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="courtD(company.id,item.id)">
                    <text>该公司<text class="red">{{item.status}}</text>的法院公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in ruling" :key="'c-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">送达公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="rulingD(company.id,item.id)">
                    <text>该公司<text class="red">{{item.status}}</text>的送达公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in register" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">立案信息</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="registerD(company.id,item.id)">
                    <text>该公司<text class="red">{{item.status}}</text>的立案信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in penalties" :key="'info2-'+item.id">
                <view class="item u-border-bottom">
                    <text class="title">行政处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="penaltiesD(company.id,item.id)">
                    <text>该公司<text class="red">{{item.status}}</text>的行政处罚</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="bankruptcy">
                <view class="item u-border-bottom">
                    <text class="title">破产重整</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="bankD(company.id)">
                    <text>该公司<text class="red">有破产重整信息</text></text>
                    <text class="gray">共{{bankruptcy}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="Inquiry">
                <view class="item u-border-bottom">
                    <text class="title">询价评估</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="InquiryD(company.id)">
                    <text>该公司<text class="red">有询价评估信息</text></text>
                    <text class="gray">共{{Inquiry}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="business">
                <view class="item u-border-bottom">
                    <text class="title">经营异常</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="busD(company.id)">
                    <text>该公司<text class="red">有经营异常信息</text></text>
                    <text class="gray">共{{business}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.consumption">
                <view class="item u-border-bottom">
                    <text class="title">限制消费令</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="consumD(company.id)">
                    <text>该公司<text class="red">有限制消费令信息</text></text>
                    <text class="gray">共{{risk.consumption}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.cases">
                <view class="item u-border-bottom">
                    <text class="title">终本案件</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="casesD(company.id)">
                    <text>该公司<text class="red">有终本案件信息</text></text>
                    <text class="gray">共{{risk.cases}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.dishonest">
                <view class="item u-border-bottom">
                    <text class="title">失信被执行人</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="dishonestD(company.id)">
                    <text>该公司<text class="red">有失信被执行人信息</text></text>
                    <text class="gray">共{{risk.dishonest}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.debtor">
                <view class="item u-border-bottom">
                    <text class="title">被执行人</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="debtorD(company.id)">
                    <text>该公司<text class="red">有被执行人信息</text></text>
                    <text class="gray">共{{risk.debtor}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.auction">
                <view class="item u-border-bottom">
                    <text class="title">司法拍卖</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="auctionD(company.id)">
                    <text>该公司<text class="red">有司法拍卖信息</text></text>
                    <text class="gray">共{{risk.auction}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.seriouslyillegal">
                <view class="item u-border-bottom">
                    <text class="title">严重违法</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="seriousD(company.id)">
                    <text>该公司<text class="red">有严重违法信息</text></text>
                    <text class="gray">共{{risk.seriouslyillegal}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.pledge">
                <view class="item u-border-bottom">
                    <text class="title">股权出质</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="pledgeD(company.id)">
                    <text>该公司<text class="red">有股权出质信息</text></text>
                    <text class="gray">共{{risk.pledge}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.equity">
                <view class="item u-border-bottom">
                    <text class="title">股权质押</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="equityD(company.id)">
                    <text>该公司<text class="red">有股权质押信息</text></text>
                    <text class="gray">共{{risk.equity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.protection">
                <view class="item u-border-bottom">
                    <text class="title">环保处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/protect?id='+company.id)">
                    <text>该公司<text class="red">有环保处罚信息</text></text>
                    <text class="gray">共{{risk.protection}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.arrears">
                <view class="item u-border-bottom">
                    <text class="title">欠税公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/qianshuigonggao?id='+company.id)">
                    <text>该公司<text class="red">有欠税公告信息</text></text>
                    <text class="gray">共{{risk.arrears}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.mortgage">
                <view class="item u-border-bottom">
                    <text class="title">动产抵押</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/dongchandiya?id='+company.id)">
                    <text>该公司<text class="red">有动产抵押信息</text></text>
                    <text class="gray">共{{risk.mortgage}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="risk.notice">
                <view class="item u-border-bottom">
                    <text class="title">公示催告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/gongshicuigao?id='+company.id)">
                    <text>该公司<text class="red">有公示催告信息</text></text>
                    <text class="gray">共{{risk.notice}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
        </view>
        <view v-if="current==1">
            <!--        下拉-->
<!--            <view class="content">-->
<!--                <sl-filter :themeColor="themeColor" :menuList="menuList" @result="result"></sl-filter>-->
<!--            </view>-->
<!--            <u-empty text="暂无数据" mode="con" v-if="this.nearcon"></u-empty>-->
            <view class="con u-margin-top-30" v-if="nearcon.opencourt" v-for="item in nearcon.opencourt" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">开庭公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/kaiting?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+item.corporate.id)">{{item.corporate.cpyname}}</text>{{item.status}}的开庭公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="nearcon.proceedings" v-for="item in nearcon.proceedings" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">法律诉讼</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lawsus?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">

                                {{item.corporate.cpyname}}

                        </text>
                       <text class="blue">{{item.status}}</text> 的法律诉讼
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="nearcon.dishonest" v-for="item in nearcon.dishonest" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">失信被执行人</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom"  @click="go('company/shixinbeizhixingren?id='+item.id+'&cid=' + item.cid)">
                    <text style="flex:1">该公司投资的<text class="red" @click="go('index/chashop?id='+item.corporate.id)">{{item.corporate.cpyname}}</text>有失信被执行人信息</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="nearcon.court" v-for="item in nearcon.court" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">法院公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lawgongg?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+item.corporate.id)">{{item.corporate.cpyname}}</text>{{item.status}}的开庭公告</text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
<!--            <view class="con u-margin-top-30" v-if="nearcon.consumption">-->
<!--                <view class="item u-border-bottom">-->
<!--                    <text class="title">限制消费令</text>-->
<!--                    <text class="warn">警示信息</text>-->
<!--                </view>-->
<!--                <view class="item2 u-border-bottom" @click="go('company/xianzhixiaofeiling?id='+nearcon.consumption.id)">-->
<!--                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+nearcon.consumption.corporate.id)">{{item.corporate.cpyname}}</text>有限制消费令信息</text>-->
<!--                    <text class="gray">共{{nearcon.consumption}}条 <u-icon name="arrow-right" size="26"></u-icon></text>-->
<!--                </view>-->
<!--            </view>-->
<!--            <view class="con u-margin-top-30" v-if="nearcon.cases">-->
<!--                <view class="item u-border-bottom">-->
<!--                    <text class="title">终本案件</text>-->
<!--                    <text class="warn">警示信息</text>-->
<!--                </view>-->
<!--                <view class="item2 u-border-bottom" @click="go('company/zhongbenanjian?id='+nearcon.cases.id)">-->
<!--                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+nearcon.cases.corporate.id)">{{item.corporate.cpyname}}</text>有终本案件信息</text>-->
<!--                    <text class="gray">共{{nearcon.cases}}条 <u-icon name="arrow-right" size="26"></u-icon></text>-->
<!--                </view>-->
<!--            </view>-->
<!--            <view class="con u-margin-top-30" v-if="nearcon.debtor">-->
<!--                <view class="item u-border-bottom">-->
<!--                    <text class="title">被执行人</text>-->
<!--                    <text class="warn">警示信息</text>-->
<!--                </view>-->
<!--                <view class="item2 u-border-bottom" @click="go('company/beiman?id='+nearcon.debtor.id)">-->
<!--                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+nearcon.debtor.corporate.id)">{{item.corporate.cpyname}}</text>有被执行人信息</text>-->
<!--                    <text class="gray">共{{nearcon.debtor}}条 <u-icon name="arrow-right" size="26"></u-icon></text>-->
<!--                </view>-->
<!--            </view>-->
<!--            <view class="con u-margin-top-30" v-if="nearcon.auction">-->
<!--                <view class="item u-border-bottom">-->
<!--                    <text class="title">司法拍卖</text>-->
<!--                    <text class="warn">警示信息</text>-->
<!--                </view>-->
<!--                <view class="item2 u-border-bottom" @click="go('company/sifapaimai?id='+nearcon.auction.id)">-->
<!--                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+nearcon.auction.corporate.id)">{{item.corporate.cpyname}}</text>有司法拍卖信息</text>-->
<!--                    <text class="gray">共{{nearcon.auction}}条 <u-icon name="arrow-right" size="26"></u-icon></text>-->
<!--                </view>-->
<!--            </view>-->
            <view class="con u-margin-top-30" v-if="nearcon.ruling" v-for="item in nearcon.ruling" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">送达公告</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/songdagongg?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">
                            {{item.corporate.cpyname}}
                        </text>
                        <text class="blue">{{item.status}}</text> 的送达公告
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="nearcon.register" v-for="item in nearcon.register" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">立案信息</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/lianxinxi?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">
                            {{item.corporate.cpyname}}
                        </text>
                        <text class="blue">{{item.status}}</text> 的立案信息
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="nearcon.business" v-for="item in nearcon.business" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">经营异常</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/jingyingyichang?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">
                            {{item.corporate.cpyname}}
                        </text>
                        <text class="blue">{{item.status}}</text> 的经营异常
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
            <view class="con u-margin-top-30" v-if="nearcon.penalties" v-for="item in nearcon.business" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">行政处罚</text>
                    <text class="warn">警示信息</text>
                </view>
                <view class="item2 u-border-bottom" @click="go('company/xingzchufa?id='+item.id+'&cid=' + item.cid)">
                    <text>该公司投资的
                        <text class="red" @click="go('index/chashop?id='+item.corporate.id)">
                            {{item.corporate.cpyname}}
                        </text>
                        <text class="blue">{{item.status}}</text> 的行政处罚
                    </text>
                    <text class="gray">共{{item.quantity}}条 <u-icon name="arrow-right" size="26"></u-icon></text>
                </view>
            </view>
<!--            <view class="con u-margin-top-30" v-if="nearcon.bankruptcy">-->
<!--                <view class="item u-border-bottom">-->
<!--                    <text class="title">破产重整</text>-->
<!--                    <text class="warn">警示信息</text>-->
<!--                </view>-->
<!--                <view class="item2 u-border-bottom" @click="go('company/pochanchongzheng?id='+nearcon.bankruptcy.id)">-->
<!--                    <text>该公司投资的<text class="red" @click="go('index/chashop?id='+nearcon.bankruptcy.corporate.id)">{{item.corporate.cpyname}}</text>有司法拍卖信息</text>-->
<!--                    <text class="gray">共{{nearcon.bankruptcy}}条 <u-icon name="arrow-right" size="26"></u-icon></text>-->
<!--                </view>-->
<!--            </view>-->
        </view>
        <view v-if="current==2">
            <view class="con u-margin-top-30" v-if="item.quantity" v-for="item in ass.change" :key="item.id">
                <view class="item u-border-bottom">
                    <text class="title">自身变更</text>
                    <text class="warn">提示信息</text>
                </view>
                <view class="item2 u-border-bottom">
                    <text>该公司
                        <text class="red">{{item.type}}</text>
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
                        <text class="red">{{item.ildtr}}</text>
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
                risk:{},
                company:[],
                opencourt:{},
                law:{},
                court:{},
                ruling:{},
                bankruptcy:[],
                Inquiry:[],
                business:[],
                register:{},
                penalties:{},
                // 周边
                nearcon:{},
                // 预警
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
                emptyShow:false,
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
                    url: 'applets/riskdetails',
                    data: {
                        id:id
                    }
                })
                this.risk=res.risk
                this.company=res.company
                this.opencourt=res.risk.opencourt
                this.law=res.risk.proceedings
                this.court=res.risk.court
                this.ruling=res.risk.ruling
                this.bankruptcy=res.risk.bankruptcy
                this.Inquiry=res.risk.Inquiry
                this.business=res.risk.business
                this.register=res.risk.register
                this.penalties=res.risk.penalties
                // console.log(res.risk)
                // uni.navigateTo({
                //     url: '/pages/ll/searchDetail?keyword=' + this.keyword
                // })
            },
            async near (id) {
                // this.pageNum++
                const { data: res } = await this.$request({
                    method: 'GET',
                    url: 'applets/periphery',
                    data: {
                        id:id
                    }
                })
                this.nearcon=res
                // console.log(res)
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
            // 开庭公告
            opencourtD(id,type){
                console.log(id,type)
                uni.navigateTo({
                    url:'/pages/company/kaiting?id='+id+'&type=' + type,
                })
            },
            // 法律诉讼
            lawD(id,type){
                console.log(id,type)
                uni.navigateTo({
                    url:'/pages/company/lawsus?id='+id+'&type=' + type,
                })
            },
            // 法院公告
            courtD(id,type){
                console.log(id,type)
                uni.navigateTo({
                    url:'/pages/company/lawgongg?id='+id+'&type=' + type,
                })
            },
            // 送达公告
            rulingD(id,type){
                console.log(id,type)
                uni.navigateTo({
                    url:'/pages/company/songdagongg?id='+id+'&type=' + type,
                })
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
        color:#fd5123;
    }
    .blue{
        color:#1283E1;
    }
.white{
    background: white;
    padding:30rpx;
}
    .flex{
        width:100%;
        align-items: center;
        justify-content: space-between;
        .shop-img{
            display: flex;
        }
        .jiankong{
            border-radius: 10rpx;
            color:#E8544A;
            align-items: center;
            font-size: 21rpx;
            border:1rpx solid #E8544A;
            display: flex;
            padding:10rpx;
        }
        .name{
            font-weight: 600;
            margin-left:10rpx;
        }
    }
    .tips{
        background: white;
        padding:10rpx 30rpx;
        display: flex;
        view{
            flex-grow: 1;
        }
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
        }
    }
</style>