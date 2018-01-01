---
ID: 240
post_title: How To Install ClickHouse on CentOS
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-install-clickhouse-on-centos/
published: true
post_date: 2018-01-01 11:41:31
---
Ensure we have <code>curl</code> installed
<pre>
sudo yum install -y curl
</pre>
Setup Altinity's repo from packagecloud
<pre>
curl -s https://packagecloud.io/install/repositories/altinity/clickhouse/script.rpm.sh | sudo bash
</pre>
Install
<pre>
sudo yum install -y 'clickhouse*'
</pre>