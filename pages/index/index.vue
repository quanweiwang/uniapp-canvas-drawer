<template>
  <view class="content">
    <image :src="shareImage" class="share-image" mode="aspectFit"></image>
    <canvasdrawer :painting="painting" class="canvasdrawer" @getImage="eventGetImage" />
    <button @click="eventDraw">绘制</button>
    <button @click="eventSave">保存到本地</button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        painting: {},
        shareImage: ''
      }
    },
    onLoad() {

    },
    methods: {
      eventDraw() {
        uni.showLoading({
          title: '绘制分享图片中',
          mask: true
        })

        this.painting = {
          width: 375,
          height: 555,
          clear: true,
          views: [{
              type: 'image',
              url: 'https://hybrid.xiaoying.tv/miniprogram/viva-ad/1/1531103986231.jpeg',
              top: 0,
              left: 0,
              width: 375,
              height: 555
            },
            {
              type: 'image',
              url: 'https://wx.qlogo.cn/mmopen/vi_32/DYAIOgq83erma73GwPeY6QhTwTlkMiaSICnA2aeW43Jv4N1fvuwRTYyxMIqVOBicKg4wBJjeCcU32uAIFf3b4mOQ/132',
              top: 27.5,
              left: 29,
              width: 55,
              height: 55
            },
            {
              type: 'image',
              url: 'https://hybrid.xiaoying.tv/miniprogram/viva-ad/1/1531401349117.jpeg',
              top: 27.5,
              left: 29,
              width: 55,
              height: 55
            },
            {
              type: 'text',
              content: '您的好友【王独秀】',
              fontSize: 16,
              color: '#402D16',
              textAlign: 'left',
              top: 33,
              left: 96,
              bolder: true
            },
            {
              type: 'text',
              content: '发现一件好货，邀请你一起0元免费拿！',
              fontSize: 15,
              color: '#563D20',
              textAlign: 'left',
              top: 59.5,
              left: 96
            },
            {
              type: 'image',
              url: 'https://hybrid.xiaoying.tv/miniprogram/viva-ad/1/1531385366950.jpeg',
              top: 136,
              left: 42.5,
              width: 290,
              height: 186
            },
            {
              type: 'image',
              url: 'https://wx.qlogo.cn/mmopen/vi_32/DYAIOgq83erma73GwPeY6QhTwTlkMiaSICnA2aeW43Jv4N1fvuwRTYyxMIqVOBicKg4wBJjeCcU32uAIFf3b4mOQ/132',
              top: 443,
              left: 85,
              width: 68,
              height: 68
            },
            {
              type: 'text',
              content: '正品MAC魅可口红礼盒生日唇膏小辣椒Chili西柚情人',
              fontSize: 16,
              lineHeight: 21,
              color: '#383549',
              textAlign: 'left',
              top: 336,
              left: 44,
              width: 287,
              MaxLineNumber: 2,
              breakWord: true,
              bolder: true
            },
            {
              type: 'text',
              content: '￥0.00',
              fontSize: 19,
              color: '#E62004',
              textAlign: 'left',
              top: 387,
              left: 44.5,
              bolder: true
            },
            {
              type: 'text',
              content: '原价:￥138.00',
              fontSize: 13,
              color: '#7E7E8B',
              textAlign: 'left',
              top: 391,
              left: 110,
              textDecoration: 'line-through'
            },
            {
              type: 'text',
              content: '长按识别图中二维码帮我砍个价呗~',
              fontSize: 14,
              color: '#383549',
              textAlign: 'left',
              top: 460,
              left: 165.5,
              lineHeight: 20,
              MaxLineNumber: 2,
              breakWord: true,
              width: 125
            }
          ]
        }
      },
      eventSave() {
        uni.saveImageToPhotosAlbum({
          filePath: this.shareImage,
          success(res) {
            uni.showToast({
              title: '保存图片成功',
              icon: 'success',
              duration: 2000
            })
          }
        })
      },
      eventGetImage(event) {
        uni.hideLoading()
        
        // const { tempFilePath, errMsg } = event.detail
        
        let result = null
        let tempFilePath = null
        let errMsg = null
        
        // #ifdef MP-WEIXIN
        result = event.detail.__args__
        tempFilePath = result[0].tempFilePath
        errMsg = result[0].errMsg
        // #endif

        // #ifdef APP-PLUS
        result = event
        tempFilePath = result.tempFilePath
        errMsg = result.errMsg
        // #endif
        
        if (errMsg === 'canvasdrawer:ok') {
          
          // #ifdef MP-WEIXIN
          this.shareImage = tempFilePath
          // #endif
          
          // #ifdef APP-PLUS
          this.shareImage = 'file:///'+plus.io.convertLocalFileSystemURL(tempFilePath)
          // #endif
          this.painting = {}
        }
				else {
					console.log(errMsg)
				}
      }
    }
  }
</script>

<style scoped>
  .share-image {
    width: 600upx;
    height: 888upx;
    margin: 0 75upx;
    border: 1px solid black;
  }

  button {
    margin-top: 20upx;
  }
</style>
