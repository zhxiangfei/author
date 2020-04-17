## 网页授权登陆 ##
微信开发文档 [https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html "网页授权")

#### 一、公众号配置 ####
在微信公众号请求用户网页授权之前，开发者需要先到公众平台官网中的“开发 - 接口权限 - 网页服务 - 网页帐号 - 网页授权获取用户基本信息”的配置选项中，修改授权回调域名。请注意，这里填写的是域名（是一个字符串），而不是URL，因此请勿加 http:// 等协议头；

![](https://i.imgur.com/uK5n6Gt.png)

![](https://i.imgur.com/xGdPKEJ.png)

授权登陆有两种：一种是 snsapi_base 静默登陆，登陆的时候不会弹出授权弹窗，但是这种方式只能获取 openid；另一种是 snsapi_userinfo，这种方式会弹出授权框，需要用户手动同意，可以获取到用户的详细信息

access_token：网页授权用的access_token和基础支持中的“获取access_token”的接口获取的普通access_token不同；
#### 二、授权流程 ####
1、用户同意授权，获取code

在需要授权的地方引导用户进入授权页面
![授权页面](https://i.imgur.com/8EUgLkt.png)

用户同意授权后，页面会跳转到之前填写的回调页面，在回调地址url后面会携带code参数，截取url就可以得到code了

注意：每次授权携带的code都不一样

2、通过code换取网页授权access_token
如果之前选择的授权作用域是snsapi_base，那么在本步骤获取access_token的同时，openid也会获取到，那么snsapi_base方式的网页授权也就到此结束了；如果用的是snsapi_userinfo，那还要继续往下。

需要注意的是access_token有过期时间，所以注意这个时间，避免access_token过期。

3、获取用户信息

通过前几步获取到的access_token和openid，去请求接口，就额可以获取用户的详细信息了
![用户信息](https://i.imgur.com/b8K4Hzk.png)