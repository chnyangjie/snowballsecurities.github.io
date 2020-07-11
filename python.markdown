---
layout: post
title:  "雪盈证券 Open Api Python SDK 接入文档"
categories: overview
---

# 安装

## pip 安装

### 测试仓库

`pip install -i https://test.pypi.org/simple/ snbpy==1.0.0`

### 正式仓库(暂未发布)

`pip install snbpy`

## 源码安装

[源码仓库](https://github.com/snowballsecurities/snbpy)

> `https://github.com/snowballsecurities/snbpy`

`python3 setup.py install`

> 请与客户经理联系获取源码或者访问项目 [GitHub](https://github.com/snowballsecurities/snbpy) 首页获取

# 快速开始

## 代码概要

SDK 主要有以下几个类 

* SnbConfig SDK 的 Client 的基础配置
  > `from snbpy.common.domain.snb_config import SnbConfig`
* TradeInterface API 的 接口类,包含 10 个抽象方法,对应 10 种 API.
* SnbApiClient SDK 的基础框架.
  > `from snbpy.snb_api_client import SnbHttpClient, TradeInterface`

## 配置项

| **key**    | **含义**        | **备注** |
| ---------- | --------------- | -------- |
| account    | U 账户          |          |
| key        | API access Key  |          |
| sign_type  | 加密方式        | 暂不支持 |
| snb_server | API 服务器地址  |          |
| snb_port   | API 服务器端口  |          |
| timeout    | Http 超时时间   |          |
| cache_path | 缓存路径        | 暂不支持 |
| schema     | API Http Schema |          |
| auto_login | 是否自动登陆    | 暂不支持 |

## 调用示例

SDK 提供了Http API 的 requests 实现 `SnbHttpClient(SnbApiClient)`, 如想替换其他 httpClient 可以重写 `_do_execute` 方法, 下面是登陆并查询订单的示例代码. 

```python
from snbpy.common.domain.snb_config import SnbConfig
from snbpy.snb_api_client import SnbHttpClient
if __name__ == '__main__':
    config = SnbConfig()
    config.account = "DU876752"
    config.key = '123456'
    config.sign_type = 'None'
    config.snb_server ='sandbox.snbsecurities.com'
    config.snb_port = '443'
    config.timeout = 1000
    config.schema = 'https'

    client = SnbHttpClient(config)
    client.login()
    order_list_response = client.get_order_list()
```



## 管理

token是一串无序加密的字符串，形如: `pwQxtqj3Bl1q3ThX3I5rRJyUyQxffWX9`，在访问 API 时，用户需携带该 token 作为身份凭证。用户获取 token 的个数没有限制，但服务器仅为每个用户保存 10 个有效 token ，再用户连续申请第 11 个 token 时，第一个 token 开始失效，以此类推。

`SnbHttpClient` 中封装了token相关的方法，login 方法会直接访问API获取一个Auth对象，包含了token和过期时间.

## 方法描述

更多详情请使用 `help(TradeInterface)` 方法获取文档

```python
>>> from snbpy.snb_api_client import TradeInterface
>>> help(TradeInterface)
```

以下是方法列表

| 方法名               | 描述                                   |
| -------------------- | -------------------------------------- |
| login                | 访问API生成一个新token，不会使用缓存   |
| get_token_status     | 查询token，一般用于查询token的过期时间 |
| place_order          | 下单                                   |
| get_order_by_id      | 订单查询，单条                         |
| get_order_list       | 订单查询，批量                         |
| cancel_order         | 撤销订单                               |
| get_position_list    | 持仓查询                               |
| get_balance          | 资产查询                               |
| get_security_detail  | 证券信息查询                           |
| get_transaction_list | 成交查询                               |

# 数据字典
[数据字典](./data-dictionary)
# 更新日志

| 更新日期   | 更新内容                         |
| ---------- | -------------------------------- |
| 2020-06-08 | 初始化更新                       |
| 2020-07-08 | 更新至当前最新安装方式与连接方式 |

