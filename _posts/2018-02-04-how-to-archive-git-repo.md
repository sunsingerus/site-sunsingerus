---
ID: 392
post_title: How To Archive Git Repo
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-archive-git-repo/
published: true
post_date: 2018-02-04 18:51:39
---
<h5>Intro</h5>
Suppose we have the following git repo
<pre>
.git/
dict/
src/
LICENSE  
README.md  
build.sh  
</pre>
and we need to have repo archived without git information.

<h5>Archive</h5>
Apply <code>git archive</code> command. Archive latest commit on the current branch i.e. <code>HEAD</code>
<pre>
git archive --format=tar.gz HEAD > /tmp/head_no_prefix.tar.gz
</pre>
Archive content:
<pre>
dict/
src/
LICENSE  
README.md  
build.sh  
</pre>

git archive --format=tar.gz --prefix=v1.1/ HEAD > /tmp/2.tgz
<pre>
v1.1
  dict/
  src/
  LICENSE  
  README.md  
  build.sh  
</pre>

git archive --prefix=v1.2/ -o /tmp/3.tar.gz HEAD
git archive --prefix=v1.2/ -o /tmp/3.tgz HEAD


git archive -o latest.zip HEAD

Create a Zip archive that contains the contents of the latest commit on the current branch. Note that the output format is inferred by the extension of the output file.