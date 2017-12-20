---
ID: 146
post_title: How To Check If a Directory Exists
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-check-if-a-directory-exists/
published: true
post_date: 2017-12-20 08:53:54
---
<pre>
if [ -d "$DIR" ]; then
    # $DIR exists
else
    # $DIR does not exist
fi
</pre>

<pre>
if [ ! -d "$DIR" ]; then
    # $DIR does not exist
else
    # $DIR exists
fi
</pre>