---
ID: 276
post_title: Python. Enumerate() function
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/python-enumerate-function/
published: true
post_date: 2018-01-04 21:04:30
---
Enumerate each item in iterable. Very useful when you not only need to iterate over iterable, but also to keep track of iteration number/index.
Better to explain on example.
<pre>
letters = ['a', 'b', 'c']
for letter in letters:
    print(letter)
</pre>

Run code, got as expected:
<pre>
a
b
c
</pre>

Now let's add index of each entry in the list
<pre>
for i, letter in enumerate(letters):
    print(i, letter)
</pre>
<pre>
0 a
1 b
2 c
</pre>

And now final touch - add start index to enumerate
<pre>
for i, letter in enumerate(letters, 1):
    print(i, letter)
</pre>
<pre>
1 a
2 b
3 c
</pre>

very nice, no need to meddle with explicit indexes as <code>i = 1</code> and <code>i += 1</code> on each iteration