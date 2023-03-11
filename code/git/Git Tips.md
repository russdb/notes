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

