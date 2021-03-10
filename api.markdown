---
layout: post
title:  "雪盈证券 Open Api 说明"
categories: api
---

# 通讯协议 

## 接口版本

通过 http header Accept 属性声明 `application/vnd.snowx+json; version={version}` 

> 当前支持最低版本为: 1.0，最高版本为:1.0 

### 示例
`Accept:application/vnd.snowx+json; version=1.0`

## 访问权限

所有接口访问建立在会话之上，access_token 表达会话权限，会话有效期为一天。 access_token 可以参数或者 Cookie 的方式传值。

### 示例

```
curl -H"Accept:application/vnd.snowx+json; version=1.0" "https://open.snowballsecurities.com/U123456/order/1?access_token=dc80e1c216155591833ec56cf0c 7f91eb3faa2e6"

curl -H"Accept:application/vnd.snowx+json; version=1.0" -H"Cookie:access_token=dc80e1c216155591833ec56cf0c7f91eb3faa2e6" "https://open.snowballsecurities.com/U123456/order/1"
```

# 数据格式约定

## 响应示例

```json
{
  "result_code": "60000", "msg": null, "result_data": {
    "access_token": "9fk3HoyaD2EgxAC1sPg1dP2QjOwJDPSn",
    "expiry_time": 1591696693584 
  }
}
```

## 字段描述

| 字段名称    | 描述                                                     |
| ----------- | -------------------------------------------------------- |
| result_code | 响应代码，含义参考数据字典                               |
| msg         | 响应信息，当正常响应是为 null                            |
| result_data | 返回数据，以下所有 API 响应数据统一封装在 result_data 中 |

# API 说明 

## 生成 AccessToken

请求地址: `https://{domain}/auth/{account_id}/access-token` 请求方法:POST

是否登陆:否

返回格式:JSON

### 请求参数

| 变量名     | 必填 | 类型   | 描述    | 支持版本 |
| ---------- | ---- | ------ | ------- | -------- |
| account_id | 是   | string | 账户 ID | 1.0      |
| secret_key | 是   | string | 密钥    | 1.0      |

### 返回结果

| 变量名       | 必填 | 类型   | 描述                                                   | 支持版本 |
| ------------ | ---- | ------ | ------------------------------------------------------ | -------- |
| access_token | 是   | string | Access Token                                           | 1.0      |
| expiry_time  | 是   | long   | 过期时间，expiry_time 小于当前时间 毫秒值时 token 失效 | 1.0      |

## 查询 AccessToken

请求地址:https://{domain}/auth/{account_id}/access-token/{access_token} 请求方法:GET

是否登陆:否

返回格式:JSON

### 请求参数

| 变量名       | 必填 | 类型   | 描述         | 支持版本 |
| ------------ | ---- | ------ | ------------ | -------- |
| account_id   | 是   | string | 账户 ID      | 1.0      |
| access_token | 是   | string | Access Token | 1.0      |

### 返回结果

证券信息查询

请求地址:https://{domain}/security/details 请求方法:GET

是否登陆:是

返回格式:JSON

请求参数:

| 变量名       | 必填 | 类型   | 描述         | 支持版本 |
| ------------ | ---- | ------ | ------------ | -------- |
| access_token | 是   | string | Access Token | 1.0      |
| expiry_time  | 是   | long   | 过期时间     | 1.0      |

| 变量名     | 必填 | 类型   | 描述                                                      | 支持版本 |
| ---------- | ---- | ------ | --------------------------------------------------------- | -------- |
| account_id | 是   | string | 账户 ID                                                   | 1.0      |
| symbol     | 是   | string | 证券代码，多个 symbol 用半角逗号分 隔，单次最多查询 20 个 | 1.0      |

返回结果:

| 变量名    | 必填 | 类型   | 描述             | 支持版本 |
| --------- | ---- | ------ | ---------------- | -------- |
| symbol    | 是   | string | 证券代码         | 1.0      |
| tick_size | 是   | string | 最小报价单位     | 1.0      |
| lot_size  | 是   | string | 最小委托数量单位 | 1.0      |

## 下单

请求地址:https://{domain}/order/{id} 请求方法:POST

是否登陆:是

返回格式:JSON

请求参数:

| 变量名        | 必填 | 类型    | 描述                                     | 支持版本 |
| ------------- | ---- | ------- | ---------------------------------------- | -------- |
| id            | 是   | string  | 订单 ID，数字字母组合，1-20 位           | 1.0      |
| account_id    | 是   | string  | 账户 ID                                  | 1.0      |
| security_type | 是   | enum    | 证券类型，见:数据字典                    | 1.0      |
| symbol        | 是   | string  | 证券代码                                 | 1.0      |
| exchange      | 是   | string  | 市场                                     | 1.0      |
| order_type    | 是   | enum    | 订单类型                                 | 1.0      |
| side          | 是   | enum    | 买卖方向，见:数据字典                    | 1.0      |
| currency      | 是   | enum    | 币种，见:数据字典                        | 1.0      |
| quantity      | 是   | int     | 委托数量                                 | 1.0      |
| price         | 否   | double  | 委托价格，不传默认为 0                   | 1.0      |
| tif           | 否   | enum    | 订单有效期，不传默认为 DAY，见: 数据字典 | 1.0      |
| rth           | 否   | boolean | 仅限盘中交易，不传默认为 false           | 1.0      |

