---
ID: 378
post_title: How To Configure SSH
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-configure-ssh/
published: true
post_date: 2018-02-01 09:50:19
---
<h1>Key-Based Authentication</h1>
Generate key pair
<pre>
ssh-keygen -t rsa -b 2048
</pre>
<pre>
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
</pre>
In case passphrase specified - it will be asked each time key accessed. For example, ssh login will ask not for remote server's password, but for local passphrase, like the following:
<pre>
Enter passphrase for key '/home/user/.ssh/id_rsa':
</pre>
Verify keys generated
<pre>
ls -lh ~/.ssh
total 8.0K
-rw------- 1 user user 1.7K Jan 31 13:02 id_rsa
-rw-r--r-- 1 user user  408 Jan 31 13:02 id_rsa.pub
</pre>

<pre>
cat ~/.ssh/id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAsfPlP02eB8Dt1W9hA2uw0pS6QAARHIrHF8CojHb8cL3tExog
... cut ...
q+nen95Z+cKN+Falxf+IdNxxlRtGuElernIGh7W1hA+/e5rqwZk=
-----END RSA PRIVATE KEY-----
</pre>

<pre>
cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3Nz ... cut ...
</pre>

Now we need to copy public key to remote server. This can be done either by <code>ssh-copy-id</code> tool.
Short form - just call it with remote server specified and it will copy <code>.ssh/id_rsa.pub</code> file
<pre>
ssh-copy-id 192.168.74.142
</pre>
<pre>
INFO: Source of key(s) to be installed: "/home/user/.ssh/id_rsa.pub"
</pre>
Extended form - explicitly specify key file to copy
<pre>
ssh-copy-id -i $HOME/.ssh/id_rsa.pub USER@192.168.1.198
</pre>

Or we can copy key file manually and setup correct access privileges
<pre>
ssh user@192.168.74.142 'mkdir -p .ssh'
cat ~/.ssh/id_rsa.pub | ssh user@192.168.74.142 'cat >> .ssh/authorized_keys'
ssh user@192.168.74.142 'chmod 700 .ssh && chmod 600 .ssh/authorized_keys'
</pre>

<h1>Tune SSH server</h1>
Turn off password authentication. It can be done now - we have key-based authentication configured
Edit <code>/etc/ssh/sshd_config</code> file
<pre>
PasswordAuthentication no
</pre>


Protocol 2

PermitRootLogin no

Port 2200

<pre>
AllowUsers = *@123.123.123.123
</pre>

<pre>
sudo service ssh restart
</pre>