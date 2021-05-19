<template>
    <view style="width: 100%;" >
        <web-view  :src="pdfUrl"></web-view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                pdfUrl:'',
                htmlUrl: '/pages/common/viewer.html',
            }
        },
        onLoad(options) {
            //从A页面点击跳转传递pdf文件路径过来
            let fileUrl = encodeURIComponent(options.pdfUrl) // encodeURIComponent 函数可把字符串作为 URI 组件进行编码。
            this.pdfUrl= this.htmlUrl+ '?file=' + fileUrl
        }
    }
</script>