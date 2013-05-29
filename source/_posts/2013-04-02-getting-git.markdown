---
layout: post
title: "Getting Git"
date: 2013-04-02 20:09
comments: true
categories: 
---
Since working on our group project a couple of weeks ago, I've gotten more familiar with using Git. After suffering through some painful merging of branches into master, I have learned some important lessons of what to do (e.g., make sure your local master is up to date before rebasing and merging branches!) and what <em>not</em> to do (e.g., panic and type arbitrary git commands during a rebase!)

Here are 10 steps for Git success (for branching and merging):

1) Before branching, make sure your local master is up to date with remote master.

  <code>git pull origin master</code>

2) Create and check out a new branch.

  <code>git checkout -b [NAME_OF_FEATURE_BRANCH]</code>

3) Do all your work on this branch. Once your branch is complete, commit all of your changes and push them to the branch. 

  <code>git commit -am "helpful commit message!"</code>

4) Check out master and make sure that your local master is up to date with the latest changes on master.

  <code>git pull origin master</code>

5) Check out your feature branch.

  <code>git co [FEATURE_BRANCH]</code>

6) From your feature branch, rebase master onto the feature branch.

  <code>git rebase master</code>

7) Resolve all conflicts on the feature branch. After resolving conflicts in your files, add your changes and continue the rebase.
  
  <code>git add . </code><br>
  <code>git rebase --continue</code>

8) Once the rebase is complete, check out master.

  <code>git co master</code>

9) Merge feature branch into master.

  <code>git merge [FEATURE_BRANCH]</code>

10) Double check that all conflicts have been resolved and that your code is working properly. If everything looks good, push the merge to remote master.

  <code>git push origin master</code>

Some additional thoughts on good practices:<br>
- Keep remote master clean. Write any new code on branches.<br>
- Don't branch off a feature branch. You should generally branch off master.<br>
- Don't merge a branch into master until the feature is fully complete.<br>
- Keep your changes small so that you don't spend too much time working on the same branch.<br>
- Write succinct but descriptive commit messages.<br>
- Once your branch is complete and merged, any new work should be done on a new branch.

