# Shell Scripting Basics

## 🎯 Problem

You're running the same sequence of commands repeatedly — deploying, building, or setting up your environment. Manual repetition wastes time and introduces human error.

## ✨ Solution

Write a shell script to automate the sequence. Even basic scripting skills save hours of work.

## 💻 Example

### Your First Script

```bash
#!/usr/bin/env bash
# ─────────────────────────────────────────────
# deploy.sh — Deploy the application
# Usage: ./deploy.sh [environment]
# ─────────────────────────────────────────────
set -euo pipefail   # e=exit on error, u=undefined vars error, o pipefail

ENVIRONMENT="${1:-staging}"   # first arg, default 'staging'
APP_DIR="/opt/myapp"
LOG_FILE="/var/log/deploy.log"
TIMESTAMP=$(date '+%Y-%m-%d %H:%M:%S')

echo "[$TIMESTAMP] Deploying to $ENVIRONMENT..."

# Functions
build_app() {
    echo "Building..."
    npm ci
    npm run build
}

run_tests() {
    echo "Running tests..."
    npm test
    if [ $? -ne 0 ]; then      # check exit code
        echo "Tests failed! Aborting."
        exit 1
    fi
}

deploy() {
    local env=$1    # local makes variable function-scoped

    if [ "$env" = "production" ]; then
        echo "⚠️  Deploying to PRODUCTION — are you sure? (y/N)"
        read -r response
        [ "$response" != "y" ] && exit 0
    fi

    rsync -avz --delete dist/ user@server.com:$APP_DIR/
    ssh user@server.com "pm2 restart myapp"
    echo "✅ Deployed to $env successfully!"
}

# Control flow
if [ "$ENVIRONMENT" = "local" ]; then
    echo "Starting local dev server..."
    npm run dev
elif [ "$ENVIRONMENT" = "staging" ] || [ "$ENVIRONMENT" = "production" ]; then
    build_app
    run_tests
    deploy "$ENVIRONMENT"
else
    echo "Unknown environment: $ENVIRONMENT"
    echo "Usage: $0 [local|staging|production]"
    exit 1
fi
```

```bash
# Make executable and run
chmod +x deploy.sh
./deploy.sh staging
./deploy.sh production
```

### Common Patterns
```bash
# Iterate over files
for file in *.log; do
    echo "Processing $file"
    gzip "$file"
done

# Read file line by line
while IFS= read -r line; do
    echo "Line: $line"
done < users.txt

# Arrays
SERVERS=("web1" "web2" "web3")
for server in "${SERVERS[@]}"; do
    ssh "$server" "sudo systemctl restart nginx"
done

# String manipulation
NAME="hello world"
echo "${NAME^^}"           # HELLO WORLD
echo "${NAME// /_}"        # hello_world
echo "${NAME:0:5}"         # hello (substring)
echo "${#NAME}"            # 11 (length)
```

## 🔗 Related Tips

- [Piping and Redirection](piping-and-redirection.md)
- [Useful Aliases](useful-aliases.md)

---

[← Back to Terminal Tips](README.md)
