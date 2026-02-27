# Gitignore Best Practices

##  Problem

Accidentally committing `node_modules`, `.env` files, build artifacts, or OS-generated junk to your repository creates bloat, security risks, and headaches for collaborators.

##  Solution

Create a well-structured `.gitignore` file that excludes all files that don't belong in your repository.

##  Example

### Comprehensive .gitignore Template

```gitignore
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Environment and Secrets
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
.env
.env.*
!.env.example     # ← commit the EXAMPLE, not the actual
*.pem
*.key
secrets/

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# OS Files
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
.DS_Store
.DS_Store?
._*
Thumbs.db
ehthumbs.db
Desktop.ini

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Node.js
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.npm
.pnp.*
.yarn/cache

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Build Outputs
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
dist/
build/
out/
.next/
.nuxt/
.vite/
*.min.js
*.min.css

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Python
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
__pycache__/
*.py[cod]
.venv/
venv/
*.egg-info/
dist/

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Editor Files
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
.vscode/settings.json   # team settings: commit; personal: ignore
.idea/
*.swp
*.swo
*~

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Logs and Temp
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*.log
logs/
tmp/
temp/
*.tmp

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# Test Coverage
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
coverage/
.nyc_output/
```

### Already Tracked File? Use This:
```bash
# Stop tracking a file (but keep it locally)
git rm --cached .env
git commit -m "chore: remove .env from tracking"
# Then add .env to .gitignore
```

### Global Gitignore (for personal patterns)
```bash
# Create a global gitignore for your machine
git config --global core.excludesfile ~/.gitignore_global

# ~/.gitignore_global
.DS_Store
*.swp
.idea/
.vscode/
```

##  Explanation

### Pattern Reference
| Pattern | Matches |
|---------|---------|
| `*.log` | Any .log file anywhere |
| `logs/` | logs directory and contents |
| `/logs/` | logs only in root |
| `!important.log` | Negate — don't ignore this |
| `**/*.pyc` | .pyc in any subdirectory |
| `doc/*.txt` | .txt files directly in doc/ |

##  Related Tips

- [Useful Aliases](useful-aliases.md)
- [Undo Mistakes](undo-mistakes.md)

---

[← Back to Git Tips](README.md)