返回结果:

| 变量名 | 必填 | 类型   | 描述                      | 支持版本 |
| ------ | ---- | ------ | ------------------------- | -------- |
| id     | 是   | string | 订单唯一标识              | 1.0      |
| memo   | 否   | string | 提示信息                  | 1.0      |
| status | 是   | enum   | 当前订单状态，见:数据字典 | 1.0      |

## 订单查询(单条) 

请求地址:https://{domain}/order/{id}

请求方法:GET

是否登陆:是

返回格式:JSON

请求参数:

| 变量名     | 必填 | 类型   | 描述    | 支持版本 |
| ---------- | ---- | ------ | ------- | -------- |
| account_id | 是   | string | 账户 ID | 1.0      |
| id         | 是   | string | 订单 ID | 1.0      |

返回结果:

| 变量名         | 必填 | 类型    | 描述                    | 支持版本 |
| -------------- | ---- | ------- | ----------------------- | -------- |
|id             | 是   | string  | 订单 ID                 | 1.0      |
|account_id     | 是   | string  | 账户 ID                 | 1.0      |
|security_type  | 是   | enum    | 证券类型，见:数据字典   | 1.0      |
|symbol         | 是   | string  | 证券代码                | 1.0      |
|exchange       | 是   | string  | 市场                    | 1.0      |
|order_type     | 是   | enum    | 订单类型，见:数据字典   | 1.0      |
|side           | 是   | enum    | 买卖方向，见:数据字典   | 1.0      |
|currency       | 是   | enum    | 币种，见:数据字典       | 1.0      |
|quantity       | 是   | int     | 委托数量                | 1.0      |
|price          | 否   | double  | 委托价格                | 1.0      |
|tif            | 否   | enum    | 订单有效期，见:数据字典 | 1.0      |
|rth            | 否   | boolean | 仅限盘中交易            | 1.0      |
|status         | 是   | enum    | 订单状态，见:数据字典   | 1.0      |
|filled_quantity | 否   | enum    | 已成交数量              | 1.0      |
|order_time | 否   | long | 下单时间 | 1.0  |

## 订单查询(批量)

请求地址:https://{domain}/order 请求方法:GET

是否登陆:是

返回格式:JSON

请求参数:

| 变量名        | 必填 | 类型   | 描述                                                         | 支持版本 |
| ------------- | ---- | ------ | ------------------------------------------------------------ | -------- |
| account_id    | 是   | string | 账户 ID                                                      | 1.0      |
| page          | 否   | int    | 页码，从 1 开始计数，默认值:1                                | 1.0      |
| size          | 否   | int    | 每页条数，最大 500，默认值:10                                | 1.0      |
| status        | 否   | enum   | 订单状态，取值范围:"REPORTED", "CONCLUDED", "WITHDRAWED", "ALL" |          |
| security_type | 否   | enum   | 证券类型，多个状态以英文半角,拼接                            |          |

返回结果:

| 变量名     | 必填 | 类型   | 描述         | 支持版本 |
| ---------- | ---- | ------ | ------------ | -------- |
| page       | 是   | int    | 页码         | 1.0      |
| size       | 是   | int    | 每页显示条数 | 1.0      |
| count      | 是   | long   | 总条数       | 1.0      |
| id         | 是   | string | 订单 ID      | 1.0      |
| account_id | 是   | string | 账户 ID      | 1.0      |
| security_type    | 是   | enum    | 证券类型     | 1.0  |
| symbol           | 是   | string  | 证券代码     | 1.0  |
| exchange         | 是   | string  | 市场         | 1.0  |
| order_type       | 是   | enum    | 订单类型     | 1.0  |
| side             | 是   | enum    | 买卖方向     | 1.0  |
| currency         | 是   | enum    | 币种         | 1.0  |
| quantity         | 是   | int     | 委托数量     | 1.0  |
| price            | 否   | double  | 委托价格     | 1.0  |
| tif              | 否   | enum    | 订单有效期   | 1.0  |
| rth              | 否   | boolean | 仅限盘中交易 | 1.0  |
| status           | 是   | enum    | 订单状态     | 1.0  |
| filled_quantity | 是   | enum    | 已成交数量   | 1.0  |
| order_time       | 是   | long    | 下单时间     | 1.0  |

## 成交查询

请求地址:https://{domain}/trade

请求方法:GET

是否登陆:是

返回格式:JSON

请求参数:

