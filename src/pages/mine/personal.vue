<template>
    <view class="page">
        <view class="person">
            <view class="p-l">
                <u-image src="http://images.yiqiwang360.com/yiqicha/tou.png" width="140" height="140"></u-image>
                <view class="camera">
                    <u-icon name="camera" color="#ffffff"></u-icon>
                </view>
            </view>
            <view class="p-r">
                <view class="top">
                    <text class="name">韩梅梅</text>
                    <u-icon name="edit-pen" size="35"></u-icon>
                </view>
                <view>账号：123456789</view>
                <view class="flex">
                    <text>资料完善度：</text>
                    <u-line-progress active-color="#E22619" :percent="20" style="width:250rpx" height="20"></u-line-progress>
                </view>
            </view>
        </view>
        <view class="form">
            <u-form :model="form" ref="uForm">
                <u-form-item label="毕业学校" label-width="200">
                <picker mode="multiSelector" :range="dateTimeArray"  v-model="dateTime" @change="change" @columnchange="columnchange">
                    <view>
<!--                        //disable = "true" 是禁用input 防止点击弹出键盘-->
                        <input type="text" disabled="true" v-model="upTower" placeholder="请选择生日" placeholder-class="inputPlace" />
                    </view>
                </picker>
                </u-form-item>
            </u-form>
            <u-form :model="form" ref="uForm">
                <u-form-item label="毕业学校" label-width="200"><u-input v-model="form.school" placeholder="请输入学校名称"/></u-form-item>
            </u-form>
            <view class="u-border-bottom" style="line-height:100rpx">
                <view class="flex">
                    <text class="u-font-31" style="width:200rpx">学历</text>
                    <u-input v-model="form.education" :type="types" @click="edu = true" placeholder="请选择所在行业"
                             placeholder-style="color:#C0C4CC"/>
                </view>
                <view class="flex">
                    <u-action-sheet :list="eduList" v-model="edu" @click="Edu"></u-action-sheet>
                </view>
            </view>
            <view class="u-border-bottom" style="line-height:100rpx">
                <view class="flex">
                    <text class="u-font-31" style="width:200rpx">毕业年份</text>
                    <u-input v-model="form.year" :type="types" @click="years = true" placeholder="请选择毕业年份"
                             placeholder-style="color:#C0C4CC;margin-top: 30rpx"/>
                </view>
                <view class="flex">
                    <u-action-sheet :list="yearList" v-model="years" @click="nian"></u-action-sheet>
                </view>
            </view>
        </view>
        <view class="form">
            <u-form :model="form" ref="uForm">
                <u-form :model="form.unit" ref="uForm">
                    <u-form-item label="公司/单位" label-width="200"><u-input v-model="form.unit" placeholder="请输入公司/单位名称"/></u-form-item>
                </u-form>
            </u-form>
            <view class="u-border-bottom" style="line-height:100rpx">
                <view class="flex">
                    <text class="u-font-31" style="width:200rpx">所在行业</text>
                    <u-input v-model="form.industry" :type="types" @click="shows = true" placeholder="请选择所在行业" placeholder-style="color:#C0C4CC;margin-top: 30rpx"/>
                </view>
                <view class="flex">
                    <u-action-sheet :list="actionSheetList" v-model="shows" @click="actionSheetCallback"></u-action-sheet>
                </view>
            </view>
            <view class="u-border-bottom" style="line-height:100rpx">
                <view class="flex">
                    <text class="u-font-31" style="width:200rpx">身份</text>
                    <u-input v-model="form.identity" :type="types" @click="shens = true" placeholder="请选择身份"
                             placeholder-style="color:#C0C4CC;margin-top: 30rpx"/>
                </view>
                <view class="flex">
                    <u-action-sheet :list="shenfenlist" v-model="shens" @click="shenfen"></u-action-sheet>
                </view>
            </view>
            <view class="u-border-bottom" style="line-height:100rpx">
                <view class="flex">
                    <text class="u-font-31" style="width:200rpx">工作年限</text>
                    <u-input v-model="form.working" :type="types" @click="job = true" placeholder="请选择所在行业"
                             placeholder-style="color:#C0C4CC;margin-top: 30rpx"/>
                </view>
                <view class="flex">
                    <u-action-sheet :list="jobList" v-model="job" @click="Job"></u-action-sheet>
                </view>
            </view>
        </view>
        <u-button :customStyle="bao" @click="submit">保存</u-button>
    </view>
</template>

