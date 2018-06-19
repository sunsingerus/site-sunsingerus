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

<h2>Delete value</h2>
<pre>
echo ${ARR[@]}
one two three
unset ARR[1]
echo ${ARR[@]}
one three
</pre>

<h2>Iterate over array</h2>
<pre>
for i in ${ARR[@]}; do
  echo $i
done
</pre>

<h2>Count values</h2>
Loop until empty string found
<pre>
COUNT=0
while [ "x${ARR[COUNT]}" != "x" ]
do
   count=$(( $COUNT + 1 ))
done
</pre>