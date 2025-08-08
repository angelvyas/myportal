---
title: 'GIT - Global Information Tracker'
date: 2025-07-08
draft:  false
featured: false  
description: "GIT - Global Information Tracker"
thumbnail: "/posts/general/images/git.png"
featureImage: "/posts/general/images/git.png" 
shareImage: "/posts/general/images/git.png"
author: "Angel Vyas"
tags:
    - Git
categories:     
    - DevOps
    - Git
---

## 1. **What is Git?**
Git is a **distributed version control system** (DVCS) that helps track changes in code and coordinate work between multiple people.  
It works locally on your machine and allows you to:
- Save snapshots of your code (commits).
- View and revert changes.
- Work in multiple branches for different features.
- Merge changes from different sources.

**Key points about Git:**
- **Distributed** → Every developer has the full history of the project.
- **Snapshots** → Git stores snapshots, not just file differences.
- **Branching** → Create and switch between versions of code easily.
- **Merging & Rebasing** → Combine work from different branches.

---

## 2. **Git Core Concepts**
### Repository (Repo)
A directory containing:
- Your code.
- A hidden `.git` folder (stores Git’s history and metadata).

### Commit
A saved version of your project at a specific time.

### Branch
A parallel line of development in Git.  
Example: `main`, `dev`, `feature-xyz`.

### Remote
A version of your repository hosted elsewhere (like on GitHub).

### HEAD
A pointer to your current commit/branch.

---

## 3. **What is GitHub?**
GitHub is a **cloud-based hosting service** for Git repositories.  
It adds features on top of Git:
- Remote repository hosting.
- Collaboration tools (Pull Requests, Issues, Discussions).
- Access control and team management.
- CI/CD integrations.

**Key difference:**
- **Git** → The tool for version control.
- **GitHub** → A platform to store, share, and collaborate using Git.

---

## 4. **Git Workflow Overview**
1. **Local Work** (in your machine):
   - Edit files.
   - Stage changes → `git add` (to stage all deletions in one go use `git add -u`)
   - Commit changes → `git commit`

2. **Sync with Remote**:
   - Pull latest changes → `git pull`
   - Push your changes → `git push`

3. **Collaboration**:
   - Create branches for features or fixes.
   - Merge changes via Pull Requests (PRs) or locally.
   - Resolve conflicts if multiple people edit the same lines.

---

# 🧠 **Git Command Cheat Sheet**

## 🔧 SETUP & CONFIGURATION

| Command | Description |
|--------|-------------|
| `git --version` | Check Git version |
| `git config --global user.name "Your Name"` | Set Git username |
| `git config --global user.email "you@example.com"` | Set Git email |
| `git config --global core.editor code` | Set default editor (like VS Code) |
| `git config --list` | See current Git settings |
| `git config --global push.autoSetupRemote true` | to always set upstream automatically on first push. </br> Then git push on a new branch will automatically do the linking.|


---

## 📁 REPOSITORY MANAGEMENT

| Command | Description |
|--------|-------------|
| `git init` | Create a new local Git repo |
| `git clone <url>` | Clone remote repo to local |
| `cd folder_name` </br> `git clone <url> .` | then the folder becomes the repo root.|
| `git remote add origin <url>` | Add remote repo (Now your local repo knows that origin = that GitHub repo, </br> it's just the nickname for the url (repo), could be anything prod,</br> upstream, github,etc.)|
| `git remote set-url origin <url>` | To change the origin url|
| `git remote rename origin github` | changing name of remote from origin to github|
| `git remote remove origin` | To delete the link to remote repo|
| `git remote -v` | Show remote URLs |



---

## 📊 STATUS & INFO

| Command | Description |
|--------|-------------|
| `git status` | Show current status (changes, staged files, etc.) |
| `git log` | Show commit history |
| `git log --oneline` | Compact log |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |

---

## 📥 STAGING & COMMITTING

| Command | Description |
|--------|-------------|
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Commit staged changes |
| `git commit -am "message"` | Stage and commit tracked files only |
| `git restore <file>` | Undo changes in working directory |
| `git reset <file>` | Unstage a file |
| `git reset --hard` | Reset working and staging to last commit, means you told git </br> to thow away all uncommitted changes in both working and staging area </br> If you're file has uncommitted changes then it's gone. |

---

## 🔁 BRANCHING & MERGING

| Command | Description |
|--------|-------------|
| `git branch` | List branches |
| `git branch <name>` | Create a branch |
| `git checkout <name>` | Switch to branch |
| `git checkout -b <name>` | Create + switch |
| `git merge <branch>` | Merge into current branch |
| `git rebase <branch>` | Reapply commits onto another branch |
| `git branch -d <name>` | Delete branch |

> **NOTE:** Consider two branches main and testing, when you're running rebase, i.e., git rebase testing (inside main branch), then what it does is base as testing, main’s commits are temporarily detached from the branch and being applied onto testing.
> if we consider two branches as main and feature, then rebasing on main is blowing away the feature branch commits, and dupicating them as new commits on the top of the main branch.

**AFTER REBASING**:
When you try to push, Git says:

“Your branch history is different from the remote — I won’t overwrite without your permission.”
two options two solve this:</br>
-  Force push (safe only if you’re the only one working on this branch)</br>
`git push -f` or `git push --force-with-lease`
- Don’t rewrite history (merge instead)</br>
`git pull --rebase=false`</br>
then, `git push`
---

## 📤 PUSHING & PULLING

| Command | Description |
|--------|-------------|
| `git push` | Push changes to remote |
| `git push origin <branch>` | Push branch to remote |
| `git pull` | Fetch + merge changes from remote |
| `git fetch` | Fetch changes without merging |
| `git push -u origin <branch-name>` |If you only want to set upstream for a specific branch, -u (or --set-upstream)|

> **NOTE:** - When you clone a repo, your default branch (often main or master) already has an upstream — it’s linked to the remote’s same branch.
>- But when you make a new local branch: it’s not automatically connected to a remote branch. (last bullet).
>- Note for each new repo, you have to add upstream or remote.
>- Note if you're using ssh key for your system, then don't just clone using search bar, clone usign ssh url only.


---

## 🚑 UNDO & CLEANUP

| Command | Description |
|--------|-------------|
| `git reset --hard HEAD` | Undo all local changes |
| `git revert <commit>` | Undo a specific commit (safely) |
| `git stash` | Save changes temporarily |
| `git stash pop` | Reapply stashed changes |
| `git clean -fd` | Remove untracked files/directories |

---

## 🧪 TAGGING & RELEASES

| Command | Description |
|--------|-------------|
| `git tag` | List tags |
| `git tag <name>` | Create tag |
| `git tag -a <name> -m "message"` | Annotated tag |
| `git push origin <tagname>` | Push tag to remote |

---

## 🧠 INSPECTION & DEBUGGING

| Command | Description |
|--------|-------------|
| `git show <commit>` | Show details of a commit |
| `git reflog` | Show history of HEAD movements |
| `git blame <file>` | Show who edited each line |
| `git bisect` | Find commit that introduced a bug |

---

## 🔧 ADVANCED (OPTIONAL)

| Command | Description |
|--------|-------------|
| `git cherry-pick <commit>` | Apply a specific commit |
| `git archive` | Export repo to zip/tar |
| `git submodule` | Manage nested repos |
| `git worktree` | Manage multiple working directories |

>**NOTE:** git cherry-pick lets you take a specific commit from any branch and apply it onto your current branch — without merging the entire branch.</br>
Think of it like:</br>
`I don’t want the whole cake, just that one slice.`

---


