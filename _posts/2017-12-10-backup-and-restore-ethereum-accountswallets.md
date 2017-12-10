---
ID: 14
post_title: >
  Backup and restore Ethereum
  accounts/wallets
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/backup-and-restore-ethereum-accountswallets/
published: true
post_date: 2017-12-10 16:59:03
---
In order to backup ethereum accounts (wallets) just make a copy of the key files located in your ethereum directory. On Linux it would be the following dirs (for different networks respectively):
[code language="bash" title="mainnet"]
~/.ethereum/keystore
[/code]
[code language="bash" title="ropsten"]
~/.ethereum/testnet/keystore
[code language="bash" title="rinkeby"]
~/.ethereum/rinkeby/keystore
[/code]

Each of these directories contains files like the following:
[code language="bash"]
UTC--2017-11-26T08-09-02.536023214Z--164619fcbcdf6e4ef1e3db1dc0021bc2d910104b
UTC--2017-12-02T16-26-59.253668139Z--8d7e31f97f6b422a5ea01e936788741fb096afe9
UTC--2017-12-02T16-31-58.652789498Z--8397cd797e2627d2ccf3ef2d2182bc1bacefaebc
[/code]

[code language=bash]
mkdir -p ~/.ethereum/testnet/keystore/
chmod 700 ~/ethereum
chmod 700 ~/ethereum/testnet
chmod 700 ~/ethereum/testnet/keystore

rw------- 1 user user  491 Dec 10 20:28 UTC--2017-11-26T08-09-02.536023214Z--164619fcbcdf6e4ef1e3db1dc0021bc2d910104b
-rw------- 1 user user  491 Dec 10 20:28 UTC--2017-12-02T16-26-59.253668139Z--8d7e31f97f6b422a5ea01e936788741fb096afe9
-rw------- 1 user user  491 Dec 10 20:28 UTC--2017-12-02T16-31-58.652789498Z--8397cd797e2627d2ccf3ef2d2182bc1bacefaebc

./geth-ropsten-account-list.sh 
Account #0: {164619fcbcdf6e4ef1e3db1dc0021bc2d910104b} keystore:///home/user/.ethereum/testnet/keystore/UTC--2017-11-26T08-09-02.536023214Z--164619fcbcdf6e4ef1e3db1dc0021bc2d910104b
Account #1: {8d7e31f97f6b422a5ea01e936788741fb096afe9} keystore:///home/user/.ethereum/testnet/keystore/UTC--2017-12-02T16-26-59.253668139Z--8d7e31f97f6b422a5ea01e936788741fb096afe9
Account #2: {8397cd797e2627d2ccf3ef2d2182bc1bacefaebc} keystore:///home/user/.ethereum/testnet/keystore/UTC--2017-12-02T16-31-58.652789498Z--8397cd797e2627d2ccf3ef2d2182bc1bacefaebc

./geth-ropsten-run.sh 
INFO [12-10|20:33:30] Starting peer-to-peer node               instance=Geth/v1.7.3-stable-4bb3c89d/linux-amd64/go1.9
INFO [12-10|20:33:30] Allocated cache and file handles         database=/home/user/.ethereum/testnet/geth/chaindata cache=1024 handles=1024
INFO [12-10|20:33:30] Writing custom genesis block 
INFO [12-10|20:33:30] Initialised chain configuration          config="{ChainID: 3 Homestead: 0 DAO: <nil> DAOSupport: true EIP150: 0 EIP155: 10 EIP158: 10 Byzantium: 1700000 Engine: ethash}"
INFO [12-10|20:33:30] Disk storage enabled for ethash caches   dir=/home/user/.ethereum/testnet/geth/ethash count=3
INFO [12-10|20:33:30] Disk storage enabled for ethash DAGs     dir=/home/user/.ethash                       count=2
INFO [12-10|20:33:30] Initialising Ethereum protocol           versions="[63 62]" network=3
INFO [12-10|20:33:30] Loaded most recent local header          number=0 hash=419410…ca4a2d td=1048576
INFO [12-10|20:33:30] Loaded most recent local full block      number=0 hash=419410…ca4a2d td=1048576
INFO [12-10|20:33:30] Loaded most recent local fast block      number=0 hash=419410…ca4a2d td=1048576
INFO [12-10|20:33:30] Regenerated local transaction journal    transactions=0 accounts=0
INFO [12-10|20:33:30] Starting P2P networking 
INFO [12-10|20:33:32] UDP listener up                          self=enode://f7463f0e1af193fe673960d3199d58d6ce0268ec0d8501dfffc7501234a9557a0f201886fb0d1775f4770cbda2c5db7b49c95b2413a9f6c137d1abd446465796@[::]:30303
INFO [12-10|20:33:32] RLPx listener up                         self=enode://f7463f0e1af193fe673960d3199d58d6ce0268ec0d8501dfffc7501234a9557a0f201886fb0d1775f4770cbda2c5db7b49c95b2413a9f6c137d1abd446465796@[::]:30303
INFO [12-10|20:33:32] IPC endpoint opened: /home/user/.ethereum/geth.ipc 
INFO [12-10|20:33:32] HTTP endpoint opened: http://0.0.0.0:8545 
Welcome to the Geth JavaScript console!

instance: Geth/v1.7.3-stable-4bb3c89d/linux-amd64/go1.9
coinbase: 0x164619fcbcdf6e4ef1e3db1dc0021bc2d910104b
at block: 0 (Thu, 01 Jan 1970 03:00:00 MSK)
 datadir: /home/user/.ethereum/testnet
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

> 

INFO [12-10|20:34:12] Block synchronisation started 


user@mint182 ~/dev/eth-misc-scripts $ du -sh ~/.ethereum/testnet/geth/chaindata/
46M	/home/user/.ethereum/testnet/geth/chaindata/


You can backup the entire /ethereum directory with all chaindata files - which requires much more free space. On the other hand, you'll save some time on downloading cbaindata after restroing backup
To import saved account/wallet files, just copy them into the new keystore directory