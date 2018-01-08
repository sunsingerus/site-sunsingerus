---
ID: 281
post_title: Python. Freeze and restore requirements
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/python-freeze-and-restore-requirements/
published: true
post_date: 2018-01-08 19:40:54
---
<h5>Create full list of requirements of the app</h5>:
<pre>
pip freeze > requirements.txt
</pre>

<h5>Restore freezed earlier requirements</h5>:
<pre>
pip install -r requirements.txt
</pre>