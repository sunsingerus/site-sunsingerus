---
ID: 64
post_title: How To Install Python 3 on CentOS 7
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-install-python-3-on-centos-7/
published: true
post_date: 2017-12-12 11:25:30
---
Optional - update packages
<pre class="prettyprint">
sudo yum -y update
</pre>
Prepare
<pre class="prettyprint">
sudo yum -y install yum-utils
</pre>

Install IUS repo
<pre class="prettyprint">
sudo yum -y install https://centos7.iuscommunity.org/ius-release.rpm
</pre>

Install Python 3.6
<pre class="prettyprint">
sudo yum -y install python36u python36u-pip python36u-devel
</pre>

Ensure Python available
<pre class="prettyprint">
python3.6 -V
</pre>

Install packages you need
<pre class="prettyprint">
sudo pip3.6 install package_name
</pre>