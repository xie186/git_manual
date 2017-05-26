## How to ignore files


https://www.visualstudio.com/en-us/docs/git/tutorial/ignore-files


## How to Check if pull needed in Git

First use `git remote update`, to bring your remote refs up to date. Then you can do one of several things, such as:

`git status -uno` will tell you whether the branch you are tracking is ahead, behind or has diverged.
If it says nothing, the local and remote are the same.
git show-branch *master will show you the commits in all of the branches whose names end in master (eg master and origin/master).
If you use -v with git remote update (git remote -v update) you can see which branches got updated, so you don't really need any further commands.

However, it looks like you want to do this in a script or program and end up with a true/false value. If so, there are ways to check the relationship between your current HEAD commit and the head of the branch you are tracking, although since there are four possible outcomes you can't reduce it to a yes/no answer. However, if you're prepared to do a pull --rebase then you can treat "local is behind" and "local has diverged" as "need to pull", and the other two as "don't need to pull".

You can get the commit id of any ref using git rev-parse <ref>, so you can do this for master and origin/master and compare them. If they are equal, the branches are the same. If they're unequal, you want to know which is ahead of the other. Using git merge-base master origin/master will tell you the common ancestor of both branches, and if they haven't diverged this will be the same as one or the other. If you get three different ids, the branches have diverged.
