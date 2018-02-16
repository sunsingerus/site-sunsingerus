---
ID: 414
post_title: How To Update Time With ntp?
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-update-time-with-ntp/
published: true
post_date: 2018-02-16 10:58:42
---
In case we need to update time with <code>mtp</code> just run
<pre>
sudo bash -c "service ntp stop && ntpdate time.nist.gov && service ntp start && date"
</pre>