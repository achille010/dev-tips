# Interactive Rebase

##  Problem

Your commit history is messy — typo fixes, WIP commits, and forgotten changes are cluttering the log before you open a pull request. You need a way to clean up commits before sharing your work.

##  Solution

`git rebase -i` (interactive rebase) lets you rewrite commit history: squash commits, reword messages, reorder commits, or drop them entirely — before sharing with others.

##  Example

```bash
# Rewrite the last 4 commits
git rebase -i HEAD~4

# Git opens your editor with:
pick a1b2c3d Add user authentication
pick e4f5a6b Fix typo in auth service
pick b7c8d9e WIP: add password validation
pick f1a2b3c Add password validation tests

# Commands you can use:
# p, pick   = use commit as-is
# r, reword = use commit, but edit the message
# e, edit   = use commit, but stop for amending
# s, squash = meld into previous commit (keeps both messages)
# f, fixup  = meld into previous commit (discards this message)
# d, drop   = remove the commit

# Clean version:
pick a1b2c3d Add user authentication
fixup e4f5a6b Fix typo in auth service
squash b7c8d9e WIP: add password validation
pick f1a2b3c Add password validation tests
```

After saving, git replays commits with your changes. The result is a clean, logical history.

```bash
# Resulting commits:
a1b2c3d Add user authentication
c3d4e5f Add password validation  (squashed from 2 commits)
f1a2b3c Add password validation tests
```

##  Explanation

Interactive rebase rewrites local history. The commits get new SHA hashes, so:
-  Safe on feature branches you haven't shared yet
-  **DON'T rebase shared/public branches** — it will confuse teammates

### Useful Rebase Flags
```bash
git rebase -i HEAD~n     # Rewrite last n commits
git rebase -i <commit>   # Rewrite commits after this SHA
git rebase --abort       # Cancel rebase, restore original state
git rebase --continue    # After resolving conflicts, continue
```

##  Related Tips

- [Merge vs Rebase](merge-vs-rebase.md)
- [Undo Mistakes](undo-mistakes.md)
- [Commit Message Conventions](commit-message-conventions.md)

---

[← Back to Git Tips](README.md)
