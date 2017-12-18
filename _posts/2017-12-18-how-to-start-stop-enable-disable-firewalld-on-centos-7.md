---
ID: 125
post_title: >
  How To start/stop enable/disable
  Firewalld on CentOS 7
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-start-stop-enable-disable-firewalld-on-centos-7/
published: true
post_date: 2017-12-18 08:30:06
---
Difference between stop and disable:
<ul>
 	<li>stop - shutdown the service now</li>
 	<li>disable - do not run on system start</li>
</ul>
It you' d like to turn it off and do not see it again - stop and disable.

The same with start and enable:
<ul>
 	<li>start - launch the service now</li>
 	<li>enable - run on system start</li>
</ul>
Completely turn it off
<pre>systemctl stop firewalld
systemctl disable firewalld
</pre>
Turn it on:
<pre>systemctl enable firewalld
systemctl start firewalld
</pre>