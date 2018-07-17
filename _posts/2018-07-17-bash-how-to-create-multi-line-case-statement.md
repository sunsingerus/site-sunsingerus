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
What if you'd like to have multi-line case statement?
Here is an example:
<pre>
#!/bin/bash

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
Mainly, it is multi-line version of
<pre>
case "$A" in
        A | B | C )
                echo $A
                ;;
        *)
                echo "Unknown"
                ;;
esac
</pre>
and provides the most benefits when there are really many options to choose from.