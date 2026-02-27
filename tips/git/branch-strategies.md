# Branch Strategies

##  Problem

Without a consistent branching strategy, teams push directly to main, step on each other's work, and end up with integration nightmares. Features, fixes, and releases are hard to track.

##  Solution

Adopt a structured branching strategy. The three most popular are **Git Flow**, **GitHub Flow**, and **Trunk-Based Development**.

##  Example

### GitHub Flow (Recommended for Most Teams)

Simple, perfect for continuous deployment:

```bash
# 1. Always start from up-to-date main
git checkout main
git pull origin main

# 2. Create a descriptive feature branch
git checkout -b feat/user-authentication
# naming: type/short-description
# type: feat, fix, docs, refactor, test, chore

# 3. Work in small commits
git commit -m "feat(auth): add login form"
git commit -m "feat(auth): validate credentials against DB"
git commit -m "test(auth): add login form unit tests"

# 4. Keep up-to-date with main (avoid merge conflicts)
git fetch origin
git rebase origin/main

# 5. Push and open Pull Request
git push origin feat/user-authentication
# → Open PR on GitHub → Review → Merge → Delete branch

# 6. Clean up
git checkout main
git pull origin main
git branch -d feat/user-authentication
```

### Branch Naming Conventions
```bash
feat/user-authentication      # New feature
fix/login-redirect-bug        # Bug fix
docs/update-api-readme        # Documentation
refactor/auth-service         # Refactoring
chore/update-dependencies     # Maintenance
hotfix/critical-payment-bug   # Emergency fix to production
release/v2.1.0               # Release preparation
```

### Git Flow (For Scheduled Releases)
```
main ────────────────────────────────→ production
  └── develop ──────────────────────→ integration
        ├── feature/user-auth
        ├── feature/payment
        └── release/v2.0 ────────── → main (tagged)
              └── hotfix/urgent-fix → main + develop
```

##  Explanation

| Strategy | Best For |
|----------|----------|
| **GitHub Flow** | Continuous deployment, small teams |
| **Git Flow** | Scheduled releases, desktop apps |
| **Trunk-Based** | Large teams, feature flags, CI/CD |

### Golden Rules
1. **Never commit directly to main**
2. **Keep branches short-lived** (days, not weeks)
3. **Names reflect purpose**: `fix/header-overflow` not `branch2`
4. **Delete after merge**: keep repo clean

##  Related Tips

- [Merge vs Rebase](merge-vs-rebase.md)
- [Stash Management](stash-management.md)
- [Undo Mistakes](undo-mistakes.md)

---

[← Back to Git Tips](README.md)
