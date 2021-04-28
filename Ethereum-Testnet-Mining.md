# 以太坊本地测试网单节点挖矿

作者：bulldoge

邮箱：bulldoge@163.com

## 一、新建数据目录

1. 新建数据存放目录

`mkdir -p testnetdata/data00`

2. 新建日志信息存放目录

`mkdir testnetlog`

## 二、配置创世区块文件

参考Ethereum-genesis.json-Analysis.md文档创建创世区块文件，并放置在testnetdata文件夹中。

或执行以下命令生成：

```

echo '{"config": {"chainId": 6666,"homesteadBlock": 0,"eip150Block": 0,"eip155Block": 0,"eip158Block": 0,"byzantiumBlock": 0,"constantinopleBlock": 0,"petersburgBlock": 0,"istanbulBlock": 0},"alloc": {},"coinbase": "0xa994AD984690390AEE4DD0B536721259cC361546","difficulty": "0x20000","extraData": "","gasLimit": "0x2fefd8","nonce": "0x0000000000000042","mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000","parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000","timestamp": "0x00"}' > testnetdata/genesis.json

```

## 三、初始化本地网络

1. 执行命令

如有旧数据可先清理旧数据
`geth removedb --datadir ~/code/ethereum/testnetdata/data00`

初始化
`geth --datadir testnetdata/data00 init testnetdata/genesis.json`

2. 返回初始化成功数据

```

INFO [04-28|13:17:35.521] Maximum peer count                       ETH=50 LES=0 total=50
INFO [04-28|13:17:35.523] Set global gas cap                       cap=25000000
INFO [04-28|13:17:35.524] Allocated cache and file handles         database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata cache=16.00MiB handles=16
INFO [04-28|13:17:35.567] Writing custom genesis block
INFO [04-28|13:17:35.568] Persisted trie from memory database      nodes=0 size=0.00B time="53.263µs" gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [04-28|13:17:35.569] Successfully wrote genesis state         database=chaindata hash="0dd27f…e308f9"
INFO [04-28|13:17:35.569] Allocated cache and file handles         database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/lightchaindata cache=16.00MiB handles=16
INFO [04-28|13:17:35.604] Writing custom genesis block
INFO [04-28|13:17:35.605] Persisted trie from memory database      nodes=0 size=0.00B time="6.571µs"  gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [04-28|13:17:35.606] Successfully wrote genesis state         database=lightchaindata hash="0dd27f…e308f9"

```

3. 新增目录和文件

观察到testnetdata/data00文件夹中多出两个新目录；

geth目录存储区块数据，keystore目录则保存账户信息；

其中geth目录中：

chaindata目录用来存放区块链数据；

lightchaindata目录用来以轻客户端模式存放区块链数据；

nodekey文件保存节点的唯一编号。

## 四、启动本地以太坊网络

```
nohup geth --miner.threads 1 --cache 512 --datadir testnetdata/data00 --networkid 8888 --nodiscover --port 40400 --verbosity 5 1>>$logdir/log_data_err_00 2>>testnetlog/log_data_info_00 &
```

将以上内容保存进starteth.sh脚本文件中，并赋予脚本可执行权限：

`chmod 777 starteth.sh`

执行以上脚本即可。

1. 参数说明

nohup command &  后台运行程序

--cache 512 挖矿程序内存设置 默认1024MB

--mine 允许geth启动时进行挖矿，需要与--miner.etherbase一起使用

--miner.etherbase ethaddr 指定挖矿收入地址，需要与--mine一起使用

--miner.threads 指定挖矿线程数，默认是4

--datadir testnetdata/data00 指定数据存储目录

--networkid port 指定geth节点网络ID

--nodiscover 不被其他节点发现

--ipcdisable 不允许ipc方式进行连接，可根据需要选择

--port 指定geth程序端口，默认30303

--http 开启http模块

--http.corsdomain "*" 允许跨域访问

--http.port 指定http通信端口，默认8545

