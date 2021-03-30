*git diff* - https://git-scm.com/docs/git-diff 



Show changes between the working tree and the index or a tree, changes between the index and a tree, changes between two trees, changes between two blob objects, or changes between two files on disk.

git diff [<options>] [--] [<path>…​]

    This form is to view the changes you made relative to the index (staging area for the next commit). In other words, the differences are what you could tell Git to further add to the index but you still haven’t. You can stage these changes by using git-add[1].
git diff [<options>] --no-index [--] <path> <path>

    This form is to compare the given two paths on the filesystem. You can omit the --no-index option when running the command in a working tree controlled by Git and at least one of the paths points outside the working tree, or when running the command outside a working tree controlled by Git. This form implies --exit-code.
git diff [<options>] --cached [<commit>] [--] [<path>…​]

    This form is to view the changes you staged for the next commit relative to the named <commit>. Typically you would want comparison with the latest commit, so if you do not give <commit>, it defaults to HEAD. If HEAD does not exist (e.g. unborn branches) and <commit> is not given, it shows all staged changes. --staged is a synonym of --cached.
git diff [<options>] <commit> [--] [<path>…​]

    This form is to view the changes you have in your working tree relative to the named <commit>. You can use HEAD to compare it with the latest commit, or a branch name to compare with the tip of a different branch.
git diff [<options>] <commit> <commit> [--] [<path>…​]

    This is to view the changes between two arbitrary <commit>.
git diff [<options>] <commit>..<commit> [--] [<path>…​]

    This is synonymous to the previous form. If <commit> on one side is omitted, it will have the same effect as using HEAD instead.
git diff [<options>] <commit>...<commit> [--] [<path>…​]

    This form is to view the changes on the branch containing and up to the second <commit>, starting at a common ancestor of both <commit>. "git diff A...B" is equivalent to "git diff $(git merge-base A B) B". You can omit any one of <commit>, which has the same effect as using HEAD instead.

Just in case you are doing something exotic, it should be noted that all of the <commit> in the above description, except in the last two forms that use ".." notations, can be any <tree>.

For a more complete list of ways to spell <commit>, see "SPECIFYING REVISIONS" section in gitrevisions[7]. However, "diff" is about comparing two endpoints, not ranges, and the range notations ("<commit>..<commit>" and "<commit>...<commit>") do not mean a range as defined in the "SPECIFYING RANGES" section in gitrevisions[7].

git diff [<options>] <blob> <blob>

    This form is to view the differences between the raw contents of two blob objects.


### Output
Raw output format

The raw output format from "git-diff-index", "git-diff-tree", "git-diff-files" and "git diff --raw" are very similar.

These commands all compare two sets of things; what is compared differs:

git-diff-index <tree-ish>

    compares the <tree-ish> and the files on the filesystem.
git-diff-index --cached <tree-ish>

    compares the <tree-ish> and the index.
git-diff-tree [-r] <tree-ish-1> <tree-ish-2> [<pattern>…​]

    compares the trees named by the two arguments.
git-diff-files [<pattern>…​]

    compares the index and the files on the filesystem.


### Examples


Various ways to check your working tree

    $ git diff            (1)
    $ git diff --cached   (2)
    $ git diff HEAD       (3)

        Changes in the working tree not yet staged for the next commit.

        Changes between the index and your last commit; what you would be committing if you run "git commit" without "-a" option.

        Changes in the working tree since your last commit; what you would be committing if you run "git commit -a"

Comparing with arbitrary commits

    $ git diff test            (1)
    $ git diff HEAD -- ./test  (2)
    $ git diff HEAD^ HEAD      (3)

        Instead of using the tip of the current branch, compare with the tip of "test" branch.

        Instead of comparing with the tip of "test" branch, compare with the tip of the current branch, but limit the comparison to the file "test".

        Compare the version before the last commit and the last commit.

Comparing branches

    $ git diff topic master    (1)
    $ git diff topic..master   (2)
    $ git diff topic...master  (3)

        Changes between the tips of the topic and the master branches.

        Same as above.

        Changes that occurred on the master branch since when the topic branch was started off it.

Limiting the diff output

    $ git diff --diff-filter=MRC            (1)
    $ git diff --name-status                (2)
    $ git diff arch/i386 include/asm-i386   (3)

        Show only modification, rename, and copy, but not addition or deletion.

        Show only names and the nature of change, but not actual diff output.

        Limit diff output to named subtrees.

Munging the diff output

    $ git diff --find-copies-harder -B -C  (1)
    $ git diff -R                          (2)

        Spend extra cycles to find renames, copies and complete rewrites (very expensive).

        Output diff in reverse.

