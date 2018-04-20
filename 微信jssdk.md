[TOC]
> [官网jssdk的接口参考网址](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421141115)
> [下载官网demo](http://demo.open.weixin.qq.com/jssdk/sample.zip)中的`jssdk.php`和`sample.php`


## 绑定域名
“公众号设置”的“功能设置”里填写“JS接口安全域名”

## 引入js文件
`<script src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>`

## 通过config接口注入权限验证配置
```
wx.config({
    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
    appId: '', // 必填，公众号的唯一标识
    timestamp: , // 必填，生成签名的时间戳
    nonceStr: '', // 必填，生成签名的随机串
    signature: '',// 必填，签名
    jsApiList: [] // 必填，需要使用的JS接口列表
});
```

## 通过ready接口处理成功验证
```js
wx.ready(function(){
    // config信息验证后会执行ready方法，
    //所有接口调用都必须在config接口获得结果之后，加载时就要调用的写在ready中  
     //对于用户触发时才调用的接口，则可以直接调用，不需要放在ready函数中。
});
```

## 通过error接口处理失败验证
```
wx.error(function(res){
    // config信息验证失败会执行error函数，
    //具体错误信息可以打开config的debug模式查看，也可以在返回的res参数中查看，对于SPA可以在这里更新签名。
});
```

## 接口调用说明
```
所有接口通过wx对象(也可使用jWeixin对象)来调用，参数是一个对象，除了每个接口本身需要传的参数之外，还有以下通用参数：

1.success：接口调用成功时执行的回调函数。

2.fail：接口调用失败时执行的回调函数。

3.complete：接口调用完成时执行的回调函数，无论成功或失败都会执行。

4.cancel：用户点击取消时的回调函数，仅部分有用户取消操作的api才会用到。

5.trigger: 监听Menu中的按钮点击时触发的方法，该方法仅支持Menu中的相关接口。


调用成功时："xxx:ok" ，其中xxx为调用的接口名

用户取消时："xxx:cancel"，其中xxx为调用的接口名

调用失败时：其值为具体错误信息
```

## 常用接口案例
### 基础接口

```js
wx.checkJsApi({
    jsApiList: ['chooseImage'],  // 需要检测的JS接口列表，所有JS接口列表见附录2,
    success: function(res) {
    
    // res：{"checkResult":{"chooseImage":true},"errMsg":"checkJsApi:ok"}
    }
});
```
### 微信支付
```
wx.chooseWXPay({
    timestamp: 0, // 支付签名时间戳，注意微信jssdk中的所有使用timestamp字段均为小写。但最新版的支付后台生成签名使用的timeStamp字段名需大写其中的S字符
    nonceStr: '', // 支付签名随机串，不长于 32 位
    package: '', // 统一支付接口返回的prepay_id参数值，提交格式如：prepay_id=\*\*\*）
    signType: '', // 签名方式，默认为'SHA1'，使用新版支付需传入'MD5'
    paySign: '', // 支付签名
    success: function (res) {
    // 支付成功后的回调函数
    }
});
备注：prepay_id 通过微信支付统一下单接口拿到，
paySign 采用统一的微信支付 
Sign 签名生成方法，
注意这里 appId 也要参与签名，
appId 与 config 中传入的 appId 一致，
即最后参与签名的参数有appId, timeStamp, nonceStr, package, signType。
```

### 分享接口
#### 分享到朋友圈
```js
wx.onMenuShareTimeline({
    title: '', // 分享标题
    link: '', // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
    imgUrl: '', // 分享图标
    success: function () {
    // 用户确认分享后执行的回调函数
	},
    cancel: function () {
        // 用户取消分享后执行的回调函数
     }
});
```
#### 分享给朋友
```
wx.onMenuShareAppMessage({
    title: '', // 分享标题
    desc: '', // 分享描述
    link: '', // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
    imgUrl: '', // 分享图标
    type: '', // 分享类型,music、video或link，不填默认为link
    dataUrl: '', // 如果type是music或video，则要提供数据链接，默认为空
    success: function () {
    // 用户确认分享后执行的回调函数
    },
    cancel: function () {
    // 用户取消分享后执行的回调函数
    }
});
```