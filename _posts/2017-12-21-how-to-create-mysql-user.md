---
ID: 170
post_title: How To Create MySQL User
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-create-mysql-user/
published: true
post_date: 2017-12-21 16:26:28
---
<h5>Introduction</h5>
Suppose we'd like to have MySQL user, able to access MySQL from all hosts of the network.
<pre>
CREATE USER 'testuser'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'testuser'@'%';
FLUSH PRIVILEGES;
</pre>

All looks fine - <code>'testuser'@'%'</code> indeed means 'from all hosts'
However, there is a subtle nuance. Attempt to login with <code>testuser </code> locally (i.e. from the same server where MySQL is running) fails.

<pre>
[user@localhost ~]$ mysql -utestuser -ppassword
Warning: Using a password on the command line interface can be insecure.
ERROR 1045 (28000): Access denied for user 'testuser'@'localhost' (using password: YES)
</pre>

On the other hand, the same user can login from non-localhost
<pre>
[user@druid ~]$ mysql -h192.168.74.136 -utestuser -ppassword
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 502
Server version: 5.6.38-log MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
</pre>

<h5>So, what's going on?</h5>
The issue at hand is an <strong>anonymous user for localhost</strong>. It takes precedence when 'testuser' connects from the localhost. Why so? The reason for this is that the anonymous user has a more specific <code>hostname</code> specified than the <code>'%'</code> and thus comes earlier in the user table sort order. Let's take a look on this anonymous user:
<pre>
mysql> SELECT Host, User, Password FROM mysql.user WHERE user = '';
+-----------------------+------+----------+
| Host                  | User | Password |
+-----------------------+------+----------+
| localhost             |      |          |
| localhost.localdomain |      |          |
+-----------------------+------+----------+
</pre>

<h5>Solution</h5>
Explicitly create user on localhost in addition to 'user from all hosts'
<pre>
CREATE USER 'testuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'testuser'@'localhost';

CREATE USER 'testuser'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'testuser'@'%';

FLUSH PRIVILEGES;
</pre>

Now all is OK
<pre>
[user@localhost ~]$ mysql -utestuser -ppassword
Warning: Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 505
Server version: 5.6.38-log MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
</pre>