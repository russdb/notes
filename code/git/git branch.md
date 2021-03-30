https://git-scm.com/docs/git-branch


```git branch <new-branch>              // create a new branch with all the contents of working directory
git branch <new-branch> f71ac24d     // create a new branch based on a commit
git branch <new-branch> v1.2         // create a new branch from a tag
git branch --track <new-branch> origin/<base-branch> // create a new branch from remote branch
git branch -d <branch-name    // delete a branch
```

### Description

If --list is given, or if there are no non-option arguments, existing branches are listed; the current branch will be highlighted in green and marked with an asterisk. Any branches checked out in linked worktrees will be highlighted in cyan and marked with a plus sign. Option -r causes the remote-tracking branches to be listed, and option -a shows both local and remote branches.

For branching you need to use git branches command. It can be used to create a branch based on another branch or a tag its syntax is as follows:

### Examples
Start development from a known tag

	$ git clone git://git.kernel.org/pub/scm/.../linux-2.6 my2.6
	$ cd my2.6
	$ git branch my2.6.14 v2.6.14   (1)
	$ git switch my2.6.14

1. This step and the next one could be combined into a single step with "checkout -b my2.6.14 v2.6.14".

Delete an unneeded branch

    $ git clone git://git.kernel.org/.../git.git my.git
    $ cd my.git
    $ git branch -d -r origin/todo origin/html origin/man (1)
    $ git branch -D test (2)

1. Delete the remote-tracking branches "todo", "html" and "man". The next fetch or pull will create them again unless you configure them not to. See git-fetch[1].

2.  Delete the "test" branch even if the "master" branch (or whichever branch is currently checked out) does not have all commits from the test branch.

Listing branches from a specific remote

    $ git branch -r -l '<remote>/<pattern>'                 (1)
    $ git for-each-ref 'refs/remotes/<remote>/<pattern>'    (2)

1. Using -a would conflate <remote> with any local branches you happen to have been prefixed with the same <remote> pattern.
2. Patterns will normally need quoting.
