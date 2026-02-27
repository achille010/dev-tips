# Process Management

## 🎯 Problem

A process is hanging, consuming too much CPU, running on a port you need, or you want to run a task in the background. You need to view, control, and manage running processes.

## ✨ Solution

Use `ps`, `top`/`htop`, `kill`, `bg`/`fg`, and `nohup` to manage processes from the terminal.

## 💻 Example

### Viewing Processes
```bash
# Quick process list
ps                     # current session processes
ps aux                 # all processes (user, PID, CPU%, MEM%, command)
ps aux | grep node     # find node processes

# Interactive process monitor
top                    # real-time process monitor (press 'q' to quit)
htop                   # better top with colors (install separately)

# Port occupancy
lsof -i :3000          # what's using port 3000?
lsof -i :3000 -t       # just the PID
ss -tulpn | grep 3000  # alternative (systems without lsof)
netstat -ano | grep 3000  # Windows
```

### Sending Signals
```bash
# Kill by PID
kill 1234              # send SIGTERM (polite request to stop)
kill -9 1234           # send SIGKILL (force kill, no cleanup)
kill -l                # list all signals

# Kill by name
pkill node             # kill all processes named 'node'
pkill -9 node          # force kill
killall node           # similar to pkill

# Kill what's on a port
kill $(lsof -i :3000 -t)
# or
lsof -ti :3000 | xargs kill -9
```

### Background and Foreground
```bash
# Run a command in background
./long-script.sh &
# → [1] 12345  (job ID, PID)

# Suspend current process (Ctrl+Z), then background it
./server.sh
# Press Ctrl+Z → stopped
bg            # resume in background
fg            # bring back to foreground
fg %1         # bring job #1 to foreground

# List background jobs
jobs
# [1]  Running    ./server.sh &
# [2]- Running    ./worker.sh &

# Disconnect-proof background (survives terminal close)
nohup ./server.sh > server.log 2>&1 &

# Modern alternative: screen or tmux
tmux new -s myserver     # start named session
# ... start your process
# Detach: Ctrl+B then D
tmux attach -t myserver  # reattach later
```

## 📝 Explanation

| Signal | Number | Meaning |
|--------|--------|---------|
| SIGTERM | 15 | Polite stop (allows cleanup) |
| SIGKILL | 9  | Force kill (no cleanup) |
| SIGINT  | 2  | Interrupt (Ctrl+C) |
| SIGSTOP | 19 | Pause process |
| SIGCONT | 18 | Resume paused process |

## 🔗 Related Tips

- [Keyboard Shortcuts](keyboard-shortcuts.md)
- [SSH Tips](ssh-tips.md)

---

[← Back to Terminal Tips](README.md)
