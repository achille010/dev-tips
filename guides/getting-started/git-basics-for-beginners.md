# Git Basics for Beginners

## 📖 Overview

Git is the industry-standard version control system. This guide covers the essential commands you need to start using Git effectively in real projects.

## 🎯 Prerequisites

- Terminal installed and comfortable with basic commands
- Git installed (see [Setting Up Development Environment](setting-up-development-environment.md))

## 📋 Core Concepts

### What is Git?
Git tracks changes to your files over time. Think of it like save points in a video game — you can always go back to a previous save if something goes wrong.

```
Working Directory → Staging Area → Repository (History)
     (files)          (index)        (.git folder)
```

## 📋 Steps

### Step 1: Initialize or Clone a Repository
```bash
# Start a new project
mkdir my-project && cd my-project
git init              # creates .git folder

# Clone an existing project
git clone https://github.com/username/repo.git
git clone git@github.com:username/repo.git  # via SSH
```

### Step 2: The Basic Workflow
```bash
# 1. Check what's changed
git status

# 2. Stage files for commit
git add filename.js       # stage one file
git add .                 # stage everything changed

# 3. Review what you're about to commit
git diff --staged

# 4. Commit with a message
git commit -m "Add user authentication form"
```

### Step 3: Working with Branches
```bash
# Create and switch to new branch
git checkout -b feature/login-page
# (modern alternative)
git switch -c feature/login-page

# Switch between branches
git checkout main
git switch main

# List all branches
git branch              # local only
git branch -a           # including remote

# Merge feature into main
git checkout main
git merge feature/login-page

# Delete branch after merge
git branch -d feature/login-page
```

### Step 4: Working with GitHub/Remote
```bash
# Link local repo to GitHub
git remote add origin git@github.com:username/repo.git

# Push commits to GitHub
git push origin main            # first push
git push                        # subsequent pushes (if tracking set)

# Pull latest changes from GitHub
git pull origin main

# See remote info
git remote -v
```

### Step 5: Everyday Commands
```bash
git log --oneline               # compact history
git diff                        # unstaged changes
git diff --staged               # staged changes (before commit)
git show a1b2c3d                # details of a commit
git blame filename.js           # who changed each line
```

## ⚠️ Common Pitfalls

1. **Committing to main directly** — always use feature branches
2. **Committing secrets** — add `.env` to `.gitignore` BEFORE the first commit
3. **`git add .` without `git status` first** — check what you're staging
4. **Merge conflicts panic** — they're normal, just edit the file to resolve

## ✅ Best Practices

- Commit early, commit often (small commits)
- Write clear commit messages (imperative mood: "Add feature")
- Pull before you push
- Never force push to shared branches

## 📚 Further Reading

- [Commit Message Conventions](../../tips/git/commit-message-conventions.md)
- [Branch Strategies](../../tips/git/branch-strategies.md)

---

[← Back to Getting Started](../README.md) | [← Back to Guides](../../README.md)
