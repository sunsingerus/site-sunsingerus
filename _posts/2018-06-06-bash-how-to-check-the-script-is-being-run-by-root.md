---
ID: 487
post_title: >
  BASH. How To Check the Script is Being
  Run by Root
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/bash-how-to-check-the-script-is-being-run-by-root/
published: true
post_date: 2018-06-06 09:24:36
---
There are two ways at the moment.
Classic style
<pre>
if [ "$(id -u)" != "0" ]; then
   echo "Need to be root" 1>&2
   exit 1
fi
</pre>

or BASH-specific style
<pre>
if [[ $EUID -ne 0 ]]; then
   echo "Need to be root" 1>&2
   exit 1
fi
</pre>