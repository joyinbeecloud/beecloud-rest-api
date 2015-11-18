#BeeCloud打款REST API

### 简介

>1. 场景  
>商户需要将资金从自己的账户/虚拟账户 转入他人的账户/虚拟账户，例如：  
>代理商返点；用户提现；用户返点
>2. 目前支持渠道及产品  
>微信(公众号)  
>支付宝  
>**持续增加中**
>3. 目前支持方式  
>单笔  
>批量（批量目前只支持支付宝）
	
### 使用前准备
> 1. 注册成为BeeCloud用户并通过企业认证
> 3. 选择您需要的支付渠道及产品， 自助开通或**关注BeeCloud官网是否开放代申请服务**
> 4. 选择使用的SDK  &ensp;&ensp;[SDK下载地址](https://beecloud.cn/download/)&ensp;&ensp;[在线文档地址](https://beecloud.cn/doc/) &ensp;&ensp; [SDK开源代码库](https://github.com/beecloud/)
> 5. 参考在[在线文档](https://beecloud.cn/doc/)及SDK里的demo工程，开发您自己的优秀产品!!!
> 6. 附： [FAQ页面(不断完善中)](https://beecloud.cn/faq/) &ensp;&ensp; [错误码对照表](https://github.com/beecloud/beecloud-rest-api/tree/master/error%20code)

### Server 列表
>#### Mode : HTTPS
所有server可无差别使用，也可随机使用，请根据需要选择.

>域名 | 位置
---- | ----
apidynamic.beecloud.cn | 随机DNS解析到以下一台上
apibj.beecloud.cn| 北京 
apisz.beecloud.cn| 深圳 
apiqd.beecloud.cn| 青岛 
apihz.beecloud.cn| 杭州 
	
## API

### 一. 单笔打款
> ####1. URL: */2/rest/transfer/*
> ####2. METHOD: *POST*
> ####3. Content-type: *application/json*
> ####4. 请求参数详情
> > ####参数:
> > 
> > 参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ----
app_id | String | BeeCloud平台的AppID | App在BeeCloud平台的唯一标识 | 0950c062-5e41-44e3-8f52-f89d8cf2b6eb | 是
timestamp | Long | 签名生成时间 | 时间戳，毫秒数 | 1435890533866 | 是
app_sign | String | 加密签名 | 算法: md5(app\_id+timestamp+**master\_secret**)，32位16进制格式,不区分大小写 | b927899dda6f9a04afc57f21ddf69d69 | 是
channel| String | 渠道类型 | 根据不同场景选择不同的支付方式 | WX_REDPACK, WX\_TRANSFER, ALI\_TRANSFER(详见附注）| 是
transfer_no | String | 打款单号 | 支付宝为11-32位数字字母组合， 微信为10位数字 | udjfiienx2334/8372839123 | 是
total_fee | Int | 打款金额 | 此次打款的金额,单位分,正整数(微信红包1.00-200元，微信打款>=1元) | 1 | 是
desc | String | 打款说明 | 此次打款的说明 | 赔偿 | 是
channel_user\_id | String | 用户id | 支付渠道方内收款人的标示, 微信为openid, 支付宝为支付宝账户 | someone@126.com |是
channel_user\_name | String | 用户名| 支付渠道内收款人账户名， 支付宝必填 | 支付宝某人 | 否
redpack_info | Map | 红包信息 | 微信红包的详细描述，详见附注, 微信红包必填 | - | 否
account_name|String|打款方账号名称|打款方账号名全称，支付宝必填|苏州比可网络科技有限公司|否


>> 注1：channel的参数值含义：  
WX\_REDPACK: 微信红包  
WX\_TRANSFER: 微信企业打款  
ALI_TRANSFER: 支付宝企业打款 

>> 注2: redpack_info 参数列表
>> 
>> 参数名 | 类型 | 含义 | 例子
---- | ---- | ---- | ----
send_name| String | 红包发送者名称 32位 | BeeCloud
wishing | String | 红包祝福语 128 位| BeeCloud祝福开发者工作顺利!
act_name | String | 红包活动名称 32位 | BeeCloud开发者红包轰动

> ####5. 返回结果 (JSON, Map)
>> 
>> 参数名 | 类型 | 含义 
---- | ---- | ----
result_code | Integer | 返回码，0为正常
result_msg  | String | 返回信息， OK为正常
err_detail  | String | 具体错误信息
url | String | 支付宝需要跳转到支付宝链接输入支付密码确认
>> 
>> 注1: 错误码（错误详细信息 参考 **err_detail**字段)
>> 
>> result_code | result_msg             | 含义
----        | ----      		       | ----
0           | OK                     | 调用成功
1           | APP\_INVALID           | 根据app\_id找不到对应的APP或者app\_sign不正确
2           | PAY\_FACTOR_NOT\_SET   | 支付要素在后台没有设置
3           | CHANNEL\_INVALID       | channel参数不合法
4           | MISS\_PARAM            | 缺少必填参数
5           | PARAM\_INVALID         | 参数不合法
6           | CERT\_FILE\_ERROR      | 证书错误
7           | CHANNEL\_ERROR         | 渠道内部错误
14          | RUN\_TIME_ERROR        | 实时未知错误，请与技术联系帮助查看
>> 
>> 注2:  
>> 微信返回result_code 0 代表打款成功  
>> 支付宝返回result\_code 0 需要跳转到url 地址的页面去输入支付宝支付密码
>> 

### 二. 批量打款

> ####1. URL: */2/rest/transfers/*
> ####2. METHOD: *POST*
> ####3. Content-type: *application/json*
> ####4. 请求参数详情
> > ####参数:
> > 
> > 参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ----
app_id | String | BeeCloud平台的AppID | App在BeeCloud平台的唯一标识 | 0950c062-5e41-44e3-8f52-f89d8cf2b6eb | 是
timestamp | Long | 签名生成时间 | 时间戳，毫秒数 | 1435890533866 | 是
app_sign | String | 加密签名 | 算法: md5(app\_id+timestamp+**master\_secret**)，32位16进制格式,不区分大小写 | b927899dda6f9a04afc57f21ddf69d69 | 是
channel| String | 渠道类型 | 根据不同场景选择不同的支付方式 | 目前只支持ALI| 是
batch_no | String | 打款单号 | 支付宝为11-32位数字字母组合 | 2015110525023331aa | 是
account_name | String | 付款方名称| 付款账号账户全称 | 苏州xx科技有限公司 | 是
transfer_data | List<Map> | 付款详细 | 包含每一笔的具体信息(参见注释) |  -- | 是

>> 注2: 支付宝时transfer_data 每一个Map的参数列表
>> 
>> 参数名 | 类型 | 含义 | 例子
---- | ---- | ---- | ----
transfer_id| String | 打款流水号 | 0315006
receiver_account | String | 收款方账户| someone@126.com
receiver_name | String | 收款方账号姓名 | 支付宝某人
transfer_fee | Int | 打款金额，单位为分 | 10
transfer_note | String | 打款备注 | 赔款

> ####5. 返回结果 (JSON, Map)
>> 
>> 参数名 | 类型 | 含义 
---- | ---- | ----
result_code | Integer | 返回码，0为正常
result_msg  | String | 返回信息， OK为正常
err_detail  | String | 具体错误信息
url | String | 支付宝需要跳转到支付宝链接输入支付密码确认
>> 
>> 支付宝返回result\_code 0 需要跳转到url 地址的页面去输入支付宝支付密码

## 联系我们
- 如果有什么问题，可以到BeeCloud开发者3群:**102350518** 提问
- 如果发现了bug，欢迎提交[issue](https://github.com/beecloud/beecloud-rest-api/issues)
- 如果有新的需求，欢迎提交[issue](https://github.com/beecloud/beecloud-rest-api/issues)

## 代码许可
The MIT License (MIT).



