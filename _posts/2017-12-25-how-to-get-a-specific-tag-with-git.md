---
ID: 209
post_title: How To Get a Specific Tag With Git
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-get-a-specific-tag-with-git/
published: true
post_date: 2017-12-25 11:06:58
---
Suppose we'd like to get sources tagged <code>v1.1.54327-stable</code> from <code>https://github.com/yandex/ClickHouse</code> repo

<h5>Clone repo</h5>
Newer git versions support <code>--branch</code> option with tags:
<pre>
git clone --branch v1.1.54327-stable https://github.com/yandex/ClickHouse ClickHouse-1.1.54327-stable
</pre>

if you need <strong>submodules</strong>, append <code>--recursive</code>

<pre>
git clone --recursive --branch v1.1.54327-stable https://github.com/yandex/ClickHouse ClickHouse-1.1.54327-stable
</pre>

<strong>Fore never git ALL IS DONE</strong>

Older version can't fetch tag with <code>--branch v1.1.54327-stable</code>, we need another approach

<pre>
$ git clone https://github.com/yandex/ClickHouse
</pre>
will give the whole repo.

<h5>Checkout required tag</h5>
<pre>
$ cd ClickHouse
</pre>
We can list the tags with 
<pre>
$ git tag -l
</pre>
and checkout a specific tag:
<pre>
$ git checkout v1.1.54327-stable
</pre>
We are on a branch named after the revision number of tag, which is sometimes inconvenient.
We can checkout and create a branch in one move:
<pre>
$ git checkout v1.1.54327-stable -b v1.1.54327-stable
</pre>

<h5>Init submodules</h5>
<pre>
git submodule update --init --recursive
</pre>
<strong>DONE</strong>