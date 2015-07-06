商家 APP 被修改和新增的API列表
===========
## 订单

### 2. 创建订单（完成）

**请求路径：** `/stores/{store_id}/orders`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
recipient | string | 否 | 收货人
recipient_phone | string | 是 | 收货人电话
recipient_address | string | 是 | 收货人地址
amount | float | 是 | 订单金额
is_pay | int | 是 | 是否付款，0：未付款；1：已付款
pay_type | int | 是 | 付款方式，0：线下付款；1：在线付款
remark | string | 否 | 捎句话
delivery_freight | float | 否 | 商家出的配送费
gratuity_freight | float | 否 | 商家给的小费
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 订单ID
city_id | int | 城市ID
store_id | int | 商家ID
courier_id | int | 接单人ID
courier_phone | string | 接单人电话
courier_name | string | 接单人名字
order_lng | float | 订单经纬度
order_lat | float | 订单经纬度
amount | float | 订单金额
delivery_freight | float | 商家出的配送费
gratuity_freight | float | 商家给的小费
recipient | string | 收货人
recipient_phone | string | 收货人电话
recipient_address | string | 收货人地址
remark | string | 捎句话
is_pay | int | 是否付款
pay_type | int | 是 | 付款方式
status | string | 状态
receive_at | datetime | 接单时间
take_off_at | datetime | 取货时间
finish_at | datetime | 完成时间
publish_at | datetime | 发布时间
created_at | datetime | 创建时间
updated_at | datetime | 更新时间

** 订单status说明，详见：补充说明 1 **

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            id: 1,
            city_id: 1,
            store_id: 1,
            courier_id: 0,
            courier_phone: '',
            order_lng: 25.234234,
            order_lat: 25.234234,
            amount: 399.00,
            delivery_freight: 5.00,
            gratuity_freight: 0.00,
            recipient: '',
            recipient_phone: '13800138000',
            recipient_address: '东方路1217号13F',
            remark: '路上带包卫生巾，我要当鞋垫。',
            is_pay: 0,
            pay_type: 0,
            status: 'DRAFTED',
            receive_at: '2015-05-07 21:43:00',
            take_off_at: '2015-05-07 21:43:00',
            finish_at: '2015-05-07 21:43:00',
            created_at: '2015-05-07 21:43:00',
            updated_at: '2015-05-07 21:43:00'
        }
    }


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
        message: 'ok',
        result: {
            store_id: 1,
            money: 100.05
        }
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
        result: {
            store_id: 1,
            money_list: {
                100,
                200,
                500
                }
        }
    }


### 3. 获取充值url(APP内部根据返回值发起充值请求)

**请求路径：** `/stores/{store_id}/money_url`

**请求方法：** GET

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
        result: {
            store_id: 1,
            order_no: '51pay201506191144340897'
            url: "_input_charset=\"utf-8\"&body=\"安居客订单：CUSR20150619043863\"&it_b_pay=\"30m\"&notify_url=\"http://my.anjuke.com/acenter/alipay/sdk/notify/\"&out_trade_no=\"ac347836314346853822574\"&partner=\"2088501178389921\"&payment_type=\"1\"&seller_id=\"ajkzf@anjukeinc.com\"&service=\"mobile.securitypay.pay\"&show_url=\"m.alipay.com\"&subject=\"支付宝购买\"&total_fee=\"120\"&sign=\"gPqHrl8%2BNUNaqUBUdi9VtxNmOHyGIgPpy380viy%2BO%2F5Pjxp0wii4VAER%2F8VBemm4L8AS32sgAblj8kNtLIx8AKRuZLgkIYgOyyeYULY%2BkU7Ertq%2FRdwAsXG%2FK5eTxxpAXn15P5ed6%2B3zyPFBLS3ueiDHlTjnA3RDY8kAs26CeFY%3D\"&sign_type=\"RSA\""
        }
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
        result: {
            store_id: 1,
            order_no: '51pay201506191144340897'
            money_result: "SUCCESS"
            }
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


## 补充说明

### 1. 订单 status 说明

参数名 | 状态 | 描述
----- | --- | ---------
DRAFTED | 待发布 | 草稿种，还没发布
PUBLISHED | 待接单 | 已经发布，只有这种状态的可以抢
PICKUP | 待取货 | 已经接单，还没有取货
ENROUTE | 配送中 | 已经取货，正在配送
FINISHED | 已完成 | 客户已确认，配送完成
DELETED | 已删除 | 已经删除


### 2 审核 status 说明

当某个状态没有返回数据的时候，说明这个数据还没有提交

例如： 取不到身份验证状态，说明用户还没有提交

参数名 | 状态 | 描述
----- | --- | ---------
NORMAL | 初始状态 | 初始状态，默认状态
PENDING | 待审核 | 用户已经提交，等待工作人员审核
APPROVED | 审核通过 | 已经审核通过
APPROVING | 审核中 | 审核中，复核种，都是一个意思
REJECTED | 审核不通过 | 被拒绝了，没有审核通过
DELETED | 已删除 | 已经删除
