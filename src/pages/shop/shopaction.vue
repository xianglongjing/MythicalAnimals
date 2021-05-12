<template>
    <view class="page">
      <view class="new-body">
        <view class="title">{{shopList.title}}</view>
          <view class="flex">
              <text>{{shopList.category.name}}</text>
              <text>{{shopList.category.created_at}}</text>
          </view>
          <view class="new-con">
              {{shopList.body}}
          </view>
          <u-image src="https://yiqiwang360.com/images/yiqiguanjia/yigao.png" width="100%" height="400"></u-image>
          <view class="new-con">
              {{shopList.body}}
          </view>
      </view>
        <view class="comment">
            <view class="title">热门评论(444)</view>
            <view class="comm-con u-border-bottom" :key="item.id" v-for="item in comment" v-if="storage.token !== ''">
                <u-image :src="item.avatarUrl ||'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg'" width="80" height="80"
                         shape="circle"></u-image>
                <view class="con-desc">
                    <view class="name">
                        {{item.nickName}}
                    </view>
                    <view>{{item.pivot.content}}</view>
                    <text class="date">{{item.pivot.created_at}}</text>
                    <view class="num" @click="heart" :data-id="item.pivot.id" :data-status="item.pivot.status">{{item.pivot.like}}
<!--                        <u-icon name="heart" class="u-margin-left-20" @click="heart"></u-icon>-->

                        <text :class="item.pivot.status?'cuIcon-likefill text-red':'cuIcon-like'"></text>
                    </view>
                </view>
            </view>
        </view>
        <view class="write">
            <view class="input">
            <u-input v-model="value" placeholder="写评论"/>
            </view>
            <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/icons/hua.png" width="60" height="60" class="u-margin-left-40" @click="write(shopList.id)"></u-image>
            <u-image mode="aspectFill" src="https://yiqiwang360.com/images/yiqiguanjia/icons/zhuan.png" width="60" height="60" class="u-margin-left-50"></u-image>
        </view>
    </view>
</template>

<script>
    export default {
        data(){
            return {
                storage:[],
                value:'',
                shopList:[],
                sta:'',
                comment:[],
                status:[],
                input:{
                  width:'100rpx'
                }
            }
        },
        onLoad (options) {
            this.getNavList(options.category_id)
        },
        onShow(){
            this.getStorage()
        },
        // 获取本地存储

        methods:{
            getStorage () {
                this.storage.token = uni.getStorageSync('token')
                this.storage.id = uni.getStorageSync('id')
                this.storage.nickName = uni.getStorageSync('nickName')
                this.storage.avatarUrl = uni.getStorageSync('avatarUrl')
            },
            async getNavList (id) {
                const user_id=uni.getStorageSync('id')
                const { news:res } =await this.$request({
                    method: 'POST',
                    url: '/show/news/'+id,
                    data:{
                        new_id:this.shopList.id,
                        user_id:uni.getStorageSync('id'),
                    }
                }).then(res=>{
                    console.log(res.data.data)
                    this.shopList = res.data.data.news
                    this.comment = res.data.data.news.user_and_replies
                    this.status = res.data.data.news.user_like;
                })

                // this.menuNum = 12 / res.data.length
            },
            async heart (reply_id) {
                const user_id=uni.getStorageSync('id')
                const { res } =await this.$request({
                    method: 'POST',
                    url: '/like',
                    data:{
                        status:reply_id.currentTarget.dataset.status,
                        reply_id:reply_id.currentTarget.dataset.id,
                        user_id:uni.getStorageSync('id'),
                        new_id:this.shopList.id
                    }
                }).then(res=>{
                    if( reply_id.currentTarget.dataset.status==0){
                       this.comment.pivot.status=false
                    }else{
                        this.comment.pivot.status=true
                    }
                        this.getNavList(id);
                })
                // if(reply_id.currentTarget.dataset.status==0){
                //     reply_id.currentTarget.dataset.status==1
                // }else{
                //     reply_id.currentTarget.dataset.status==0
                // }
                console.log( user_id)
            },
            async write (id) {
                const user_id=uni.getStorageSync('id')
                const { res } =await this.$request({
                    method: 'POST',
                    url: '/reply/store/',
                    data:{
                        user_id:user_id,
                        new_id:this.shopList.id,
                        content:this.value,
                        nickName:this.comment.nickName
                    }
                })
                console.log(res)
                this.getNavList(id);
            },
        }
    }
</script>
<style lang="scss">
    page {
        background: #f8f8f8;
    }
</style>
<style lang="scss" scoped>
.page{
    background: #f8f8f8;
}
    .new-body{
        background: white;
        margin:30rpx;
        padding:20rpx;
        .title{
            font-size: 30rpx;
            font-weight: 1000;
        }
        .flex{
            line-height: 60rpx;
            color:#B8B8B8;
            display: flex;
            flex-direction: row;
            justify-content: space-between;
        }
        .new-con{
            line-height: 50rpx;
            margin:20rpx 0;
            color:#585858;
            text-indent: 1em;
        }
    }
    .comment{
        background: white;
        padding:20rpx;
        margin:0 30rpx;
        .title{
            font-size: 30rpx;
            font-weight: 1000;
        }
        .comm-con{
            position: relative;
            padding:50rpx 0;
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            .con-desc{
                margin-left:20rpx;
                .name{
                    color:grey;
                }
                .num{
                    color:grey;
                    position: absolute;
                    top:60rpx;
                    right:10rpx;
                }
                .date{
                    color:grey;
                    font-size: 25rpx;
                    line-height: 50rpx;
                }
            }
        }
    }
    .write{
        display: flex;
        align-items: center;
        flex-direction: row;
        padding:0 30rpx;
        line-height: 100rpx;
        background: white;
        height: 100rpx;
        .input{
            text-indent: 2em;
            width:400rpx;
            line-height:50rpx;
            background:#F7F7F7;
            border-radius: 50rpx;
        }
    }
</style>