--http.api eth,web3,admin,personal,net,miner,debug,ethash 指定http协议加载模块，可根据需要选择 

--verbosity 5 打印日志级别 0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail (default: 3)

1>>$logdir/log_data_err_00

2>>$logdir/log_data_info_00 指定geth正常日志追加目录

2. 查看日志目录下启动成功日志

```

INFO [04-28|13:48:44.920] Maximum peer count                       ETH=50 LES=0 total=50
DEBUG[04-28|13:48:44.922] FS scan times                            list="229.684µs" set="1.404µs" diff="8.888µs"
DEBUG[04-28|13:48:44.922] Sanitizing Go's GC trigger               percent=100
INFO [04-28|13:48:44.922] Set global gas cap                       cap=25000000
INFO [04-28|13:48:44.923] Allocated trie memory caches             clean=76.00MiB dirty=128.00MiB
TRACE[04-28|13:48:44.923] Started watching keystore folder         path=/Users/bulldoge/code/ethereum/testnetdata/data00/keystore
INFO [04-28|13:48:44.923] Allocated cache and file handles         database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata cache=256.00MiB handles=5120
DEBUG[04-28|13:48:44.990] Chain freezer table opened               database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata/ancient table=diffs items=0 size=0.00B
DEBUG[04-28|13:48:44.999] Chain freezer table opened               database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata/ancient table=headers items=0 size=0.00B
DEBUG[04-28|13:48:45.009] Chain freezer table opened               database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata/ancient table=hashes  items=0 size=0.00B
DEBUG[04-28|13:48:45.018] Chain freezer table opened               database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata/ancient table=bodies  items=0 size=0.00B
DEBUG[04-28|13:48:45.027] Chain freezer table opened               database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata/ancient table=receipts items=0 size=0.00B
INFO [04-28|13:48:45.027] Opened ancient database                  database=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/chaindata/ancient readonly=false
DEBUG[04-28|13:48:45.029] Current full block not old enough        number=0 hash="0dd27f…e308f9" delay=90000
INFO [04-28|13:48:45.030] Initialised chain configuration          config="{ChainID: 6666 Homestead: 0 DAO: <nil> DAOSupport: false EIP150: 0 EIP155: 0 EIP158: 0 Byzantium: 0 Constantinople: 0 Petersburg: 0 Istanbul: 0, Muir Glacier: <nil>, Berlin: <nil>, YOLO v3: <nil>, Engine: unknown}"
INFO [04-28|13:48:45.031] Disk storage enabled for ethash caches   dir=/Users/bulldoge/code/ethereum/testnetdata/data00/geth/ethash count=3
INFO [04-28|13:48:45.031] Disk storage enabled for ethash DAGs     dir=/Users/bulldoge/Library/Ethash count=2
INFO [04-28|13:48:45.031] Initialising Ethereum protocol           network=8888 dbversion=<nil>
WARN [04-28|13:48:45.031] Upgrade blockchain database version      from=<nil> to=8
INFO [04-28|13:48:45.034] Loaded most recent local header          number=0 hash="0dd27f…e308f9" td=131072 age=52y3w4d
INFO [04-28|13:48:45.034] Loaded most recent local full block      number=0 hash="0dd27f…e308f9" td=131072 age=52y3w4d
INFO [04-28|13:48:45.034] Loaded most recent local fast block      number=0 hash="0dd27f…e308f9" td=131072 age=52y3w4d
WARN [04-28|13:48:45.034] Failed to load snapshot, regenerating    err="missing or corrupted snapshot"
INFO [04-28|13:48:45.034] Rebuilding state snapshot
DEBUG[04-28|13:48:45.034] Journalled generator progress            progress=empty
DEBUG[04-28|13:48:45.035] Start snapshot generation                root="56e81f…63b421"
DEBUG[04-28|13:48:45.035] Reinjecting stale transactions           count=0
INFO [04-28|13:48:45.036] Regenerated local transaction journal    transactions=0 accounts=0
INFO [04-28|13:48:45.056] Allocated fast sync bloom                size=255.00MiB
INFO [04-28|13:48:45.057] Initialized state bloom                  items=0 errorrate=0.000 elapsed="69.135µs"
DEBUG[04-28|13:48:45.058] Recalculated downloader QoS values       rtt=20s confidence=1.000 ttl=1m0s
WARN [04-28|13:48:45.058] Error reading unclean shutdown markers   error="leveldb: not found"
INFO [04-28|13:48:45.058] Wiper running, state snapshotting paused accounts=0 slots=0 storage=0.00B elapsed=23.818ms
INFO [04-28|13:48:45.058] Starting peer-to-peer node               instance=Geth/v1.10.2-stable/darwin-amd64/go1.16.3
INFO [04-28|13:48:45.058] Deleted state snapshot leftovers         kind=accounts wiped=0 elapsed="52.962µs"
INFO [04-28|13:48:45.060] Deleted state snapshot leftovers         kind=storage  wiped=0 elapsed="81.941µs"
INFO [04-28|13:48:45.060] Compacting snapshot account area
DEBUG[04-28|13:48:45.113] IPCs registered                          namespaces=admin,debug,web3,eth,txpool,personal,ethash,miner,net
INFO [04-28|13:48:45.114] IPC endpoint opened                      url=/Users/bulldoge/code/ethereum/testnetdata/data00/geth.ipc
DEBUG[04-28|13:48:45.116] TCP listener up                          addr=[::]:40400
INFO [04-28|13:48:45.121] New local node record                    seq=1 id=76b8b028afc47c2f ip=127.0.0.1 udp=0 tcp=40400
INFO [04-28|13:48:45.121] Started P2P networking                   self="enode://9865976bea46f6bf6bbcf8fe476adcc2e654f678c33bdb34cb3b36a2cb77656b23f97a9ab44a589202972bfa667dee445892d55c8e0fa8a8df7cc32c451623db@127.0.0.1:40400?discport=0"
INFO [04-28|13:48:45.183] Mapped network port                      proto=tcp extport=40400 intport=40400 interface=NAT-PMP(192.168.1.1)
INFO [04-28|13:48:45.197] Compacting snapshot storage area
INFO [04-28|13:48:45.197] Compacted snapshot area in database      elapsed=136.922ms
INFO [04-28|13:48:45.198] Resuming state snapshot generation       root="56e81f…63b421" accounts=0 slots=0 storage=0.00B elapsed="4.699µs"
DEBUG[04-28|13:48:45.198] Journalled generator progress            progress=done
INFO [04-28|13:48:45.198] Generated state snapshot                 accounts=0 slots=0 storage=0.00B elapsed="265.747µs"
DEBUG[04-28|13:49:05.059] Recalculated downloader QoS values       rtt=20s confidence=1.000 ttl=1m0s
DEBUG[04-28|13:49:25.060] Recalculated downloader QoS values       rtt=20s confidence=1.000 ttl=1m0s

```

