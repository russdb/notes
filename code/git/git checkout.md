https://git-scm.com/docs/git-checkout  
https://www.w3docs.com/learn-git/git-checkout.html

Git checkout is used to switch branches and if you don’t specify a branch name it updates files in the working tree to that in the index (staging area).

```
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [--] <pathspec>…​
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] --pathspec-from-file=<file> [--pathspec-file-nul]
git checkout (-p|--patch) [<tree-ish>] [--] [<pathspec>…​]
````

### Description  


Updates files in the working tree to match the version in the index or the specified tree. If no pathspec was given, git checkout will also update HEAD to set the specified branch as the current branch.

git checkout [branch]

*To prepare for working on [branch], switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the [branch].*

### Examples
The following sequence checks out the master branch, reverts the Makefile to two revisions back, deletes hello.c by mistake, and gets it back from the index.

	$ git checkout master             (1)
	$ git checkout master~2 Makefile  (2)
	$ rm -f hello.c
	$ git checkout hello.c            (3)

1. switch branch

2. take a file out of another commit

3. restore hello.c from the index

If you want to check out all C source files out of the index, you can say
