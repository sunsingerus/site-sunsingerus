---
ID: 520
post_title: >
  Mozilla Firefox. Save Entire Page as an
  Image
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/mozilla-firefox-save-entire-page-as-an-image/
published: true
post_date: 2018-09-05 10:07:18
---
Press <strong>Shift-F2</strong>
In the console type 
<pre>
screenshot [/path/to/file.png] --fullscreen
</pre>

Where:
<ul>
<li><code>/path/to/file.png</code> must be with <code>.png</code> extension. Relative paths are relative to <code>downloads</code> folder</li>
<li><code>--fullscreen</code> specifies that we'd like to have the entire page, not only visible part</li>
</ul>