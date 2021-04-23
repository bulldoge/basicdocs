# Keystore文件字段解析

作者：bulldoge

邮箱：bulldoge@163.com

## 一、背景

使用geth生成的以太坊账户默认是不会直接提供私钥，而是只会生成一个加密的私钥文件，想要得到私钥需要借助第三方工具。

## 二、以太坊私钥加密文件生成
执行命令`geth account new`，通过设置密码会生成一个包含以太坊私钥的加密文件。

## 三、以太坊私钥加密文件位置
位置默认在：
`~/Library/Ethereum/keystore/UTC--2021-04-23T10-12-54.707072000Z--ca9d4cdb48359e4844872da41ef08890c644be67`

## 四、以太坊私钥加密文件结构

```
{
"address":"ca9d4cdb48359e4844872da41ef08890c644be67",
"crypto":{
    "cipher":"aes-128-ctr",
    "ciphertext":"6eafd361d4371259f59366c278a88371f164ed91de2d67a4b2c2138678ade8ac",
    "cipherparams":{
        "iv":"1be7c140754ed5fc8c9c8d6bba4fca44"
        },
    "kdf":"scrypt",
    "kdfparams":{
        "dklen":32,
        "n":262144,
        "p":1,
        "r":8,
        "salt":"3d94386e8d975746b284bd175de4070b5bcebdb8c600442fb059b55bb17785a5"
        },
    "mac":"84b04ecb5b9414f457e545a1304e85186d8883c9a47615e07219373f2ff35821"
    },
"id":"a4ba0537-e5ab-4dfd-819a-be3fabdd1a3f",
"version":3
}
```

## 五、以太坊私钥加密文件字段含义

address: 账号地址。

version: Keystore文件的版本，目前为第3版，也称为V3 KeyStore。

id: uuid 。

crypto: 加密推倒的相关配置。

cipher: 是用于加密以太坊私钥的对称加密算法。用的是 aes-128-ctr 。

ciphertext: 是加密算法输出的密文，也是将来解密时的需要的输入。

cipherparams: 是 aes-128-ctr 加密算法需要的参数。在这里，用到的唯一的参数 iv。

kdf: 指定使用哪一个算法，这里使用的是 scrypt。

kdfparams: scrypt函数需要的参数。

mac: 用来校验密码的正确性， mac= sha3(DK[16:32], ciphertext)。
