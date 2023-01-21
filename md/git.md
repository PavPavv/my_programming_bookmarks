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

Delete local branch

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
git pill origin branch-name-here
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

Cancel last local commit of the current branch

```bash
git reset --hard HEAD^
```

## Commits

Commits history

```bash
git log
```

Restore file of the current branch from stages status

```bash
git reset HEAD file-name-here
```

Roll back commit by commit hash from the log

```bash
git revert commit-hash-here
```

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
