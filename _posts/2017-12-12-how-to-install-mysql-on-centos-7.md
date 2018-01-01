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
<pre>
sudo yum install -y mysql-community-devel mysql-community-server
sudo systemctl start mysqld
sudo mysql_secure_installation
</pre>
Check available packages:
<pre class="prettyprint">[user@localhost ~]$ yum list 'mysql-community*'</pre>