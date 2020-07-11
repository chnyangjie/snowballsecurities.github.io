---
layout: post
title:  "雪盈证券 Open Api 数据字典"
categories: api
---

# 雪盈证券 Open API 数据字典

## Currency

| 名称 | 描述         |
| ---- | ------------ |
| BASE | 基础货币     |
| USX  |              |
| CNY  | 人民币       |
| USD  | 美元         |
| SEK  | 瑞典克朗     |
| SGD  | 新加坡币     |
| TRY  | 土耳其里拉   |
| ZAR  | 南非兰特     |
| JPY  | 日元         |
| AUD  | 澳元         |
| CAD  | 加币         |
| CHF  | 瑞士法郎     |
| CNH  | 人民币       |
| HKD  | 港币         |
| NZD  | 新西兰币     |
| CZK  | 捷克克朗     |
| DKK  | 丹麦克朗     |
| HUF  | 匈牙利福林   |
| NOK  | 挪威克朗     |
| PLN  | 波兰兹罗提   |
| EUR  | 欧元         |
| GBP  | 英镑         |
| ILS  | 以色列谢克尔 |
| MXN  | 墨西哥比索   |
| RUB  | 卢布         |
| KRW  | 韩元         |

## SecurityType

| 名称  | 描述               |
| ----- | ------------------ |
| STK   | 股票               |
| CS    | 股票               |
| FUT   | 期货               |
| OPT   | 期权               |
| FOP   | 期货期权           |
| WAR   | 涡轮               |
| MLEG  | 不支持             |
| CASH  | 外汇               |
| CFD   | 差价合约           |
| CMDTY | 大宗商品           |
| FUND  | 基金               |
| IOPT  | 牛熊证             |
| BOND  | 债券               |
| ALL   | 全部类型(查询条件) |

## OderType

| 名称              | 描述       |
| ----------------- | ---------- |
| LIMIT             | 限价单     |
| MARKET            | 市价单     |
| AT                | 不支持     |
| ATL               | 不支持     |
| SSL               | 不支持     |
| SEL               | 不支持     |
| STOP              | 止损单     |
| STOP_LIMIT        | 限价止损单 |
| TRAIL             | 追踪单     |
| TRAIL_LIMIT       | 限价追踪单 |
| LIMIT_ON_OPENING  | 开市限价单 |
| MARKET_ON_OPENING | 开市市价单 |
| LIMIT_ON_CLOSE    | 闭市限价单 |
| MARKET_ON_CLOSE   | 闭市市价单 |

## OrderSide

| 名称 | 描述 |
| ---- | ---- |
| BUY  | 买入 |
| SELL | 卖出 |

## OrderStatus

| 名称               | 描述     |
| ------------------ | -------- |
| NO_REPORT          | 未报     |
| WAIT_REPORT        | 待报     |
| REPORTED           | 已报     |
| WAIT_WITHDRAW      | 已报待撤 |
| PART_WAIT_WITHDRAW | 部成待撤 |
| PART_WITHDRAW      | 部撤     |
| WITHDRAWED         | 已撤     |
| PART_CONCLUDED     | 部成     |
| CONCLUDED          | 已成     |
| INVALID            | 废单     |

## TimeInForce

| 名称 | 描述       |
| ---- | ---------- |
| DAY  | 当日有效   |
| GTC  | 撤单前有效 |

# 更新日志

| 更新日期   | 更新内容                         |
| ---------- | -------------------------------- |
| 2020-06-08 | 初始化更新                       |
