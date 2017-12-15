---
ID: 71
post_title: How To Install MySQL on CentOS 7
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-install-mysql-on-centos-7/
published: true
post_date: 2017-12-12 11:45:00
---
<pre class="prettyprint">sudo yum install -y https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
</pre>
<pre class="prettyprint">[user@localhost ~]$ yum list 'mysql-community*'
Installed Packages
mysql-community-common.x86_64          5.7.20-1.el7 @mysql57-community
mysql-community-devel.x86_64           5.7.20-1.el7 @mysql57-community
mysql-community-libs.x86_64            5.7.20-1.el7 @mysql57-community
mysql-community-libs-compat.x86_64     5.7.20-1.el7 @mysql57-community
Available Packages
mysql-community-client.x86_64          5.7.20-1.el7 mysql57-community
mysql-community-embedded.x86_64        5.7.20-1.el7 mysql57-community
mysql-community-embedded-compat.x86_64 5.7.20-1.el7 mysql57-community
mysql-community-embedded-devel.x86_64  5.7.20-1.el7 mysql57-community
mysql-community-release.noarch         el7-7        mysql57-community
mysql-community-server.x86_64          5.7.20-1.el7 mysql57-community
mysql-community-test.x86_64            5.7.20-1.el7 mysql57-community
</pre>
<pre class="prettyprint">sudo yum install -y mysql-community-devel
</pre>