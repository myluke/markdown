驻店模式
===========
## 配送端

### 1. 驻店信息获取

**请求路径：** `/couriers/{user_id}/resident`

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
store_id | int | 商家ID
store_name | string | 商店名
store_mobile | string | 商店注册电话
store_address | string | 商店地址
days | string | 驻店时间(7天/1年23天)
order_count | string | 完成驻店订单(100单/1.5万单)
money | string | 总收入(1000元/1.2万)

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            store_id: 1,
            store_name: '黄焖鸡米饭很好吃哟',
            store_mobile: '13709800011',
            store_address: '东方路1217号',
            days: '100天',
            order_count: '100单',
            money: '1234元',
        }
    }


### 2. 发布订单

**请求路径：** `/couriers/{user_id}/resident_order`

**请求方法：** POST 可批量

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
user_lng | string | 是 | 经度
user_lat | string | 是 | 纬度
order_data | string | 是 | json数组(编辑时传入ID即可)
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 订单ID
receipt_image | string | 订单小票图片
recipient_phone | string | 收货人电话

**输入json示例：**

    [
        {
            receipt_image: 'http://img.51diansong.com/media/images/cb/cbb7ff32d535ae0c4423b2e020a9680ccaf654ae.jpg',
            recipient_phone: '13701816554'
        },
        {
            receipt_image: 'http://img.51diansong.com/media/images/cb/cbb7ff32d535ae0c4423b2e020a9680ccaf654ae.jpg',
            recipient_phone: '13701816555'
        }
    ]


**返回示例：**

    {
        code: 0,
        message: 'ok'
    }


### 3. 订单列表(包含搜索)

**请求路径：** `/couriers/{user_id}/resident_list`

**请求方法：** GET 搜索条件为 在当前分类下根据收货人手机号搜索

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
type | string | 是 | 类型( ENROUTE (配送中) / COMMITED(待完善) / CONFIRMED(待确认) / REJECTED(商家拒绝) )
mobile | string | 否 | 收货人手机号码(查询条件)
page | int | 否 | 非搜索时需要传入页码
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 订单编号
receipt_image | string | 订单小票图片
recipient_phone | string | 收货人电话
recipient_address | string | 收货人地址
amount | float | 货品价值
delivery_freight | float | 配送费
created_at | string | 创建时间
commit_at | string | 配送送达时间
status | string | 订单状态 见注释
allege_result | string | 申述结果（申述信息）
count | int | 该分类下订单数量

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            orders: [{
                id: 1,
                receipt_image: 'http://img.51diansong.com/media/images/cb/cbb7ff32d535ae0c4423b2e020a9680ccaf654ae.jpg',
                recipient_phone: '13701816554',
                created_at: '2015-07-06 11:11:11',
                recipient_address: '',
                amount: 0,
                delivery_freight: 0,
                commit_at: '0000-00-00 00:00:00',
                status: '',
                allege_result: ''
            },
            {
                id: 2,
                receipt_image: 'http://img.51diansong.com/media/images/cb/cbb7ff32d535ae0c4423b2e020a9680ccaf654ae.jpg',
                recipient_phone: '13701816554',
                created_at: '2015-07-06 11:11:12',
                recipient_address: '淞沪路100号',
                amount: 20,
                delivery_freight: 3,
                enroute_at: '2015-07-06 12:00:00',
                status: '',
                allege_result: '申述成功'
            }],
            count: 56
        }
    }


### 4. 删除订单

**请求路径：** `/couriers/{user_id}/{order_id}/resident_delete`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
user_lng | string | 是 | 经度
user_lat | string | 是 | 纬度
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回示例：**

    {
        code: 0,
        message: 'ok'
    }


### 5. 确认送达

**请求路径：** `/couriers/{user_id}/{order_id}/resident_confirm`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
user_lng | string | 是 | 经度
user_lat | string | 是 | 纬度
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回示例：**

    {
        code: 0,
        message: 'ok'
    }


### 6. 完善订单信息

**请求路径：** `/couriers/{user_id}/{order_id}/residnet_commit`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
amount | float | 是 | 物品金额
recipient_address | string | 是 | 收货人地址
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回示例：**

    {
        code: 0,
        message: 'ok'
    }


