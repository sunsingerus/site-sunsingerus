---
ID: 116
post_title: How To Add Git Submodule
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-add-git-submodule/
published: true
post_date: 2017-12-17 18:37:06
---
Suppose we'd like to add the following project <code>https://github.com/sunsingerus/eth-misc-scripts</code> into <code>bin</code> folder of the current project. Run the following command:
<pre>
git submodule add https://github.com/sunsingerus/eth-misc-scripts bin
</pre>
Important - <code>bin</code> folder should not exist when running this command - git will complain like the following:
<pre>
'bin' already exists and is not a valid git repo
</pre>

So, after running <code>git submodule add</code> we'll have added:
<pre>
drwxrwxr-x   2 user user  4096 Dec 17 21:04 bin/
-rw-rw-r--   1 user user    85 Dec 17 21:04 .gitmodules
</pre>

<strong>However, there is a small trick.</strong>
In case added submodule has nested submodules - submodule inside submodule, etc - they <strong>ARE NOT INITIALIZED</strong> by default - meaning their folders are empty.
Need to run 
<pre>
git submodule update --init --recursive
</pre>
in order to initialize the whole submodules tree.

Let's take a look into <code>.gitmodules</code>
<pre>
user@cinnamon ~/dev/eth-dapp-petshop $ cat .gitmodules 
[submodule "bin"]
	path = bin
	url = https://github.com/sunsingerus/eth-misc-scripts
</pre>
Full list of submodules with their local and github paths.