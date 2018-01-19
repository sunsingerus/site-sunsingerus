---
ID: 317
post_title: How To Use Bash options
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-use-bash-options/
published: true
post_date: 2018-01-19 12:11:40
---
<h5>How to use bash options</h5>
Bash provides possibility to set options. We'd like to take a look on the most popular ones <code>set -x</code> and <code>set -e</code>

<h5>set -x</h5>
According to the doc <code>set -x</code> "Print commands and their arguments as they are executed."
Let's take a look on example:
<code>1.sh</code>
<pre>
#!/bin/bash

set -x
echo "1. exec cmd 1"
echo "1. exec cmd 2"
./2.sh
echo "1. exec cmd 3"
echo "1. exec cmd 4"
exit 0
</pre>
<code>2.sh</code>
<pre>
#!/bin/bash

echo "2 exec cmd 1"
echo "2 exec cmd 2"

RET=1
echo "2 exit code $RET"
exit $RET
</pre>

Run <code>1.sh</code>
<pre>
+ echo '1. exec cmd 1'
1. exec cmd 1
+ echo '1. exec cmd 2'
1. exec cmd 2
+ ./2.sh
2 exec cmd 1
2 exec cmd 2
2 exit code 1
+ echo '1. exec cmd 3'
1. exec cmd 3
+ echo '1. exec cmd 4'
1. exec cmd 4
+ exit 0
</pre>

As we can see,
<code>set -x</code> print each command before executing it. Nice feature!
In case we'd like to disable it, just use <code>set +x</code>
Let's modify <code>1.sh</code>
<pre>
#!/bin/bash

set -x
echo "1. exec cmd 1"
echo "1. exec cmd 2"
set +x
./2.sh
echo "1. exec cmd 3"
echo "1. exec cmd 4"
exit 0
</pre>
and run it
<pre>
+ echo '1. exec cmd 1'
1. exec cmd 1
+ echo '1. exec cmd 2'
1. exec cmd 2
+ set +x
2 exec cmd 1
2 exec cmd 2
2 exit code 1
1. exec cmd 3
1. exec cmd 4
</pre>

<h5>set -e</h5>
According to the doc set -e “Exit immediately if a command exits with a non-zero status.”
Let’s take a look on example:
<code>1.sh</code>
<pre>
#!/bin/bash

set -e

echo "1. exec cmd 1"
echo "1. exec cmd 2"
echo "1. calling 2.sh"
./2.sh
echo "1. got exit code $? from 2.sh"
echo "1. exec cmd 3"
exit 0

</pre>
<code>2.sh</code> is the same as before
Run <code>1.sh</code>
<pre>
1. exec cmd 1
1. exec cmd 2
1. calling 2.sh
2 exec cmd 1
2 exec cmd 2
2 exit code 1
</pre>
As we can see, no commands after the first with non-zero exit code.

<h5>set -e combined with a trap call</h5>
Modify <code>1.sh</code>
<pre>
#!/bin/bash

set -e

trap on_err ERR
function on_err()
{
	echo "1. trap error on line $(caller)" >&2
}

echo "1. exec cmd 1"
echo "1. exec cmd 2"
echo "1. calling 2.sh"
./2.sh
echo "1. got exit code $? from 2.sh"
echo "1. exec cmd 3"
exit 0
</pre>
And run it
<pre>
1. exec cmd 1
1. exec cmd 2
1. calling 2.sh
2 exec cmd 1
2 exec cmd 2
2 exit code 1
1. trap error on line 14 ./1.sh
</pre>
Observe <code>1. trap error on line 14 ./1.sh</code> which points directly to the line and file where non-zero exit code detected.
Can be of a great help for debug.

<h5>Exclude command from exit code check</h5>
<code>1.sh</code>
<pre>
#!/bin/bash

set -e

trap on_err ERR
function on_err()
{
        echo "1. trap error on line $(caller)" >&2
}

echo "1. exec cmd 1"
echo "1. exec cmd 2"
echo "1. calling 2.sh"
set +e
./2.sh
echo "1. got exit code $? from 2.sh"
set -e
echo "1. exec cmd 3"
./2.sh
echo "1. exec cmd 4"
exit 0
</pre>
As expected the first run of <code>2.sh</code> does not terminate <code>1.sh</code>, but the seconds call - terminates
<pre>
. exec cmd 1
1. exec cmd 2
1. calling 2.sh
2 exec cmd 1
2 exec cmd 2
2 exit code 1
1. trap error on line 15 ./1.sh
1. got exit code 1 from 2.sh
1. exec cmd 3
2 exec cmd 1
2 exec cmd 2
2 exit code 1
1. trap error on line 19 ./1.sh
</pre>