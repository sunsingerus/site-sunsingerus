---
ID: 428
post_title: 'BASH How To Use &#8211; pushd, popd, dirs'
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/bash-how-to-use-pushd-popd-dirs/
published: true
post_date: 2018-04-07 08:03:24
---
<h5>pushd, popd, dirs - what is it</h5>

These are BASH-build-ins to make directory tree navigation easier
Let's cite man page:
<blockquote>
DIRSTACK
    An  array  variable  ... containing the current contents of the directory stack.  ... pushd and popd builtins must be used to  add and remove directories. 
</blockquote>

Now, jump into examples:
Current location:
<pre>
user@cinnamon ~ $ pwd
/home/user
</pre>
Add current location (which is <code>/home/user</code>) to stack and switch to <code>/bin</code> - <strong>just switch to <code>/bin</code> - it will not be added to stack</strong>
<pre>
user@cinnamon ~ $ pushd /bin
/bin ~
user@cinnamon /bin $ pwd
/bin
</pre>
Add some more dirs into stack
<pre>
user@cinnamon /bin $ pushd /var
/var /bin ~
user@cinnamon /var $ pushd /tmp
/tmp /var /bin ~
</pre>
Let's review <code>dirs</code> command output
<pre>
user@cinnamon /tmp $ dirs
/tmp /var /bin ~
</pre>
It outputs current directory and stack afterwards - <strong>/tmp is not inside stack</strong>. To illustrate - lets <code>cd</code> into another dir and review <code>dir</code> output again
<pre>
user@cinnamon /tmp $ cd /home
user@cinnamon /home $ dirs
/home /var /bin ~
</pre>
We are inside <code>/home</code> and <code>/var /bin ~</code> are in stack

Let's access <code>DIRSTACK</code> directly
<pre>
user@cinnamon /home $ echo ${DIRSTACK[0]}
/home
user@cinnamon /home $ echo ${DIRSTACK[1]}
/var
user@cinnamon /home $ echo ${DIRSTACK[2]}
/bin
user@cinnamon /home $ echo ${DIRSTACK[3]}
/home/user
</pre>

And now lets use stacked dirs:
<pre>
user@cinnamon /home $ popd
/var /bin ~
user@cinnamon /var $ popd
/bin ~
user@cinnamon /bin $ popd
~
user@cinnamon ~ $ popd
bash: popd: directory stack empty
user@cinnamon ~ $ 
</pre>