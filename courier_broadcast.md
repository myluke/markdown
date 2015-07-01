快递员APP 顶部消息通知 API 说明
===========
### 1. 获取顶部消息

**请求路径：** `/courier/{user_id}/broadcast`

**请求方法：** GET

**特殊说明：** `返回最多10条消息，按照倒序取最新的`

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
limit | int | 是 | 返回的消息数量
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | ID
info | string | 消息内容

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
                {
                    id: 1,
                    info: '下雨回家收衣服啦'
                },
                {
                    id: 2,
                    info: '快看地上谁的100快钱'
                },
                {
                    id: 3,
                    info: '今天下雨了补贴100块'
                }
        ]
    }
