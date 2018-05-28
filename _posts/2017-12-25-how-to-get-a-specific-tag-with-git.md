---
ID: 209
post_title: How To Get a Specific Tag With Git
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-get-a-specific-tag-with-git/
published: true
post_date: 2017-12-25 11:06:58
---
Suppose we'd like to get sources tagged <code>v1.1.54327-stable</code> from <code>https://github.com/yandex/ClickHouse</code> repo
<h5>Clone repo</h5>
Newer git versions support <code>--branch</code> option with tags:
<pre>git clone --branch v1.1.54327-stable https://github.com/yandex/ClickHouse ClickHouse-1.1.54327-stable
</pre>
if you need <strong>submodules</strong>, append <code>--recursive</code>
<pre>git clone --recursive --branch v1.1.54327-stable https://github.com/yandex/ClickHouse ClickHouse-1.1.54327-stable
</pre>
For newer git<strong> ALL IS DONE</strong>

Older versions can't fetch tag with <code>--branch v1.1.54327-stable</code>, we need another approach: clone repo first and checkout to specific tag within cloned repo afterwards.
<pre>$ git clone https://github.com/yandex/ClickHouse
</pre>
will give the whole repo. We need to checkout a specific tag within repo.
<h5>Checkout required tag</h5>
<pre>$ cd ClickHouse
</pre>
We can list the tags with
<pre>$ git tag -l
</pre>
and checkout a specific tag:
<pre>$ git checkout v1.1.54327-stable
</pre>
Running <code>git checkout <tag></code> puts repository in "detached HEAD" state, which is sometimes inconvenient. Main issue with "detached HEAD" is that in case you'd make new commit it would not belong to any branch (because we are not on any branch right now, but in "detached HEAD" state) and this commit will be accessible by direct checksum. In most cases, this is not what we'd like to have, so in case you'd like to make commits you'd like to create a branch.
We can checkout tag and create a branch in one move:
<pre>$ git checkout v1.1.54327-stable -b v1.1.54327-stable
</pre>
<h5>Init submodules</h5>
<pre>git submodule update --init --recursive
</pre>
<strong>ALL IS DONE</strong>