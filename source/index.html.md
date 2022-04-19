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

此接口返回TEE中的远程认证报告，同时交换通信密钥。
密钥交换算法：ECDH，基于NIST-P256椭圆曲线
具体方法：服务端和客户端基于双方的公钥和自己的私钥生成共享的通信密钥。
具体参考[ Diffie-Hellman Group Exchange for
            the Secure Shell (SSH) Transport Layer Protocol](https://www.ietf.org/rfc/rfc4419.txt)

> Request:

```json
{
    "publicKey":"0x5f7dfa28bf72dc3479c7c2d40096c93e68b075641c8600d0d84a0393610652fb"
}
```

### HTTP 请求

- POST `/report`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |          描述          | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------------- | -------- |
| publicKey | string   | true     | NA     | 客户端基于私钥生成的公钥 | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "report":"eX26q+uozgOQvTmTkaUj1ABv7oIdZjMQ1h4p51fi7Di7rGD+tlZG9SNfkRAVujoOohkg8laRsTAtQiSChPj4/VfrHMDVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLFUAJUfjsAm+ZYvW6hnvcRpjdq4hqrp74E5+fuvS35O1Mxni9RRt9zkcBDE2b5QS0GCFTHw+zSrnF9AU8RxfzIhEpEu9u/7iw2d8eqEMZotf5CnR3ypt7mlErkz8nMAnUG6CSjzpT78LnrPZALp4L3LuuuPhmstAJB+MK2dxD8J0wEG8qc8ZtEHLd3DfsdKla6UdvSKDH70mXdXJKLNjtGwOUY/rPzheAwBAcXoD60o42RrmMQCOw2z99zZHGOe2GIp3jypF7XkUW3tXsgwBMbjcnP0+yAoGy0tzC7oQushNfMYhfw/EKVW1PvoD58OKTaGotc9/tDVrE1XcJAMA4/iNbDWlngscX/d3PHYwSLcdP51cb+nJKJ4tACbQNZCrwPrLKNleiQ6/84mUUPNOzXzR1ShC5VTeZl9SyIZqOfxSk81MkzAD0PnqWbVHhdjJUYjzy/S0cD/cVQdbzkHfHDKgQIMhBv0HxU24o5In+r/PbLd3MlQMjV/toYPylk8=",
        "publicKey":"0x5f7dfa28bf72dc3479c7c2d40096c93e68b075641c8600d0d84a0393610652fb",
    }
}
```

### 响应数据

|  字段名称  | 数据类型 |            描述             |
| --------- | -------- | --------------------------- |
| status    | string   | 请求处理结果  "ok","error"   |
| \<data\>  | object   |                             |
| report    | string   | 远程认证报告，base64-encoded |
| publicKey | string   | 服务器端基于私钥生成的公钥     |
| \</data\> |          |                             |

# 账户

## 简介

账户相关接口提供了账户查询以及资产交易等功能。

## 账户信息

查询当前账户地址 `address` 及其相关信息


> Request:

```json
{
    "data":{
        "address":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/account/accounts`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |       描述       | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------- | -------- |
| \<data\>  | object   | true     | NA     |                  | NA       |
| address   | string   | true     | NA     | 账户地址          | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                  | NA       |
| signature | string   | true     | NA     | 账户签名          | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "address":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "balance":10000000000,
        "nonce":10,
        "count":10,
    },
    "ts":1650333610000,
}
```

### 响应数据

|  字段名称  | 数据类型 |            描述            |
| --------- | -------- | ------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                           |
| address   | string   | 账户地址                   |
| balance   | int      | 账户余额                   |
| nonce     | int      | 账户交易次数               |
| count     | int      | 账户中文件数量              |
| \</data\> |          |                           |
| ts        | int      | 时间戳                     |