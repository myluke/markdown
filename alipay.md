## 商户充值模块

### 1. 查询商户余额

**请求路径：** `/stores/{store_id}/money`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
store_id | int | 商户ID
money | float | 商户余额 元


**返回示例：**

    {
        code: 0,
        message : 'ok',
        result: [{
            store_id: 1,
            money: 100.05
        }]
    }


### 2. 获取充值金额列表

**请求路径：** `/stores/{store_id}/money_list`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
store_id | int | 商户ID
money | float | 可充值金额 元


**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [{
            store_id: 1,
            money_list: [{
                100,
                200,
                500
                }]
        }]
    }


### 3. 获取充值url(APP内部根据返回值发起充值请求)

**请求路径：** `/stores/{store_id}/money_url`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
money  | int | 是 | 充值金额 元
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
store_id | int | 商户ID
url | string | 充值url


**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [{
            store_id: 1,
            order_no: '51pay201506191144340897'
            url: "_input_charset=\"utf-8\"&body=\"安居客订单：CUSR20150619043863\"&it_b_pay=\"30m\"&notify_url=\"http://my.anjuke.com/acenter/alipay/sdk/notify/\"&out_trade_no=\"ac347836314346853822574\"&partner=\"2088501178389921\"&payment_type=\"1\"&seller_id=\"ajkzf@anjukeinc.com\"&service=\"mobile.securitypay.pay\"&show_url=\"m.alipay.com\"&subject=\"支付宝购买\"&total_fee=\"120\"&sign=\"gPqHrl8%2BNUNaqUBUdi9VtxNmOHyGIgPpy380viy%2BO%2F5Pjxp0wii4VAER%2F8VBemm4L8AS32sgAblj8kNtLIx8AKRuZLgkIYgOyyeYULY%2BkU7Ertq%2FRdwAsXG%2FK5eTxxpAXn15P5ed6%2B3zyPFBLS3ueiDHlTjnA3RDY8kAs26CeFY%3D\"&sign_type=\"RSA\""
        }]
    }

### 4. 获取订单充值的结果(APP内部根据接口3返回值 order_no 获取充值结果)

**请求路径：** `/stores/{store_id}/money_result`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
order_no  | string | 是 | 充值订单号
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
store_id | int | 商户ID
order_no | string | 充值订单号
money_result | string | 充值结果 (SUCCESS 或者 NORMAL)


**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [{
            store_id: 1,
            order_no: '51pay201506191144340897'
            money_result: "SUCCESS"
            }]
    }

### 5. 获取资金明细

**请求路径：** `/stores/{store_id}/money_log`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
page_no  | int | 是 | 页码
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 日志ID
fund_id | int | 账户ID
money | float | 金额
money_type | string | 金额类型( + 加钱 - 减钱 )
type | string | 变动类型 (CHARGE 充值+ ORDER_PAY 订单运费支付- ORDER_REFUND 订单运费退还+ WITHDRAW 提现-)
order_no | string | 订单流水号码(充值订单号/货运订单ID/提现订单号)
balance | float | 操作后账户余额
created_at | string | 创建时间

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
                {
                    id: 100,
                    fund_id: 2,
                    money: 3,
                    money_type: '-'
                    type: 'ORDER_PAY',
                    order_no: '1435053149',
                    balance: 1024.2,
                    created_at: '2015-06-19 10:24:00'
                },
                {
                    id: 95,
                    fund_id: 2,
                    money: 100,
                    money_type: '+'
                    type: 'CHARGE',
                    order_no: '51pay201506191000001024',
                    balance: 1124.2,
                    created_at: '2015-06-19 10:00:00'
                },
                {
                    id: 90,
                    fund_id: 2,
                    money: 3,
                    money_type: '-'
                    type: 'ORDER_PAY',
                    order_no: '1435053149',
                    balance: 521.2,
                    created_at: '2015-06-18 18:24:00'
                },
                {
                    id: 89,
                    fund_id: 2,
                    money: 500,
                    money_type: '-'
                    type: 'ORDER_REFUND',
                    order_no: '51refund201506181100001024',
                    balance: 524.2,
                    created_at: '2015-06-18 11:00:00'
                }
        ]
    }
