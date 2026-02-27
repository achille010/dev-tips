# Undo Mistakes in Git

## 🎯 Problem

You accidentally committed to the wrong branch, pushed sensitive data, or made changes you need to undo. Git has many undo mechanisms but they're confusing to distinguish.

## ✨ Solution

Match the undo operation to the situation. Git mistakes are almost always recoverable.

## 💻 Example

### Uncommitted Changes
```bash
# Discard changes to a specific file (irreversible!)
git checkout -- filename.js
# or (modern syntax)
git restore filename.js

# Discard ALL uncommitted changes (irreversible!)
git restore .
# or
git reset --hard

# Unstage a file (keep changes in working directory)
git restore --staged filename.js
# or (older syntax)
git reset HEAD filename.js
```

### Amending the Last Commit
```bash
# Change the commit message of the last commit
git commit --amend -m "New correct message"

# Add a forgotten file to the last commit
git add forgotten-file.js
git commit --amend --no-edit   # uses existing message

# ⚠️ Don't amend commits you've already pushed to shared branches!
```

### Undoing Recent Commits
```bash
# Undo 1 commit — keep changes STAGED
git reset --soft HEAD~1

# Undo 1 commit — keep changes in WORKING DIRECTORY (unstaged)
git reset --mixed HEAD~1

# Undo 1 commit — DISCARD all changes (dangerous!)
git reset --hard HEAD~1

# Undo N commits
git reset --mixed HEAD~3
```

### Safe Undo for Shared Branches (git revert)
```bash
# Creates a NEW commit that reverses the specified commit
# Safe! Doesn't rewrite history.
git revert a1b2c3d

# Revert a range of commits (exclusive..inclusive)
git revert HEAD~3..HEAD
```

### Recover Lost Commits (Reflog)
```bash
# Every HEAD movement is recorded in reflog
git reflog
# HEAD@{0}: reset: moving to HEAD~1
# HEAD@{1}: commit: Add payment feature  ← your "lost" commit

# Restore the lost commit
git reset --hard HEAD@{1}
# or create a new branch from it
git checkout -b recovery HEAD@{1}
```

## 📝 Explanation

### Decision Tree
```
Did you push?
├── No → reset --soft/mixed/hard OR amend
└── Yes → Shared branch?
    ├── No → git push --force (with care)
    └── Yes → git revert (creates new undo commit)
```

### reset vs revert
| | `reset` | `revert` |
|-|---------|----------|
| History | Rewrites it | Adds to it |
| Shared branches | ❌ Dangerous | ✅ Safe |
| Undone how | Moves HEAD back | New commit |

## 🔗 Related Tips

- [Interactive Rebase](interactive-rebase.md)
- [Bisect for Debugging](bisect-for-debugging.md)

---

[← Back to Git Tips](README.md)
