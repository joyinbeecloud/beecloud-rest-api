#BeeCloud 错误码对应详细信息
##返回码简介

参数 | 含义
----|----
result_code | 结果码
result_msg  | 结果信息描述
err_detail  | 详细错误信息

##错误码对应详细信息表

result_code | result_msg | 含义
----        |  --------   | -------
0           | OK                     | 调用成功
1           | APP\_INVALID           | app_id错误，或者签名错误，或者timestamp过期
2           | PAY\_FACTOR_NOT\_SET   | 支付要素在后台没有设置， 参考err_detail给的具体错误信息
3           | CHANNEL\_INVALID       | channel参数不合法， 参考err_detail给的具体错误信息  
4           | MISS\_PARAM            | 缺少必填参数， 参考err_detail给的具体错误信息
5           | PARAM\_INVALID         | 参数不合法， 参考err_detail给的具体错误信息
6           | CERT\_FILE\_ERROR      | 证书错误， 参考err_detail给的具体错误信息
7           | CHANNEL\_ERROR         | 渠道内部错误， 代表经过了BeeCloud的参数检查但是提交到渠道时发生错误，可以参考err_detail的具体信息
8           | NO\_SUCH_BILL             | 没有该订单，一般发生在退款时没有找到bill_no对应的订单号
9           | BILL\_UNSUCCESS            | 该订单没有支付成功，一般发生在退款时，这笔订单并没有支付成功
10          | REFUND\_EXCEED\_TIME       | 已超过可退款时间，一般发生在退款时，这笔订单已经超过可退款时间
11          | ALREADY\_REFUNDING         | 该订单已有正在处理中的退款， 一般发生在退款时，这笔订单已经有正在提交的退款了
12          | REFUND\_AMOUNT\_TOO\_LARGE | 提交的退款金额超出可退额度，一般发生在退款时，这笔订单的退款总额超出了订单总金额
13          | NO\_SUCH\_REFUND           | 没有该退款记录，一般发生在退款状态查询时，传入的退款单号找不到退款记录
14          | RUN\_TIME\_ERROR        | 运行时未知错误
15          | NETWORK_ERROR           | 网络异常错误
16          | PREREFUND\_DUPLICATE    | 预退款记录重复
17          | BILL\_NO\_DUPLICATE     | 订单号重复
