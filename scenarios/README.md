#BeeCloud应用场景

###BeeCloud 为移动端应用以及PC网站/WAP网站提供一站式的支付解决方案；使用BeeCloud SDK方便快捷的接入主流支付渠道

##BeeCloud产品简介

1. APP SDK:      
   [iOS SDK](https://github.com/beecloud/beecloud-ios)  &ensp;&ensp;  *适用在原生的iOS APP中接入支付功能*  
   [Android SDK](https://github.com/beecloud/beecloud-android) &ensp;&ensp;  *适用在原生的android APP中接入支付功能*  
   [AppCan SDK](http://plugin.appcan.cn/details.html?id=481) &ensp;&ensp; *适用于在使用AppCan SDK开发的H5 APP中接入支付功能*  
   [APICloud SDK](http://docs.apicloud.com/%E7%AB%AFAPI/%E5%BC%80%E6%94%BESDK/beecloud) &ensp;&ensp; *适用于在使用APICloud SDK开发的H5 APP中接入支付功能*   
   
2. PC及WAP SDK: 
	[JAVA SDK](https://github.com/beecloud/beecloud-java) &ensp;&ensp;   *适用于JAVA开发的网站中接入支付功能*  
	[PHP SDK](https://github.com/beecloud/beecloud-php)  &ensp;&ensp;   *适用于PHP开发网站中接入支付功能*  
	[.NET SDK](https://github.com/beecloud/beecloud-dotnet)  &ensp;&ensp;*适用于.NET开发网站中接入支付功能*  
	[Python SDK](https://github.com/beecloud/beecloud-python) &ensp;&ensp;*适用于Python开发网站中接入支付功能*

	
3. 线下收银:  
	[线下REST API](https://github.com/beecloud/beecloud-rest-api/blob/master/offline/README.md) &ensp;&ensp;   *适用于线下门店接入微信支付和支付宝支付（二维码展示支付 及 扫条形码/二维码支付）, 并根据API自主研发接入现有的收银系统中*  
	[**线下收款 APP iOS**]()  &ensp;&ensp;   **只需一个APP无需任何开发就可支持微信，支付宝收款**  
	[**线下收款 APP Android版**]() &ensp;&ensp;   **只需一个APP无需任何开发就可支持微信，支付宝收款**
	
## 接入步骤
> 1. 注册成为BeeCloud用户并通过企业认证
> 2. 选择符合您的应用场景（参见后文**应用场景分析**）
> 3. 选择您需要的支付渠道及产品， 自助开通或**关注BeeCloud官网是否开放代申请服务**
> 4. 选择使用的SDK  &ensp;&ensp;[SDK下载地址](https://beecloud.cn/download/)&ensp;&ensp;[在线文档地址](https://beecloud.cn/doc/) &ensp;&ensp; [SDK开源代码库](https://github.com/beecloud/)
> 5. 参考在[在线文档](https://beecloud.cn/doc/)及SDK里的demo工程，开发您自己的优秀产品!!!
> 6. 附： [FAQ页面(不断完善中)](https://beecloud.cn/faq/) &ensp;&ensp; [错误码对照表](https://github.com/beecloud/beecloud-rest-api/tree/master/error%20code)
	
## 应用场景分析

### 一.网页场景
>##### i. PC端网上商城 
>>1. 概念  
>>开发者正在开发一个运行在**PC浏览器**的网站，在其上售卖一些商品/服务
>>2. 可以接入的支付渠道及产品  
>>[微信 二维码 (公众号支付)](https://mp.weixin.qq.com/cgi-bin/loginpage?t=wxm2-login&lang=zh_CN)  
>>[支付宝 (即时到帐)](https://b.alipay.com/order/productDetail.htm?productId=2012111200373124)  
>>[银联 (网关支付)](https://open.unionpay.com/ajweb/product/detail?id=1)  
>>[京东支付 (PC端)](http://www.chinabank.com.cn/)   
>>[易宝支付 (网银支付)](http://www.yeepay.com/)  
>>[百度钱包 (即时到帐)](http://b.baifubao.com/sp_register/0/check_login/0)    
>>[PAYPAL](https://www.paypal.com/webapps/mpp/home)
>>3. 可以使用的SDK  
>>JAVA [开源代码库](https://github.com/beecloud/beecloud-java) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-java.zip)  
>>PHP [开源代码库](https://github.com/beecloud/beecloud-php) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-php.zip)  
>>Python [开源代码库](https://github.com/beecloud/beecloud-python) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-python.zip)  
>>.NET [开源代码库](https://github.com/beecloud/beecloud-dotnet) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-dotnet.zip)  

>##### ii.WAP端网上商城
>>1. 概念  
>>开发者正在开发一个运行在**手机浏览器**的移动网站，在其上售卖一些商品/服务
>>2. 可以接入的支付渠道及产品
>>[支付宝 (手机网站支付)](https://b.alipay.com/order/productDetail.htm?productId=2014110308142133)  
>>[银联 (网关支付)](https://open.unionpay.com/ajweb/product/detail?id=1)  
>>[京东支付 (WAP端)](http://www.chinabank.com.cn/)   
>>[易宝支付 (一键支付)](http://www.yeepay.com/)  
>>[百度钱包 (H5)](http://b.baifubao.com/sp_register/0/check_login/0)    
>>[PAYPAL](https://www.paypal.com/webapps/mpp/home)
>>3. 可以使用的SDK
>>JAVA [开源代码库](https://github.com/beecloud/beecloud-java) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-java.zip)  
>>PHP [开源代码库](https://github.com/beecloud/beecloud-php) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-php.zip)  
>>Python [开源代码库](https://github.com/beecloud/beecloud-python) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-python.zip)  
>>.NET [开源代码库](https://github.com/beecloud/beecloud-dotnet) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-dotnet.zip)  

>##### iii.微信公众号/微信内 运营商城
>>1. 概念  
>>开发者正在开发一个针运行在**微信内浏览器**的移动网站，在其上售卖一些商品/服务
>>2. 可以接入的支付渠道及产品  
>>[微信 (公众号支付)](https://mp.weixin.qq.com/cgi-bin/loginpage?t=wxm2-login&lang=zh_CN)   
>>[银联 (网关支付)](https://open.unionpay.com/ajweb/product/detail?id=1)  
>>[京东支付 (WAP端)](http://www.chinabank.com.cn/)   
>>[易宝支付 (一键支付)](http://www.yeepay.com/)  
>>[百度钱包 (H5)](http://b.baifubao.com/sp_register/0/check_login/0)    
>>[PAYPAL](https://www.paypal.com/webapps/mpp/home)
>>3. 可以使用的SDK  
>>JAVA [开源代码库](https://github.com/beecloud/beecloud-java) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-java.zip)  
>>PHP [开源代码库](https://github.com/beecloud/beecloud-php) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-php.zip)  
>>Python [开源代码库](https://github.com/beecloud/beecloud-python) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-python.zip)  
>>.NET [开源代码库](https://github.com/beecloud/beecloud-dotnet) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-dotnet.zip)

### 二.APP场景
>#####i. 原生语言的APP
>>1. 概念  
>>开发者正在使用**原生语言**开发一个**移动APP**（游戏，应用等等），在其上售卖一些商品/服务
>>2. 可以接入的支付渠道及产品  
>>[微信 (APP支付)](https://open.weixin.qq.com/)  
>>[支付宝 (移动支付)](https://b.alipay.com/order/productDetail.htm?productId=2014110308141993)  
>>[银联 (手机控件支付)](https://open.unionpay.com/ajweb/product/detail?id=3)  
>>[百度钱包 (快捷支付)](http://b.baifubao.com/sp_register/0/check_login/0)    
>>[PAYPAL](https://www.paypal.com/webapps/mpp/home)
>>3. 可以使用的SDK  
>>iOS 
>>[开源代码库](https://github.com/beecloud/beecloud-ios) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-ios.zip)  
>>Android [开源代码库](https://github.com/beecloud/beecloud-android) &ensp;&ensp;[下载地址](https://beecloud.cn/download/archive/beecloud-android.zip)

>#####ii. H5 APP
>>1. 概念  
>>开发者正在使用**H5语言**开发一个**移动APP**（游戏，应用等等），在其上售卖一些商品/服务
>>2. 可以接入的支付渠道及产品  
>>[微信 (APP支付)](https://open.weixin.qq.com/)  
>>[支付宝 (移动支付)](https://b.alipay.com/order/productDetail.htm?productId=2014110308141993)  
>>[银联 (手机控件支付)](https://open.unionpay.com/ajweb/product/detail?id=3) 
>>3. 可以使用的SDK  
>>[AppCan SDK](http://plugin.appcan.cn/details.html?id=481)  
>>[APICloud SDK](http://docs.apicloud.com/%E7%AB%AFAPI/%E5%BC%80%E6%94%BESDK/beecloud)

