---
tags:
  - git
see also: "[[Git Tips]]"
---
see also: [[Git Tips]]

Git offers a variety of configuration options that can enhance your workflow and improve usability. Here are some notable settings to consider:

### Commit and Merge Settings

|Config Option|Description|
|---|---|
|`rebase.autosquash true`|Automatically squashes commits during a rebase, making it easier to clean up commit history.|
|`merge.conflictstyle diff3`|Provides a clearer view of merge conflicts by showing the common ancestor, aiding in conflict resolution.|
|`commit.verbose true`|Displays the diff of changes in the commit message editor, helping you remember what changes are being committed.|

### Editor and Display Preferences

|Config Option|Description|
|---|---|
|`core.editor "your-editor"`|Sets your preferred text editor for Git commands, improving your editing experience.|
|`color.ui auto`|Enables colored output in the terminal, making it easier to read Git commands and their results.|
|`pager`|Configures the output display for commands like `git log`, enhancing readability.|

### Branch and Tag Management

|Config Option|Description|
|---|---|
|`branch.sort -committerdate`|Sorts branches by the most recent commit date, making it easier to find active branches.|
|`tag.sort version:refname`|Sorts tags by version, which can be useful for managing releases.|

### Miscellaneous Options

|Config Option|Description|
|---|---|
|`core.excludeFiles ~/.gitignore`|Sets a global `.gitignore` file to exclude certain files from all repositories.|
|`push.default simple`|Ensures that `git push` only pushes the current branch to its upstream counterpart.|
|`fetch.prune true`|Automatically removes remote-tracking branches that no longer exist on the remote.|