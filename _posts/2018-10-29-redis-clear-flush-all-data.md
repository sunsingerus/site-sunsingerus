---
ID: 527
post_title: Redis. Clear/Flush all data
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/redis-clear-flush-all-data/
published: true
post_date: 2018-10-29 18:28:51
---
Redis provides plain-text API. Issue <strong>FLUSHALL</strong> command to flush all data.

<code>echo "FLUSHALL" |  nc 127.0.0.1 6379</code>