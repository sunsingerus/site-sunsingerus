---
ID: 123
post_title: How To Update a Submodule in Git Repo
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/how-to-update-a-submodule-in-git-repo/
published: true
post_date: 2017-12-17 19:21:13
---
Suppose we have a submodule and it is behind its github repo. Say, submodule project is going forward, while we have outpdated version. We'd like to update submodule in our repo to its latest version.
<h5>1. Make a pull inside submodule</h5>
<pre>cd bin/
git pull origin master
</pre>
Now we have submodule updated
<pre>user@cinnamon ~/tmp/eth-dapp-petshop $ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add ..." to update what will be committed)
  (use "git checkout -- ..." to discard changes in working directory)

	modified:   bin (new commits)
</pre>
<h5>2. Add submodule, commit and push main repo</h5>
<pre>user@cinnamon ~/tmp/eth-dapp-petshop $ git add bin/
user@cinnamon ~/tmp/eth-dapp-petshop $ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD ..." to unstage)

	modified:   bin

user@cinnamon ~/tmp/eth-dapp-petshop $ git commit -m "update submodule bin"
[master f066b0a] update submodule bin
 1 file changed, 1 insertion(+), 1 deletion(-)

user@cinnamon ~/tmp/eth-dapp-petshop $ git push
</pre>