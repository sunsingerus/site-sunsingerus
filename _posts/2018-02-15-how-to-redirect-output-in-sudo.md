---
ID: 410
post_title: 'How To Redirect Output In &#8216;sudo&#8217;'
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-redirect-output-in-sudo/
published: true
post_date: 2018-02-15 12:11:29
---
<h5>Intro</h5>
Suppose we'd like to redirect output inside <code>sudo</code>. This can be useful in case we'd like to have output files owned by <code>sudo</code>-ed user. Simple example - we'd like to write <code>stdout</code> into file somewhere in <code>/var/log/</code> and are ready to launch command as a <code>root</code>
Straightforward attempt like
<pre>
sudo -u root echo "qwe" > /var/log/test_output.txt
</pre>
fails:
<pre>
bash: /var/log/test_output.txt: Permission denied
</pre>
<h5>Why so?</h5>
This is because output redirection is done outside of <code>sudo</code> and our current user is not able to write into <code>/var/log</code>
<h5>What to do?</h5>
Let's move output redirection inside <code>sudo</code>
However, straightforward attempt like this:
<pre>
sudo -u root "echo 'qwe' > /var/log/test_output.txt"
</pre>
fails again
<pre>
sudo: echo 'qwe' > /var/log/test_output.txt: command not found
</pre>
<h5>Why so?</h5>
This is because the whole line <code>echo 'qwe' > /var/log/test_output.txt</code> is interpreted as a single command to run, which can't be found
<h5>Solution</h5>
We need to call <code>shell</code> instance within <code>sudo</code> in order to correctly interpret and run the whole command.
<pre>
sudo -u root bash -c "echo 'qwe' > /var/log/test_output.txt"
cat /var/log/test_output.txt 
qwe
</pre>