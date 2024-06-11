# Cheat sheet: Git

## Set up

Check current credentials

```bash
git config -l
```

Set up git credentials

```bash
git config user.email "some@email.com"
```

```bash
git config user.name "SomeName"
```

---

## Start

Initialize new project

```bash
git init
```

Clone project

```bash
git clone https://...
```

Add remote origin

```bash
git remote origin https://...
```

---

## Branches

Get all the branches

```bash
git fetch
```

Get all the repo's branches

```bash
git branch -a
```

Check all the branches

```bash
git branch
```

Create new branch

```bash
git branch branch-name-here
```

Create new branch and switch to it

```bash
git checkout -b branch-name-here
```

Delete local branch after checking if local branch already been merged

```bash
git branch -d branch-name-here
```

Rename branch name

```bash
git branch -m old-name new-name
```

Switch to a branch

```bash
git checkout branch-name-here
```

Get changes from the remote origin to the current branch

```bash
git pull origin branch-name-here
```

Check differences between two branches

```bash
git diff main..develop
```

To look at the difference between not staged changes and current staged state

```bash
git diff
```

---

## Workflow

Check the status of the current branch changes

```bash
git status
```

Stage all the current branch changes

```bash
git add .
```

Commit all the current branch changes

```bash
git commit -m 'some: message'
```

Publish all the commited current branch changes to the remote origin

```bash
git push origin branch-name-here
```

Checkout to develop branch and update it after merge feature branch

```bash
git checkout develop && git pull origin develop
```

---

## Tips

Hide uncommited changes of the current branch

```bash
git stash
```

Get back hidden uncommited changes of the current branch

```bash
git stash pop
```

Cancel uncommited changes of the current branch

```bash
git restore file-name-here
```

```bash
git restore .
```

Cancel last local commit of the current branch

```bash
git reset --hard HEAD^
```

Archive local repo from git

```bash
git archive --format=zip
```

Verifies the connectivity and validity of the objects in the database

```bash
git fsck
```

Set current file state back to last commit state

```bash
 git checkout HEAD -- <file>
```

## Commits

Commits history

```bash
git log
```

Search for commit with certain text

```bash
git log -S
```

Restore file of the current branch from stages status

```bash
git reset HEAD file-name-here
```

Cancel last local commit of the current branch

```bash
git reset --hard HEAD^
```

Get working flow and index of git to last commit state:

```bash
git reset --hard HEAD
```

Roll back commit by commit hash from the log

```bash
git revert commit-hash-here
```

Check difference between two commits

```bash
git diff <commit_hash_1> <commit_hash_2>
```

Change only author of the last commit

```bash
git commit --amend --reset-author
```

Change text of the last commit without changing codebase

```bash
git commit --amend --no-edit
```

## Blame

Check who changed certain (10, for example) line in certain file last time

```bash
git blame -L 10 <filename>
```

### What the difference between git reset and git revert?

The **git reset** and **git revert** commands in Git are both used to undo changes in a repository, but they work in different ways.

**git reset**: This command is used to reset the current branch to a specific commit. It can be used to move the HEAD and the current branch pointer to a different commit, effectively "rewinding" the history of the branch. There are different modes of git reset such as --soft, --mixed, and --hard, which determine whether the changes made after the specified commit are kept, staged, or discarded.

This command will move the HEAD and the current branch pointer three commits back, discarding any changes made after that point.

```bash
git reset --hard HEAD~3
```

**git revert**: This command creates a new commit that undoes the changes made in a specific commit. It does not modify the existing commit history; instead, it creates a new commit that represents the inverse of the specified commit. This is useful when you want to keep a record of the fact that a particular commit was undone.

This command will create a new commit that undoes the changes introduced by the most recent commit

```bash
git revert HEAD
```

In summary, **git reset** is used to move the current branch to a different point in history, potentially discarding changes, while **git revert** is used to create a new commit that undoes the changes introduced by a specific commit without altering the existing commit history.

## Using rebase

```bash
git pull origin <dev-branch-name>
```

```bash
git checkout <local-branch>
```

```bash
git rebase develop
```

```bash
git push —force-with-lease origin <local-branch>
```

How to undo certain push to origin:

Using **git rebase -i** allows check, edit and delete commits in commit logs in interactive mode.
You should delete target commit and then run **git push --force** to update remote origin forcibly.

```bash
git rebase -i
```

```bash
git push --force
```

Interactive copy commits from one branch to another since certain commit, where **since** is commit, **branch** - source branch and **newbase** is a target branch

```bash
git rebase --onto <newbase> <since> <branch>
```

## Cherry-pick

Put last commit of _feature_ branch to the top od the **main** branch

```bash
git cherry-pick <feature>
```

Cherry-pick commit with certain date

```bash
git log --after='YYYY-MM-DD' --before='YYYY-MM-DD' -1 | grep commit | cut -d ' ' -f 2 | xargs git cherry-pick
```

The following command allows you to apply the changes from a specific commit to your current branch without automatically creating a new commit. This means that the changes will be staged in your working directory, but you will have the opportunity to review and modify them before committing the changes.

```bash
git cherry-pick --no-commit <commit-hash>
```
