---
ID: 128
post_title: >
  How To Check Whether Bash Parameter is
  Set
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-check-whether-bash-parameter-is-set/
published: true
post_date: 2017-12-18 12:21:54
---
<pre>function test()
{
        if [ -z ${1+x} ]; then
                echo "param 1 is unset"
... more code ...
        else
                echo "param 1 is set to $1"
... more code ...
        fi
}
</pre>
where ${1+x} is a first function parameter <a href="http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_06_02" target="_blank" rel="noopener">expansion</a> (check <code>${parameter+word}</code> explanation)

call function as
<pre>test
</pre>
or
<pre>test qweqwe
</pre>