# Customizing Your Shell Prompt

##  Problem

The default terminal prompt is plain and tells you nothing useful. You want to see the current git branch, project, or error status at a glance.

##  Solution

Customize your `PS1` (Bash prompt variable) or `PROMPT` (Zsh). Better yet, use a modern prompt framework like **Starship** or **Oh My Zsh** themes.

##  Example

### Bash Custom Prompt
```bash
# ~/.bashrc

# Colors
RED='\[\033[0;31m\]'
GREEN='\[\033[0;32m\]'
YELLOW='\[\033[0;33m\]'
BLUE='\[\033[0;34m\]'
PURPLE='\[\033[0;35m\]'
CYAN='\[\033[0;36m\]'
RESET='\[\033[0m\]'

# Git branch function
git_branch() {
    git branch 2>/dev/null | grep '^*' | sed 's/* //'
}

# Git status indicator
git_status() {
    if [ -n "$(git status --porcelain 2>/dev/null)" ]; then
        echo " *"   # dirty
    fi
}

# Custom PS1:
# [user@host ~/project] (main *) $
PS1="${GREEN}\u${RESET}@${BLUE}\h${RESET} ${YELLOW}\w${RESET}"
PS1+='$([ -n "$(git_branch)" ] && echo " ${PURPLE}($(git_branch)$(git_status))${RESET}")'
PS1+="${CYAN} \$ ${RESET}"

export PS1
```

### Starship (Cross-shell, Highly Recommended)
```bash
# Install
curl -sS https://starship.rs/install.sh | sh

# Add to ~/.bashrc / ~/.zshrc
eval "$(starship init bash)"
# or
eval "$(starship init zsh)"

# Configure in ~/.config/starship.toml
```

```toml
# ~/.config/starship.toml

# Add newline between prompts
add_newline = true

[character]
success_symbol = "[❯](bold green)"
error_symbol   = "[❯](bold red)"

[git_branch]
symbol = " "
style  = "bold purple"

[git_status]
conflicted = "⚔️ "
modified   = "📝"
staged     = "✅"
untracked  = "🤷"

[nodejs]
symbol = " "
style  = "bold green"

[python]
symbol = " "
style  = "bold yellow"

[directory]
style = "bold cyan"
truncation_length = 3
```

##  Related Tips

- [Useful Aliases](useful-aliases.md)
- [SSH Tips](ssh-tips.md)

---

[← Back to Terminal Tips](README.md)
