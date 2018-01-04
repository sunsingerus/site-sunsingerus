---
ID: 262
post_title: >
  Python. Positional and Keyword (Named)
  Arguments
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/python-positional-and-keyword-named-arguments/
published: true
post_date: 2018-01-04 21:05:52
---
Let's take a look on examples:

<h5>Positional agrs</h5>
<pre>
def positional(*args):
    for arg in args:
        print(arg)
</pre>

<pre>
>>>positional(1, 2, 3)
1
2
3
</pre>
<pre>
>>> positional(*[1, 2, 3])
1
2
3
</pre>

<h5>Keyword agrs</h5>
<pre>
def keyword(**kwargs):
    for key, value in kwargs.items():
        print("kwargs[{}]={}".format(key, value))
</pre>
<pre>
>>> keyword(a=1, b=2)
kwargs[a]=1
kwargs[b]=2
</pre>
<pre>
>>> keyword(**{'a':1, 'b':2})
kwargs[a]=1
kwargs[b]=2
</pre>

<h5>Put all together</h5>
<pre>
def mix(a, b, *args, **kwargs):
    print("a={}".format(a))
    print("b={}".format(b))
    for arg in args:
        print("args[]={}".format(arg))
    for key, value in kwargs.items():
        print("kwargs[{}]={}".format(key, value))
</pre>
Rule of a thumb is:
<ul>
<li>First go in args list and filled explicitly specified args (a, b in this case)</li>
<li>Than go variable number of positional args</li>
<li>And after that go variable number of keyword args</li>
</ul>

<strong>Examples:</strong>
No keyword args in this call.
<pre>
>>> mix(1, 2, 3, 4, 5)
a=1
b=2
args[]=3
args[]=4
args[]=5
</pre>
As expected, we can see explicitly specified args and variable number of positional args

Now let's add keyword args
<pre>
>>> mix(1, 2, 3, 4, 5, x=6, y=7)
a=1
b=2
args[]=3
args[]=4
args[]=5
kwargs[x]=6
kwargs[y]=7
</pre>

And now let's omit positional args
<pre>
>>> mix(a=1, b=2, c=3, d=4, e=5, x=6, y=7)
a=1
b=2
kwargs[c]=3
kwargs[d]=4
kwargs[e]=5
kwargs[x]=6
kwargs[y]=7
</pre>