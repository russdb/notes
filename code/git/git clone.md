https://git-scm.com/docs/git-clone

`git clone [--template=<template_directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git dir>]
	  [--depth <depth>] [--[no-]single-branch] [--no-tags]
	  [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
	  [--[no-]remote-submodules] [--jobs <n>] [--sparse]
	  [--filter=<filter>] [--] <repository>
	  [<directory>]`  
	  
### Description

Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository (visible using git branch --remotes), and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

After the clone, a plain git fetch without arguments will update all the remote-tracking branches, and a git pull without arguments will in addition merge the remote master branch into the current master branch, if any (this is untrue when "--single-branch" is given; see below).

This default configuration is achieved by creating references to the remote branch heads under refs/remotes/origin and by initializing remote.origin.url and remote.origin.fetch configuration variables.

	  
### Options:  

EXAMPLES

    Clone from upstream:

    $ git clone git://git.kernel.org/pub/scm/.../linux.git my-linux
    $ cd my-linux
    $ make

    Make a local clone that borrows from the current directory, without checking things out:

    $ git clone -l -s -n . ../copy
    $ cd ../copy
    $ git show-branch

    Clone from upstream while borrowing from an existing local directory:

    $ git clone --reference /git/linux.git \
    	git://git.kernel.org/pub/scm/.../linux.git \
    	my-linux
    $ cd my-linux

    Create a bare repository to publish your changes to the public:

    $ git clone --bare -l /home/proj/.git /pub/scm/proj.git

