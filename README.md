<img height="200" src="./weixin.png?raw=true">

# React-Native-Wechat

[React Native] bridging library that integrates WeChat SDKs:

- [x]  iOS SDK 1.8.2
- [x]  Android SDK ++

And [react-native-wechat] has the following tracking data in open source world:

| NPM                                  | Dependency                                     | Downloads                                      | Build                                       |
| ------------------------------------ | ---------------------------------------------- | ---------------------------------------------- | ------------------------------------------- |
| [![NPM version][npm-image]][npm-url] | [![Dependency Status][david-image]][david-url] | [![Downloads][downloads-image]][downloads-url] | [![Build Status][travis-image]][travis-url] |

## Table of Contents

- [Introduction](#introduction )
- [Use Case](#use-case)
- [Effect Picture](#effect-picture)
- [Get Startted](#get-startted)
- [API Documentation](#api-documentation)
- [Installation](#installation)
- [Community](#community)

## Introduction

- 该组件用于调起微信app 适用于安卓和ios，应用场景目前包括微信支付和微信分享等场景

## Use Case

- 微信支付
- 微信分享功能

## Effect Picture
- 微信支付效果

<a><img width="200" src="./docs/images/wechatPay.jpg"></a>
<a><img width="200" src="./docs/images/payNum.jpg"></a>
<a><img width="200" src="./docs/images/paySucess2.png"></a>
<a><img width="200" src="./docs/images/paySucess.jpg"></a>

- 微信分享效果

<a><img width="200" src="./docs/images/wechat1.png"></a>
<a><img width="200" src="./docs/images/send.png"></a>
<a><img width="200" src="./docs/images/chat.jpg"></a>
<a><img width="200" src="./docs/images/redPackect.jpg"></a>

## Get Startted

- [Build setup on iOS](./docs/build-setup-ios.md)
- [Build setup on Android](./docs/build-setup-android.md)

## API Documentation

[react-native-wechat] exposes the promise-based, therefore you could use `Promise`
or `async/await` to manage your dataflow.

#### registerApp(appid)

- `appid` {String} the appid you get from WeChat dashboard 
-  [登录微信开发者平台获取appid , ](https://open.weixin.qq.com/)账号：les2018@163.com 密码：les1028789
 
 <a><img width="200" src="./docs/images/appId.jpg"></a>

- returns {Boolean} explains if your application is registered done

This method should be called once globally.

```js
import * as WeChat from 'react-native-wechat';

WeChat.registerApp('appid');
```

#### registerAppWithDescription(appid, description)

- `appid` {String} the appid you get from WeChat dashboard
- `description` {String} the description of your app
- returns {Boolean} explains if your application is registered done

This method is only available on iOS.

#### isWXAppInstalled()

- returns {Boolean} if WeChat is installed.

Check if wechat installed in this app.

#### isWXAppSupportApi() (iOS平台)

- returns {Boolean}  Contain the result.

Check if wechat support open url.
#### isWXAppSupportApi(supportSdk) (Android平台)
```java
    //传入对应的字符串判断是否支持,没有找到微信文档,字面意思自己理解
    public static final int SDK_INT = 620824064;
    public static final int MIN_SDK_INT = 553713665;
    public static final int CHECK_TOKEN_SDK_INT = 620824064;
    public static final int TIMELINE_SUPPORTED_SDK_INT = 553779201;
    public static final int EMOJI_SUPPORTED_SDK_INT = 553844737;
    public static final int MUSIC_DATA_URL_SUPPORTED_SDK_INT = 553910273;
    public static final int PAY_SUPPORTED_SDK_INT = 570425345;
    public static final int OPENID_SUPPORTED_SDK_INT = 570425345;
    public static final int FAVORITE_SUPPPORTED_SDK_INT = 570425345;
    public static final int MESSAGE_ACTION_SUPPPORTED_SDK_INT = 570490883;
    public static final int SCAN_QRCODE_AUTH_SUPPORTED_SDK_INT = 587268097;
    public static final int MINIPROGRAM_SUPPORTED_SDK_INT = 620756993;
    public static final int VIDEO_FILE_SUPPORTED_SDK_INT = 620756996;
    public static final int SUBSCRIBE_MESSAGE_SUPPORTED_SDK_INT = 620756998;
    public static final int LAUNCH_MINIPROGRAM_SUPPORTED_SDK_INT = 620757000;
    public static final int CHOOSE_INVOICE_TILE_SUPPORT_SDK_INT = 620822528;
    public static final int INVOICE_AUTH_INSERT_SDK_INT = 620823552;
    public static final int NON_TAX_PAY_SDK_INT = 620823552;
    public static final int PAY_INSURANCE_SDK_INT = 620823552;
    public static final int SUBSCRIBE_MINI_PROGRAM_MSG_SUPPORTED_SDK_INT = 620823808;
    public static final int OFFLINE_PAY_SDK_INT = 620823808;
    public static final int SEND_TO_SPECIFIED_CONTACT_SDK_INT = 620824064;
    public static final int OPEN_BUSINESS_WEBVIEW_SDK_INT = 620824064;
```
- returns {Boolean}  Contain the result.

Check if wechat support open url.

#### getApiVersion()

- returns {String}  Contain the result.

Get api version of WeChat SDK.

#### openWXApp()

- returns {Boolean} 

Open the WeChat app from your application.

#### sendAuthRequest([scope[, state]])

- `scope` {Array|String} Scopes of auth request.
- `state` {String} the state of OAuth2
- returns {Object}

Send authentication request, and it returns an object with the 
following fields:

| field   | type   | description                         |
| ------- | ------ | ----------------------------------- |
| errCode | Number | Error Code                          |
| errStr  | String | Error message if any error occurred |
| openId  | String |                                     |
| code    | String | Authorization code                  |
| url     | String | The URL string                      |
| lang    | String | The user language                   |
| country | String | The user country                    |

#### class `ShareMetadata`

- `type` {Number} type of this message. Can be {news|text|imageUrl|imageFile|imageResource|video|audio|file}
- `thumbImage` {String} Thumb image of the message, which can be a uri or a resource id.
- `description` {String} The description about the sharing.
- `webpageUrl` {String} Required if type equals `news`. The webpage link to share.
- `imageUrl` {String} Provide a remote image if type equals `image`.
- `videoUrl` {String} Provide a remote video if type equals `video`.
- `musicUrl` {String} Provide a remote music if type equals `audio`.
- `filePath` {String} Provide a local file if type equals `file`.
- `fileExtension` {String} Provide the file type if type equals `file`.

#### shareToTimeline(message)

- `message` {ShareMetadata} This object saves the metadata for sharing
- returns {Object}

Share a `ShareMetadata` message to timeline(朋友圈) and returns:

| name    | type   | description                         |
| ------- | ------ | ----------------------------------- |
| errCode | Number | 0 if authorization successed        |
| errStr  | String | Error message if any error occurred |

These example code need 'react-native-chat' and 'react-native-fs' plugin.


#### shareToSession(message)

- `message` {ShareMetadata} This object saves the metadata for sharing
- `userName` {String} 拉起的小程序的username

<a><img width="200" src="./docs/images/username.png"></a>

- returns {Object}

Similar to `shareToTimeline` but send message to a friend or chat group.
```js

//微信发红包的方法
let url = '/pages/index/welcome/welcome?from=shareRedPacket&hbb_id=' + that.state.hbb_id
        let weixinMiniProgramShareInfo = {
            type: 'mini',//类型小程序 Could be {news|text|imageUrl|imageFile|imageResource|video|audio|file|mini}
            title:"标题名",//红包标题
            description: '描述内容',//描述
            thumbImage://发送的红包图片链接
                "https://xcx.yizhenit.com/lsxcx/0130685c53bf4ca801203d2245c5db.png",
            hdImageData://发送的红包高清图片链接
                "https://xcx.yizhenit.com/lsxcx/0130685c53bf4ca801203d2245c5db.png",
            userName: "gh_c12c60de6e9c",//你的小程序的username
            webpageUrl: "www.baidu.com",//Required if type equals news or mini. The webpage link to share.  如果是网页或者小程序  网页地址（需要填但是没作用）
            miniProgramType: 0,//拉起小程序的类型. 0-正式版 1-开发版 2-体验版
            path: url,//小程序页面路径
            shareTicket: false //是否使用带 shareTicket 的转发
        }
        Wechat.isWXAppInstalled()
            .then((isInstalled) => {
                if (isInstalled) {
                    Wechat.shareToSession(weixinMiniProgramShareInfo)
					.then((requestJson) => {
					console.log("requestJson=="+JSON.stringify(requestJson))
					//只要微信安装并登陆 不管分享有没有成功 ，返回值requestJson都是包含"errCode":0的json数据
                            /*requestJson=={"type":"SendMessageToWX.Resp",
                             "transaction":"de221ac7-2fba-41ec-bb4e-cdf422912c35",
                             "openId":"ovUt51AOoM2BEDcY2r0ciW74dxXc",
                            "errStr":null,"errCode":0}*/
                        }).
					.catch((err) => {
                        console.log(err.message)
						//err.message==-2（微信未登录）
                    });
                } else {
                    Alert.alert('请安装微信');
                }
            });

```
#### launchMini(params)

- `params` {Object} 打开小程序的参数

  - `userName` {String} 拉起的小程序的username

  - `miniProgramType` {Integer} 拉起小程序的类型. 0-正式版 1-开发版 2-体验版

  - `path` {String} 拉起小程序页面的可带参路径，不填默认拉起小程序首页

    

#### pay(payload)

- `payload` {Object} the payment data
  - `partnerId` {String} 商家向财付通申请的商家ID
  - `prepayId` {String} 预支付订单ID
  - `nonceStr` {String} 随机串
  - `timeStamp` {String} 时间戳
  - `package` {String} 商家根据财付通文档填写的数据和签名
  - `sign` {String} 商家根据微信开放平台文档对数据做的签名
- returns {Object}
```js


//微信支付的方法和参数
let datas = {
                partnerId: param.partnerid,  // 商家向财付通申请的商家id
                prepayId: param.prepayid,   // 预支付订单
                nonceStr: param.noncestr,   // 随机串，防重发
                timeStamp: param.timestamp.toString(),  // 时间戳，防重发
                package: param.package,    // 商家根据财付通文档填写的数据和签名
                sign: param.sign        // 商家根据微信开放平台文档对数据做的签名

            };
            Wechat.pay(datas).then((requestJson) => {
                //支付成功回调
                if (requestJson.errCode == "0") {
                    //回调成功处理
                } else {
                    //回调失败处理
                }
            }).catch((err) => {
                //捕获失败异常
            })

```
Sends request for proceeding payment, then returns an object:

| name    | type   | description                         |
| ------- | ------ | ----------------------------------- |
| errCode | Number | 0 if authorization successed        |
| errStr  | String | Error message if any error occurred |

## Installation

```sh
$ npm install react-native-wechat --save
```

## Community

#### Tutorials

- [react-native-wechat组件的安装与配置步骤](http://www.jianshu.com/p/3f424cccb888)
- [利用react-native-wechat实现实现微信好友/朋友圈分享功能-Android/iOS双平台通用](http://www.jianshu.com/p/ce5439dd1f52)
- [利用react-native-wechat实现微信作为游戏或者app的第三方登录](http://www.cnblogs.com/zhangdw/p/6194345.html)




