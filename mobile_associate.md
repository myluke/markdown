商户手机号码联想功能 API 说明
===========
### 1. 手机号码联想

**请求路径：** `/stores/{store_id}/associate`

**请求方法：** GET

**特殊说明：** `返回值最多7个手机号码`

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
query | string | 是 | 最少手机号码前7位(长度>=7)
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 历史订单ID
mobile | string | 完整的手机号码
address | string | 地址(同一手机号码)

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
                {
                    id: 101,
                    mobile: '13701816550',
                    address: [
                        "军工路516号",
                        "军工路512号"
                    ]
                },
                {
                    id: 102,
                    mobile: '13701816551',
                    address: [
                        '翔殷路1300号'
                    ]
                },
                {
                    id: 103,
                    mobile: '13701816552',
                    address: [
                        '翔殷路1500号'
                    ]
                }
        ]
    }
