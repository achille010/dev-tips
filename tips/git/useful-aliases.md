# Useful Git Aliases

##  Problem

Typing `git status`, `git checkout`, `git log --oneline --graph` repeatedly is slow and error-prone. You waste keystrokes on commands you run dozens of times per day.

##  Solution

Configure Git aliases to create shortcuts for frequently used commands. Add them to your global `~/.gitconfig` or per-project `.git/config`.

##  Example

### Essential Aliases
```bash
# Set via command line:
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.lg "log --oneline --graph --decorate --all"

# Or edit ~/.gitconfig directly:
```

```ini
[alias]
    # Shortcuts
    st   = status
    co   = checkout
    br   = branch
    cm   = commit
    sw   = switch              # modern checkout replacement
    df   = diff
    dfs  = diff --staged       # diff of what's about to be committed

    # History
    lg   = log --oneline --graph --decorate --all
    last = log -1 HEAD --stat  # show last commit with file stats
    hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short

    # Productivity
    unstage = reset HEAD --      # unstage a file
    undo    = reset HEAD~1       # undo last commit (keep changes staged)
    save    = !git add -A && git commit -m 'SAVEPOINT'
    wip     = !git add -u && git commit -m 'WIP'
    undo-wip = reset HEAD~1 --mixed

    # Branches
    brs  = branch -a            # list all branches (including remotes)
    bdel = branch -d            # delete local branch (safe)
    bdf  = branch -D            # force delete
    prune-branches = !git branch --merged main | grep -v main | xargs git branch -d

    # Show aliases
    aliases = config --get-regexp alias
```

### Usage
```bash
git st          # instead of: git status
git lg          # beautiful graph log
git last        # see what you just committed
git co -b feat/new-feature   # create and checkout branch
git unstage file.js          # unstage a file
git undo        # undo last commit, keep changes staged
```

##  Explanation

Git aliases also support shell commands by prefixing with `!`:

```ini
[alias]
    # Find the commit that deleted a file
    find-deleted = "!f() { git log --all -- $1; }; f"

    # Undo all local changes (dangerous!)
    nuke = !git reset --hard && git clean -fd

    # List files changed in last commit
    show-files = show --name-only --pretty=format:''
```

##  Related Tips

- [Undo Mistakes](undo-mistakes.md)
- [Stash Management](stash-management.md)

---

[← Back to Git Tips](README.md)
