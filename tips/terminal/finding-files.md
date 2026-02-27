# Finding Files

## 🎯 Problem

You need to locate a file, find all files of a certain type, or search inside files for specific content — but don't know the right commands.

## ✨ Solution

Use `find` for file discovery, `grep` for searching file content, and `locate` for quick indexed search.

## 💻 Example

### `find` — Find Files by Properties
```bash
# Find by name
find . -name "*.log"              # current dir, case-sensitive
find . -iname "*.log"             # case-insensitive
find / -name "nginx.conf" 2>/dev/null  # search from root

# Find by type
find . -type f   # files only
find . -type d   # directories only
find . -type l   # symbolic links only

# Find by size
find . -size +10M    # files larger than 10MB
find . -size -1k     # files smaller than 1KB
find . -size +1M -size -100M  # between 1MB and 100MB

# Find by time
find . -mtime -7       # modified in last 7 days
find . -newer file.txt # modified more recently than file.txt
find . -mmin -30       # modified in last 30 minutes

# Find and execute
find . -name "*.tmp" -delete         # delete all .tmp files
find . -name "*.js" -exec wc -l {} + # count lines in JS files
find . -name "*.jpg" -exec mv {} ./images/ \;  # move images

# Combine with -not
find . -name "*.js" -not -path "*/node_modules/*"
```

### `grep` — Search Inside Files
```bash
# Basic search
grep "TODO" app.js             # find TODO in one file
grep -r "TODO" src/            # recursive search in directory
grep -ri "todo" src/           # case-insensitive recursive

# Control output
grep -n "function" app.js      # show line numbers
grep -l "import React" src/    # show only filenames
grep -c "error" app.log        # count matches per file
grep -v "DEBUG" app.log        # show lines NOT matching

# Patterns
grep -E "error|warning" *.log  # extended regex: OR
grep -P "^\d{3}-\d{4}$" data.txt  # Perl regex

# Context around matches
grep -A 3 "function" app.js    # 3 lines After match
grep -B 3 "function" app.js    # 3 lines Before match
grep -C 3 "function" app.js    # 3 lines Context (before AND after)

# Exclude paths
grep -r "TODO" . --include="*.js" --exclude-dir=node_modules
```

### `fd` and `ripgrep` — Modern Alternatives
```bash
# fd — faster, friendlier find
fd "*.js"             # find .js files (simpler syntax)
fd -t f "config"      # find files named config
fd -e js -e ts        # find .js and .ts files

# ripgrep (rg) — faster grep
rg "TODO"             # search recursively (ignores .gitignore)
rg -t js "TODO"       # search only in .js files
rg -l "TODO"          # show filenames only
```

## 📝 Explanation

| Tool | Best For |
|------|----------|
| `find` | File properties (size, date, type) |
| `grep` | Content inside files |
| `locate` | Quick filename search (from index) |
| `fd` | Faster, user-friendly `find` replacement |
| `rg` | Faster, smarter `grep` replacement |

## 🔗 Related Tips

- [Piping and Redirection](piping-and-redirection.md)
- [Shell Scripting Basics](shell-scripting-basics.md)

---

[← Back to Terminal Tips](README.md)
