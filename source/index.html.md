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

<!-- ### 密钥交换

密钥交换算法：ECDH

椭圆曲线：secp256k1椭圆曲线，参考文档：[SEC 2: Recommended Elliptic Curve Domain Parameters](https://www.secg.org/sec2-v2.pdf)，Chapter 2.4.1

具体方法：服务端和客户端基于双方的公钥和自己的私钥生成共享的通信密钥。

具体步骤：

* 若服务端私钥为a，客户端私钥为a，互相共享公钥$g^a$，$g^b$；
* 双方计算得到$g^{ab}$，取得$g^{ab}$的$x$坐标为共享秘密(Shared Secret)；
* 将$x$转化为二进制表示并作哈希，得到密钥，Shared Private Key = Keccak256(x)；
* Shared Private Key为服务端和客户端共享密钥。

参考文档：[Elliptic Curve Groups modulo a Prime (ECP Groups) for IKE and IKEv2](https://www.rfc-editor.org/rfc/rfc5903.html)的Section 9 -->

### 对称加密

### 通信

本文档通信采用TLS加密通信，Certificate格式如下：

|    参数 | 数据类型 | 是否必须 | 默认值|          描述   | 取值范围 |
| --------- | -------- | -------- | ------| ----------------------| -------- |
| 无参数 |   |   |  |      |   |

<!--本文文档通过 [Slate](https://github.com/slatedocs/slate)驱动。-->

# 认证

## 获取远程认证报告

此接口返回TEE中的远程认证报告，同时交换通信密钥。

> Request:

### HTTP 请求

- POST `/report`

### 请求参数

|    参数 | 数据类型 | 是否必须 | 默认值|          描述   | 取值范围 |
| --------- | -------- | -------- | ------| ----------------------| -------- |
| 无参数 |   |   |  |      |   |

> Response:

```json
{
    "status":"ok",
    "data":{
        "report":"eX26q+uozgOQvTmTkaUj1ABv7oIdZjMQ1h4p51fi7Di7rGD+tlZG9SNfkRAVujoOohkg8laRsTAtQiSChPj4/VfrHMDVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLFUAJUfjsAm+ZYvW6hnvcRpjdq4hqrp74E5+fuvS35O1Mxni9RRt9zkcBDE2b5QS0GCFTHw+zSrnF9AU8RxfzIhEpEu9u/7iw2d8eqEMZotf5CnR3ypt7mlErkz8nMAnUG6CSjzpT78LnrPZALp4L3LuuuPhmstAJB+MK2dxD8J0wEG8qc8ZtEHLd3DfsdKla6UdvSKDH70mXdXJKLNjtGwOUY/rPzheAwBAcXoD60o42RrmMQCOw2z99zZHGOe2GIp3jypF7XkUW3tXsgwBMbjcnP0+yAoGy0tzC7oQushNfMYhfw/EKVW1PvoD58OKTaGotc9/tDVrE1XcJAMA4/iNbDWlngscX/d3PHYwSLcdP51cb+nJKJ4tACbQNZCrwPrLKNleiQ6/84mUUPNOzXzR1ShC5VTeZl9SyIZqOfxSk81MkzAD0PnqWbVHhdjJUYjzy/S0cD/cVQdbzkHfHDKgQIMhBv0HxU24o5In+r/PbLd3MlQMjV/toYPylk8=",
        "cert":"DVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLbQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896PbQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896PbQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896PbQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P",
    }
}
```

### 响应数据

|  字段名称 | 数据类型 |            描述    |
| --------- | -------- | --------------------------- |
| status | string | 请求处理结果  "ok","error"    |
| \<data\> | object |        |
| report | string | 远程认证报告，base64-encoded |
| cert  | string | tls证书，base64-encoded  |
| \</data\> |   |        |

# 区块与交易信息

## 区块信息

查询当前区块区块号 `number` 相关信息

> Request:

```json
{
    "data":{
        "number":1684633435,
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/block/info`

### 请求参数

|    参数 | 数据类型 | 是否必须 | 默认值|       描述  | 取值范围 |
| --------- | -------- | -------- | ------| ---------------- | -------- |
| \<data\> | object | true  | NA |     | NA  |
| number | int | true  | NA | 区块号   | NA  |
| ts  | int  | true  | NA | UTC时间戳（毫秒） | NA  |
| \</data\> |   | true  | NA |     | NA  |
| signature | string | true  | NA | 账户签名   | NA  |

> Response:

```json
{
    "status":"ok",
    "data":{
        "number":1684633435,
        "transactions":[
            "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
            "0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
            ],
        "count":2,
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| number   | int64   | 区块号                   |
| \<transactions\>   | array      | 列举交易哈希                   |
| hash1   | string   | 交易哈希                   |
| hash2   | string   | 交易哈希                   |
| ...   | ...   | ...                   |
| hashn   | string   | 交易哈希                   |
| \</transactions\>   |       |                    |
| count     | int      | 区块中的交易数量           |
| \</data\> |          |                            |
| ts        | int      | 时间戳                     |

## 交易信息

查询当前交易哈希 `hash` 相关信息

> Request:

```json
{
    "data":{
        "hash":"0x02cd1c248d6bb2a1f2002646a29cb9cfda45b61d8f43fb8328e221224ef38d4f56",
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/transaction/info`

### 请求参数

|    参数 | 数据类型 | 是否必须 | 默认值|       描述  | 取值范围 |
| --------- | -------- | -------- | ------| ---------------- | -------- |
| \<data\> | object | true  | NA |     | NA  |
| hash | string | true  | NA | 交易哈希   | NA  |
| ts  | int  | true  | NA | UTC时间戳（毫秒） | NA  |
| \</data\> |   | true  | NA |     | NA  |
| signature | string | true  | NA | 账户签名   | NA  |

> Response:

```json
{
    "status":"ok",
    "data":{
        "hash":"0x02cd1c248d6bb2a1f2002646a29cb9cfda45b61d8f43fb8328e221224ef38d4f56",
        "type":"File store",
        "transactionTs":1640111610000,
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| hash   | string   | 交易哈希                   |
| type   | string   | 交易类型（"File store", "KV store", "Contract depoly", "Contract call"）                   |
| transactionTs        | int      | 交易时间戳                     |
| \</data\> |          |                            |
| ts        | int      | 时间戳                     |

# 账户

## 简介

账户相关接口提供了账户查询以及资产交易等功能。

> Example:

```json
{
    "private_key":"0x449287999732a7785e00aa9f152db6de35187d3a3502cb26069a5a94248e61c1",
    "address":"0x02cd1c248d6bb2a1f2002646a29cb9cfda45b61d8f43fb8328e221224ef38d4f56",
    "address":"0x04cd1c248d6bb2a1f2002646a29cb9cfda45b61d8f43fb8328e221224ef38d4f563235a022a049c938a4c553b9b7db9fc5b5e73e855050ca28eb2210a37fecf01cdc5bcebe460d886587125e57791a25ce1d9eae7cdc4c12018492dadef23433c178845b2f8bf7f7b1a2467e5983d90adc34ec794e28d9f82fa80e3aa30acd817f00"
}
```

### 账户地址格式

地址为以太坊格式的公钥，压缩公钥或非压缩公钥均可。（私钥32字节，压缩公钥33字节，非压缩公钥65字节）

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

|    参数 | 数据类型 | 是否必须 | 默认值|       描述  | 取值范围 |
| --------- | -------- | -------- | ------| ---------------- | -------- |
| \<data\> | object | true  | NA |     | NA  |
| address | string | true  | NA | 账户地址   | NA  |
| ts  | int  | true  | NA | UTC时间戳（毫秒） | NA  |
| \</data\> |   | true  | NA |     | NA  |
| signature | string | true  | NA | 账户签名   | NA  |

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

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| address   | string   | 账户地址                   |
| balance   | int      | 账户余额                   |
| nonce     | int      | 账户操作次数               |
| count     | int      | 账户拥有文件数量           |
| \</data\> |          |                            |
| ts        | int      | 时间戳                     |

## 转账(未生效)

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

| 参数      | 数据类型 | 是否必须 | 默认值 | 描述              | 取值范围 |
| --------- | -------- | -------- | ------ | ----------------- | -------- |
| \<data\>  | object   | true     | NA     |                   | NA       |
| from      | string   | true     | NA     | 转出账户地址      | NA       |
| to        | string   | true     | NA     | 转入账户地址      | NA       |
| nonce     | int      | true     | NA     | 账户操作次数      | NA       |
| value     | int      | true     | NA     | 转账金额          | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                   | NA       |
| signature | string   | true     | NA     | 转出账户签名      | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "to": "0x1c1643c57b0ec7542498f693f201da4ccbb9991289e45631436bad366fdc111d",
        "nonce": 15,
        "value": 100000000,
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称         | 数据类型 | 描述                       |
| ---------------- | -------- | -------------------------- |
| status           | string   | 请求处理结果  "ok","error" |
| \<data\>         | object   |                            |
| hash             | string   | 交易哈希                   |
| from             | string   | 转出账户地址               |
| to               | string   | 转入账户地址               |
| nonce            | int      | 账户操作次数               |
| value            | int      | 转账金额                   |
| \</data\>        |          |                            |
| ts               | int      | UTC时间戳（毫秒）          |

# 文件

## 简介

文件提供文件存储以及KV键值对存储相关接口信息

<aside class="notice">文件存储和KV存储需要占用账户操作nonce，文件和KV读取不占用操作nonce</aside>

## 文件存储

将文件加密存储到地址`from`下

> Request:

```json
{
    "data":{
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "content":"eX26q+uozgOQvTmTkaUj1ABv7oIdZjMQ1h4p51fi7Di7rGD+tlZG9SNfkRAVujoOohkg8laRsTAtQiSChPj4/VfrHMDVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLFUAJUfjsAm+ZYvW6hnvcRpjdq4hqrp74E5+fuvS35O1Mxni9RRt9zkcBDE2b5QS0GCFTHw+zSrnF9AU8RxfzIhEpEu9u/7iw2d8eqEMZotf5CnR3ypt7mlErkz8nMAnUG6CSjzpT78LnrPZALp4L3LuuuPhmstAJB+MK2dxD8J0wEG8qc8ZtEHLd3DfsdKla6UdvSKDH70mXdXJKLNjtGwOUY/rPzheAwBAcXoD60o42RrmMQCOw2z99zZHGOe2GIp3jypF7XkUW3tXsgwBMbjcnP0+yAoGy0tzC7oQushNfMYhfw/EKVW1PvoD58OKTaGotc9/tDVrE1XcJAMA4/iNbDWlngscX/d3PHYwSLcdP51cb+nJKJ4tACbQNZCrwPrLKNleiQ6/84mUUPNOzXzR1ShC5VTeZl9SyIZqOfxSk81MkzAD0PnqWbVHhdjJUYjzy/S0cD/cVQdbzkHfHDKgQIMhBv0HxU24o5In+r/PbLd3MlQMjV/toYPylk8=",
        "fileHash":"0xa4473b3f3a90025c936646d75195a3ab0a4685a31142423121375baed271dd6d",
        "nonce":15,
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/files/store`

### 请求参数

| 参数      | 数据类型 | 是否必须 | 默认值 | 描述                     | 取值范围 |
| --------- | -------- | -------- | ------ | ------------------------ | -------- |
| \<data\>  | object   | true     | NA     |                          | NA       |
| from   | string   | true     | NA     | 转出账户地址             | NA       |
| content   | string   | true     | NA     | 文件内容(base64-encoded) | NA       |
| fileHash  | string   | true     | NA     | 文件哈希（Keccak256）  | NA       |
| nonce     | int      | true     | NA     | 账户操作次数             | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒）        | NA       |
| \</data\> |          | true     | NA     |                          | NA       |
| signature | string   | true     | NA     | 转出账户签名             | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "fileHash": "0x1c1643c57b0ec7542498f693f201da4ccbb9991289e45631436bad366fdc111d",
        "nonce": 15,
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称         | 数据类型 | 描述                       |
| ---------------- | -------- | -------------------------- |
| status           | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| hash             | string   | 交易哈希（文件存储）       |
| from          | string   | 文件存储账户地址           |
| fileHash         | string   | 文件哈希(Keccak256)                   |
| nonce            | int      | 账户操作次数               |
| \</data\> |          |                            |
| ts               | int      | UTC时间戳（毫秒）          |

## 文件读取

读取地址`from`下的文件内容，不计入账户操作次数

> Request:

```json
{
    "data":{
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "fileHash":"0xa4473b3f3a90025c936646d75195a3ab0a4685a31142423121375baed271dd6d",
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/files/retrieve`

### 请求参数

| 参数      | 数据类型 | 是否必须 | 默认值 | 描述                    | 取值范围 |
| --------- | -------- | -------- | ------ | ----------------------- | -------- |
| \<data\>  | object   | true     | NA     |                         | NA       |
| from   | string   | true     | NA     | 拥有者账户地址          | NA       |
| fileHash  | string   | true     | NA     | 文件哈希（Keccak256） | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒）       | NA       |
| \</data\> |          | true     | NA     |                         | NA       |
| signature | string   | true     | NA     | 拥有者账户签名          | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "fileHash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "content":"eX26q+uozgOQvTmTkaUj1ABv7oIdZjMQ1h4p51fi7Di7rGD+tlZG9SNfkRAVujoOohkg8laRsTAtQiSChPj4/VfrHMDVRp/bQjvMyZ7xmDK1LTZAyIkDwOFnrhqqFr4gDUI9XS53bY6yLpnVFcN7e896P+CHQ4FLbCm5UOdJxGcoLFUAJUfjsAm+ZYvW6hnvcRpjdq4hqrp74E5+fuvS35O1Mxni9RRt9zkcBDE2b5QS0GCFTHw+zSrnF9AU8RxfzIhEpEu9u/7iw2d8eqEMZotf5CnR3ypt7mlErkz8nMAnUG6CSjzpT78LnrPZALp4L3LuuuPhmstAJB+MK2dxD8J0wEG8qc8ZtEHLd3DfsdKla6UdvSKDH70mXdXJKLNjtGwOUY/rPzheAwBAcXoD60o42RrmMQCOw2z99zZHGOe2GIp3jypF7XkUW3tXsgwBMbjcnP0+yAoGy0tzC7oQushNfMYhfw/EKVW1PvoD58OKTaGotc9/tDVrE1XcJAMA4/iNbDWlngscX/d3PHYwSLcdP51cb+nJKJ4tACbQNZCrwPrLKNleiQ6/84mUUPNOzXzR1ShC5VTeZl9SyIZqOfxSk81MkzAD0PnqWbVHhdjJUYjzy/S0cD/cVQdbzkHfHDKgQIMhBv0HxU24o5In+r/PbLd3MlQMjV/toYPylk8=",
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| fileHash  | string   | 文件哈希(Keccak256)                   |
| from   | string   | 文件存储账户地址           |
| content   | string   | 文件内容(base64-encoded)   |
| \</data\> |          |                            |
| ts        | int      | UTC时间戳（毫秒）          |

## KV存储

将KV键值对加密存储到地址`from`下

> Request:

```json
{
    "data":{
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "value":"yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
        "nonce":15,
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/kv/store`

### 请求参数

| 参数      | 数据类型 | 是否必须 | 默认值 | 描述              | 取值范围 |
| --------- | -------- | -------- | ------ | ----------------- | -------- |
| \<data\>  | object   | true     | NA     |                   | NA       |
| from   | string   | true     | NA     | 转出账户地址      | NA       |
| key       | string   | true     | NA     | 键值对的key       | NA       |
| value     | string   | true     | NA     | 键值对的value     | NA       |
| nonce     | int      | true     | NA     | 账户操作次数      | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                   | NA       |
| signature | string   | true     | NA     | 转出账户签名      | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "nonce": 15,
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称         | 数据类型 | 描述                       |
| ---------------- | -------- | -------------------------- |
| status           | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| hash             | string   | 交易哈希（KV存储）         |
| from          | string   | 文件存储账户地址           |
| key              | string   | KV存储的key                |
| nonce            | int      | 账户操作次数               |
| \</data\> |          |                            |
| ts               | int      | UTC时间戳（毫秒）          |

## KV读取

读取地址`from`下的KV内容，不计入账户操作次数

> Request:

```json
{
    "data":{
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "ts":1650333610000,
    },
    "signature":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b"
}
```

### HTTP 请求

- POST `/kv/retrieve`

### 请求参数

| 参数      | 数据类型 | 是否必须 | 默认值 | 描述              | 取值范围 |
| --------- | -------- | -------- | ------ | ----------------- | -------- |
| \<data\>  | object   | true     | NA     |                   | NA       |
| from   | string   | true     | NA     | 拥有者账户地址    | NA       |
| key       | string   | true     | NA     | KV键值对的key     | NA       |
| ts        | int      | true     | NA     | UTC时间戳（毫秒） | NA       |
| \</data\> |          | true     | NA     |                   | NA       |
| signature | string   | true     | NA     | 拥有者账户签名    | NA       |

> Response:

```json
{
    "status":"ok",
    "data":{
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "value": "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| from   | string   | 拥有者账户地址             |
| key       | string   | KV键值对的key              |
| value     | string   | KV键值对的value            |
| \</data\> |          |                            |
| ts        | int      | UTC时间戳（毫秒）          |



# 智能合约

## 智能合约代码示例

> Example:

```go
package evidence_v6

import (
	"encoding/json"
	"ContractContext"
)

type Error struct {
	message string
	payload string
}

type EvidenceInfo struct {
	EvidenceId   string `json:"evidenceId"`
	UploaderSign string `json:"uploaderSign"`
	EvidenceTxId string `json:"evidenceTxId"`
	Content      string `json:"content"`
}

type CreateResult struct {
	EvidenceId  string `json:"evidenceId,omitempty"`
	TxId        string `json:"txId,omitempty"`
	TxTimestamp string `json:"txTimestamp,omitempty"`
}

type QueryResult struct {
	Key      string `json:"key,omitempty"`
	Record   string `json:"record,omitempty"`
	Bookmark string `json:"bookmark,omitempty"`
}

func AddEvidence(context ContractContext.Context, data string) *CreateResult {
	evidenceinfo := &EvidenceInfo{}
	err := json.Unmarshal([]byte(data), evidenceinfo)
	stub := context.Getstub()
	key := FormatEvidenceKey(evidenceinfo.EvidenceId)
	evidenceState, err := stub.GetStringState(key)
	if err != nil {
		panic(Error{
			message: "Evidence " + evidenceinfo.EvidenceId + " already exists",
			payload: "EVIDENCE_ALREADY_EXIST",
		})

	}
	txId := stub.GetTxId()
	timeStamp := stub.GetTxTimestamp()
	evidenceinfo.EvidenceTxId = txId
	stub.PutStringState(key, evidenceState)
	return &CreateResult{
		EvidenceId:  evidenceinfo.EvidenceId,
		TxId:        txId,
		TxTimestamp: timeStamp,
	}
}

func QueryEvidenceById(context ContractContext.Context, evidenceId string) *QueryResult {
	stub := context.Getstub()
	evidenceState, err := stub.GetStringState(evidenceId)
	if err != nil {
		panic(Error{
			message: evidenceId,
			payload: "NO_EVIDENCE_FOUND",
		})
	}
	return &QueryResult{
		Key:      evidenceId,
		Record:   evidenceState,
		Bookmark: "",
	}
}

func QueryEvidenceByTxId(context ContractContext.Context, txId string) *QueryResult {
	stub := context.Getstub()
	query, _ := json.Marshal(struct {
		Selector string `json:"selector"`
	}{Selector: txId})
	evidenceState, _ := json.Marshal(stub.GetQueryResult(string(query)))
	return &QueryResult{
		Key:      txId,
		Record:   string(evidenceState),
		Bookmark: "",
	}
}

func FormatEvidenceKey(evidenceId string) string {
	return "Evi_" + evidenceId
}


```

## 智能合约ABI示例

> Example:

```json
{
    "contract_name" : "evidence_v6",
    "contract_info" : "This is contract evidence_v6",
    "contract_function" : [
        {
            "function_name" : "AddEvidence",
            "function_inputs" : [
                {
                    "input_name" : "context",
                    "input_type" : "context" 
                },
                {
                    "input_name" : "data",
                    "input_type" : "string" 
                }
            ],
            "function_outputs" : [
                {
                    "output_name" : "CreateResult",
                    "output_type" : "struct",
                    "output_component" : [
                        {
                            "component_name" : "evidenceId",
                            "component_type" : "string"
                        },
                        {
                            "component_name" : "txId",
                            "component_type" : "string"
                        },
                        {
                            "component_name" : "txTimestamp",
                            "component_type" : "string"
                        }
                    ] 
                }
            ]
        },
        {
            "function_name" : "QueryEvidenceById",
            "function_inputs" : [
                {
                    "input_name" : "context",
                    "input_type" : "context" 
                },
                {
                    "input_name" : "evidenceId",
                    "input_type" : "string" 
                }
            ],
            "function_outputs" : [
                {
                    "output_name" : "QueryResult",
                    "output_type" : "struct",
                    "output_component" : [
                        {
                            "component_name" : "key",
                            "component_type" : "string"
                        },
                        {
                            "component_name" : "record",
                            "component_type" : "string"
                        },
                        {
                            "component_name" : "bookmark",
                            "component_type" : "string"
                        }
                    ] 
                }
            ]
        },
        {
            "function_name" : "AddEvidence",
            "function_inputs" : [
                {
                    "input_name" : "context",
                    "input_type" : "context" 
                },
                {
                    "input_name" : "txId",
                    "input_type" : "string" 
                }
            ],
            "function_outputs" : [
                {
                    "output_name" : "QueryResult",
                    "output_type" : "struct",
                    "output_component" : [
                        {
                            "component_name" : "key",
                            "component_type" : "string"
                        },
                        {
                            "component_name" : "record",
                            "component_type" : "string"
                        },
                        {
                            "component_name" : "bookmark",
                            "component_type" : "string"
                        }
                    ] 
                }
            ]
        }
    ]
}
```


## FunctionInputs示例

> Example:

```json
[
    {
        "input_name" : "context",
        "input_type" : "context", 
        "input_value" : ""
    },
    {
        "input_name" : "data",
        "input_type" : "string",
        "input_value" : "{\"evidenceId\":\"aa\",\"uploaderSign\":\"cc\",\"content\":\"dd\"}"
    }
]
```

## 智能合约部署

智能合约信息部署

> Request:

```json
{
    "data":{
        "name":"evidence_v6",
        "abi":"智能合约ABI示例中的内容",
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "code":"智能合约代码示例中的内容",
        "codeHash":"0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b",
        "ts":1650333610000,
    },
    "signature":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
}
```

### HTTP 请求

- POST `/contract/deploy`

### 请求参数

|    参数 | 数据类型 | 是否必须 | 默认值|       描述  | 取值范围 |
| --------- | -------- | -------- | ------| ---------------- | -------- |
| \<data\> | object | true  | NA |     | NA  |
| name | string | true  | NA | 合约名称   | NA  |
| abi | string | true  | NA | 合约ABI   | NA  |
| from | string | true  | NA | 合约拥有者账户地址   | NA  |
| code | string | true  | NA | 合约代码   | NA  |
| codeHash | string | true  | NA | 合约代码哈希(keccak-256)   | NA  |
| ts  | int  | true  | NA | UTC时间戳（毫秒） | NA  |
| \</data\> |   | true  | NA |     | NA  |
| signature | string | true  | NA | 账户签名   | NA  |

> Response:

```json
{
    "status":"ok",
    "data":{
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "contractAddress" : "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "nonce" : 10,
        "codeHash": "0x4c49d393b56749d6a2048f2ef6eaa60dba54b45d78f3d0ce9bccb97f6f1e884b",
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| from   | string   | 拥有者账户地址             |
| hash       | string   | 交易哈希              |
| contractAddress     | string   | 智能合约地址            |
| nonce       | int   | 账户操作次数              |
| codeHash     | string   | 智能合约代码哈希            |
| \</data\> |          |                            |
| ts        | int      | UTC时间戳（毫秒）          |

## 智能合约调用

智能合约函数调用

> Request:

```json
{
    "data":{
        "codeHash":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "contractAddress": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "from":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "functionName":"AddEvidence",
        "functionInputs" : "FunctionInputs示例中的内容",
        "ts":1650333610000,
    },
    "signature":"0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
}
```

### HTTP 请求

- POST `/contract/deploy`

### 请求参数

|    参数 | 数据类型 | 是否必须 | 默认值|       描述  | 取值范围 |
| --------- | -------- | -------- | ------| ---------------- | -------- |
| \<data\> | object | true  | NA |     | NA  |
| codeHash | string | true  | NA | 合约代码哈希(keccak-256)   | NA  |
| contractAddress | string | true  | NA | 合约地址  | NA  |
| from | string | true  | NA | 合约拥有者账户地址   | NA  |
| functionName | string | true  | NA | 函数名称   | NA  |
| functionInputs | string | true  | NA | 函数输入   | NA  |
| ts  | int  | true  | NA | UTC时间戳（毫秒） | NA  |
| \</data\> |   | true  | NA |     | NA  |
| signature | string | true  | NA | 账户签名   | NA  |

> Response:

```json
{
    "status":"ok",
    "data":{
        "from": "0x95b01199edc2d8943ea9edb0ae5908a70bb960f23bc23310ed030e15ecc60b18",
        "hash": "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "contractAddress" : "0xcc7c9dbe7bb4e409967803c6a2c4859e5068d4044ff7cf91a1c5179b92bbf967",
        "nonce" : 10,
        "result": "",
    },
    "ts":1650333610000,
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                       |
| --------- | -------- | -------------------------- |
| status    | string   | 请求处理结果  "ok","error" |
| \<data\>  | object   |                            |
| from   | string   | 拥有者账户地址             |
| hash       | string   | 交易哈希              |
| contractAddress     | string   | 智能合约地址            |
| nonce       | int   | 账户操作次数              |
| result     | string   | 智能合约执行返回值（需使用json再次对result返回字符串进行解析）            |
| \</data\> |          |                            |
| ts        | int      | UTC时间戳（毫秒）          |
