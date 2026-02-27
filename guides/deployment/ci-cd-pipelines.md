# CI/CD Pipelines

## 📖 Overview

**CI/CD (Continuous Integration / Continuous Deployment)** automates the process of testing and deploying your application every time code is pushed. This guide covers setting up a complete CI/CD pipeline using GitHub Actions.

## 🎯 Prerequisites

- Git and GitHub account
- A Node.js or Python project
- Basic understanding of YAML syntax

## 📋 Steps

### Step 1: Understanding CI vs CD

```
Developer → Push code → CI (test, lint, build) → CD (deploy)

CI: Continuous Integration
  - Run tests automatically on every PR
  - Catch bugs before they reach main
  - Ensures code always works

CD: Continuous Deployment/Delivery
  - Deploy automatically when tests pass
  - Ship faster, more reliably
  - Rollback easily if something breaks
```

### Step 2: Create a GitHub Actions Workflow

```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  # CI: Test and Build
  # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  test:
    name: Test
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [18.x, 20.x]  # test on multiple Node versions
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'

      - name: Install dependencies
        run: npm ci  # use ci instead of install for reproducibility

      - name: Run linter
        run: npm run lint

      - name: Run tests
        run: npm test -- --coverage

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        if: matrix.node-version == '20.x'

      - name: Build
        run: npm run build

  # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  # CD: Deploy (only on main)
  # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  deploy:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: test  # only deploy if tests pass
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    
    environment:
      name: production
      url: https://yourapp.com

    steps:
      - uses: actions/checkout@v4

      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
          vercel-args: '--prod'
```

### Step 3: Set Up Secrets

```bash
# Navigate to GitHub repo → Settings → Secrets → Actions
# Add: VERCEL_TOKEN, ORG_ID, PROJECT_ID

# Access in workflow:
${{ secrets.VERCEL_TOKEN }}
```

### Step 4: Branch Protection Rules

```
GitHub → Settings → Branches → Add rule for 'main':
✅ Require status checks to pass before merging
  ✅ test (node 18.x)
  ✅ test (node 20.x)
✅ Require branches to be up to date before merging
✅ Require pull request reviews before merging
✅ Do not allow bypassing the above settings
```

## ⚠️ Common Pitfalls

1. **Using `npm install` instead of `npm ci`** in CI — `npm ci` installs exactly from `package-lock.json`
2. **Not caching dependencies** — add `cache: 'npm'` to `setup-node` to avoid re-downloading
3. **Secrets in workflow logs** — GitHub masks strings matching secrets, but don't `echo ${{ secrets.X }}`

## ✅ Best Practices

- Run tests in parallel where possible (`matrix` strategy)
- Cache `node_modules` between runs
- Fail fast on linter errors before running expensive tests
- Deploy to staging first, then production

## 📚 Further Reading

- [Docker Basics](docker-basics.md)
- [Environment Management](environment-management.md)

---

[← Back to Deployment](../README.md) | [← Back to Guides](../../README.md)
