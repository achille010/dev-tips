# Useful Terminal Aliases

##  Problem

You type the same long commands dozens of times a day: `ls -la`, `cd ..`, `git status`. Your fingers are tired.

##  Solution

Add shell aliases for your most-used commands. A one-time 5-minute setup eliminates thousands of keystrokes.

##  Example

```bash
# ~/.bashrc or ~/.zshrc

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Navigation
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias ~='cd ~'
alias back='cd -'       # go to previous directory

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# File Listing
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias ls='ls --color=auto'
alias ll='ls -alF'          # long, all, classify
alias la='ls -A'            # almost all (no . and ..)
alias l='ls -CF'
alias lh='ls -alh'          # human readable sizes

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Safety Nets
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias rm='rm -i'            # prompt before delete
alias cp='cp -i'            # prompt before overwrite
alias mv='mv -i'            # prompt before overwrite

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Git Shortcuts
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias g='git'
alias gst='git status'
alias ga='git add'
alias gc='git commit'
alias gco='git checkout'
alias gp='git push'
alias gl='git pull'
alias glg='git log --oneline --graph --decorate --all'

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Development
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias py='python3'
alias pip='pip3'
alias serve='python3 -m http.server 8000'  # quick local server
alias hosts='sudo nano /etc/hosts'

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# System
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias df='df -h'            # human readable disk usage
alias du='du -sh *'         # dir sizes in current folder
alias free='free -m'        # memory in megabytes
alias myip='curl ipinfo.io/ip'   # public IP address
alias weather='curl wttr.in'     # terminal weather!
alias ports='netstat -tulanp'    # show open ports

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Reload config
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
alias reload='source ~/.bashrc'  # reload bash config
# or for zsh:
alias reload='source ~/.zshrc'
```

```bash
# Apply changes to current session
source ~/.bashrc
# or just open a new terminal
```

##  Explanation

### Functions > Aliases for complex commands
```bash
# Alias can't easily take arguments — use functions:
function mkcd() { mkdir -p "$1" && cd "$1"; }
function backup() { cp "$1"{,.bak}; }
# Usage:
mkcd my-new-project  # creates and enters directory
backup config.json   # creates config.json.bak
```

##  Related Tips

- [Command History](command-history.md)
- [Customizing Prompt](customizing-prompt.md)

---

[← Back to Terminal Tips](README.md)
