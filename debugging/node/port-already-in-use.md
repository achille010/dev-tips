# Error: Port Already in Use (EADDRINUSE)

## 🔴 The Error

```
Error: listen EADDRINUSE: address already in use :::3000
Error: listen EADDRINUSE :::8080
```

## 🤔 Common Causes

1. **Previous server process still running** — didn't properly stop it
2. **Another application using the port** — database, system service
3. **Multiple terminal tabs running the same server**
4. **Zombie process** — server crashed but OS didn't release port

## ⚡ Quick Fix

```bash
# Kill whatever is on port 3000
# macOS / Linux:
kill $(lsof -t -i:3000)
# or
fuser -k 3000/tcp

# Windows:
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

## 🔧 Detailed Solution

### Solution 1: Find and Kill the Process
```bash
# Find process using port (macOS/Linux)
lsof -i :3000
# COMMAND   PID   USER   TYPE
# node     1234   alice  TCP *:3000

kill 1234        # graceful
kill -9 1234     # force kill

# Find process using port (Windows)
netstat -ano | findstr :3000
# TCP    0.0.0.0:3000    0.0.0.0:0    LISTENING    5678
taskkill /PID 5678 /F
```

### Solution 2: Use a Different Port
```javascript
// app.js — use environment variable with fallback
const PORT = process.env.PORT || 3001;  // try 3001 instead
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

### Solution 3: Add Graceful Shutdown
```javascript
const server = app.listen(PORT);

// Handle Ctrl+C
process.on('SIGINT', () => {
  console.log('Shutting down...');
  server.close(() => process.exit(0));
});

// Handle nodemon restart
process.on('SIGTERM', () => {
  server.close(() => process.exit(0));
});
```

## 🛡️ Prevention

- Always stop your dev server before closing the terminal (Ctrl+C)
- Use environment variables for ports to avoid hardcoded conflicts
- `nodemon` automatically handles restarts cleanly

---

[← Back to Node Debugging](README.md)
