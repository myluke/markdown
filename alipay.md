商家 APP
===========

这个是初稿，可能会有微调，请及时联系 QQ：81595945




## 注册登录

### 1. 注册（完成）

**请求路径：** `/stores/register`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
mobile  | string | 是 | 手机号
password  | string | 是 | 密码
captcha  | string | 是 | 验证码
city_id  | int | 是 | 城市ID
city_name  | int | 是 | 城市名称，城市名称和城市ID任选其一
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 用户ID
city_id | int | 城市ID
mobile | string | 手机号
token | string | 已经登录了，可以直接使用
stores | array | 商户列表，第一次注册时没有商户

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            id: 1,
            city_id: 0,
            mobile: '13800138000',
            token: '3|yf7Ke2SyFUcwjCVWWoRDY3fwX1z5detajH2lp2DNjK78ISfqBATFWTxq3CMV',
            stores: [
                {
                    id : 22,
                    city_id : 1,
                    city_name : '上海',
                    name : '',
                    area_id : 0,
                    block_id : 0,
                    telephone : '',
                    address : '',
                    map_lng : 0.00000000000000000,
                    map_lat : 0.00000000000000000,
                    status : 'NORMAL',
                    created_at : '2015-05-27 13:42:50',
                    updated_at : '2015-05-27 13:42:50',
                    user_id : 1,
                    store_id : 22,
                    idcard_number: '',
                    idcard_images: [],
                    idcard_real_name: '',
                    idcard_status: 'NORMAL', // 身份证验证状态，APPROVED：审核通过，APPROVING：审核中
                    business_number: '',
                    business_images: [],
                    business_status: 'NORMAL', // 营业执照验证状态，APPROVED：审核通过，APPROVING：审核中
                    catering_number: '',
                    catering_images: [],
                    catering_status: 'NORMAL', // 餐饮许可证验证状态，APPROVED：审核通过，APPROVING：审核中
                }
            ]
        }
    }

### 2. 登录（完成）

**请求路径：** `/stores/login`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
mobile  | string | 是 | 手机号
password  | string | 是 | 密码
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 用户ID
city_id | int | 城市ID
mobile | string | 手机号
token | string | 用户登录token，后续需要用户登录的地方都需要
stores | array | 商户列表
store_id | int | 商户ID


** 审核status说明，详见：补充说明 2 **

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            id: 1,
            city_id: 0,
            mobile: '13800138000',
            token: '3|yf7Ke2SyFUcwjCVWWoRDY3fwX1z5detajH2lp2DNjK78ISfqBATFWTxq3CMV',
            stores: [
                {
                    id: 3,
                    city_id: 1,
                    city_name : '上海',
                    name: 'test133',
                    area_id: 1,
                    block_id: 2,
                    telephone: '23485053525',
                    address: '东方路1217号',
                    map_lng: 12.34243400000000000,
                    map_lat: 12.43535300000000000,
                    status: 'NORMAL', // 商户状态，(NORMAL：正常；DELETED：已删除，APPROVED：审核通过，不能修改地址)
                    created_at: '2015-05-10 20:57:24',
                    updated_at: '2015-05-26 21:31:33',
                    user_id: 1,
                    store_id: 3,
                    idcard_number: '140830199011268445',
                    idcard_images1: "http:\/\/xxx.com\/asfasd\/jkjk12312.jpg",
                    idcard_images2: "http:\/\/xxx.com\/asfasd\/jkjk12312.jpg",
                    idcard_real_name: '张小二',
                    idcard_status: 'NORMAL', // 身份证验证状态，APPROVED：审核通过，APPROVING：审核中
                    business_number: '23049820394802',
                    business_images: "http:\/\/xxx.com\/asfasd\/jkjk111.jpg",
                    business_status: 'NORMAL', // 营业执照验证状态，APPROVED：审核通过，APPROVING：审核中
                    catering_number: '234234234',
                    catering_images: "http:\/\/xxx.com\/asfasd\/jkjk.jpg",
                    catering_status: 'NORMAL', // 餐饮许可证验证状态，APPROVED：审核通过，APPROVING：审核中
                }
            ]
        }
    }


### 3. 退出登录（完成）

**请求路径：** `/stores/logout`

