---
ID: 359
post_title: >
  How To Download RPM and All Dependencies
  with YUM
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-download-rpm-and-all-dependencies-with-yum/
published: true
post_date: 2018-01-23 18:04:58
---
Install <code>yum-plugin-downloadonly</code>
<pre>
yum install yum-plugin-downloadonly
</pre>

Suppose we'd like to download ClickHouse RPMs and all dependencies
<pre>
yum install --downloadonly --downloaddir=. $(yum deplist 'clickhouse*'|grep provider|sort|uniq|awk '{print $2}')
</pre>