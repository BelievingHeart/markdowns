[//]: # (#git commands)
## log
```
git help log
git log --oneline #see all commit hashes
git log -2 		  #last two commit
git log --before|after="2018-01-11"|"10 minutes\hours\months... ago"
git log --author="Afterbu"
```

## checkout
```
git checkout 1bf0f0 #checkout specific commit by hash
git checkout master #get back to normal state
git checkout version-1.2 #checkout tag 'version-1.2'
git checkout -b newfeature #create and checkout branch newfeature
git checkout hello.cpp #unstaged hello.cpp
```

## mv rm
```git
git mv foo.txt bar.txt #rename while staying staged
git rm bar.txt 		   #remove bar.txt while staying staged   
```

## diff
```git
git diff --staged #difference of all staged contents
git diff 4d4070   #difference between commit 4d4070 and now, see **line 4**
git diff HEAD^	  #difference between current and previous commit
git diff 3dftq3..8hg42k #between 2 commits
```

##
```git

```

# config
```git
git config core.editor<editor_name>
```

## commit
### commit means that all of your current work has been tested
```git
git commit --amend #commit to previous commit so that you can change previous commit msg

```

## merge
```git 
git branch newfeature				#create branch newfeature
git checkout newfeature 			#switch to branch newfeature
# do soome work on newfeature branch
git checkout master					#swithc back to master branch
git merge newfeature				#merge newfeature branch in master branch
git branch -d newfeature			#delete newfeature branch
```

## tag
```
git tag					#see all the tags
git tag version-1.2		#tag the current branch(HEAD) current state as version-1.2
```

## remote
```
git remote -v 			#see the remote repo that associates with this local repo
```

## pull = fetch + merge
```
#(local in master branch)noticify local repo any remote updates of origin/master and merge origin/master to local repo
git pull origin master
#(local in master branch)this equals
git fetch origin master			#noticify local repo any updates of origin/master
git merge origin master			#merge origin/master to local master branch
```

## push
```
(in newfeature branch)
git push -u origin newfeature #-u = --set-upstream, if you don't specify remote branch, it will defaults to 
							  #origin/newfeature for push, fetch and pull
git push origin -d newfeature # delelte remote branch 'newfeature' 
```

## fetch
```
git fetch --all 				#this will add any new branch of remote repo and update existing branch, can't
								#delete any branch of local according to remote deletion

git fetch --all --prune			#this will also delele local branches that not exist in remote repo      
								#--all must be specified in order to prune
```

## submodule
```
#when you first add in a third party module
$ git submodule add <url>
#next time, you use a new computer, after you clone the parent repo:
$ git submodule update --init
#note that if any change happens in submodule, submodule should be pushed first
```

## reset
```git
git reset HEAD some_file
git reset #undo add .
git reset --hard #undo modifications before add
```

## stash
stash allow you to save current work without commiting
```git
git stash [save <message>]
git stash list
git stash drop <stash-id> #discard stash
git stash pop <stash-id> #merge stash into current commit
git stash show -p <stash-id> #show difference from stash
```

## clean
clear any untracked file
```git
git clean -df #directories + force
```

## reflog
[can go back to lost commits](https://www.youtube.com/watch?v=FdZecVxzJbk)18:00
```git
git relog
```

## revert
[copy a commit to head](https://www.youtube.com/watch?v=FdZecVxzJbk)19:50
```
git revert <git-hash>
```

## gitignore
```git
#ignore a folder
*/bin/*
*bin/*
```