| 变量名     | 必填 | 类型   | 描述                          | 支持版本 |
| ---------- | ---- | ------ | ----------------------------- | -------- |
| account_id | 是   | string | 账户 ID                       | 1.0      |
| page       | 否   | int    | 页码，从 1 开始计数，默认值:1 | 1.0      |
| size            | 否   | int  | 每页条数，最大 500，默认值:10 | 1.0  |
| --------------- | ---- | ---- | ----------------------------- | ---- |
| side            | 否   | enum | 买卖方向                      | 1.0  |
| order_time_min | 否   | int  | 下单时间左区间，时间戳(毫秒)    | 1.0  |
| order_time_max | 否   | int  | 下单时间右区间，时间戳(毫秒)    | 1.0  |

返回结果:

| 变量名        | 必填 | 类型    | 描述         | 支持版本 |
| ------------- | ---- | ------- | ------------ | -------- |
| page          | 是   | int     | 页码         | 1.0      |
| size          | 是   | int     | 每页显示条数 | 1.0      |
| count         | 是   | long    | 总条数       | 1.0      |
| id            | 是   | string  | 订单 ID      | 1.0      |
| account_id    | 是   | string  | 账户 ID      | 1.0      |
| security_type | 是   | string  | 证券类型     | 1.0      |
| symbol        | 是   | string  | 证券代码     | 1.0      |
| exchange      | 是   | string  | 市场         | 1.0      |
| order_type    | 是   | enum    | 订单类型     | 1.0      |
| side          | 是   | enum    | 买卖方向     | 1.0      |
| currency      | 是   | enum    | 币种         | 1.0      |
| quantity      | 是   | int     | 成交数量     | 1.0      |
| price         | 否   | double  | 成交价格     | 1.0      |
| tif           | 否   | enum    | 订单有效期   | 1.0      |
| rth           | 否   | boolean | 仅限盘中交易 | 1.0      |
| status     | 是   | enum | 订单状态 | 1.0  |
| trade_time | 是   | long | 成交时间 | 1.0  |
| order_time | 是   | long | 下单时间 | 1.0  |

## 撤单

请求地址:https://{domain}/order/{original_id} 请求方法:DELETE

是否登陆:是

返回格式:JSON

请求参数:

| 变量名      | 必填 | 类型   | 描述        | 支持版本 |
| ----------- | ---- | ------ | ----------- | -------- |
| account_id  | 是   | string | 账户 ID     | 1.0      |
| original_id | 是   | string | 原始订单 ID | 1.0      |
| id          | 是   | string | 新订单 ID   | 1.0      |

返回结果:

## 持仓

请求地址:https://{domain}/position 请求方法:GET

是否登陆:是

返回格式:JSON

请求参数:

| 变量名 | 必填 | 类型   | 描述       | 支持版本 |
| ------ | ---- | ------ | ---------- | -------- |
| id     | 是   | string | 新订单 ID  | 1.0      |
| status | 是   | enum   | 新订单状态 | 1.0      |

| 变量名        | 必填 | 类型   | 描述                                | 支持版本 |
| ------------- | ---- | ------ | ----------------------------------- | -------- |
| account_id    | 是   | string | 账户 ID                             | 1.0      |
| security_type | 否   | enum   | 证券类型，多个值用英文半角逗号拼 接 | 1.0      |

返回结果:

| 变量名        | 必填 | 类型   | 描述       | 支持版本 |
| ------------- | ---- | ------ | ---------- | -------- |
| account_id    | 是   | string | 账户 ID    | 1.0      |
| security_type | 是   | string | 证券类型   | 1.0      |
| symbol        | 是   | string | 证券代码   | 1.0      |
| exchange      | 是   | string | 市场       | 1.0      |
| position      | 是   | int    | 持仓数量   | 1.0      |
| average_price | 是   | double | 持仓均价   | 1.0      |
| market_price  | 是   | double | 市场价     | 1.0      |
| realized_pnl  | 是   | double | 已实现盈亏 | 1.0      |

## 资产

请求地址:https://{domain}/funds 请求方法:GET

是否登陆:是

返回格式:JSON

请求参数:

| 变量名     | 必填 | 类型   | 描述    | 支持版本 |
| ---------- | ---- | ------ | ------- | -------- |
| account_id | 是   | string | 账户 ID | 1.0      |

返回结果:

| 变量名                                | 必填 | 类型   | 描述         | 支持版本 |
| ------------------------------------- | ---- | ------ | ------------ | -------- |
| net_liquidation_value                | 是   | double | 净资产       | 1.0      |
| equity_with_loan_value               | 是   | double | 总资产       | 1.0      |
| previous_day_equity_with_loan_value | 是   | double | 昨日总资产   | 1.0      |
| securities_gross_position_value     | 是   | double | 证券总价值   | 1.0      |
| sma                                   | 是   | double |              | 1.0      |
| cash                                  | 是   | double | 账户金额     | 1.0      |
| current_available_funds              | 是   | double | 可用资金     | 1.0      |
| current_excess_liquidity             | 是   | double | 剩余流动性   | 1.0      |
| leverage                              | 是   | double | 杠杆，GPV/NL | 1.0      |
| current_initial_margin               | 是   | double | 初始保证金   | 1.0      |
| current_maintenance_margin          | 是   | double | 维持保证金   | 1.0      |
| currency                              | 是   | enum   | 币种         | 1.0      |
