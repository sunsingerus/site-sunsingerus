---
ID: 81
post_title: How To Install gcc 7 on CentsOS 6/7
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-install-gcc-7-on-centsos-6-7/
published: true
post_date: 2017-12-15 10:35:04
---
<a href="https://www.softwarecollections.org/en/scls/rhscl/devtoolset-7/" target="_blank" rel="noopener">Software Collections</a> rpm is distributed with CentOS
<pre class="prettyprint">sudo yum install centos-release-scl
</pre>
For the whole collection just install:
<pre class="prettyprint">sudo yum install devtoolset-7
</pre>
Or you can choose components:
<pre class="prettyprint">sudo yum install devtoolset-7-gcc-7.2.1 devtoolset-7-gcc-c++-7.2.1
</pre>

Enable SCLs - for convenient usage
<pre class="prettyprint">scl enable devtoolset-7 bash
</pre>

In practice, it means start a new <code>bash</code> instance and call <code>/opt/rh/devtoolset-7/enable</code> which exports <code>PATH</code>s
Like the following:
<pre>
 \_ -bash
   \_ scl enable devtoolset-7 bash
     \_ /bin/bash /var/tmp/sclgiIFjh
       \_ bash
</pre>

Of course, <code>gcc</code> can be used by its full path <code>/opt/rh/devtoolset-7/root/usr/bin/gcc</code> or by adding <code>/opt/rh/devtoolset-7/root/usr/bin</code> to <code>PATH</code>