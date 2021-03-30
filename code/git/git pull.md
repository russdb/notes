https://git-scm.com/docs/git-pull



git-pull - Fetch from and integrate with another repository or a local branch


`git pull options | repository | refspec…`

### Description

ncorporates changes from a remote repository into the current branch. In its default mode, git pull is shorthand for git fetch followed by git merge FETCH_HEAD.

More precisely, git pull runs git fetch with the given parameters and calls git merge to merge the retrieved branch heads into the current branch. With --rebase, it runs git rebase instead of git merge.

<repository> should be the name of a remote repository as passed to git-fetch[1]. <refspec> can name an arbitrary remote ref (for example, the name of a tag) or even a collection of refs with corresponding remote-tracking branches (e.g., refs/heads/*:refs/remotes/origin/*), but usually it is the name of a branch in the remote repository.

### Examples


Update the remote-tracking branches for the repository you cloned from, then merge one of them into your current branch:

```
$ git pull
$ git pull origin
```

Normally the branch merged in is the HEAD of the remote repository, but the choice is determined by the branch.<name>.remote and branch.<name>.merge options; see git-config[1] for details.

Merge into the current branch the remote branch next:

`$ git pull origin next`

This leaves a copy of next temporarily in FETCH_HEAD, and updates the remote-tracking branch origin/next. The same can be done by invoking fetch and merge:

`$ git fetch origin`
`$ git merge origin/next`

If you tried a pull which resulted in complex conflicts and would want to start over, you can recover with git reset.

