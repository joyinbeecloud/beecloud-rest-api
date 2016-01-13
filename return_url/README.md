## BeeCloud return_url详解
1. 只列举重要的参数
2. return_url应只做结果展示
3. 业务处理应使用webhook

## return_url返回页面所带的参数 

## 1. 支付宝
key |  说明  | 
---- | ----
subject| 标题 
out\_trade_no| 订单号
buyer_email| 买家账户 
seller_email| 卖家账户 
trade_no| 支付宝内部订单号 
total_fee | 支付金额，单位为元
trade_status| "TRADE\_FINISHED" 和 "TRADE_SUCCESS"代表成功 

## 2. 银联
key |  说明  | 
---- | ----
subject| 标题 
orderId| 订单号
txnAmt | 支付金额，单位为分
respCode| "00" 代表成功 


