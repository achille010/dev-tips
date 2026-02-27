# Terminal Keyboard Shortcuts

##  Problem

You're constantly reaching for the mouse or retyping commands character by character, wasting time on basic navigation when there are faster keyboard-driven ways.

##  Solution

Learn these essential terminal keyboard shortcuts for Bash/Zsh. Once memorized, they dramatically speed up your workflow.

##  Example

### Cursor Movement
```bash
Ctrl + A    # Move cursor to BEGINNING of line
Ctrl + E    # Move cursor to END of line
Ctrl + F    # Move Forward one character (same as →)
Ctrl + B    # Move Backward one character (same as ←)
Alt  + F    # Move Forward one WORD
Alt  + B    # Move Backward one WORD

Ctrl + XX   # Toggle between current position and beginning
```

### Editing
```bash
Ctrl + K    # Kill (cut) from cursor to END of line
Ctrl + U    # Kill (cut) from cursor to BEGINNING of line
Ctrl + W    # Kill (cut) the WORD before cursor
Alt  + D    # Kill (cut) the WORD after cursor
Ctrl + Y    # Yank (paste) what was killed

Ctrl + D    # Delete character UNDER cursor (or logout if empty)
Ctrl + H    # Delete character BEFORE cursor (Backspace)
Alt  + U    # UPPERCASE the word from cursor to end
Alt  + L    # lowercase the word from cursor to end
Alt  + C    # Capitalize the word from cursor to end
```

### Process Control
```bash
Ctrl + C    # Interrupt/kill current process (SIGINT)
Ctrl + Z    # Suspend current process (send to background)
Ctrl + D    # Send EOF / exit current shell
Ctrl + \    # Quit current process (SIGQUIT, stronger than Ctrl+C)
```

### Screen
```bash
Ctrl + L    # Clear screen (same as 'clear' command)
Ctrl + S    # Pause output to terminal (stop)
Ctrl + Q    # Resume output to terminal (flow)
```

### History Navigation
```bash
Ctrl + P    # Previous command (same as ↑ arrow)
Ctrl + N    # Next command (same as ↓ arrow)
Ctrl + R    # Reverse search through history
Ctrl + G    # Exit history search without running
```

##  Explanation

These are based on **readline** keybindings (emacs mode, which is the default). Your terminal can also be set to vi mode:
```bash
# Switch to vi mode (for vim users)
set -o vi

# Switch back to emacs mode (default)
set -o emacs
```

### Most Impactful Shortcuts to Learn First
1. `Ctrl+A` / `Ctrl+E` — jump to start/end
2. `Ctrl+R` — history search
3. `Ctrl+L` — clear screen
4. `Ctrl+C` / `Ctrl+D` — stop/exit

##  Related Tips

- [Command History](command-history.md)
- [Useful Aliases](useful-aliases.md)

---

[← Back to Terminal Tips](README.md)