**请求方法：** POST

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


### 4. 找回密码

**请求路径：** `/stores/resetpwd`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
mobile  | string | 是 | 手机号
captcha  | string | 是 | 验证码
password  | string | 是 | 密码
password_confirmation | string | 是 | 重复输入密码
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
id | int | 用户ID
mobile | string | 手机号

**返回示例：**

    返回结果和登录相同。



## 商家资料

### 1. 获取商户资料（完成）

**请求路径：** `/stores/{store_id}`

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
id | int |  商户ID
city_id | int | 城市ID
name | string | 商户名
area_id | int | 区域ID
block_id | int | 板块ID
telephone | string | 商户电话
address | string | 商户地址
map_lng | float | 商户经度
map_lat | float | 商户纬度
status | string | 商户状态，(NORMAL：正常；DELETED：已删除，APPROVED：审核通过)
created_at | datetime | 创建时间
updated_at | datetime | 更新时间

** 审核status说明，详见：补充说明 2 **

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: {
            id: 1,
            city_id: 11,
            name: '安居客',
            area_id: 111,
            area_name: '区域',
            block_id: 222,
            block_name: '板块',
            telephone: '138636372722',
            address: '东方路1217号',
            map_lng: 23.345345,
            map_lat: 23.345345,
            status: 'NORMAL',
            created_at: '2015-05-07 21:43:00',
            updated_at: '2015-05-07 21:43:00'
        }
    }

### 2. 新增商户（完成）

**请求路径：** `/stores`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
name  | string | 是 | 商户名称
area_id  | int | 是 | 商户区域ID
block_id  | int | 否 | 商户板块ID
address  | string | 是 | 商户地址
map_lng | float | 是 | 商户经度
map_lat | float | 是 | 商户纬度
telephone  | string | 是 | 商户联系方式
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

### 3. 修改商户资料（完成）

**请求路径：** `/stores/{store_id}`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
name  | string | 是 | 商户名称
city_id | int | 使用 area_name 则必填 | 城市ID
area_id  | int | 是 | 商户区域ID
area_name  | int | 是 | 商户区域名称，area_id 和 area_name 必须填写一个，使用此参数，city_id 必填
block_id  | int | 否 | 商户板块ID
block_name  | int | 否 | 商户板块名称，block_id 和 block_name 必须填写一个
address  | string | 是 | 商户地址
map_lng | float | 否 | 商户经度
map_lat | float | 否 | 商户纬度
telephone  | string | 是 | 商户联系方式
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

** 审核status说明，详见：补充说明 2 **

**返回示例：**

    {
        code: 0,
        message: 'ok'
    }

### 4. 获取认证资料（完成）

包含：身份证、营业执照、服务许可

**请求路径：** `/stores/{store_id}/proofs`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
type  | string | 否 | 类型，IDCARD：身份证；BUSINESS：营业执照；CATERING：餐饮许可证
token  | string | 是 | 用户令牌
app_id | string | 是 | app id，系统分配
nonce | int | 是 | 随机正整数
timestamp  | int | 是 | 请求时间戳
signature  | string | 是 | hmac sha1 计算签名

**返回值说明：**

参数名 | 类型 | 示例及描述
----- | --- | ---------
type | string | 类型，IDCARD：身份证；BUSINESS：营业执照；CATERING：餐饮许可证
status | string | 状态，APPROVED：审核通过，APPROVING：审核中
real_name | string | 真实姓名
number | string | 身份证、营业执照、餐饮许可证
images1 | string | 图片，示例：http://xxxx.com/xxx/xxx.jpg
images2 | string | 图片，示例：http://xxxx.com/xxx/xxx.jpg
created_at | datetime | 创建时间
updated_at | datetime | 更新时间

** 审核status说明，详见：补充说明 2 **

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
            {
                type: 'IDCARD',
                status: 'APPROVED',
                data: {
                    real_name: '张小二',
                    number: '37292219839293429',
                    images1: 'http://xxx.com/japsf.jpg',
                    images2: 'http://xxx.com/japsf.jpg'
                }
            },
            {
                type: 'BUSINESS',
                status: 'APPROVED',
                data: {
                    number: '19091223023489',
                    images1: 'http://xxx.com/japsf.jpg'
                }
            },
            {
                  type: 'CATERING',
                  status: 'APPROVED',
                  data: {
                      number: '1290480231501304982',
                      images1: 'http://xxx.com/japsf.jpg'
                  }
              }
        ]
    }



