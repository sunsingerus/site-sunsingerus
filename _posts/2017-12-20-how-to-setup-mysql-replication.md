---
ID: 148
post_title: How To Setup MySQL Replication
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-setup-mysql-replication/
published: true
post_date: 2017-12-20 12:30:45
---
<h5>Configuration file on Master</h5>
Edit <code>my.cnf</code>
<pre># MANDATORY. Master ID. Random unique number.
server-id = 1

# MANDATORY. Where to write MySQL's binary log
log_bin = /var/lib/mysql/bin.log

# OPTIONAL. Which DB to replicate.
binlog_do_db = db_name
</pre>
Restart MySQL
<pre>/etc/init.d/mysql restart
</pre>

<h5>User on Master</h5>
<pre>GRANT REPLICATION SLAVE ON *.* TO 'replication_user'@'%' IDENTIFIED BY 'qwerty';
FLUSH PRIVILEGES;
</pre>

<h5>Check Master Status</h5>
<pre>
SHOW MASTER STATUS;
</pre>
<pre>
mysql> SHOW MASTER STATUS;
+----------+--------+------------+------------------+
| File     |Position|Binlog_Do_DB| Binlog_Ignore_DB |
+----------+--------+------------+------------------+
|bin.000001|     123|  db_name   |                  |
+----------+--------+------------+------------------+
1 row in set (0.00 sec)
</pre>
<code>File</code> and <code>Position</code> field values (<code>bin.000001</code> and <code>123</code> respectively) are important and will be used later - on Slave during <strong>Start Replication on Slave</strong> procedure.

<h5>Migrate data from Master to Slave</h5>
<h6>On Master</h6>
<pre>
USE db_name;
FLUSH TABLES WITH READ LOCK;
</pre>
<pre>
mysqldump -u root -p db_name > db_name.sql
</pre>

<pre>
UNLOCK TABLES;
</pre>
<h6>On Slave</h6>

<pre>
CREATE DATABASE db_name;
</pre>
<pre>
mysql -u root -p db_name < db_name.sql
</pre>

<h5>Configuration file on Slave</h5>
<pre>
# MANDATORY. Slave ID. Random unique number.
server-id = 2

# MANDATORY. Where to write MySQL's replication/relay binary log
relay-log = /var/lib/mysql/relay-bin.log

# MANDATORY. Where to read MySQL Master's binary log
# MUST BE THE SAME as in Master's config
log_bin = /var/lib/mysql/bin.log

# OPTIONAL. Which DB to replicate.
binlog_do_db = db_name
</pre>

<h5>Start Replication on Slave</h5>
<pre>
CHANGE MASTER TO MASTER_HOST='10.10.0.1', MASTER_USER='replication_user', MASTER_PASSWORD='qwerty', MASTER_LOG_FILE = 'bin.000001', MASTER_LOG_POS = 123;
</pre>
<pre>
START SLAVE;
SHOW SLAVE STATUS;
</pre>