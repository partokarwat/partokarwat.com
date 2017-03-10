+++
date = "2017-02-26"
topics = ["Development"]
tags = ["udacity","version control","git","github"]
description = "This is my summary of the same spelling udacity course."
title = "How to use Git and GitHub"

+++
You can find the corresponding udacity course [here] (https://www.udacity.com/course/how-to-use-git-and-github--ud775).

# Command-line basics

| Command        | What does it?           | Did you know?  |
| -------------- |-------------------------| ------------------|
| mkdir name    | Create new folder "name"      |    |
| subl filename.txt     | Create new file, opened with sublime |      |
| pwd     | Shows what directory you are in | pwd = **p**rint **w**orking **d**irectory     |
| ls     | List the files in this directory |      |

# Git

There exist 3 locations for a file:

- The **working directory** is the folder, where you work in. If you create a file it is in it.
- The **staging area** is the area between your directory and the repository. If you want to bring a file from your working directory to the repository it has to pass through the staging area. The staging area holds what will go to the repository.
- The **repository** is a folder that contains a documented state of every file in it.

Octopus = strategy Git uses to combine many different versions together.

## How often to commit?

- keep commits small, but not to small
- **one commit per logical change**:
  - 1 commit for fixed a typo
  - 1 commit for fixed a bug

## Basic commands

| Command        | What does it?           |
| -------------- |-------------------------|
| git log | Show the log of the current branch |
| git log \-\-oneline | Show short log for the current branch |
| git log \-\-stat | Show the log with changed files log |
| git diff file1 file2 | Compare two versions of a file *line by line* |

 All file content in 1 line will always diff &rArr; **keep lines short!** (max. length of 80 - 120 characters)

| Command        | What does it?           |
| -------------- |-------------------------|
| git checkout versionId | Go to a specific commit version |
| git status | Show all files changed since the last commit |
Run ```git status``` frequently!

| Command        | What does it?           |
| -------------- |-------------------------|
| git init | Make a repository out of a folder |
| git add | Add files to staging area |
| git commit -m "Message" | Bring files from staging area to the repository|
| git diff \-\-staged | Show diff between staging area and repository |
| git diff | Show delta between working directory and staging area |
| git reset \-\-hard | Delete all changes in working directory and staging area. Use carefully |

## Commit message structure

```
type: Subject

body

footer
```

### The type can be one of these

| Type | Description |
| --- | --- |
| **feat:** | a new feature |
| **fix:** | a bug fix |
| **docs:** | changes to documentation |
| **style:** | formatting, missing semi colons, etc.: no code change |
| **refactor:** | refactoring production code |
| **test:** | adding tests, refactoring tests; no production code change |
| **chore:** | updating build tasks, package manager configs, etc; no production code here |

### Subject < 50 characters

It has to start with a capital letter and no period at the end. Use imperative tone to describe: "Change" not "changed" or "changes".

### Body (optional)

Explain the **what** and **why** of a commit. Don't explain the how! The length of each line should be < 72 characters.

### Footer (optional)

Reference **issue tracker IDs** here. Ex.:
```
Resolves: #123
See also: #456, #789
```
## Branches

| Command        | What does it?           |
| -------------- |-------------------------|
| git branch | Show all branches |
| git branch name-of-branch | Create branch |
| git log \-\-graph \-\-oneline branchname1 branchname2 | Generate diagram = Show log of 2 branches graphically|

Use always ```-``` instead of spaces in branch names.

Every commit (o) only knows his precursor (&larr;o&larr;o). Means that if one commit is lost, you will lose all the commits that have been before this one.

| Command        | What does it?           |
| -------------- |-------------------------|
| git checkout -b new-branch-name | Corresponds to git branch new-branch-name and git checkout new-branch-name |
| git merge master coins | Merge coins branch into master branch |

**Always checkout one** of the two **branch**es you are planning on merging **before doing the merge**.

| Command        | What does it?           |
| -------------- |-------------------------|
| git merge \-\-abort | Restore file to state before start of merge |
| git merge coins | Merge branch coins into active branch |

```git merge master coins``` and ```git merge coins``` are equal if you are on master branch.

| Command        | What does it?           |
| -------------- |-------------------------|
| git branch -d coins | Delete branch "coins" |
| git log -n 1 | Give the log a fix number of commits. Here 1 commit. |

## GitHub

| Command        | What does it?           |
| -------------- |-------------------------|
| git fetch | Update local copy (working directory) |
| git push | Bring staging area to the repository |
| git pull | git fetch and then git merge |
| git remote add origin link@website | Create remote |
| git remote -v | Show remotes with url for fetch and push |

Forking is a fair and better way to start an own work based on an existing repository. It is a clone from GitHub to GitHub. Fork the repository and then clone your fork and start working.

| Command        | What does it?           |
| -------------- |-------------------------|
| git clone link@website | Clone a repository |

<div style="float: left">
![Parto Karwat](/media/pull-request.png)
</div>
A **pull request** is a GitHub specific request to pull a branch into the master branch. If it is your repository and you got the pull request, then you can use the button *merge pull request* to complete.

**Written with <span style="color:firebrick">&hearts;</span> in Kiel.**
