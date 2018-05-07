---
ID: 442
post_title: Ubuntu. Old Kernels Use Disk Space
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/ubuntu-old-kernels-use-disk-space/
published: true
post_date: 2018-05-07 10:29:45
---
Ubuntu accumulates installed kernels, and, in some time, it consumes a lot of disk space. Here is an example:
<pre>
user@ubuntu: sudo du -sh /lib/modules/* /usr/src/* 2>/dev/null
209M    /lib/modules/4.4.0-101-generic
209M    /lib/modules/4.4.0-103-generic
209M    /lib/modules/4.4.0-104-generic
209M    /lib/modules/4.4.0-108-generic
209M    /lib/modules/4.4.0-112-generic
212M    /lib/modules/4.4.0-116-generic
209M    /lib/modules/4.4.0-96-generic
209M    /lib/modules/4.4.0-97-generic
209M    /lib/modules/4.4.0-98-generic
106M    /usr/src/linux-headers-4.4.0-101
15M     /usr/src/linux-headers-4.4.0-101-generic
106M    /usr/src/linux-headers-4.4.0-103
15M     /usr/src/linux-headers-4.4.0-103-generic
106M    /usr/src/linux-headers-4.4.0-104
15M     /usr/src/linux-headers-4.4.0-104-generic
106M    /usr/src/linux-headers-4.4.0-108
15M     /usr/src/linux-headers-4.4.0-108-generic
106M    /usr/src/linux-headers-4.4.0-112
15M     /usr/src/linux-headers-4.4.0-112-generic
106M    /usr/src/linux-headers-4.4.0-116
15M     /usr/src/linux-headers-4.4.0-116-generic
106M    /usr/src/linux-headers-4.4.0-96
15M     /usr/src/linux-headers-4.4.0-96-generic
106M    /usr/src/linux-headers-4.4.0-97
15M     /usr/src/linux-headers-4.4.0-97-generic
106M    /usr/src/linux-headers-4.4.0-98
15M     /usr/src/linux-headers-4.4.0-98-generic
</pre>
There is not much kernels installed, but in long-running system this list can be much longer. So, we'd like to clean old kernels and free some space.

The simplest way possible for 16.04 and newer versions of Ubuntu is:
<pre>
sudo apt autoremove
</pre>

However, <code>autoremove</code> is not perfect, and sometimes it does not clean all old kernels. So, we can do it manually.


Check what kernel version we are running:
<pre>
user@ubuntu: uname -r
4.4.0-112-generic
</pre>

Looks like we can remove old kernels. Let's keep couple of latest, thus we can remove 4.4.0-96 4.4.0-97 4.4.0-98 kernels .

<pre>
user@ubuntu: sudo apt purge '*4.4.0-96*' '*4.4.0-96*' '*4.4.0-98*'
</pre>

That's all!