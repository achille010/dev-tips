# Productivity Hacks

## 🎯 Problem

You feel busy but not productive. Context switching, interruptions, and inefficient workflows are stealing hours from your day.

## ✨ Solution

Protect your deep work time, reduce context switching, master your tools, and automate repetitive tasks.

## 💻 Example

### Keyboard-First Workflow
```bash
# Learn your editor shortcuts — VSCode most-used:
Ctrl+P          # Quick Open (fuzzy find any file)
Ctrl+Shift+P    # Command Palette (run any command)
Ctrl+`          # Toggle terminal
Ctrl+D          # Select next occurrence (multi-cursor)
Alt+Click       # Add cursor
Ctrl+/          # Toggle comment
Ctrl+Shift+K    # Delete line
Alt+↑/↓         # Move line up/down
F12             # Go to definition
Ctrl+Shift+F   # Global search in project

# Browser DevTools:
F12 / Ctrl+Shift+I  # Open DevTools
Ctrl+Shift+C         # Inspect element
Ctrl+L               # Focus address bar
```

### Automate Repetitive Tasks
```json
// package.json scripts
{
  "scripts": {
    "dev":      "vite",
    "build":    "vite build",
    "lint":     "eslint src --ext .js,.jsx,.ts,.tsx",
    "lint:fix": "eslint src --fix",
    "format":   "prettier --write src/",
    "test":     "vitest",
    "test:ui":  "vitest --ui",
    "check":    "npm run lint && npm run test"
  }
}
```

```bash
# Use 'npm run check' before every commit
# Or automate with pre-commit hooks (husky)
npx husky add .husky/pre-commit "npm run check"
```

### Focus Time Strategies
```
Deep Work Schedule (Example):
09:00 - 12:00  → Deep work block (no meetings, notifications off)
12:00 - 13:00  → Email/Slack/reviews
13:00 - 15:30  → Deep work block
15:30 - 17:00  → Meetings, code reviews, admin

Rules:
- Silence Slack/email notifications during deep work
- 25-min Pomodoro timers for focused sessions
- Keep a "distraction log" — write down intrusive thoughts, come back later
```

### Use Snippets
```json
// VSCode snippet: Add to settings
{
  "Console Log": {
    "prefix": "cl",
    "body": ["console.log('$1:', $1);"],
    "description": "console.log with label"
  },
  "React Component": {
    "prefix": "rfc",
    "body": [
      "function ${1:ComponentName}() {",
      "  return (",
      "    <div>",
      "      $0",
      "    </div>",
      "  );",
      "}",
      "",
      "export default ${1:ComponentName};"
    ]
  }
}
```

## 📝 Explanation

### High-Impact Habits
1. **Morning ritual** — before email, plan your top 3 tasks
2. **Keyboard shortcuts** — invest 1 hour learning, save hours daily
3. **Batch similar tasks** — code reviews 2x/day, not constantly
4. **End-of-day shutdown routine** — write tomorrow's top 3 tasks, close IDE

## 🔗 Related Tips

- [Code Organization](code-organization.md)
- [Useful Aliases](../terminal/useful-aliases.md)

---

[← Back to General Tips](README.md)
