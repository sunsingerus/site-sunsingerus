---
ID: 37
post_title: >
  Packaging and Distributing Python
  Projects
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/packaging-and-distributing-python-projects/
published: true
post_date: 2017-12-27 10:52:19
---
<h5>Introduction</h5>
We'd like to provide users with convenient way to install our application. Of course, it is not that hard to <code>git clone</code> sources from <code>github</code> and run the app, but we are looking for something more convenient - to install Python project with a <code>pip</code>
There are two main ways to distribute Python app:
<ul>
 	<li>Source Distribution</li>
 	<li>Wheels Dirctibution</li>
</ul>
A <strong>Source Distribution</strong> requires a build process when installed by <code>pip</code>. Even if the distribution is Python-only, it still requires to build out the installation metadata from <code>setup.py</code>.
In practice this means that you have to have some dev packages installed on your target server. Not a big deal, but this may be inconvenient.

A <strong>Wheels Distribution</strong> is a built package that can be installed without needing to go through the build process. Installing wheels is expected to be fasterfor the end user than installing from a source distribution.

<strong>Goal</strong> - to make the project available for installation with <code>pip</code>
<h5>Requirements</h5>
Files in the project's root:
<ul>
 	<li>setup.py (mandatory) - contains project packaging info</li>
 	<li>setup.cfg (optional)</li>
 	<li>README.rst (optional)</li>
 	<li>MANIFEST.in (optional)</li>
 	<li>LICENSE.txt (recommended)</li>
</ul>
First of all, we need to create <code>setup.py</code> file with package description. Generally speaking, it consists of a single function
<pre>from setuptools import setup, find_packages
setup(
   ...params...
)
</pre>
Take a look on a real life <a href="https://github.com/sunsingerus/clickhouse-mysql-data-reader/blob/master/setup.py" target="_blank" rel="noopener">example</a>. All <code>setup</code>'s params are listed <a href="https://packaging.python.org/tutorials/distributing-packages/#setup-args" target="_blank" rel="noopener">here</a>. One more interesting feature is an <strong>executable script</strong>. This is where <code>pip</code>-installed app really shines. In case you'd like to run your app as, say, <code>/usr/bin/myapp</code> there is nice way to do this.
<pre>setup(
...
    entry_points={
        'console_scripts': [
            # executable name=what to call
            'clickhouse-mysql=clickhouse_mysql:main',
        ],
},
...
)
</pre>
This section describes console scripts - entry points. In plain words we have here: "make <code>clickhouse-mysql</code> executable which will launch <code>clickhouse_mysql:main</code> function from the app" After that, we'll be able to run the app as
<pre>/usr/bin/clickhouse-mysql
</pre>
or even
<pre>clickhouse-mysql
</pre>
depending on your <code>$PATH</code> settings
<h5>Source Distribution</h5>
In order to make source distribution we need to run <code>setup.py</code> script with <code>sdist</code> param
<pre class="prettyprint">python3 setup.py sdist

running sdist
running egg_info
writing clickhouse_mysql_data_reader.egg-info/PKG-INFO
... cut ....
Creating tar archive
removing 'clickhouse-mysql-data-reader-0.0.1' (and everything under it)
</pre>
Now let's check directory contents and we'll see new directories:
<pre class="prettyprint">drwxrwxr-x  2 user user  4096 Dec 11 14:17 clickhouse_mysql_data_reader.egg-info/
drwxrwxr-x  2 user user  4096 Dec 11 14:22 dist/
</pre>
<pre class="prettyprint">user@cinnamon ~/dev/mysqlbinlog/clickhouse-mysql-data-reader $ ls -l dist/
total 12
drwxrwxr-x  2 user user 4096 Dec 11 14:22 ./
drwxrwxr-x 10 user user 4096 Dec 11 14:23 ../
-rw-rw-r--  1 user user 2274 Dec 11 14:22 clickhouse-mysql-data-reader-0.0.1.tar.gz
</pre>
<h5>Wheels Distribution</h5>
In case the project is pure Python and natively supports both Python 2 and 3, then we can create what’s called a <strong>Universal Wheel</strong>.
In case the project is pure Python but does not natively support both Python 2 and 3, then we can create what's called a Pure Python Wheel.
In case the project contains compiled extensions, then we can create what's called <strong>Platform Wheel</strong>.

Install the wheel package:
<pre class="prettyprint">pip3 install wheel
</pre>
In order to make wheel distribution we need to run <code>setup.py</code> script with <code>bdist_wheel</code> param
<pre class="prettyprint">python setup.py bdist_wheel
</pre>
<pre class="prettyprint">user@cinnamon ~/dev/mysqlbinlog/clickhouse-mysql-data-reader $ ls -l dist/
total 32
-rw-rw-r-- 1 user user 28928 Dec 12 14:09 clickhouse_mysql-0.0.1-py3-none-any.whl
</pre>
<h5>Publish</h5>
Now we know how to build both <strong>Source</strong> and <strong>Wheels</strong> distributions. Time to publish packages.
First of all, we need to register on <a href="https://pypi.python.org/pypi" target="_blank" rel="noopener">pypi</a>

Once you have an account you can upload your distributions to PyPI using <code>twine</code>.
<pre class="prettyprint">pip3 install twine
</pre>
And now we are ready to upload packages to <strong>pypi</strong>
<pre class="prettyprint">twine upload dist/*
</pre>
After that check package status on pypi.

<img class="alignnone size-full wp-image-221" src="http://sunsingerus.com/wp-content/uploads/2017/12/pypi_package_page.png" alt="" width="600" height="650" />

<h5>Installation</h5>
Now we are ready to install the app from PyPi
<pre class="prettyprint">sudo pip3 install clickhouse-mysql</pre>
And let's check the app entry script
<pre>
[user@localhost ~]$ which clickhouse-mysql
/usr/bin/clickhouse-mysql
</pre>
Nice! We can call Python app as 
<pre>
clickhouse-mysql
</pre>
directly.