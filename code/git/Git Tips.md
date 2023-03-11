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

One can also use `cherr-pick`
```git
git checkout name-of-the-correct-branch
# grab the last commit to master
git cherry-pick master
# delete it from master
git checkout master
git reset HEAD~ --hard
``` 

### Run `diff` and nothing happens? 

probably `add`-ed your files to staging and you need to use a special flag.

```git
git diff --staged
```  

Need to do a commit from like 10 minutes ago?  
```git
# find the commit you need to undo
git log
# use the arrow keys to scroll up and down in history
# once you've found your commit, save the hash
git revert [saved hash]
# git will create a new commit that undoes that commit
# follow prompts to edit the commit message
# or just save and commit
```

If you committed a bug, you can undo the commit all in one go with `revert`.

You can also revert a single file instead of a full commit! But of course, in true git fashion, it's a completely different set of fucking commands...  

### Undo changes to a file

```git
# find a hash for a commit before the file was changed
git log
# use the arrow keys to scroll up and down in history
# once you've found your commit, save the hash
git checkout [saved hash] -- path/to/file
# the old version of the file will be in your index
git commit -m "Wow, you don't have to copy-paste to undo"
```  

If you need to give up 
```git
cd ..
sudo rm -r fucking-git-repo-dir
git clone https://some.github.url/fucking-git-repo-dir.git
cd fucking-git-repo-dir
```

if your branch is sooo borked that you need to reset the state of your repo to be the same as the remote repo in a "git-approved" way, try this, but beware these are destructive and unrecoverable actions  

```git
# get the lastest state of origin
git fetch origin
git checkout master
git reset --hard origin/master
# delete untracked files and directories
git clean -d --force
# repeat checkout/reset/clean for each borked branch
```