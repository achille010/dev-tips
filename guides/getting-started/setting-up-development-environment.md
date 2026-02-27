# Setting Up Your Development Environment

## 📖 Overview

This guide walks you through setting up a professional development environment from scratch. By the end, you'll have a working terminal, code editor, version control, and Node.js environment ready for modern web development.

**Who this is for:** Complete beginners or developers setting up a new machine.

## 🎯 Prerequisites

No prior experience needed, just a computer with internet access.

## 📋 Steps

### Step 1: Install a Package Manager

**macOS — Homebrew:**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Windows — Chocolatey (run as Administrator):**
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

**Ubuntu/Debian:**
Package manager is `apt`, already installed.

### Step 2: Install Git
```bash
# macOS
brew install git

# Ubuntu/Debian
sudo apt update && sudo apt install git

# Windows
choco install git

# Verify
git --version

# Configure your identity (used in commit history)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

### Step 3: Install a Code Editor (VS Code)
```bash
# macOS
brew install --cask visual-studio-code

# Ubuntu
sudo snap install code --classic

# Windows
choco install vscode

# Verify: open from terminal
code --version
code .    # open current directory in VS Code
```

**Essential VS Code Extensions:**
- ESLint — `dbaeumer.vscode-eslint`
- Prettier — `esbenp.prettier-vscode`
- GitLens — `eamodio.gitlens`
- Thunder Client — `rangav.vscode-thunder-client` (API testing)

### Step 4: Install Node.js (via nvm — Node Version Manager)
```bash
# Install nvm (macOS/Linux)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
# Restart terminal, then:
nvm install --lts           # install latest LTS version
nvm use --lts
nvm alias default node      # set as default

# Windows: use nvm-windows
# Download from: https://github.com/coreybutler/nvm-windows/releases

# Verify
node --version
npm --version
```

### Step 5: Set Up SSH Keys for GitHub
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Copy public key to clipboard
# macOS:
cat ~/.ssh/id_ed25519.pub | pbcopy
# Linux:
cat ~/.ssh/id_ed25519.pub | xsel --clipboard
# Windows:
cat ~/.ssh/id_ed25519.pub | clip

# → Paste at GitHub.com → Settings → SSH Keys → New SSH Key

# Test connection
ssh -T git@github.com
# "Hi username! You've successfully authenticated."
```

### Step 6: Configure Your Terminal
```bash
# Install Oh My Zsh (macOS/Linux — zsh required)
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Install Starship prompt (cross-platform)
curl -sS https://starship.rs/install.sh | sh
echo 'eval "$(starship init bash)"' >> ~/.bashrc

# Useful global npm tools
npm install -g nodemon          # auto-restart Node.js apps
npm install -g http-server      # quick local servers
```

## ⚠️ Common Pitfalls

- **Permission errors with npm** — Never use `sudo npm install -g`. Use nvm instead.
- **Git identity not set** — Commits will fail without `user.name` and `user.email`
- **Wrong Node version** — Use `nvm use <version>` to match project's `.nvmrc`

## ✅ Verification

```bash
git --version           # git 2.x.x
node --version          # v20.x.x (or current LTS)
npm --version           # 10.x.x
code --version          # 1.x.x
ssh -T git@github.com   # authenticates
```

## 📚 Further Reading

- [Git Basics for Beginners](git-basics-for-beginners.md)
- [Understanding the Terminal](understanding-the-terminal.md)

---

[← Back to Getting Started](../README.md) | [← Back to Guides](../../README.md)
