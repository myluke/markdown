配送员 APP 新增的API列表
===========
### 1. 补贴订单列表

**请求路径：** `/couriers/{user_id}/subsidy`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
page_no | int | 是 | 页码,从1开始
limit | int | 否 | 每页显示条数,不传默认10,最大30
type | string | 是 | 列表类型(`SUCCESS -> 成功 FAIL -> 失败 PENDING -> 放款审核 `)
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 订单ID
subsidy | float | 补贴金额
finish_at | datetime | 完成时间
finish_day | date | 完成日期
reason | string | 失败原因

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
                {
                    id: 101,
                    subsidy: 7.0,
                    finish_day: '2015-06-19',
                    finish_at: '2015-06-19 10:24:00',
                    reason: '小票不清晰'
                },
                {
                    id: 100,
                    subsidy: 7.0,
                    finish_day: '2015-06-19',
                    finish_at: '2015-06-19 10:24:00',
                    reason: '商家投诉成立'
                },
                {
                    id: 102,
                    subsidy: 7.0,
                    finish_day: '2015-06-19',
                    finish_at: '2015-06-19 10:24:00',
                    reason: ''
                }
        ]
    }
