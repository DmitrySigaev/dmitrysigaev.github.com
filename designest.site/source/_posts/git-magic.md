title: git magic
date: 2015-12-05 20:58:49
tags:
---

Первым делом этот пост содержит шпору по командам гита, которые я использую в своей работе

1. git pull or git fetch
2. How to do rebase:
   a. chech your git status
```
D:\vs>git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```
then
git chechuot  chem-decom

git status

you should check sha from master branch. assume sha is equal to c4e661de4c      
then

git rebase c4e661de4c1ea89eb2ceed92574f6e47fe8cefe0

At the time of rebasing some colapse can appere and after resoving you should terminate:

git rebase -continue

After that you should apply force push like:
 

git push origin +chem-decom
   b. 

                       
                               

                                             