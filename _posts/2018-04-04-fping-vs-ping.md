---
ID: 423
post_title: fping vs ping
author: sunsingerus
post_excerpt: ""
layout: post
permalink: https://sunsingerus.com/fping-vs-ping/
published: true
post_date: 2018-04-04 08:36:22
---
<code>fping</code> is a program like <code>ping</code>. The main difference from <code>ping</code> in that you can specify any number of targets on the command line, or specify a file containing the lists of targets to ping.
Example:
<pre>
fping -as nohost.example.com google.com yahoo.com
</pre>
where
-a   Show systems that are alive
-s   Print cumulative statistics upon exit.
<pre>
fping -as nohost.example.com google.com yahoo.com
nohost.example.com: Name or service not known
google.com
yahoo.com

       2 targets
       2 alive
       0 unreachable
       1 unknown addresses

       0 timeouts (waiting for response)
       2 ICMP Echos sent
       2 ICMP Echo Replies received
       0 other ICMP received

 33.3 ms (min round trip time)
 100 ms (avg round trip time)
 167 ms (max round trip time)
        0.193 sec (elapsed real time)
</pre>