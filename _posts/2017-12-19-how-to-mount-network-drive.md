---
ID: 142
post_title: How To Mount Network Drive
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-mount-network-drive/
published: true
post_date: 2017-12-19 09:46:12
---
<strong>List windows shares</strong> on desired host.

For anonymous list use:
<pre>smbclient -N -L //192.168.1.41
</pre>
If you need to specify username use:
<pre>smbclient -L //192.168.1.41 -U user
</pre>
We'll see output like the following:
<pre>	Sharename       Type      Comment
	---------       ----      -------
	Volume_1        Disk      
	IPC$            IPC       IPC Service (DNS-320L)
	lp              Printer   USB Printer
</pre>
<strong>Mount share</strong> <code>Volume_1</code> to <code>/media/nas</code>
<pre>sudo mount -t cifs //192.168.1.41/Volume_1 -o username=user,password=qwerty /media/nas
</pre>