---
ID: 468
post_title: Git. How To Work with Tags
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/git-how-to-work-with-tags/
published: true
post_date: 2018-05-28 12:53:20
---
List all tags
<pre>
git tag
v1.1.54011-stable
v1.1.54015-testing
...
</pre>

List specific tags
<pre>
git tag -l '*stable'
v1.1.54011-stable
v1.1.54019-stable
...
</pre>

Create tag
<pre>
git tag t1
</pre>

Create tag with additional text annotation
<pre>
git tag -a t1-annotated -m "text annotation to the tag"
</pre>
or
<pre>
git tag -a t1-annotated
</pre>
and git will call a text editor to enter annotation. Annotations can be multi-line.

Create tag for a specific commit
<pre>
git tag -a v1.2 8a5cbc430f1a9c3d00faaeffd07798508422908a 
</pre>

By default, tags are not pushed to remote repo, so you'd need to say something like
<pre>
git push origin --tags
</pre>
in case you'd like to push all tags, or
<pre>
git push origin t1
</pre>
in case you'd like to push one tag only
You can always <code>checkout</code> any tag with
<pre>
git checkout t1
</pre>
More details on getting specific tags in <a href="https://sunsingerus.com/how-to-get-a-specific-tag-with-git/" rel="noopener" target="_blank">this post</a>