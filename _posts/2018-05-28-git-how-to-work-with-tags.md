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
...
v1.1.54011-stable
...
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