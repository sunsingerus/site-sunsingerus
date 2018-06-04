---
ID: 481
post_title: >
  Git. How To Pull Changes From Another
  Repo
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/git-how-to-pull-changes-from-another-repo/
published: true
post_date: 2018-06-04 14:08:28
---
Suppose we just found interesting changes in another clone of our repo on Github we'd like to have. How to pull these commits into our repo?
Here are the steps:
Add repo from which we'd like to fetch changes, as a remote repo
<pre>
git remote add interestingrepo https://github.com/user/repo-with-interesting-changes
</pre>
Check all is fine with:
<pre>
git remote -v
</pre>

<code>git pull</code> is a convenient shortcut for <code>git fetch</code> and <code>git merge</code>:
<pre>
git pull interestingrepo master
</pre>
As pull performs a merge on the fetched changes, we should ensure that local work is committed before running the pull command.
Or, we can go with more classical way as <code>git fetch</code> and <code>git merge</code>
Fetch everything from remote repo
<pre>
git fetch interesting repo
</pre>

Merge <code>master</code> branch from interesting repo
<pre>
git merge interestingrepo/master
</pre>

Verify status of the repo
<pre>
git status
On branch master
Your branch is ahead of 'origin/master' by 9 commits.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean
</pre>
And push changes
<pre>
git push
</pre>