https://git-scm.com/docs/git-reset
git reset 

f you want to unstage files from index (staging area) you can use git reset. It is the opposite of git add and clears all files from staging area.  
```
git reset [-q] [<tree-ish>] [--] <pathspec>…​
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…​]
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
```

examples
```
git reset              // unstage all the files
git reset file.html    // unstage only file.html
```

You can also use git reset to discard last commit and revert back to the previous one like this
```
git reset --hard HEAD~1        // discard last commit and checkout the commit done before
git reset --hard HEAD~3        // discard last 3 commits and revert back to the 4th last commit
```

