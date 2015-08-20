## BeeCloud 线下 RESTful API (产品开发中）

## Part1. 文档

### 1. Server 列表
#### Mode : *HTTPS*

所有server可无差别使用，也可随机使用，请根据需要选择.

域名 | 位置
---- | ----
apibj.beecloud.cn| 北京 
apisz.beecloud.cn| 深圳 
apiqd.beecloud.cn| 青岛 
apihz.beecloud.cn| 杭州 

<BR>

### 2. 支付

此接口为支付流程的第一步，主要功能在于生成订单，获取必要的参数信息，来进行下一步的支付流程. 对于不同的渠道和支付方式，接口的返回值与后续的操作（例如微信App支付需要调用微信支付SDK的接口，支付宝网页支付需要跳转到获取的一段HTML网址等）都不尽相同，请根据每一个channel的详细描述分别处理.

#### URL:   */1/rest/offline/bill*
#### Method: *POST*
#### 请求参数格式: *JSON: Map*

#### 请求参数详情:
- 以下为公共参数：

参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ----
app_id | String | BeeCloud平台的AppID | App在BeeCloud平台的唯一标识 | 0950c062-5e41-44e3-8f52-f89d8cf2b6eb | 是
timestamp | Long | 签名生成时间 | 时间戳，毫秒数 | 1435890533866 | 是
app_sign | String | 加密签名 | 算法: md5(app\_id+timestamp+app\_secret)，32位16进制格式,不区分大小写 | b927899dda6f9a04afc57f21ddf69d69 | 是
channel| String | 渠道类型 | 根据不同场景选择不同的支付方式 | WX\_NATIVE、WX_SCAN、ALI\_OFFLINE\_QRCODE、ALI_SCAN(详见附注）| 是
total_fee | Integer | 订单总金额 | 必须是正整数，单位为分 | 1 | 是
bill_no | String | 商户订单号 | 8到32位数字和/或字母组合，请自行确保在商户系统中唯一，同一订单号不可重复提交，否则会造成订单重复 | 201506101035040000001 | 是
title| String | 订单标题 | UTF8编码格式，32个字节内，最长支持16个汉字 | 白开水 | 是
optional | Map | 附加数据 | 用户自定义的参数，将会在webhook通知中原样返回，该字段主要用于商户携带订单的自定义数据 | {"key1":"value1","key2":"value2",...} | 否
auth_code | String | 用户授权码| 当商户用扫码枪扫用户的条形码时得到的字符串 | 23891113455872 | 当channel参数为 WX_SCAN或ALI_SCAN 时为必填

> 注1：channel的参数值含义：  
WX\_NATIVE: 微信二维码支付   
ALI\_OFFLINE\_QRCODE: 支付宝二维码支付  
WX_SCAN: 微信条形码支付
ALI_SCAN: 支付宝条形码支付 


- 以下是支付宝条码(ALI_SCAN)的选填参数：

参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ---
terminal_id | string | 机具终端编号 | 商户机具终端编号 最长32位 | NJ_T_001 | 若机具商接入，terminal_id(机具终端编号)必填，store_id(商户门店编号)选填
store_id | string | 商户门店编号 | 商户门店编号 最长32位 | NJ_001 | 若系统商接入，store_id（商户的门店编号）必填，terminal_id(机具终端编号)选填

#### 返回类型: *JSON: Map*
#### 返回参数:

- **公共返回参数**

参数名 | 类型 | 含义 
---- | ---- | ----
result_code | Integer | 返回码，0为正常
result_msg  | String | 返回信息， OK为正常
err_detail  | String | 具体错误信息

- **公共返回参数取值列表及其含义**

result_code | result_msg             | 含义
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

> **当result_code不为0时，如需详细信息，请查看err\_detail字段**

**<mark>以下字段在result_code为0时有返回</mark>**

- WX_NATIVE

参数名 | 类型 | 含义 
---- | ---- | ----
qr_code | String | 二维码地址

- WX_JSAPI

参数名 | 类型 | 含义 
---- | ---- | ----
submit_result | Bool | 是否下单
submit_msg  | String | 下单返回信息
pay_result  | Bool | 用户是否支付


</br>

### 3. 订单状态查询

#### URL:   */1/rest/offline/bill/{bill_no}*
#### Method: POST

#### 请求参数类型:JSON

#### 请求参数详情:

参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ----
app_id | String | BeeCloud应用APPID | BeeCloud的唯一标识 | 0950c062-5e41-44e3-8f52-f89d8cf2b6eb | 是
timestamp | Long | 签名生成时间 | 时间戳，毫秒数 | 1435890533866 | 是
app_sign | String | 加密签名 | 算法: md5(app\_id+timestamp+app_key)，32位16进制格式，不区分大小写 | b927899dda6f9a04afc57f21ddf69d69 | 是
channel| String | 渠道类型 | 根据不同场景选择不同的支付方式 | WX\_NATIVE、WX_SCAN、ALI\_OFFLINE\_QRCODE、ALI_SCAN(详见支付附注） | 否
method | String | 订单修改的方法 | UPDATE代表去渠道更新订单 | UPDATE | 是

#### 返回类型: *JSON, Map*
#### 返回详情:

- 公共返回参数

参数名 | 类型 | 含义 
---- | ---- | ----
result\_code | Integer | 返回码，0为正常
result\_msg  | String | 返回信息， OK为正常
err\_detail  | String | 具体错误信息
pay_result | Bool | 订单是否成功

> 公共返回参数取值及含义参见支付公共返回参数部分

### 4. 撤销订单

#### URL:   */1/rest/offline/bill/{bill_no}*
#### Method: POST JSON
#### bill_no : 订单号

#### 请求参数类型:JSON

#### 请求参数详情:

参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ----
app_id | String | BeeCloud应用APPID | BeeCloud的唯一标识 | 0950c062-5e41-44e3-8f52-f89d8cf2b6eb | 是
timestamp | Long | 签名生成时间 | 时间戳，毫秒数 | 1435890533866 | 是
app_sign | String | 加密签名 | 算法: md5(app\_id+timestamp+app\_secret)，32位16进制格式，不区分大小写 | b927899dda6f9a04afc57f21ddf69d69 | 是
channel| String | 渠道类型 | 根据不同场景选择不同的支付方式 | WX\_NATIVE、WX_SCAN、ALI\_OFFLINE\_QRCODE、ALI_SCAN(详见支付附注） | 否
method | String | 订单修改的方法 | REVERT代表取消订单 | REVERT | 是

#### 返回类型: *JSON, Map*
#### 返回详情:

- 公共返回参数

参数名 | 类型 | 含义 
---- | ---- | ----
result\_code | Integer | 返回码，0为正常
result\_msg  | String | 返回信息， OK为正常
err\_detail  | String | 具体错误信息
revert_result | bool | 订单是否取消	

> 公共返回参数取值及含义参见支付公共返回参数部分


### 5. 订单查询

#### URL:   */1/rest/offline/bills*
#### Method: *GET*

#### 请求参数类型: *JSON, 以para=**{}**的方式请求*

示例: para={"key\_a":1,"key\_b":"value\_b"}, 需要对para=后面的部分做URL encode.

#### 请求参数详情:
参数名 | 类型 | 含义 | 描述 | 例子 | 是否必填
----  | ---- | ---- | ---- | ---- | ----
app_id | String | BeeCloud应用APPID | BeeCloud的唯一标识 | 0950c062-5e41-44e3-8f52-f89d8cf2b6eb | 是
timestamp | Long | 签名生成时间 | 时间戳，毫秒数 | 1435890533866 | 是
app_sign | String | 加密签名 | 算法: md5(app\_id+timestamp+app\_secret)，32位16进制格式,不区分大小写 | b927899dda6f9a04afc57f21ddf69d69 | 是
channel| String | 渠道类型 | 根据不同场景选择不同的支付方式 |  WX\_NATIVE、WX_SCAN、ALI\_OFFLINE\_QRCODE、ALI_SCAN(详见支付附注）| 否
bill_no | String | 商户订单号 | 发起支付时填写的订单号 | 201506101035040000001 | 否
start_time | Long | 起始时间 | 毫秒时间戳, 13位 | 1435890530000 | 否
end_time | Long | 结束时间 | 毫秒时间戳, 13位   | 1435890540000 | 否
skip | Integer| 查询起始位置 | 默认为0. 设置为10表示忽略满足条件的前10条数据| 0 | 否
limit| Integer | 查询的条数 | 默认为10，最大为50. 设置为10表示只返回满足条件的10条数据 | 10 | 否

> 注：  
1. bill\_no, start\_time, end\_time等查询条件互相为**<mark>且</mark>**关系  
2. start\_time, end\_time指的是订单生成的时间，而不是订单支付的时间   


#### 返回类型: *JSON: Map*
#### 返回参数:

- 公共返回参数

参数名 | 类型 | 含义 
---- | ---- | ----
result\_code | Integer| 返回码，0为正常
result\_msg  | String | 返回信息， OK为正常
err\_detail  | String | 具体错误信息
count | Integer | 查询订单结果数量
bills | List<Map> | 订单列表

> 公共返回参数取值及含义参见支付公共返回参数部分  

- bills说明，每个Map的key\-value

参数名         | 类型          | 含义 
----          | ----         | ----
bill\_no      | String       | 订单号
total\_fee    | Integer      | 订单金额，单位为分
channel       | String       |  WX\_NATIVE、WX_SCAN、ALI\_OFFLINE\_QRCODE、ALI\_SCAN(详见支付附注）
title         | String       | 订单标题
pay\_result   | Bool         | 订单是否成功
created\_time | Long         | 订单创建时间, 毫秒时间戳, 13位

## Part2. 应用场景简介

### 1.条形码支付
####第一步： 商户（例如超市）中， 用户结账时使用支付宝或者微信的条形码支付，向收银员展示条形码；  
####第二步： 商户收银员使用扫码枪扫描用户的条形码获得授权码auth_code，并连同订单信息 使用下单接口；  
####第三步： 下单接口可能有三种返回状态：  
1. submit\_result = False(测试过程中出现，生产环境一般不会，如出现请重新调用下单）  
2. submit\_result = True && pay\_result = True （对应用户的此次支付无需输入密码情况）代表支付成功。 **<mark>可以结束此次支付**</mark>  
3. submit\_result = True && pay\_result = False （对应用户需要输入密码确认，代表用户还在支付过程。） **<mark>需进行第四步</mark>**  
   
####第四步： 如果下单返回是3状态， 则需要循环调用订单状态查询接口， 直至返回结果是支付成功则**<mark>可以结束此次支付**</mark>；或者超过时间或者重试次数 调用 撤销订单接口


### 2.二维码支付
####第一步： 商户（例如超市）中， 用户结账时使用支付宝或者微信的二维码支付；  
####第二步： 商户收银员整理订单信息 使用下单接口；
####第三步： 利用下单接口返回的qr_code连接生成二维码图片供用户扫描支付
####第四步： 循环调用订单状态查询接口直至返回支付成功结果**<mark>可以结束此次支付**； 或者超时，超出重试次数， 调用 撤销订单接口

## 联系我们
- 如果有什么问题，可以到QQ群 **321545822** BeeCloud开发者大联盟 提问
- 如果发现了bug，欢迎提交[issue](https://github.com/beecloud/beecloud-rest-api/issues)
- 如果有新的需求，欢迎提交[issue](https://github.com/beecloud/beecloud-rest-api/issues)

## 代码许可
The MIT License (MIT).
