#### uniapp-canvas-drawer
**uniapp-canvas-drawer** 是基于 **kuckboy1994** 的 [mp_canvas_drawer](https://github.com/kuckboy1994/mp_canvas_drawer/) 移植的 **uni-app** 版本。**之后同步更新**。

**下载地址** [uniapp-canvas-drawer](https://github.com/quanweiwang/uniapp-canvas-drawer/)。

当前环境下，大家都非常需要分享到朋友圈这个功能，但是实现起来各有心酸（坑比较多），所以才有了如下的 `canvas` 绘图工具。

#### 具有如下特性：
##### 简单易用
一个 `json` 搞定绘制图片
##### 功能全满足 `90%` 的使用场景
1、绘制文本（换行、超出内容省略号、中划线、下划线、文本加粗）
2、绘制图片
3、绘制矩形
4、保存图片
5、多图绘制
6、代码量小

#### 体验
```
git clone https://github.com/quanweiwang/uniapp-canvas-drawer
```
想在手机上使用配置自己的 `appid` 即可。

#### 使用
1、clone 到本地
```javascript
git clone https://github.com/quanweiwang/uniapp-canvas-drawer
```
2、把 `components` 中的 `uniapp-canvas-drawer` 拷贝到自己项目下。
3、在 **pages.json** 使用页面注册组件
```json
{
  	"path": "pages/index/index",
  	"style": {
		"navigationBarTitleText": "uni-app",
		"usingComponents": {
			"canvasdrawer": "/components/uniapp-canvas-drawer/uniapp-canvas-drawer"
		}
  	}
}
```
4、在页面 `**.vue` 文件中加入如下代码
```objc
<canvasdrawer painting="{{painting}}" bind:getImage="eventGetImage"/>
```
`painting` 是需要传入的 `json`。 `getImage` 方法是绘图完成之后的回调函数，在 `event.detail` 中返回绘制完成的图片地址。
当前栗子中的 `painting` 简单展示一下。详细配置请看 [API]
```js
  {
    width: 375,
    height: 555,
    views: [
      {
        type: 'image',
        url: 'https://hybrid.xiaoying.tv/miniprogram/viva-ad/1/1531103986231.jpeg',
        top: 0,
        left: 0,
        width: 375,
        height: 555
      },
      {
        type: 'image',
        url: 'https://wx.qlogo.cn/mmopen/vi_32/DYAIOgq83epJEPdPqQVgv6D8bojGT4DrGXuEC4Oe0GXs5sMsN4GGpCegTUsBgL9SPJkN9UqC1s0iakjQpwd4h4A/132',
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
        content: '您的好友【kuckboy】',
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
        url: 'https://hybrid.xiaoying.tv/miniprogram/viva-ad/1/1531385433625.jpeg',
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
```
#### API
```js
{
  width: 375,
  height: 555,
  views: [
    {
      type: 'image',
      url: 'url',
      top: 0,
      left: 0,
      width: 375,
      height: 555
    },
    {
      type: 'text',
      content: 'content',
      fontSize: 16,
      color: '#402D16',
      textAlign: 'left',
      top: 33,
      left: 96,
      bolder: true
    },
    {
      type: 'rect',
      background: 'color',
      top: 0,
      left: 0,
      width: 375,
      height: 555
    }
  ]
}
```
数据对象的第一层需要三个参数: `width`、`height`、`mode`、`views`。配置中所有的数字都是没有单位的。这就意味着 `canvas` 绘制的是一个比例图。具体显示的大小直接把返回的图片路径放置到 `image` 标签中即可。

`mode` 可选值有 `same`, 默认值为空，常规下尽量不要使用。如要使用请看 Q&A的第1点。

当前可以绘制3种类型的配置: `image`、`text`、`rect`。配置的属性基本上使用的都是 `css` 的驼峰名称，还是比较好理解的。 

##### image（图片）
[![](https://img.wangquanwei.com/wp-content/uploads/2019/10/1571491779-C509C509-7570-4CBF-AF35-429ACD3882E6.jpeg)](https://img.wangquanwei.com/wp-content/uploads/2019/10/1571491779-C509C509-7570-4CBF-AF35-429ACD3882E6.jpeg)

##### text（文本）
[![](https://img.wangquanwei.com/wp-content/uploads/2019/10/1571491829-A6CD7773-0577-4AF0-AC0A-E80BA92E0632.jpg)](https://img.wangquanwei.com/wp-content/uploads/2019/10/1571491829-A6CD7773-0577-4AF0-AC0A-E80BA92E0632.jpg)
##### rect (矩形，线条)
[![](https://img.wangquanwei.com/wp-content/uploads/2019/10/1571491861-8002F2FD-A8B4-4674-99F6-719A13F8711B.jpeg)](https://img.wangquanwei.com/wp-content/uploads/2019/10/1571491861-8002F2FD-A8B4-4674-99F6-719A13F8711B.jpeg)

#### Q&A
##### 1、最佳实践
绘制操作的时候最好 `锁住屏幕` ，例如在点击绘制的时候
```js
uni.showLoading({
	title: '绘制分享图片中',
	mask: true
})
```
绘制完成之后
```js
uni.hideLoading()
```
具体可以参考项目下的`/pages/index/index.vue`

##### 2、二维码和小程序码如何绘制？
二维码和小程序码可以通过调用[微信官方的接口](https://developers.weixin.qq.com/miniprogram/dev/api/qrcode.html)产生，需要后端配合。然后走 `type: image` 类型进行绘制即可。

##### 3、绘制流程相关
`views` 数组中的顺序代表绘画的先后顺序，会有覆盖的现象。请各位使用者注意。

##### 4、如何实现圆形头像？
由于完成一些效果，例如： `文字下划线` 等。必须要使用微信小程序 `rect` 相关的接口，和 `clip` 接口感觉相处的不好（存在bug）。可以查看 [微信小程序社区的帖子](https://developers.weixin.qq.com/blogdetail?action=get_post_info&docid=00086255ef09d0df4b0751f6651000&highline=clip&token=895863755&lang=zh_CN)。

so，提供一种解决方式：`使用一张中间镂空的图片盖在头像上`。

##### 5、`canvas drawer` 组件为什么不直接显示 `canvas` 画板和其内容呢？
考虑到大部分场景，我们都是用来把图片保存到本地，或用以展示。
保存到本地，返回临时文件给调用者一定是最佳的解决方式。
展示，转化成图片之后，就可以使用 `image` 基础组件的所有显示模式了，还能设置宽高。

#### 更新计划
~~图片缓存机制 - 加快相同图片绘制的速度~~  
~~增加 `measureText` 方法对于低版本的提示~~  
~~安卓下文本绘制稳定性修复~~  
增加圆角属性 `borderRadius`、`border` 支持 `待原作者更新后 同步更新`  
~~错误异常回调支持~~  
预缓存模式 `待原作者更新后 同步更新`  
优化 `measureText` 测量模式 `待原作者更新后 同步更新`  
~~mpvue 版本小程序~~

#### TIPS

如果有什么疑问，欢迎 `issues`。 如果觉得不错，能不能送我小 ✨ ✨ ，让我有更多的动力。
