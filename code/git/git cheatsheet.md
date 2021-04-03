[[git init]]   //initialize or reinitialize a repository   
[[git clone]] https://github.com/mateenkiani/react-tutorials     // clone a repository  
[[git add]] hello.py     // add hello.py file to staging area  
[[git add]] -A           // add new files, update modified files and remove deleted files from staging area  
[[git add]] -u           // update modified files and remove deleted files from staging area
[[git status]]     // current status of the working tree  
[[git diff]]              // show all the unstaged changes  
[[git diff]] index.html   // show all the unstaged changes in index.html file  
[[git commit]] -m "commit message here"       // commit staged changes  
[[git commit]] -a -m "commit message here"    // stage and commit changes but ignores newly created files.
[[git reset]]              // unstage all the files
[[git reset]] file.html    // unstage only file.html
[[git reset]] --hard HEAD~1        // discard last commit and checkout the commit done before
[[git reset]] --hard HEAD~3        // discard last 3 commits and revert back to the 4th last commit
[[git remove]] index.html     // delete index.html from staging area and working directory.
[[git mv]] index.html file.html        // rename index.html to file.html
[[git mv]] index.html ./src            // move index.html to ./src/index.html
[[git branch]] new-branch    // create a new branch with all the contents of working directory
[[git branch]] <new-branch> f71ac24d     // create a new branch based on a commit
[[git branch]] <new-branch> v1.2         // create a new branch from a tag
[[git branch]] --track <new-branch> origin/<base-branch> // create a new branch from remote branch
[[git branch]] -d <branch-name    // delete a branch
[[git switch]] <branch-name>  // switch to specifi`ed branch
[[git checkout]]                     // updates the working directory with the files in the index.
[[git checkout]] master              // alternate way to switch between branches
[[git log]]      // shows all the commits you made along with author name and time of commit
[[git remote]] add origin <repo-url>     // add a remote named origin to a remote repository
[[git remote]] -v    // verify the remotes
[[git push]] origin master       // pushes to a remote master branch, where origin is name of the remote you added
[[git fetch]] origin master     // fetch from a remote repository
[[git merge]] <branch-name>      // merge a branch with current directory
[[git pull]] origin master      // fetch and merge from remote repository
[[git stash]]             // save all the local changes
[[git stash]] pop         // apply and drop all the saved changes
[[git stash]] apply       // only apply all the previously saved changes
[[git tag]] <tag_name> <commit_id>       // add a tag to a commit
[[git tag]]                              // display all the tags
[[git checkout]] <tag>                   // checkout a specific tag