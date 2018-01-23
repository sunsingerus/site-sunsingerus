---
ID: 351
post_title: How To Update Forked Git Repository
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/how-to-update-forked-git-repository/
published: true
post_date: 2018-01-23 10:07:49
---
<h5>Introduction</h5>
Imagine we have forked Git project and some time later a change was made by another developer into the root project. Our fork does not have that change and we'd like to obtain it.

<h5>Add remote repo</h5>
Add <a href="https://git-scm.com/docs/git-remote" rel="noopener" target="_blank">remote repository</a>, call it altinity in our case.
<pre>
git remote add altinity https://github.com/Altinity/clickhouse-rpm
</pre>
Review remote repos
<pre>
git remote
altinity
origin
</pre>

<pre>
git remote show altinity

* remote altinity
  Fetch URL: https://github.com/Altinity/clickhouse-rpm
  Push  URL: https://github.com/Altinity/clickhouse-rpm
  HEAD branch: master
  Remote branch:
    master new (next fetch will store in remotes/altinity)
  Local ref configured for 'git push':
    master pushes to master (local out of date)
</pre>

<h5>Fetch remote</h5>
Fetch all branches from remote repository
<pre>
git fetch altinity

remote: Counting objects: 78, done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 78 (delta 3), reused 18 (delta 2), pack-reused 58
Unpacking objects: 100% (78/78), done.
From https://github.com/Altinity/clickhouse-rpm
 * [new branch]      master     -> altinity/master
</pre>

<h5>Merge remote changes into local repo</h5>
Ensure we are on master branch in local repo
<pre>
git checkout master
</pre>
ad merge changes fetched from remote repo into local repo
<pre>
git merge altinity/master
</pre>
<pre>
Updating 79d4260..7f58bdb
Fast-forward
 src/clickhouse.spec.in | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
</pre>

Check we have new commits in local repo
<pre>
git status
On branch master
Your branch is ahead of 'origin/master' by 72 commits.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean
</pre>