# Merge vs Rebase

##  Problem

When integrating changes from one branch to another, you can use `git merge` or `git rebase`. Choosing the wrong one leads to ugly history or confusing conflicts.

##  Solution

Use `git merge` to **preserve branch history** and **communicate that a feature was integrated**. Use `git rebase` to **create a linear history** and **replay commits** on top of the latest main.

##  Example

### The Scenario
```
Before:
main:    A - B - C
feature:     D - E

After merge:
main:    A - B - C - M   (M = merge commit)
                  \/
feature:      D - E

After rebase:
main:    A - B - C
feature:         D'- E'  (D and E replayed on top of C)
# Then fast-forward merge: A - B - C - D' - E'
```

### Using Merge
```bash
git checkout main
git merge feature/user-auth

# → Creates a merge commit that preserves history
# → History shows exactly when the feature was integrated
```

### Using Rebase (Feature Branch)
```bash
# On your feature branch:
git rebase origin/main

# → Replays your commits on top of main
# → Linear history, no merge commit
# → Resolve conflicts commit-by-commit

# After rebase, merge to main:
git checkout main
git merge feature/user-auth  # fast-forward, no merge commit needed
```

##  Explanation

|                                     | Merge                    | Rebase                         |
|-------------------------------------|--------------------------|--------------------------------|
| History                             | Preserves exact history  | Rewrites history (linear)      |
| Merge commit                        | Yes                      | No                             |
| Conflicts                           | Resolve once             | Resolve per commit             |
| Safe on shared branches             | ✅                       |  Risky                         |
| Best for m                          | main/develop integration | Keeping feature branch current |

### The Golden Rule
**Never rebase commits that have been pushed to a shared branch.** Rebasing rewrites commit hashes — if teammates have those commits, their histories diverge.

##  Related Tips

- [Interactive Rebase](interactive-rebase.md)
- [Branch Strategies](branch-strategies.md)
- [Undo Mistakes](undo-mistakes.md)

---

[← Back to Git Tips](README.md)
