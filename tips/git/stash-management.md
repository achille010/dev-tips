# Stash Management

##  Problem

You're in the middle of working on a feature when an urgent bug fix request comes in. You don't want to commit unfinished work, but you also don't want to lose it. You need a way to save your work temporarily.

##  Solution

`git stash` saves your uncommitted changes to a stack, leaving a clean working directory so you can switch contexts. You can apply the saved stash later.

##  Example

```bash
# Save current changes (tracked files)
git stash

# Save with a descriptive name (recommended)
git stash save "WIP: user profile page redesign"

# Include untracked files too
git stash -u
# or
git stash --include-untracked

# Include ignored files as well
git stash -a
# or
git stash --all

# List all stashes
git stash list
# stash@{0}: On feature/login: WIP: user profile page redesign
# stash@{1}: On main: Fix header styles
# stash@{2}: WIP on feature/auth: d4e5f6a Add JWT support

# Apply most recent stash (keeps stash on stack)
git stash apply

# Apply most recent stash (removes from stack)
git stash pop

# Apply a specific stash by index
git stash apply stash@{2}

# View contents of a stash
git stash show stash@{0}
git stash show -p stash@{0}  # show full diff

# Create a branch from a stash
git stash branch feature/login stash@{0}

# Delete a specific stash
git stash drop stash@{1}

# Delete all stashes
git stash clear
```

##  Explanation

### Stash is a Stack (LIFO)
Each stash push goes on top. `git stash pop` removes from the top. Use index notation (`stash@{n}`) to access specific entries.

### When to Use Stash vs Commits
| Situation | Use |
|-----------|-----|
| Switching to urgent task | `git stash` |
| End of work session but not done | `git commit -m "WIP: ..."` |
| Sharing WIP with colleague | `git commit` (stash is local only) |

### Stash Structure
```
stash@{0}: WIP on feature/login: a1b2c3d Add login form
            │         │          │
            │         │          └── SHA of HEAD when stashed
            │         └── Branch when stashed
            └── Index (0 = newest)
```

##  Related Tips

- [Interactive Rebase](interactive-rebase.md)
- [Branch Strategies](branch-strategies.md)
- [Undo Mistakes](undo-mistakes.md)

---

[← Back to Git Tips](README.md)
