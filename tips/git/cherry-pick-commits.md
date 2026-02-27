# Cherry Pick Commits

##  Problem

A bug fix or specific commit exists on another branch, and you need it in your current branch — without merging the entire branch.

##  Solution

`git cherry-pick` applies the changes of a specific commit onto your current branch, creating a new commit with the same changes.

##  Example

```bash
# View commits on another branch
git log feature/payment --oneline
# a3b4c5d Add payment validation
# e6f7a8b Fix null pointer in checkout  ← you want this!
# b9c1d2e WIP: payment integration

# Apply just that one commit to your branch
git checkout main
git cherry-pick e6f7a8b

# Cherry-pick a range of commits
git cherry-pick a1b2c3d..e4f5a6b  # (exclusive..inclusive)

# Cherry-pick without creating a commit (stage only)
git cherry-pick -n e6f7a8b
git status  # review staged changes
git commit -m "chore: apply fix from payment branch"

# Cherry-pick with custom commit message
git cherry-pick e6f7a8b -e  # opens editor

# If conflicts arise during cherry-pick:
# 1. Resolve conflicts
# 2. git add <resolved-files>
# 3. git cherry-pick --continue
# Or cancel: git cherry-pick --abort
```

##  Explanation

Cherry-pick is useful for:
- **Hotfixes**: Apply a fix from develop → release branch
- **Feature Subsets**: Pull a specific improvement without the full feature
- **Recovering Commits**: Bring back accidentally deleted commits

>  **Warning**: Cherry-picking creates a *copy* of the commit with a new SHA. If both branches eventually merge, git may see it as a conflict. Use sparingly — prefer regular merges when possible.

## 🔗 Related Tips

- [Merge vs Rebase](merge-vs-rebase.md)
- [Interactive Rebase](interactive-rebase.md)
- [Undo Mistakes](undo-mistakes.md)

---

[← Back to Git Tips](README.md)
