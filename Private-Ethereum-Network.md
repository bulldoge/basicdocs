# 安装本地测试环境

作者：bulldoge

邮箱：bulldoge@163.com

## 一、下载geth最新版本
`https://github.com/ethereum/go-ethereum/releases/tag/v1.10.2`

## 二、编译安装

在目录go-ethereum-1.10.2下执行命令：

`make all`

## 三、查看目录 go-ethereum-1.10.2/build/bin 下生成的工具包：

```

abidump

bootnode
Stripped down version of our Ethereum client implementation that only takes part in the network node discovery protocol, but does not run any of the higher level application protocols. It can be used as a lightweight bootstrap node to aid in finding peers in private networks.

clef
Clef can be used to sign transactions and data and is meant as a(n eventual) replacement for Geth's account management. This allows DApps to not depend on Geth's account management. When a DApp wants to sign data (or a transaction), it can send the content to Clef, which will then provide the user with context and asks for permission to sign the content. If the users grants the signing request, Clef will send the signature back to the DApp.

ethkey
ethkey is a CLI tool that allows you to interact with the Ethereum wallet. With it you can list, inspect, create, delete and modify keys and inspect, create and sign transactions.

faucet
The faucet is a simplistic web application with the goal of distributing small amounts of Ether in private and test networks.

p2psim

rlpdump
Developer utility tool to convert binary RLP (Recursive Length Prefix) dumps (data encoding used by the Ethereum protocol both network as well as consensus wise) to user-friendlier hierarchical representation (e.g. rlpdump --hex CE0183FFFFFFC4C304050583616263).

abigen
Source code generator to convert Ethereum contract definitions into easy to use, compile-time type-safe Go packages. It operates on plain Ethereum contract ABIs with expanded functionality if the contract bytecode is also available. However, it also accepts Solidity source files, making development much more streamlined. Please see our Native DApps page for details.

checkpoint-admin
Checkpoint-admin is a tool for updating checkpoint oracle status. It provides a series of functions including deploying checkpoint oracle contract, signing for new checkpoints, and updating checkpoints in the checkpoint oracle contract.

devp2p
The devp2p command line tool is a utility for low-level peer-to-peer debugging and protocol development purposes.

evm
Developer utility version of the EVM (Ethereum Virtual Machine) that is capable of running bytecode snippets within a configurable environment and execution mode. Its purpose is to allow isolated, fine-grained debugging of EVM opcodes (e.g. evm --code 60ff60ff --debug run).

geth 
Our main Ethereum CLI client. It is the entry point into the Ethereum network (main-, test- or private net), capable of running as a full node (default), archive node (retaining all historical state) or a light node (retrieving data live). It can be used by other processes as a gateway into the Ethereum network via JSON RPC endpoints exposed on top of HTTP, WebSocket and/or IPC transports. geth --help and the CLI page for command line options.	

puppeth
a CLI wizard that aids in creating a new Ethereum network.

```

详细工具包官方介绍可参考：
`https://github.com/ethereum/go-ethereum/tree/master/cmd`

## 四、常用命令

参考官方wiki：
`https://geth.ethereum.org/docs/interface/command-line-options`

## 五、私链配置

参考官方wiki：
`https://geth.ethereum.org/docs/interface/private-network`

## 六、以太坊相关知识普及

参考官方文档：
`https://ethereum.org/en/developers/`
