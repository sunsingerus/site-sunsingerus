---
ID: 255
post_title: How To Use pkg-config
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-use-pkg-config/
published: true
post_date: 2018-01-02 21:07:14
---
<h5>What is it</h5>
Main purpose of <code>pkg-config</code> tool is to provide details about installed libraries. Those details are stored in <code>pkg-config</code> files which have <code>.pc</code> suffix and typically reside in <code>/usr/lib/pkgconfig</code> and <code>/usr/share/pkgconfig</code> directories. <code>pkg-config</code> understands <code>PKG_CONFIG_PATH</code> environment variable which contains list of directories, where to search for <code>.pc</code> files.

<h5>Internals</h5>
Example <code>.pc</code> file:

<pre>
prefix=/usr/local
exec_prefix=${prefix}
includedir=${prefix}/include
libdir=${exec_prefix}/lib

Name: bar
Description: The Bar library
Version: 1.2.3
Requires.private: foo >= 0.9
Cflags: -I${includedir}/bar
Libs: -L${libdir} -lbar
</pre>

This file contains location of <code>libdir</code>, <code>includedir</code> and dependencies via <code>Requires.private</code> specification

<h5>Examples</h5>

In order to print link flags, use the <code>--libs</code> option.
<pre>
$ pkg-config --libs bar
-lbar
</pre>
For static link use <code>--static</code> option
<pre>
$ pkg-config --libs --static bar
-lbar -lfoo
</pre>
For static link we have two libs specified - <code>bar</code> and <code>foo</code> - meaning <code>bar</code> depends on <code>foo</code> and thus we have to link both of them into executable

Print compiler flags
<pre>
$ pkg-config --cflags bar
-I/usr/include/bar
</pre>
And static version:
<pre>
$ pkg-config --cflags --static bar
-I/usr/include/bar
</pre>

Another option - <code>--exists</code>, can be used to test for a lib's availability.
<pre>
$ pkg-config --exists bar
$ echo $?
0
</pre>

<code>pkg-config</code> also provides nice version checking.

<pre>
$ pkg-config --libs "bar >= 1.5"
Requested 'bar >= 1.5' but version of bar is 1.2.3
</pre>