### More details: 

_git init_  https://git-scm.com/docs/git-init

This command creates an empty Git repository - basically a .git directory with subdirectories for objects, refs/heads, refs/tags, and template files. An initial HEAD file that references the HEAD of the master branch is also created.  

If the $GIT_DIR environment variable is set then it specifies a path to use instead of ./.git for the base of the repository.

If the object storage directory is specified via the $GIT_OBJECT_DIRECTORY environment variable then the sha1 directories are created underneath - otherwise the default $GIT_DIR/objects directory is used.

Running git init in an existing repository is safe. It will not overwrite things that are already there. The primary reason for rerunning git init is to pick up newly added templates (or to move the repository to another place if --separate-git-dir is given).

### Options  

-q
--quiet

    Only print error and warning messages; all other output will be suppressed.
--bare

    Create a bare repository. If GIT_DIR environment is not set, it is set to the current working directory.

### Examples

Start a new Git repository for an existing code base

    $ cd /path/to/my/codebase
    $ git init      (1)
    $ git add .     (2)
    $ git commit    (3)

        Create a /path/to/my/codebase/.git directory.

        Add all existing files to the index.

        Record the pristine state as the first commit in the history.
