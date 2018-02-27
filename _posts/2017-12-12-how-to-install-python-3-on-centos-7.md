---
ID: 64
post_title: How To Install Python 3 on CentOS 7
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-install-python-3-on-centos-7/
published: true
post_date: 2017-12-12 11:25:30
---
<h2>Python 3.4</h2>
Python 3.4 packages for CentOS are available via <strong>epel</strong> repos
<pre class="prettyprint">
sudo yum install epel-release
</pre>
<pre class="prettyprint">
sudo yum install python34 python34-devel python34-pip
</pre>

<h2>Python 3.5</h2>
Prepare
<pre class="prettyprint">sudo yum -y install yum-utils
</pre>
Install IUS repo
<pre class="prettyprint">sudo yum -y install https://centos7.iuscommunity.org/ius-release.rpm
</pre>
Install Python 3.6
<pre class="prettyprint">sudo yum -y install python36u python36u-pip python36u-devel
</pre>
Ensure Python available
<pre class="prettyprint">python3.6 -V
</pre>
Install packages you need
<pre class="prettyprint">sudo pip3.6 install package_name
</pre>