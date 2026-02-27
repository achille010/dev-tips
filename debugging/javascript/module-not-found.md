# Error: Module Not Found (JavaScript)

##  The Error

```
Error: Cannot find module './utils'
Error: Cannot find module 'express'
Module not found: Error: Can't resolve '@/components/Button'
```

##  Common Causes

1. **Package not installed** — forgot `npm install`
2. **Wrong path** — typo in import path or wrong relative/absolute path
3. **Wrong casing** — `import Button from './button'` but file is `Button.jsx`
4. **Path alias not configured** — `@/` alias not set up in bundler

##  Detailed Solution

### Solution 1: Package Not Installed
```bash
# Check if it's in package.json
cat package.json | grep express

# Install it
npm install express          # production dependency
npm install --save-dev jest  # dev dependency

# Or reinstall everything
rm -rf node_modules package-lock.json
npm install
```

### Solution 2: Wrong Path
```javascript
// ❌ Wrong relative path
import { helper } from '../utils';    // file is at ./utils
import Button from './components/btn'; // file is Button.jsx

//  Correct
import { helper } from './utils';
import Button from './components/Button';

// Debug: check the actual file path
find . -name "Button*" -not -path "*/node_modules/*"
```

### Solution 3: Path Alias (@/)
```javascript
// vite.config.js
import path from 'path';

export default {
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
};

// tsconfig.json / jsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

### Solution 4: ESM vs CommonJS
```javascript
// ❌ CommonJS require in ESM project
const express = require('express'); // error if "type":"module" in package.json

//  Use import
import express from 'express';

// Or add to package.json to use CommonJS:
{ "type": "commonjs" }
```

##  Prevention

- Always run `npm install` after cloning a repo
- Use IDE path autocompletion to avoid typos
- Check file casing on case-sensitive systems (Linux servers)

---

[← Back to JavaScript Debugging](README.md)
