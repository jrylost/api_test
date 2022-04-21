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

## 密码学

### 哈希算法

本文档中哈希算法采用Keccak256，与以太坊采用的Keccak算法相同，参考文档：[The Keccak SHA-3 submission](https://keccak.team/files/Keccak-submission-3.pdf)

对空字串的16进制哈希结果如下 **（这是我们采用的！！！）**：

`Keccak256() = c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470`

值得注意的是，由于以太坊采用的Keccak哈希算法并非NIST-SHA3所采纳的Keccak最终版本，两者有细微差别，因此我们需要注意使用的哈希算法是否为[以太坊Keccak](https://github.com/ethereum/EIPs/issues/59)。同时根据NIST提供的[SHA3算法](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.202.pdf)的文档中，对空字串的哈希结果如下 **（这不是我们采用的！！！）**：

`SHA3-256() = a7ffc6f8bf1ed76651c14756a061d662f580ff4de43b49fa82d80a4b80f8434a`

两者区别的详情请参考：[Stackoverflow上的回答](https://ethereum.stackexchange.com/questions/550/which-cryptographic-hash-function-does-ethereum-use#:~:text=Ethereum%20uses%20KECCAK-256.%20It%20should%20be%20noted%20that,%28M%29%20%3D%20KECCAK%20%5B512%5D%20%28M%20%7C%7C%2001%2C%20256%29.)

### 签名

### 非对称加密

### 密钥交换

密钥交换算法：ECDH

椭圆曲线：secp256k1椭圆曲线，参考文档：[SEC 2: Recommended Elliptic Curve Domain Parameters](https://www.secg.org/sec2-v2.pdf)，Chapter 2.4.1

具体方法：服务端和客户端基于双方的公钥和自己的私钥生成共享的通信密钥。

具体步骤：

* 若服务端私钥为a，客户端私钥为a，互相共享公钥$g^a$，$g^b$；
* 双方计算得到$g^{ab}$，取得$g^{ab}$的$x$坐标为共享秘密(Shared Secret)；
* 将$x$转化为二进制表示并作哈希，得到密钥，Shared Private Key = Keccak256(x)；
* Shared Private Key为服务端和客户端共享密钥。

参考文档：[Elliptic Curve Groups modulo a Prime (ECP Groups) for IKE and IKEv2](https://www.rfc-editor.org/rfc/rfc5903.html)的Section 9

### 对称加密

<!--本文文档通过 [Slate](https://github.com/slatedocs/slate)驱动。-->

# 认证

## 获取远程认证报告

此接口返回TEE中的远程认证报告，同时交换通信密钥。


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
        "publicKey":"0x40b2132379c2a59096162e5e7c5f692720865a6ce105e90798981892fda7cbdb",
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

- POST `/account/info`


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
| nonce     | int      | 账户操作次数               |
| count     | int      | 账户拥有文件数量            |
| \</data\> |          |                           |
| ts        | int      | 时间戳                     |

## 转账

对任意地址 `address` 进行转账


> Request:

```json
{
    "data":{
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "to":"0x1c1643c57b0ec7542498f693f201da4ccbb9991289e45631436bad366fdc111d",
        "nonce":15,
        "value":100000000,
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/account/transfer`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |       描述       | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------- | -------- |
| \<data\>  | object   | true     | NA     |                  | NA       |
| from      | string   | true     | NA     | 转出账户地址      | NA       |
| to        | string   | true     | NA     | 转入账户地址      | NA       |
| nonce     | int      | true     | NA     | 账户操作次数      | NA       |
| value     | int      | true     | NA     | 转账金额          | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                  | NA       |
| signature | string   | true     | NA     | 转出账户签名      | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "transaction":{
            "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
            "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
            "to": "0x1c1643c57b0ec7542498f693f201da4ccbb9991289e45631436bad366fdc111d",
            "nonce": 15,
            "value": 100000000,
        }
    },
    "ts":1650333610000,
}
```

### 响应数据

|     字段名称      | 数据类型 |            描述            |
| ---------------- | -------- | ------------------------- |
| status           | string   | 请求处理结果  "ok","error" |
| \<data\>         | object   |                           |
| \<transaction\>  | object   |                           |
| hash             | string   | 交易哈希                   |
| from             | string   | 转出账户地址               |
| to               | string   | 转入账户地址               |
| nonce            | int      | 账户操作次数               |
| value            | int      | 转账金额                   |
| \</transaction\> |          |                           |
| \</data\>        |          |                           |
| ts               | int      | UTC时间戳（毫秒）           |













# 文件

## 简介
文件提供文件存储以及KV键值对存储相关接口信息

<aside class="notice">文件存储和KV存储需要占用账户操作nonce，文件和KV读取不占用操作nonce</aside>

## 文件存储

将文件加密存储到地址`address`下


> Request:

```json
{
    "data":{
        "address":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "content":"eX26q+uozgOQvTmTkaUj1ABv7oIdZjMQ1h4p51fi7Di7rGD+tlZG9SNfkRAVujoOohkg8laRsTAtQiSChPj4/VfrHMDVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLFUAJUfjsAm+ZYvW6hnvcRpjdq4hqrp74E5+fuvS35O1Mxni9RRt9zkcBDE2b5QS0GCFTHw+zSrnF9AU8RxfzIhEpEu9u/7iw2d8eqEMZotf5CnR3ypt7mlErkz8nMAnUG6CSjzpT78LnrPZALp4L3LuuuPhmstAJB+MK2dxD8J0wEG8qc8ZtEHLd3DfsdKla6UdvSKDH70mXdXJKLNjtGwOUY/rPzheAwBAcXoD60o42RrmMQCOw2z99zZHGOe2GIp3jypF7XkUW3tXsgwBMbjcnP0+yAoGy0tzC7oQushNfMYhfw/EKVW1PvoD58OKTaGotc9/tDVrE1XcJAMA4/iNbDWlngscX/d3PHYwSLcdP51cb+nJKJ4tACbQNZCrwPrLKNleiQ6/84mUUPNOzXzR1ShC5VTeZl9SyIZqOfxSk81MkzAD0PnqWbVHhdjJUYjzy/S0cD/cVQdbzkHfHDKgQIMhBv0HxU24o5In+r/PbLd3MlQMjV/toYPylk8=",
        "filehash":"0xa4473b3f3a90025c936646d75195a3ab0a4685a31142423121375baed271dd6d",
        "nonce":15,
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/files/store`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |           描述           | 取值范围 |
| --------- | -------- | -------- | ------ | ------------------------ | -------- |
| \<data\>  | object   | true     | NA     |                          | NA       |
| address   | string   | true     | NA     | 转出账户地址              | NA       |
| content   | string   | true     | NA     | 文件内容(base64-encoded) | NA       |
| filehash  | string   | true     | NA     | 文件哈希（HMAC-SHA256）   | NA       |
| nonce     | int      | true     | NA     | 账户操作次数              | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒）         | NA       |
| \</data\> |          | true     | NA     |                          | NA       |
| signature | string   | true     | NA     | 转出账户签名              | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "transaction":{
            "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
            "address": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
            "filehash": "0x1c1643c57b0ec7542498f693f201da4ccbb9991289e45631436bad366fdc111d",
            "nonce": 15,
        }
    },
    "ts":1650333610000,
}
```

### 响应数据

|     字段名称      | 数据类型 |            描述            |
| ---------------- | -------- | ------------------------- |
| status           | string   | 请求处理结果  "ok","error" |
| \<data\>         | object   |                           |
| \<transaction\>  | object   |                           |
| hash             | string   | 交易哈希（文件存储）        |
| address          | string   | 文件存储账户地址            |
| filehash         | string   | 文件哈希                   |
| nonce            | int      | 账户操作次数               |
| \</transaction\> |          |                           |
| \</data\>        |          |                           |
| ts               | int      | UTC时间戳（毫秒）           |


## 文件读取

读取地址`address`下的文件内容，不计入账户操作次数


> Request:

```json
{
    "data":{
        "address":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "filehash":"0xa4473b3f3a90025c936646d75195a3ab0a4685a31142423121375baed271dd6d",
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/files/retrieve`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |          描述           | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------------- | -------- |
| \<data\>  | object   | true     | NA     |                        | NA       |
| address   | string   | true     | NA     | 拥有者账户地址           | NA       |
| filehash  | string   | true     | NA     | 文件哈希（HMAC-SHA256） | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒）        | NA       |
| \</data\> |          | true     | NA     |                        | NA       |
| signature | string   | true     | NA     | 拥有者账户签名           | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "filehash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "address": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "content":"eX26q+uozgOQvTmTkaUj1ABv7oIdZjMQ1h4p51fi7Di7rGD+tlZG9SNfkRAVujoOohkg8laRsTAtQiSChPj4/VfrHMDVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLFUAJUfjsAm+ZYvW6hnvcRpjdq4hqrp74E5+fuvS35O1Mxni9RRt9zkcBDE2b5QS0GCFTHw+zSrnF9AU8RxfzIhEpEu9u/7iw2d8eqEMZotf5CnR3ypt7mlErkz8nMAnUG6CSjzpT78LnrPZALp4L3LuuuPhmstAJB+MK2dxD8J0wEG8qc8ZtEHLd3DfsdKla6UdvSKDH70mXdXJKLNjtGwOUY/rPzheAwBAcXoD60o42RrmMQCOw2z99zZHGOe2GIp3jypF7XkUW3tXsgwBMbjcnP0+yAoGy0tzC7oQushNfMYhfw/EKVW1PvoD58OKTaGotc9/tDVrE1XcJAMA4/iNbDWlngscX/d3PHYwSLcdP51cb+nJKJ4tACbQNZCrwPrLKNleiQ6/84mUUPNOzXzR1ShC5VTeZl9SyIZqOfxSk81MkzAD0PnqWbVHhdjJUYjzy/S0cD/cVQdbzkHfHDKgQIMhBv0HxU24o5In+r/PbLd3MlQMjV/toYPylk8=",
    },
    "ts":1650333610000,
}
```

### 响应数据

|  字段名称  | 数据类型 |            描述            |
| --------- | -------- | ------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                           |
| filehash  | string   | 文件哈希                   |
| address   | string   | 文件存储账户地址            |
| content   | string   | 文件内容(base64-encoded)   |
| \</data\> |          |                           |
| ts        | int      | UTC时间戳（毫秒）           |

## KV存储

将KV键值对加密存储到地址`address`下


> Request:

```json
{
    "data":{
        "address":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "value":"yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
        "nonce":15,
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/files/kvstore`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |       描述       | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------- | -------- |
| \<data\>  | object   | true     | NA     |                  | NA       |
| address   | string   | true     | NA     | 转出账户地址      | NA       |
| key       | string   | true     | NA     | 键值对的key       | NA       |
| value     | string   | true     | NA     | 键值对的value     | NA       |
| nonce     | int      | true     | NA     | 账户操作次数      | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                  | NA       |
| signature | string   | true     | NA     | 转出账户签名      | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "transaction":{
            "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
            "address": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
            "key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "nonce": 15,
        }
    },
    "ts":1650333610000,
}
```

### 响应数据

|     字段名称      | 数据类型 |            描述            |
| ---------------- | -------- | ------------------------- |
| status           | string   | 请求处理结果  "ok","error" |
| \<data\>         | object   |                           |
| \<transaction\>  | object   |                           |
| hash             | string   | 交易哈希（KV存储）          |
| address          | string   | 文件存储账户地址            |
| key              | string   | KV存储的key                |
| nonce            | int      | 账户操作次数               |
| \</transaction\> |          |                           |
| \</data\>        |          |                           |
| ts               | int      | UTC时间戳（毫秒）           |


## KV读取

读取地址`address`下的KV内容，不计入账户操作次数


> Request:

```json
{
    "data":{
        "address":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/files/kvretrieve`


### 请求参数

|    参数    | 数据类型 | 是否必须 | 默认值 |       描述       | 取值范围 |
| --------- | -------- | -------- | ------ | ---------------- | -------- |
| \<data\>  | object   | true     | NA     |                  | NA       |
| address   | string   | true     | NA     | 拥有者账户地址    | NA       |
| key       | string   | true     | NA     | KV键值对的key     | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                  | NA       |
| signature | string   | true     | NA     | 拥有者账户签名    | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "address": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "value": "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
    },
    "ts":1650333610000,
}
```

### 响应数据

|  字段名称  | 数据类型 |            描述            |
| --------- | -------- | ------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                           |
| address   | string   | 拥有者账户地址              |
| key       | string   | KV键值对的key              |
| value     | string   | KV键值对的value            |
| \</data\> |          |                           |
| ts        | int      | UTC时间戳（毫秒）           |