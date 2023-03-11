#git #tips
url: https://ohshitgit.com


Here are some bad situations I've gotten myself into, and how I eventually got myself out of them in plain english.  

### If you've done something terribly wrong, git has a time machine: 

```git
git reflog
# you will see a list of every thing you've
# done in git, across all branches!
# each one has an index HEAD@{index}
# find the one before you broke everything
git reset HEAD@{index}
# magic time machine
```

- get back stuff you accidentally deleted
- to remove some stuff you tried that broke the repo,
- to recover after a bad merge,
- just to go back to a time when things actually worked  

### commited but immediately need to make a change
```git
# make your change
git add . # or add individual files
git commit --amend --no-edit
# now your last commit contains that change!
# WARNING: never amend public commits
```  

You could also make the change as a new commit and then do `rebase -i` in order to squash them both together, but this is about a million times faster.

_Warning: You should never amend commits that have been pushed up to a public/shared branch! Only amend commits that only exist in your local copy or you're gonna have a bad time._ 

### To change the last commit message  
```git
git commit --amend
# follow prompts to change the commit message
```

### Accidentally commit to master branch instead of a new one 
```git
# create a new branch from the current state of master
git branch some-new-branch-name
# remove the last commit from the master branch
git reset HEAD~ --hard
git checkout some-new-branch-name
# your commit lives in this branch now :)
```  

- doesn't work if you've already pushed the commit to a public/shared branch  

### Accidentally commit to wrong brach 
```git
# undo the last commit, but leave the changes available
git reset HEAD~ --soft
git stash
# move to the correct branch
git checkout name-of-the-correct-branch
git stash pop
git add . # or add individual files
git commit -m "your message here";
# now your changes are on the correct branch
```