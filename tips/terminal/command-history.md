# Command History

## 🎯 Problem

You typed a long command earlier and need to run it again, but can't remember it. You're pressing the up arrow 30 times or re-typing from memory.

## ✨ Solution

The shell records every command in a history file. Learn to search, navigate, and control your history efficiently.

## 💻 Example

```bash
# View recent history
history          # show all history with line numbers
history 20       # show last 20 commands
history | grep docker   # find docker commands in history

# Re-run commands
!!               # repeat the LAST command
!42              # repeat command #42 from history
!git             # repeat last command starting with 'git'
!?status         # repeat last command CONTAINING 'status'

# Reverse search (most useful!)
Ctrl + R         # starts interactive reverse search
# Type part of the command → it appears
# Press Ctrl+R again → find older match
# Press Enter → run the matched command
# Press Ctrl+G → cancel search

# Edit & run with editor
fc               # open last command in $EDITOR, run on save
fc 42            # open command #42 in editor

# History expansion tricks
echo !!          # preview the command before running (dry run)
sudo !!          # re-run last command with sudo
!$               # last ARGUMENT of previous command
!*               # all arguments of previous command

# Example:
mkdir -p /very/long/path/to/project
cd !$            # → cd /very/long/path/to/project
```

### Control What Gets Saved

```bash
# ~/.bashrc or ~/.zshrc

# Larger history
export HISTSIZE=10000         # commands in memory
export HISTFILESIZE=20000     # commands on disk

# Don't save duplicates or commands starting with space
export HISTCONTROL=ignoreboth  # = ignorespace:ignoredups

# Timestamp entries
export HISTTIMEFORMAT="%Y-%m-%d %H:%M  "
# history output: 2025-02-27 14:30  git push origin main

# Ignore specific commands from history
export HISTIGNORE="ls:ll:cd:pwd:clear:exit:history"

# Append instead of overwrite (important with multiple terminals!)
shopt -s histappend  # bash
```

## 📝 Explanation

Bash defaults to `~/.bash_history`; Zsh uses `~/.zsh_history`.

The `HISTCONTROL=ignorespace` trick is useful for security: prefix a command with a space and it won't be saved:
```bash
 export SECRET_KEY=abc123  # ← leading space = not in history
```

## 🔗 Related Tips

- [Keyboard Shortcuts](keyboard-shortcuts.md)
- [Useful Aliases](useful-aliases.md)

---

[← Back to Terminal Tips](README.md)