<script>
    const dateTimePicker = require('@/util/dateTimePicker.js')
    export default {
        data(){
            return {
                dateTimeArray: null,
                dateTime: null,
                startYear: 2000,
                endYear: 2050,
                upTower:"",
                // birthday: currentDate,
                bao:{
                    background:'#F44514',
                    width:'550rpx',
                    margin:'0 auto',
                    height:'80rpx',
                    color:'white',
                    fontSize:'32rpx'
                },
                text:'',
                form: {
                    birthday:'2020-01-21',
                    school: '',
                    education: '',
                    unit: '',
                    year:'',
                    industry:'',
                    identity:'',
                    working:''
                },
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
                jobList: [
                    {
                        id: '1',
                        text: '1年'
                    },
                    {
                        id: '2',
                        text: '2年'
                    }
                ],
                eduList: [
                    {
                        id: '1',
                        text: '本科'
                    },
                    {
                        id: '2',
                        text: '大专'
                    }
                ],
                shenfenlist: [
                    {
                        id: '1',
                        text: '员工'
                    },
                    {
                        id: '2',
                        text: '法定代表人'
                    },
                    {
                        id: '3',
                        text: '股东'
                    },
                    {
                        id: '4',
                        text: '董监高'
                    },
                ],
                yearList: [
                    {
                        id: '1',
                        text: '应届毕业生'
                    },
                    {
                        id: '2',
                        text: '1年及一下'
                    },
                    {
                        id: '3',
                        text: '1-3年'
                    },
                    {
                        id: '4',
                        text: '3-5年'
                    },
                ],
                types: 'select',
                shows: false,
                show: false,
                edu: false,
                shens: false,
                job: false,
                years: false,
                date:false,
                params: {
                    year: true,
                    month: true,
                    day: true,
                    hour: false,
                    minute: false,
                    second: false
                },

                // mode: 'date'
            }
        },
        onLoad(){
            //传入开始展示年份startYear 结束展示年份endYear
            //自定义开始显示时间
            let arr = '2018/09/01 13:00'
            let obj = dateTimePicker.dateTimePicker(this.startYear, this.endYear,arr)
            this.dateTimeArray = obj.dateTimeArray
            this.dateTime = obj.dateTime
        },
        methods:{
            withData(param){
                return param < 10 ? '0' + param : '' + param;
            },
            change(e){
                let value = []
                e.detail.value.forEach((val,index) => {
                    value.push(this.withData(val))
                })
                let dateArray = "20" + value[0] + "-" + value[1] + "-" + value[2]
                this.upTower = dateArray
            },
            columnchange(e){
                let dateArr = this.dateTimeArray
                let arr = this.dateTime
                //滑动所在列的数据并对其值进行更新
                arr[e.detail.column] = e.detail.value
                //更新展示月份对应的天数（28 or 29 or 30 or 31）
                dateArr[2] = dateTimePicker.getMonthDay(dateArr[0][arr[0]], dateArr[1][arr[1]])
                //最后把最新的数值赋值到dateTimeArray
                this.dateTimeArray = dateArr
                this.dateTime = arr
            },
            async submit() {
                const token=uni.getStorageSync('token')
                const {data: res} = await this.$request({
                    method: 'POST',
                    url: 'applets/personal',
                    data: {
                        token: uni.getStorageSync('token'),
                        birthday:this.dateTime,
                        school:this.form.school,
                        education:this.form.education,
                        unit:this.form.unit,
                        industry:this.form.industry,
                        identity:this.form.identity,
                        working: this.form.working
                    }
                })
                this.form = res
                console.log(res)
                // if (!res.list) {
                //   this.followList = []
                //   return this.emptyShow = true
                // }
                // this.followList = res.list.map((item) => {
                //   return Object.assign({}, item, {show: false})
                // })
            },
            open() {
                this.show = true;
            },
            actionSheetCallback(index) {
                this.form.industry = this.actionSheetList[index].text;
                this.form.type = this.actionSheetList[index].id;
            },
            shenfen(index) {
                this.form.identity = this.shenfenlist[index].text;
                this.form.type = this.shenfenlist[index].id;
            },
            Job(index) {
                this.form.working = this.jobList[index].text;
                this.form.type = this.jobList[index].id;
            },
            Edu(index) {
                this.form.education = this.eduList[index].text;
                this.form.type = this.eduList[index].id;
            },
            nian(index) {
                this.form.year = this.yearList[index].text;
                this.form.type = this.yearList[index].id;
            },
        }
    }
</script>
<style>
    page{
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
    /deep/.u-input__input{
       min-height:39px;
    }
    .person{
        background: white;
        margin:30rpx;
        padding:30rpx;
        display: flex;
        .p-l{
            position: relative;
            .camera{
                background: #E22619;
                width:50rpx;
                height:50rpx;
                line-height:50rpx;
                border-radius: 50%;
                text-align: center;
                position: absolute;
                top:100rpx;
                left:90rpx;
            }

        }

        .p-r{
            flex:1;
            padding:0 30rpx;
            .top{
                margin-bottom: 30rpx;
                display: flex;
                flex-direction: row;
                justify-content: space-between;
                .name{
                    font-weight: 600;
                    font-size: 30rpx;
                }
            }
            .flex{
                flex-direction: row;
                display: flex;
                align-items: center;
            }
        }
    }
    .form{
        background: white;
        margin:30rpx;
        padding:0 20rpx;
        border-radius: 10rpx;
        .flex{
            justify-content: center;
            align-items: center;
        }
    }
</style>