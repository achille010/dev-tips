# Piping and Redirection

## 🎯 Problem

You have data in a file or command output that needs to be filtered, transformed, and processed — but you don't know how to chain commands together without writing temporary files.

## ✨ Solution

**Pipes** (`|`) connect commands — the output of one becomes the input of the next. **Redirection** (`>`, `>>`, `<`) connects commands with files.

## 💻 Example

### Redirection
```bash
# Standard Output (stdout) → file (overwrite)
ls -la > files.txt

# Standard Output (stdout) → file (append)
echo "new line" >> files.txt

# Standard Error (stderr) → file
./build.sh 2> errors.log

# Both stdout AND stderr → file
./build.sh > output.log 2>&1
# or (shorthand, bash 4+)
./build.sh &> output.log

# File → Standard Input
sort < unsorted.txt

# /dev/null — discard output
./annoying-script.sh > /dev/null 2>&1
```

### Pipes
```bash
# Basic pipe: output of 'ls' becomes input of 'grep'
ls -la | grep ".md"

# Chain multiple pipes
cat server.log | grep ERROR | sort | uniq -c | sort -rn | head -10
# → find top 10 most frequent errors in log file

# Word count
cat README.md | wc -l     # number of lines
cat README.md | wc -w     # number of words

# Search in compressed files
zcat archive.log.gz | grep "404"

# Count files by extension
find . -type f | sed 's/.*\.//' | sort | uniq -c | sort -rn
```

### Process Substitution (Advanced)
```bash
# Compare two command outputs without temp files
diff <(ls dir1) <(ls dir2)

# Use command output as file input
while read line; do
  echo "Processing: $line"
done < <(cat users.txt | grep active)
```

### Useful Pipeline Patterns
```bash
# Find and kill a process by name
ps aux | grep node | grep -v grep | awk '{print $2}' | xargs kill

# Most recently modified files
ls -lt | head -5

# Count occurrences of a word in logs
grep -o "ERROR" app.log | wc -l

# Unique IP addresses from access log
cat access.log | awk '{print $1}' | sort | uniq

# Search files for a pattern, then open in editor
grep -rl "TODO" src/ | xargs code
```

## 📝 Explanation

| Symbol | Meaning |
|--------|---------|
| `>`    | Redirect stdout to file (overwrite) |
| `>>`   | Redirect stdout to file (append) |
| `2>`   | Redirect stderr to file |
| `2>&1` | Redirect stderr to same place as stdout |
| `<`    | Redirect file to stdin |
| `|`    | Pipe stdout of left to stdin of right |
| `|&`   | Pipe stdout AND stderr |

## 🔗 Related Tips

- [Finding Files](finding-files.md)
- [Shell Scripting Basics](shell-scripting-basics.md)
- [Process Management](process-management.md)

---

[← Back to Terminal Tips](README.md)