### 5. 上传认证资料（完成）

包含：身份证、营业执照、服务许可

**请求路径：** `/stores/{store_id}/proofs`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
type | string | 是 | 类型，IDCARD：身份证；BUSINESS：营业执照；CATERING：餐饮许可证
real_name | string | 否（type=IDCARD，为必填） | 真实姓名
number | string | 是 | 身份证号、餐饮许可证、营业执照
images1 | string | 是 | 上传的图像，http://xxxx.com/xxx/xxx.jpg
images2 | string | 否 | 上传的图像，http://xxxx.com/xxx/xxx.jpg
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


## 订单

### 1. 我的订单列表（完成）

**请求路径：** `/stores/{store_id}/orders`

**请求方法：** GET

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
page | int | 否 | 第几页，这个页数优先级最高，此字段设置后offset 将无效
offset  | int | 否 | 起始位置，默认：0
limit  | int | 否 | 显示条数，默认：10，如果page有值，这个则代表每页多少条
status  | string | 否 | 状态，请参考status说明，默认：PUBLISHED
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
gratuity_freight | float | 商家出的小费
recipient | string | 收货人
recipient_phone | string | 收货人电话
recipient_address | string | 收货人地址
remark | string | 捎句话
is_pay | int | 是否付款
status | string | 状态
receive_at | datetime | 接单时间
take_off_at | datetime | 取货时间
finish_at | datetime | 完成时间
created_at | datetime | 创建时间
publish_at | datetime | 发布时间
updated_at | datetime | 更新时间

** 订单status说明，详见：补充说明 1 **

**返回示例：**

    {
        code: 0,
        message: 'ok',
        result: [
            {
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
                status: 'DRAFTED',
                receive_at: '2015-05-07 21:43:00',
                take_off_at: '2015-05-07 21:43:00',
                finish_at: '2015-05-07 21:43:00',
                created_at: '2015-05-07 21:43:00',
                updated_at: '2015-05-07 21:43:00'
            },
            {
                id: 2,
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
                status: 'DRAFTED',
                receive_at: '2015-05-07 21:43:00',
                take_off_at: '2015-05-07 21:43:00',
                finish_at: '2015-05-07 21:43:00',
                created_at: '2015-05-07 21:43:00',
                updated_at: '2015-05-07 21:43:00'
            }
        ]
    }


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


### 3. 修改订单（完成）

**请求路径：** `/stores/{store_id}/orders/{order_id}`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
recipient | string | 否 | 收货人
recipient_phone | string | 是 | 收货人电话
recipient_address | string | 是 | 收货人地址
amount | float | 是 | 订单金额
is_pay | int | 是 | 是否付款，已付款：1
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
created_at | datetime | 创建时间
publish_at | datetime | 发布时间
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


### 4. 订单详情（完成）

**请求路径：** `/stores/{store_id}/orders/{order_id}`

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
pay_type | int | 付款方式
status | string | 状态
receive_at | datetime | 接单时间
take_off_at | datetime | 取货时间
finish_at | datetime | 完成时间
publish_at | datetime | 发布时间
created_at | datetime | 创建时间
publish_at | datetime | 发布时间
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


### 5. 发布订单（完成）

**请求路径：** `/stores/{store_id}/orders/{order_id}`

**请求方法：** PUT

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

### 6. 取消订单（完成）

**请求路径：** `/stores/{store_id}/orders/{order_id}`

**请求方法：** DELETE

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


## 填写BD邀请码（完成）

**请求路径：** `/stores/{store_id}/invitation`

**请求方法：** POST

**参数说明：**

参数名 | 类型 | 必选 | 示例及描述
----- | ---- | --- | ---------
code  | string | 是 | BD邀请码
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



## 获取实时配置（完成）

**请求路径：** `/stores/{store_id}/config`

**请求方法：** GET

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
        message: 'ok',
        result: {
            subsidy_freight: 7, // 平台补贴配送费
            free_week: 1 // 是否在免费周，1:免费；0:收费
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