### 7. 订单申述

**请求路径：** `/couriers/{user_id}/{order_id}/resident_allege`

**请求方法：** POST (申述不填申述原因，已确认)

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名


**返回示例：**

    {
        code: 0,
        message: 'ok'
    }

## 商户端

### 1. 驻店人员信息

**请求路径：** `/stores/{store_id}/resident`

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
courier_id | int | 配送员ID
courier_name | string | 配送员姓名
courier_mobile | string | 配送员手机
courier_number | string | 配送员身份证号
resident_date | string | 配送员入驻日期
finished_order | int | 已完成驻店订单数


**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
            {
                courier_id: 1,
                courier_name: '卢先生'
                courier_mobile: '13701819999',
                courier_number: '412723199011219820',
                resident_date: '2015-07-01',
                finished_order: 50
            },
            {
                courier_id: 2,
                courier_name: '魏先生'
                courier_mobile: '13701819990',
                courier_number: '412723199011245610',
                resident_date: '2015-07-02',
                finished_order: 60
            }
        ]
    }

### 2. 待确认订单汇总列表

**请求路径：** `/stores/{store_id}/resident_sum`

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
courier_id | int | 配送员ID
courier_name | string | 配送员姓名
courier_mobile | string | 配送员手机号码
order_num | string | 配送员总的待确认订单数
order_money_sum | float | 配送员总的待确认订单运费金额

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
            {
                courier_id: 1,
                courier_name: '卢先生'
                courier_mobile: '13701819999',
                order_num: 100,
                order_money_sum: 1000
            },
            {
                courier_id: 2,
                courier_name: '魏先生'
                courier_mobile: '13701819990',
                order_num: 100,
                order_money_sum: 1000
            }
        ]
    }

### 3. 某配送员待确认订单

**请求路径：** `/stores/{store_id}/{courier_id}/resident_order`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
recipient_phone  | string | 否 | 收货人手机号码(搜索)
page  | int | 是 | 页码
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 订单编号
receipt_image | string | 订单小票图片
recipient_phone | string | 收货人电话
recipient_address | string | 收货人地址
amount | float | 货品价值
delivery_freight | float | 配送费
created_at | string | 创建时间
commit_at | string | 配送送达时间
status | string | 订单状态 见注释

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
            {
                id: 1,
                receipt_image: 'http://img.51diansong.com/media/images/cb/cbb7ff32d535ae0c4423b2e020a9680ccaf654ae.jpg',
                recipient_phone: '13701816554',
                created_at: '2015-07-06 11:11:11',
                recipient_address: '东方路1000号',
                amount: 30,
                delivery_freight: 5,
                commit_at: '2015-07-05 12:46:00',
                status: ''
            },
            {
                id: 2,
                receipt_image: 'http://img.51diansong.com/media/images/cb/cbb7ff32d535ae0c4423b2e020a9680ccaf654ae.jpg',
                recipient_phone: '13701816554',
                created_at: '2015-07-06 11:11:12',
                recipient_address: '淞沪路100号',
                amount: 20,
                delivery_freight: 3,
                commit_at: '2015-07-06 12:00:00',
                status: ''
            }
        ]
    }

### 4. 商户确认/拒绝订单(可批量)

**请求路径：** `/stores/{store_id}/handle_order`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
order_id | string | 是 | 订单ID，逗号分隔
type | string | 是 | 操作类型( REJECT / PASS )
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名


**返回示例：**

    {
        code: 0,
        message: 'ok'
    }

### 5. 本店待确认订单总数

**请求路径：** `/stores/{store_id}/resident_count`

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
count | int | 数量

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            count: 16
        }
    }



## 订单 status 说明

参数名 | 状态 | 描述
----- | --- | ---------
ENROUTE | 配送中 | 订单已经发布，还没确认送达
CONFIRMED | 待完善 | 已确认送达，还没有完善订单信息
COMMITED | 待商户确认 | 已经完善订单信息，商户还没有确认
REJECTED | 商户拒绝 | 商户审核完成之后，拒绝订单
FINISHED | 商户通过 | 商户审核完成之后，通过订单
DELETED | 删除 | 配送中/商户拒绝后/申述失败后
