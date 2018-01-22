---
ID: 346
post_title: How To Check Bash Options
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-check-bash-options/
published: true
post_date: 2018-01-22 13:48:08
---
According to the help, <strong>"The current set of flags may be found in $-."</strong>
<pre>
set -x

function is_print_commands_enabled()
{
        # The current set of flags may be found in $-.
        [[ "${-}" == *"x"* ]]
}

if is_print_commands_enabled; then
        echo "set -x detected"
else
        echo "NO set -x detetced"
fi
</pre>

Run it
<pre>
+ is_print_commands_enabled
+ [[ hxB == *\x* ]]
+ echo 'set -x detected'
set -x detected
</pre>