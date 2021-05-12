<template>
    <view class="page u-border-top">
            <u-dropdown>
                <u-dropdown-item v-model="year" title="2020三季度" :options="options1"></u-dropdown-item>
            </u-dropdown>
        <view>
            <u-cell-group>
                <u-cell-item :title-style="titles" :value-style="value" :arrow="false" title="每股指标" value=""></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="基本每股收益(元)" :value="con.beps ? con.beps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="扣非每股收益(元)" :value="con.deps ? con.deps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="稀释每股收益(元)" :value="con.ddeps ? con.ddeps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="每股净资产(元)" :value="con.naps ? con.naps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="每股公积金(元)" :value="con.pfps ? con.pfps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="每股未分配利润(元)" :value="con.upps ? con.upps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="每股经营现金流(元)" :value="con.ocfps ? con.ocfps : '-'"></u-cell-item>
            </u-cell-group>
            <u-gap height="25" bg-color="#f8f8f8"></u-gap>
            <u-cell-group>
                <u-cell-item :title-style="titles" :value-style="value" :arrow="false" title="成长能力指标" :value="con.ocfps ? con.ocfps : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="营业总收入(元)" :value="con.toi ? con.toi : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="毛利润(元)" :value="con.gross ? con.gross : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="归属净利润(元)" :value="con.anp ? con.anp : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="扣非净利润(元)" :value="con.npwd ? con.npwd : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="营业总收入同比增长(%)" :value="con.toiiyoy ? con.toiiyoy : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="归属净利润同比增长(%)" :value="con.anpiyoy ? con.anpiyoy : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="扣非净利润同比增长(%)" :value="con.npfdiyoy ? con.npfdiyoy : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="营业总收入滚动环比增长(%)" :value="con.toiioarmb ? con.toiioarmb : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="归属净利润滚动环比增长(%)" :value="con.anpioarmb ? con.anpioarmb : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="扣非净利润滚动环比增长(元)" :value="con.npwdioarmb ? con.npwdioarmb : '-'"></u-cell-item>
            </u-cell-group>
            <u-gap height="25" bg-color="#f8f8f8"></u-gap>
            <u-cell-group>
                <u-cell-item :title-style="titles" :value-style="value" :arrow="false" title="营业能力指标" value=""></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="加权净资产收益率(%)" :value="con.wroe ? con.wroe : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="摊薄净资产收益率(%)" :value="con.drona ? con.drona : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="摊薄总资产收益率(%)" :value="con.rodta ? con.rodta : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="毛利率(%)" :value="con.gmargin ? con.gmargin : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="净利率(%)" :value="con.nir ? con.nir : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="实际税率(%)" :value="con.etr ? con.etr : '-'"></u-cell-item>
            </u-cell-group>
            <u-gap height="25" bg-color="#f8f8f8"></u-gap>
            <u-cell-group>
                <u-cell-item :title-style="titles" :value-style="value" :arrow="false" title="盈利质量指标" value=""></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="预收款/营业收入" :value="con.aroi ? con.aroi : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="销售现金流/营业收入" :value="con.scfoi ? con.scfoi : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="经营现金流/营业收入" :value="con.ocfoi ? con.ocfoi : '-'"></u-cell-item>
            </u-cell-group>
            <u-gap height="25" bg-color="#f8f8f8"></u-gap>
            <u-cell-group>
                <u-cell-item :title-style="titles" :value-style="value" :arrow="false" title="运营能力指标" value=""></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="总资产周转率(次)" :value="con.trota ? con.trota : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="应收账款周转天数(天)" :value="con.artd ? con.artd : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="存货周转天数(天)" value="新版本" :value="con.itd ? con.itd : '-'"></u-cell-item>
            </u-cell-group>
            <u-gap height="25" bg-color="#f8f8f8"></u-gap>
            <u-cell-group>
                <u-cell-item :title-style="titles" :value-style="value" :arrow="false" title="财务风险指标" value=""></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="资产负债率(%)" :value="con.aal ? con.aal : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="流动负债/总负债(%)" :value="con.clta ? con.clta : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="流动比率" :value="con.current ? con.current : '-'"></u-cell-item>
                <u-cell-item :title-style="title" :value-style="value" :arrow="false" title="速动比率" :value="con.quick ? con.quick : '-'"></u-cell-item>
            </u-cell-group>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                title:{
                    color:'#959595'
                },
                titles:{
                    color:'#000000',
                    fontSize:'33rpx',
                    fontWeight:'600'
                },
                value:{
                    color:'#000000'
                },
                year:'',
                options1: [{
                    label: '2020三季度',
                    value: 1,
                },
                    {
                        label: '2020中报',
                        value: 2,
                    },
                    {
                        label: '2020一季度',
                        value: 3,
                    }
                ],
                con:[]
            }
        },
        onLoad (options) {
            this.list(options.id)
        },
        methods:{
            async list (id) {
                const { data: res } = await this.$request({
                    method: 'GET',
                    data:{
                        id:id,
                        report:2021
                    },
                    url: 'applets/indicator',
                })
                console.log(res)
                this.con=res
            },
            Change(index) {
                this.current = index;
            },
        }
    }
</script>

<style lang="scss" scoped>

</style>