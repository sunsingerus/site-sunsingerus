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
<code>
mainnet: ~/.ethereum/keystore
ropsten: ~/.ethereum/testnet/keystore
rinkeby: ~/.ethereum/rinkeby/keystore
</code>

Each of these directories contains files like the following:
<code>
UTC--2017-11-26T08-09-02.536023214Z--164619fcbcdf6e4ef1e3db1dc0021bc2d910104b
UTC--2017-12-02T16-26-59.253668139Z--8d7e31f97f6b422a5ea01e936788741fb096afe9
UTC--2017-12-02T16-31-58.652789498Z--8397cd797e2627d2ccf3ef2d2182bc1bacefaebc
</code>

You can backup the entire /ethereum directory with all chaindata files - which requires much more free space. On the other hand, you'll save some time on downloading cbaindata after restroing backup
To import saved account/wallet files, just copy them into the new keystore directory