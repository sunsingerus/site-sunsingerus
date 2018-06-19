---
ID: 494
post_title: BASH. How To Use ARRAY
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/bash-how-to-use-array/
published: true
post_date: 2018-06-19 09:00:00
---
<h2>Declaration</h2>

<pre>
ARR=("one" "two" "three")
ARR=(
  "one"
  "two"
  "three"
)
</pre>

<h2>Fetch value</h2>
Use either <code>*</code> or <code>@</code> to fetch all values from the array
<pre>
echo ${ARR[*]}
one two three
echo ${ARR[@]}
one two three
</pre>