## 五、与节点交互

`geth --datadir 'testnetdata/data00' attach ipc:testnetdata/data00/geth.ipc`


## 六、开始挖矿

1. 检测geth是否处于挖矿状态
```
> eth.mining;
false
```
2. 设置挖矿收益地址
```
> miner.setEtherbase('0x80b695ce0ceb31e856c896e68a6f85ca39d8541e');
true
```
3. 查看挖矿地址
```
> eth.coinbase;
"0x80b695ce0ceb31e856c896e68a6f85ca39d8541e"
```
4. 查看挖矿地址余额情况
```
> eth.getBalance('0x80B695cE0cEB31e856c896E68A6F85ca39D8541e')
0
```
5. 查看区块高度
```
> eth.blockNumber
0
```
6. 写入coinbase挖矿信息
```
> miner.setExtra("https://github.com/bulldoge")
true
```
7. 开始挖矿，并在挖取一个区块后停止
```
> miner.start();admin.sleepBlocks(1);miner.stop();
null
```
8. 再次查看挖矿地址余额情况
```
> eth.getBalance('0x80B695cE0cEB31e856c896E68A6F85ca39D8541e')
2000000000000000000

```
9. 转换数据格式（从单位wei转为eth，便于阅读）
```
> web3.fromWei(2000000000000000000)
"2"
```
10. 再次查看区块高度
```
> eth.blockNumber
1
```
11. 查看挖到的区块信息

