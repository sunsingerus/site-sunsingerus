---
ID: 190
post_title: 'Setup Ethereum Environment &#8211; Ganache'
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/setup-ethereum-environment-ganache/
published: true
post_date: 2017-12-23 19:19:59
---
<h5>Introduction</h5>
What is <strong>Ganache</strong>?
Ganache is your personal blockchain for Ethereum development.
Available on <a href="https://github.com/trufflesuite/ganache" target="_blank" rel="noopener">github</a>

<h5>Download</h5>
Download Ganache <a href="https://github.com/trufflesuite/ganache/releases/latest" target="_blank" rel="noopener">latest release</a>. We'll use <code>ganache-1.0.1-x86_64.AppImage</code>.
It is an executable file,
<pre>user@cinnamon ~/Downloads $ file ganache-1.0.1-x86_64.AppImage 
ganache-1.0.1-x86_64.AppImage: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.18, BuildID[sha1]=238d4487ce2f48422f53b58c579757c9e630a1ac, stripped
</pre>
so let's setup correct attributes
<pre>user@cinnamon ~/Downloads $ chmod a+x ganache-1.0.1-x86_64.AppImage 
</pre>

<h5>Launch</h5>
and just launch Ganache as
<pre>user@cinnamon ~/Downloads $ ./ganache-1.0.1-x86_64.AppImage 
</pre>

For the following question feel free to answer "No", it means you'll need to run it manually, which is ok for now.
<img class="alignnone size-full wp-image-195" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_1.png" alt="" width="665" height="250" />

<h5>GUI</h5>
Ganache GUI is quite self-explanatory.
Accounts tab:
<img class="alignnone size-full wp-image-194" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_2.png" alt="" width="1202" height="500" />

Transactions tab:
<img class="alignnone size-full wp-image-193" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_3.png" alt="" width="1202" height="654" />

<h5>RPC connect point</h5>
Ganache exposes RPC on <code>http://127.0.0.1:7545</code>
<pre>
cinnamon ~ # netstat -antp|grep Ganache
tcp        0      0 127.0.0.1:7545          0.0.0.0:*               LISTEN      16588/Ganache   
</pre>

<h5>Connect with MetaMask</h5>
Connect MetaMask to running Ganache:
<img class="alignnone size-medium wp-image-199" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_metamask.png" alt="" width="180" height="300" />

And you can see the same accounts both in Ganache and MetaMask
<img class="alignnone size-full wp-image-198" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_accounts.png" alt="" width="1080" height="300" />

ganache provides very nice GUI to explore Transactions:
<img class="alignnone size-full wp-image-192" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_4.png" alt="" width="1202" height="400" />

So it is easy to add new tokens in MetaMask
<img class="alignnone size-full wp-image-191" src="http://sunsingerus.com/wp-content/uploads/2017/12/ganache_5.png" alt="" width="730" height="400" />