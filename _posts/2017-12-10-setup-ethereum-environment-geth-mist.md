---
ID: 10
post_title: 'Setup Ethereum Environment &#8211; geth, Mist'
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/setup-ethereum-environment-geth-mist/
published: true
post_date: 2017-12-10 16:42:43
---
<h1>Install geth</h1>
Enable PPA repo
<pre class="prettyprint">
sudo add-apt-repository -y ppa:ethereum/ethereum
</pre>
Install geth
<pre class="prettyprint">
sudo apt-get update
sudo apt-get install ethereum
</pre>
<h1>Restore accounts from backup</h1>
as <a href="http://sunsingerus.com/backup-and-restore-ethereum-accountswallets/" target="_blank" rel="noopener">described here</a>
<h1>Install Mist</h1>
Download Mist distro from <a href="https://github.com/ethereum/mist/releases" target="_blank" rel="noopener">releases</a> page and install it
<pre class="prettyprint">
wget https://github.com/ethereum/mist/releases/download/v0.9.3/Mist-linux64-0-9-3.deb
sudo apt-get install ./Mist-linux64-0-9-3.deb
</pre>

<h1>Setup Launch Scripts</h1>
<pre class="prettyprint">
./mist-network-test.sh
</pre>