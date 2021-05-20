<template>
    <view class="page u-border-top">
        <view class="con">
            <view class="flex left">
                <u-image mode="aspectFill" width="80" height="80"
                         :src="item.partner.image || 'https://seopic.699pic.com/photo/50139/5280.jpg_wh1200.jpg'"></u-image>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return{

            }
        },
        onLoad(options){
            this.list(options.id)
        },
        methods:{
            async list (id) {
                const { data: res } = await this.$request({
                    method: 'GET',
                    data:{
                        id:id
                    },
                    url: 'applets/trademarksave',
                })
                console.log(res)
                this.con=res
            },
        }
    }
</script>

<style lang="scss" scoped>

</style>