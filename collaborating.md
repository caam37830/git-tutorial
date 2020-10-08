# Collaborating with Git

This file contains information about working with other people over git

## Setup

First, everyone should clone the same repository from GitHub.


## Branching

By default, git repositories have a master branch which is the "official" version of the code.

If multiple people are working on the same code at the same time, conflicts might occur.  Ideally, everyone works in an independent branch, which will eventually be merged with the master branch.

In order to create a new branch, you can run
```
git checkout -b <branchname>
```
Now, you have a branch that starts with the same code as the master branch, and can eventually be merged back into the master branch.  You can work in this branch without having conflicts with changes in other branches, such as master.

You can list available branches using
```
git branch
```

In order to switch to a different branch, you can use `git checkout`
```
git checkout branch1 # checks out branch1
```
Note that this will change the contents of the files in the repository based on their state in `branch1`

When you are done with a branch (after merging it into the master branch), you can delete the branch with
```
git branch -d <branchname>
```

## Merging

When multiple people work on the same repository, they may need to merge their work together.  Ideally, everyone works in their own branch, so it isn't necessary to resolve conflicts frequently.

In order to merge the contents of branch `branch1` into master, you can run
```
git checkout master # checks out master branch
git merge branch1 # merges contents of branch1 into master
```

If you're lucky, git will figure out how to merge everything automatically.  Otherwise, you'll need to manually merge files.

You can launch a tool to merge files using
```
git mergetool
```
You can set this using `git config --global merge.tool <mergetool name>`

Alternatively, you can edit files in a text editor.

Merging will require a new commit.  If you have to do a manual commit, you may need to do this yourself.  If the merging completes automatically, a commit will be created automatically.

Finally, you should `git push` the contents of `master` so that your collaborators can have access to the up-to-date version.

## Some Additional Commands

remove a file from the repository:
```bash
git rm badfile.txt
```
moving a file:
```bash
git mv moved.txt
```

* git log

Git log will display a history of commits and messages

```bash
git log
git log --stat # show which files were changed and # lines changed
```

* git reset  

git reset can perform the opposite of git add if you don't wish to commit changes to a particular file
```bash
git add file.txt # stage file for commit
git reset file.txt # remove file from staging
```
Sometimes you may want to completely discard your changes because you went down the wrong path.
```bash
git reset --hard <commit> # return tracked files to the state they were in at <commit>
git reset --hard # return to state of last commit
```

* git rebase

Sometimes, you may wish to change the start of a branch from one place to another.  This is useful if changes on a branch do not rely on changes that occurred after the branch was formed.

```bash
git rebase master branch # rebases branch to be on master
```

* .gitignore

This isn't actually a command, but you can create a file that will tell git to ignore certain files or types of files.

```
# .gitignore
secrets.txt # don't share secrets
*~ # emacs temp files - * is a wildcard
```

This section came from [this repository](https://github.com/icme/cme257-advanced-julia/blob/master/class/class4/class4.md)
