# Git mannual

## Create new repository on using web UI

https://help.github.com/articles/create-a-repo/

## Basic command lines

```
git branch  ## check how many branches you have and which branch you are under.
git add ./
git commit -m "Update README.md"  

git push origin dev ## push to branch dev

git checkout master  ## check out to master branch
git merge dev        ## merge changes in dev branch
git push origin master  ## push the changes. 
```

## How to create a new branch

```
git branch <new-branch-name>
```
## How to show the working tree status

```
git status
```

## How to check the commit histories?

```
git log
```

## How to go two a specific commit? 

```
git checkout <ID> . 
```

## How to ignore files


https://www.visualstudio.com/en-us/docs/git/tutorial/ignore-files

```
## Modify the file: 
$ more .git/info/exclude
# git ls-files --others --exclude-from=.git/info/exclude
# Lines that start with '#' are comments.
# For a project mostly in C, the following would be a good set of
# exclude patterns (uncomment them if you want to use them):
# *.[oa]
# *~
#
*.dir_bash_history_xie186

## ignore folders
data/

```

## what if last commit message was wrong.

```
git commit --amend -m "New commit message"
```



## How to avoid typing user name and password every time when pushing

```
$ git config credential.helper store
$ git push http://example.com/repo.git
Username: <type your username>
Password: <type your password>
```

## How to forcely merge two branches

```
git push --force origin   dev:master
```

## How to add submodule 

Reference:

https://stackoverflow.com/questions/7813030/how-can-i-have-linked-dependencies-in-a-git-repo

```
git submodule add git@github.com:heike/summerschool-2017.git bigdata/summerschool-2017

```

You can do this with submodules in git. In your repository, do:

git submodule add path_to_repo path_where_you_want_it
So, if the library's repository had a URL of git://github.com/example/some_lib.git and you wanted it at lib/some_lib in your project, you'd enter:

git submodule add git://github.com/example/some_lib.git lib/some_lib
Note that this needs to be done from the top-level directory in your repository. So don't cd into the directory where you're putting it first.

After you add a submodule, or whenever someone does a fresh checkout of your repository, you'll need to do:

git submodule init
git submodule update
And then all submodules you've added will be checked out at the same revision you have.

When you want to update to a newer version of one of the libraries, cd into the submodule and pull:

cd lib/some_lib
git pull
Then, when you do a git status you should see lib/somelib listed in the modified section. Add that file, commit, and you're up to date. When a collaborator pulls that commit into their repository, they'll see lib/somelib as modified until they run git submodule update again.


## How to Check if pull needed in Git

First use `git remote update`, to bring your remote refs up to date. Then you can do one of several things, such as:

`git status -uno` will tell you whether the branch you are tracking is ahead, behind or has diverged.
If it says nothing, the local and remote are the same.
git show-branch *master will show you the commits in all of the branches whose names end in master (eg master and origin/master).
If you use -v with git remote update (git remote -v update) you can see which branches got updated, so you don't really need any further commands.

However, it looks like you want to do this in a script or program and end up with a true/false value. If so, there are ways to check the relationship between your current HEAD commit and the head of the branch you are tracking, although since there are four possible outcomes you can't reduce it to a yes/no answer. However, if you're prepared to do a pull --rebase then you can treat "local is behind" and "local has diverged" as "need to pull", and the other two as "don't need to pull".

You can get the commit id of any ref using git rev-parse <ref>, so you can do this for master and origin/master and compare them. If they are equal, the branches are the same. If they're unequal, you want to know which is ahead of the other. Using git merge-base master origin/master will tell you the common ancestor of both branches, and if they haven't diverged this will be the same as one or the other. If you get three different ids, the branches have diverged.


## How to check and set user.name

```
git config user.name
git config user.name "JonSnow"
```
https://help.github.com/articles/setting-your-username-in-git/


## How to reset the remote url? 

```
git remote -v
```

https://help.github.com/articles/changing-a-remote-s-url/


## How to reset the user email? 

git config  user.email "xieshaojun0621@qq.com"

## How to undo a previous commit? 

### What if you want to rebate a previous commit

https://stackoverflow.com/questions/927358/how-to-undo-the-last-commits-in-git?page=1&tab=votes#tab-top

```
git reset --hard HEAD~
git push origin +master  ## "+ means forcely push the changes
```

Slides: 

https://docs.google.com/presentation/d/1MBOiTckQJ4qVcsJFnwtlt60XmbNY7UbgVRPwLELBBe8/edit?usp=sharing
