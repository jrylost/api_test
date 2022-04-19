---
title: API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:


includes:


search: true

code_clipboard: true

---

# 简介
API文档


<!--本文文档通过 [Slate](https://github.com/slatedocs/slate)驱动。-->


# 认证

## 获取远程认证报告

此接口返回TEE中的远程认证报告，同时生成通信密钥。
密钥交换算法：ECDH，基于NIST-P256椭圆曲线


> Request:

```json
{
    "publicKey":"0x"
}
```

### HTTP 请求

- POST `/report`
### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |          描述          | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------------- | -------- |
| publicKey | string   | true     | NA     | 客户端基于私钥生成的公钥 | NA       |

> Response:


### 响应数据

|  字段名称  | 数据类型 |            描述             |
| --------- | -------- | --------------------------- |
| status    | string   | 请求处理结果  "ok","error"   |
| \<data\>  | object   |                             |
| report    | string   | 远程认证报告，base64-encoded |
| publicKey | string   | 服务器端基于私钥生成的公钥     |
| \</data\> |          |                             |
