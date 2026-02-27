# Bisect for Debugging

## 🎯 Problem

A bug appeared "somewhere in the last 200 commits" but you have no idea which one introduced it. Manually checking commits one by one would take hours.

## ✨ Solution

`git bisect` performs a **binary search** through your commit history to find the exact commit that introduced a bug. It requires only O(log n) checks — about 8 checks for 200 commits.

## 💻 Example

```bash
# 1. Start bisect session
git bisect start

# 2. Mark current state as bad (bug exists here)
git bisect bad

# 3. Mark a known-good commit (bug didn't exist)
git bisect good v2.0.0       # can use a tag
# or
git bisect good a1b2c3d      # or a specific SHA

# Git automatically checks out the midpoint commit

# 4. Test that commit — does the bug exist?
# → Yes: git bisect bad
# → No:  git bisect good

# Repeat until git finds the culprit:
# "b7c8d9e is the first bad commit"

# 5. Inspect the offending commit
git show b7c8d9e

# 6. End the session (returns to original HEAD)
git bisect reset

# ─────────────────────────────────────────────
# AUTOMATED BISECT with a test script
# ─────────────────────────────────────────────
# The script should exit 0 if good, 1+ if bad

git bisect start
git bisect bad HEAD
git bisect good v2.0.0

# Automate the testing
git bisect run npm test -- --testNamePattern="failing test"
# or
git bisect run bash -c "./check_bug.sh"

# Git runs your script on each bisect step automatically!
git bisect reset
```

## 📝 Explanation

With 1000 commits between good and bad: `log2(1000) ≈ 10 manual checks` vs 1000 manual checks.

### bisect Log
```bash
git bisect log    # view your good/bad markings
git bisect replay bisect.log  # replay a bisect session
```

## 🔗 Related Tips

- [Undo Mistakes](undo-mistakes.md)
- [Useful Aliases](useful-aliases.md)

---

[← Back to Git Tips](README.md)
