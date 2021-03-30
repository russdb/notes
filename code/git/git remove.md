https://git-scm.com/docs/git-rm  



git-rm - Remove files from the working tree and from the index


```
git rm [-f | --force] [-n] [-r] [--cached] [--ignore-unmatch]
	  [--quiet] [--pathspec-from-file=<file> [--pathspec-file-nul]]
	  [--] [<pathspec>…​]
```

### Description

Remove files matching pathspec from the index, or from the working tree and the index. git rm will not remove a file from just your working directory. (There is no option to remove a file only from the working tree and yet keep it in the index; use /bin/rm if you want to do that.) The files being removed have to be identical to the tip of the branch, and no updates to their contents can be staged in the index, though that default behavior can be overridden with the -f option. When --cached is given, the staged content has to match either the tip of the branch or the file on disk, allowing the file to be removed from just the index. 

### Examples

`git rm Documentation/\*.txt`

Removes all *.txt files from the index that are under the Documentation directory and any of its subdirectories.

Note that the asterisk * is quoted from the shell in this example; this lets Git, and not the shell, expand the pathnames of files and subdirectories under the Documentation/ directory.
`git rm -f git-*.sh`

Because this example lets the shell expand the asterisk (i.e. you are listing the files explicitly), it does not remove subdir/git-foo.sh.

`git rm index.html`     // delete index.html from staging area and working directory.