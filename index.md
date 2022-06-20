---
layout: post
title:  "雪盈证券 Open Api 接入文档"
categories: api
---

# 接入准备

## 开户入金

开发者在接入雪盈证券开发平台之前，需要提前开通雪盈账号。账号开通后，您可以自己的账号ID（以后统称为：account id）作为您账号的唯一标识。

### 开户地址

[开户链接](https://www.snowballsecurities.com/xy-account-open/phone-verify)

> `https://www.snowballsecurities.com/xy-account-open/phone-verify`

### 查看账户 ID

登录雪盈证券APP，查找“我的-设置-账号与安全”，即可看到雪盈账号 ID。

### 申请密钥

获取自己的 accountId 后可以在雪盈官网-申请 API，来注册开发者信息，注册后将获得您自己的专属密钥（以后统称为：secret key）作为您登录雪盈开发平台的唯一凭证，请妥善保存。

[注册地址](https://www.snowballsecurities.com)

> `https://www.snowballsecurities.com`

## 环境说明

雪盈证券为 API 开发者提供两套环境，分别是 sit **测试环境**和 prod **生产环境**，现对这两套环境做分别说明。

| **环境** | **环境名称** | **链接方式**                             | **账号获取**     |
| -------- | ------------ | ---------------------------------------- | ---------------- |
| sit      | 测试环境     | `https://sandbox.snbsecurities.com:443` | 联系雪盈客服获得 |
| prod     | 正式环境     | `https://openapi.snbsecurities.com:443` | 参考1.1和1.2     |

>  **PORD**  环境中用户账号、资金均为真实账号、资金，所做操作全部真实有效，请**勿**做测试操作。

# 接入方式

* [HttpApi](/api)
* [PythonSDK](/python)
* [JavaSDK](/java)

# 更新日志

| 更新日期   | 更新内容                         |
| ---------- | -------------------------------- |
| 2020-06-08 | 初始化更新                       |
| 2020-07-08 | 更新至当前最新安装方式与连接方式 |
