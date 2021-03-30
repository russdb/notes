https://git-scm.com/docs/git-mv


### Description
`git mv <options>…​ <args>…​`



Move or rename a file, directory or symlink.

`git mv [-v] [-f] [-n] [-k] <source> <destination>`
`git mv [-v] [-f] [-n] [-k] <source> ... <destination directory>`

In the first form, it renames <source>, which must exist and be either a file, symlink or directory, to <destination>. In the second form, the last argument has to be an existing directory; the given sources will be moved into this directory.

The index is updated after successful completion, but the change must still be committed.

	
To move or rename a file you need to use git mv command. Its syntax is git mv `<source> <destination>.` 
To rename a file use same source and destination but change the file name.

Note: After mv you don’t need to re index any change.
`git mv index.html file.html`        // rename index.html to file.html
`git mv index.html ./src`         // move index.html to ./src/index.html
