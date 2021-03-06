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
Apply <code>git archive</code> command. Archive latest commit on the current branch i.e. <code>HEAD</code> as tar.gz
<pre>
git archive --format=tar.gz HEAD > /tmp/repo.tar.gz
</pre>
Archive content:
<pre>
dict/
src/
LICENSE  
README.md  
build.sh  
</pre>

As we can see, archive contains repo without .git dir. 

Sometimes we'd like to have archived repo inside a folder. This is convenient when archive is extracted and all files are located inside separate folder, not in current folder. In this case use <code>--prefix=folder/</code> option. <strong>IMPORTANT: / is important - in case it is omitted we'd have all file names prefixed - but not located inside a directory. This is not what we'd like to have</strong>
<pre>
git archive --format=tar.gz --prefix=v1.1/ HEAD > /tmp/2.tgz
</pre>
Archive content:
<pre>
v1.1/
  dict/
  src/
  LICENSE  
  README.md  
  build.sh  
</pre>

We can specify output file name with extension, and git is clever enough to understand what archive format we'd like to have.
<pre>
git archive --prefix=v1.2/ -o /tmp/3.tar.gz HEAD
</pre>
Short <code>.tgz</code> form is fine as well
<pre>
git archive --prefix=v1.2/ -o /tmp/3.tgz HEAD
</pre>