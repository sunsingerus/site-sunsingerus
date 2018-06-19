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
# empty ARRAY declaration
ARR=()

# one-line declaration
ARR=("one" "two" "three")

# multi-line declaration
ARR=(
  "one"
  "two"
  "three"
)

# sparse array declaration
ARR=([0]="a" [1]="b" [4]="c" [15]="d" [26]="e")
</pre>

<h2>Append value</h2>
<pre>
ARR+=("new")
</pre>

<h2>Fetch value</h2>
Use either <code>*</code> or <code>@</code> to fetch all values from the array
<pre>
echo ${ARR[*]}
one two three
echo ${ARR[@]}
one two three
</pre>

Fetch last avlue
<pre>
echo ${ARR[@]: -1}
</pre>

Fetch 3 values starting with index 2
<pre>
echo "${ARR[@]:2:3}"
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
<pre>
echo ${#ARR[@]}
</pre>

OR

Loop until empty string found - does not work for sparse arrays
<pre>
COUNT=0
while [ "x${ARR[COUNT]}" != "x" ]; do
   COUNT=$(( $COUNT + 1 ))
done
</pre>