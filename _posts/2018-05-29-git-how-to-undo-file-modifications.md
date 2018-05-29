---
ID: 476
post_title: Git. How To Undo File Modifications
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/git-how-to-undo-file-modifications/
published: true
post_date: 2018-05-29 17:07:50
---
for uncommitted files you just checkout latest committed version of the file:
<pre>
git checkout -- path/to/file
</pre>
Note <code>--</code> - it id important and specifies end of options for the command