因为会有一个创世区块，以便后续区块延续其后，所以虽然指令是挖完一个区块后停止，但是其实是不将创世区块计算在内的；
并且由于挖矿提交速度太快，我已经指定单线程挖矿了，但是有时候这个指定的数量还是无法精确保证。
经查询创世区块配置文件中指定的coinbase地址上余额为0，因为创世区块配置文件中未alloc任何地址任何以太坊；

```

> web3.eth.getBlock(0)
{
  difficulty: 131072,
  extraData: "0x",
  gasLimit: 3141592,
  gasUsed: 0,
  hash: "0x0dd27f8800c26da4e87d3a358a63aadb84088d3f5647d491326430ccdfe308f9",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0xa994ad984690390aee4dd0b536721259cc361546",
  mixHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
  nonce: "0x0000000000000042",
  number: 0,
  parentHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
  receiptsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 507,
  stateRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  timestamp: 0,
  totalDifficulty: 131072,
  transactions: [],
  transactionsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  uncles: []
}
```
```
> web3.eth.getBlock(1)
{
  difficulty: 131072,
  extraData: "0x68747470733a2f2f6769746875622e636f6d2f62756c6c646f6765",
  gasLimit: 3144658,
  gasUsed: 0,
  hash: "0xcc95f16b997219ed888ec02d75219416e0714c02d89d7d692f14965117aa8d91",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0x80b695ce0ceb31e856c896e68a6f85ca39d8541e",
  mixHash: "0x1f8cb6a46578ff9e68e76687cdc3a19f0e4102232102f1ecf4feebe876b0993c",
  nonce: "0x0fd92a8b3209f710",
  number: 1,
  parentHash: "0x0dd27f8800c26da4e87d3a358a63aadb84088d3f5647d491326430ccdfe308f9",
  receiptsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 538,
  stateRoot: "0x6864993ec3ab060d06963d9f72419dfbe6a5afc44278c9695ea418dff6f58f40",
  timestamp: 1619589618,
  totalDifficulty: 262144,
  transactions: [],
  transactionsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  uncles: []
}

```

12. 查看block中extraData信息

从另外一个终端打开python3,输入以下命令：

```

python3
Python 3.7.6 (default, Dec 27 2019, 09:51:21)
[Clang 11.0.0 (clang-1100.0.33.16)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import binascii
>>> print(binascii.a2b_hex("68747470733a2f2f6769746875622e636f6d2f62756c6c646f6765").decode("utf8"))

https://github.com/bulldoge

```

## 七、结束交互界面

`ctrl + d`

## 八、关闭geth节点

```

ps -ef|grep geth

kill -9 pid

```
## 九、ethereumtestnet.sh脚本

```

mkdir -p testnetdata/data00
mkdir testnetlog

echo '{"config": {"chainId": 6666,"homesteadBlock": 0,"eip150Block": 0,"eip155Block": 0,"eip158Block": 0,"byzantiumBlock": 0,"constantinopleBlock": 0,"petersburgBlock": 0,"istanbulBlock": 0},"alloc": {},"coinbase": "0xa994AD984690390AEE4DD0B536721259cC361546","difficulty": "0x20000","extraData": "","gasLimit": "0x2fefd8","nonce": "0x0000000000000042","mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000","parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000","timestamp": "0x00"}' > testnetdata/genesis.json

geth --datadir testnetdata/data00 init testnetdata/genesis.json

nohup geth --cache 512 --miner.threads 1 --datadir testnetdata/data00 --networkid 8888 --nodiscover --port 40400 --verbosity 5 1>>testnetlog/log_data_err_00 2>>testnetlog/log_data_info_00 &

```
