---
ID: 121
post_title: How To Clone Git Repo with Submodules
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-clone-git-repo-with-submodules/
published: true
post_date: 2017-12-17 19:02:55
---
For already cloned repo:
<pre>
git submodule update --init --recursive
</pre>
OR
Clone repo with all submodules:
<pre>
git clone --recursive https://github.com/sunsingerus/eth-dapp-petshop
</pre>