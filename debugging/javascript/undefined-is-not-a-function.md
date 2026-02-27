# Error: undefined is not a function

## 🔴 The Error

```
TypeError: undefined is not a function
TypeError: myFunction is not a function
TypeError: X.Y is not a function
```

## 🤔 Common Causes

1. **Wrong import** — function not exported, or wrong named vs default import
2. **Calling before declaration** — using a `const` function before it's defined
3. **Typo in function name** — `arrary.push()` instead of `array.push()`
4. **Method applied to wrong type** — calling `.map()` on an object instead of array

## 🔧 Detailed Solution

### Solution 1: Check Your Imports
```javascript
// ❌ Function is exported as named, but imported as default
// utils.js
export function formatDate(date) { ... }  // named export

// app.js
import formatDate from './utils';   // ❌ wrong (default import)
import { formatDate } from './utils'; // ✅ correct (named import)

// ───────────────────────────────
// ❌ Importing from wrong file
import { useState } from 'react-dom'; // ❌ wrong
import { useState } from 'react';     // ✅ correct
```

### Solution 2: Variable Initialization Timing
```javascript
// ❌ Arrow function with const cannot be hoisted
runApp(); // ❌ ReferenceError — cannot call before initialization

const runApp = () => console.log('Running!');

// ✅ Function declarations ARE hoisted
runApp(); // ✅ Works!

function runApp() { console.log('Running!'); }
```

### Solution 3: Type Mismatch
```javascript
// ❌ Object doesn't have .map()
const userObj = { name: 'Alice', age: 25 };
userObj.map(u => u.name); // ❌ TypeError

// ✅ Check type first
const users = Array.isArray(userObj) ? userObj : [userObj];
users.map(u => u.name); // ✅

// ❌ Calling method on null/undefined
const handler = null;
handler.onClick(); // ❌ TypeError

// ✅ Check before calling
handler?.onClick?.();
```

## 🛡️ Prevention

- Use TypeScript for compile-time type checking
- Run `console.log(typeof myFunction)` to debug the type of a variable
- Use ESLint `no-use-before-define` rule

---

[← Back to JavaScript Debugging](README.md)
