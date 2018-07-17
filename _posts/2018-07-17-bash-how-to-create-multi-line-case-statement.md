---
ID: 511
post_title: >
  BASH. How To Create Multi-line CASE
  Statement
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/bash-how-to-create-multi-line-case-statement/
published: true
post_date: 2018-07-17 11:11:05
---
What if you'd like to have multi0line case statement?
Here is an example:
<pre>
A=C

case "$A" in
        A | \
        B | \
        C )
                echo $A
                ;;
        *)
                echo "Unknown"
                ;;
esac
</pre>