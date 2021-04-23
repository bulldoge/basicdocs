# 以太坊创世区块文件genesis.json参数解析

作者：bulldoge

邮箱：bulldoge@163.com

## 一、测试网创世区块配置文件结构

```json
{
  "config": {
    "chainId": 666,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "istanbulBlock": 0
  },
  "alloc": {
      "0xC6DFEB9aE5291720518349A2a33D96e0a8AEAA57": {
           "balance": "300000" 
      },
      "0x929d76Dc886DFc3dE06b494ED8190e856468BaFb": { 
          "balance": "400000" 
      }
  },
  "coinbase": "0xa994AD984690390AEE4DD0B536721259cC361546",
  "difficulty": "0x20000",
  "extraData": "",
  "gasLimit": "0x2fefd8",
  "nonce": "0x0000000000000042",
  "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp": "0x00"
}
```

## 二、创世区块配置文件结构字段解析

chainId: 该链的ID。在用geth 启动区块链时，还需要指定一个network 参数。只有当network、chainID、创世区块配置都相同时，才是同一条链。

homesteadBlock: 以太坊 homested 版本硬分叉高度。

eip150Block: 以太坊 eip150 版本硬分叉高度。

eip155Block: 以太坊 eip155 版本硬分叉高度。

eip158Block: 以太坊 eip158 版本硬分叉高度。

byzantiumBlock: 以太坊 byzantium 版本硬分叉高度。

constantinopleBlock: 以太坊 constantinople 版本硬分叉高度。

petersburgBlock: 以太坊 petersburg 版本硬分叉高度。

istanbulBlock: 以太坊 istanbul 版本硬分叉高度。

alloc: 预分配的账号以及金额。

coinbase: 矿工账户。

difficulty: 当前区块的难度，如果难度过大，cpu挖矿就很难，这里设置较小难度。

extraData: 自定义额外数据。

gasLimit: 油费上限。

nonce: 一个64位随机数，用于挖矿，注意他和mixhash的设置需要满足以太坊的Yellow paper, 4.3.4. Block Header Validity, (44)章节所描述的条件。

mixhash: 与nonce配合用于挖矿，由上一个区块的一部分生成的hash。注意他和nonce的设置需要满足以太坊的Yellow paper, 4.3.4. Block Header 。

Validity, (44)章节所描述的条件。

parentHash: 上一个区块的hash值，因为是创世块，所以这个值是0 。

timestamp: 设置创世块的时间戳。

## 三、mainnet参考配置

```json
{
    "config": {
        "chainId": 1,
        "homesteadBlock": 1150000,
        "daoForkBlock": 1920000,
        "daoForkSupport": true,
        "eip150Block": 2463000,
        "eip150Hash": "0x2086799aeebeae135c246c65021c82b4e15a2c451340993aacfd2751886514f0",
        "eip155Block": 2675000,
        "eip158Block": 2675000,
        "byzantiumBlock": 4370000,
        "constantinopleBlock": 7280000,
        "petersburgBlock": 7280000,
        "ethash": {}
    },
    "nonce": "0x42",
    "timestamp": "0x0",
    "extraData": "0x11bbe8db4e347b4e8c937c1c8370e4b5ed33adb3db69cbdb7a38e1e50b1b82fa",
    "gasLimit": "0x1388",
    "difficulty": "0x400000000",
    "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x0000000000000000000000000000000000000000",
    "number": "0x0",
    "gasUsed": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "alloc": {
        "0xC6DFEB9aE5291720518349A2a33D96e0a8AEAA57": {
            "balance": "0xad78ebc5ac6200000"
        },
        "0x929d76Dc886DFc3dE06b494ED8190e856468BaFb": {
            "balance": "0xad78ebc5ac6200000"
        }
    }
}
```
