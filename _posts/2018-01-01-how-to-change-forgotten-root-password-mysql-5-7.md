---
ID: 244
post_title: >
  How To Change Forgotten root Password
  MySQL 5.7
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-change-forgotten-root-password-mysql-5-7/
published: true
post_date: 2018-01-01 13:19:54
---
Stop <code>mysqld</code>
<pre>
sudo systemctl stop mysqld
</pre>
Run <code>mysqld</code> with <code>--skip-grant-tables</code> option
<pre>
sudo -u mysql /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid --skip-grant-tables
</pre>
Now we can run <code>mysql</code> client without password. Start <code>mysql</code> client and update <code>root</code> password

<pre>
UPDATE mysql.user SET authentication_string=PASSWORD('qwerty') WHERE user='root';
</pre>
Do not forget to
<pre>
FLUSH PRIVILEGES;
</pre>

Now we can stop running instance of mysql
<pre>
sudo kill $(sudo cat /var/run/mysqld/mysqld.pid)
</pre>
And start <code>mysqld</code> as usual
<pre>
sudo systemctl start mysqld
</pre>
Login with new password
<pre>
mysql -uroot -pqwerty
</pre>

You may encounter the following error
<pre>
ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement. 
</pre>

Just setup a new decent password asa
<pre>
SET PASSWORD = PASSWORD('qwerty');
</pre>

You may encounter the following error
<pre>
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
</pre>
in case provieded password is too simple. 
<pre>
SET PASSWORD = PASSWORD('Qwerty1#');
</pre>