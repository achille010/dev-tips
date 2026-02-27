# Error: Async/Await Issues

## 🔴 The Error

```
UnhandledPromiseRejectionWarning: Error: ...
SyntaxError: await is only valid in async functions
TypeError: Cannot read property of undefined (from unresolved promise)
```

## 🤔 Common Causes

1. **Forgetting `await`** — treating a Promise as a value
2. **`await` outside async function** — syntax error
3. **Unhandled promise rejection** — no try/catch
4. **Race conditions** — parallel async operations interfering

## 🔧 Detailed Solution

### Solution 1: Always `await` Promises
```javascript
// ❌ Forgot await — user is a Promise, not a user object
async function displayUser(id) {
  const user = getUser(id); // ❌ no await
  console.log(user.name);   // [object Promise].name → undefined
}

// ✅ Await the promise
async function displayUser(id) {
  const user = await getUser(id); // ✅
  console.log(user.name);
}
```

### Solution 2: Error Handling in Async Functions
```javascript
// ❌ Unhandled rejection crashes the process
async function loadData() {
  const data = await fetch('/api/data').then(r => r.json());
  return data;
}

// ✅ With try/catch
async function loadData() {
  try {
    const response = await fetch('/api/data');
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } catch (err) {
    console.error('loadData failed:', err.message);
    throw err; // re-throw so caller can handle
  }
}

// ✅ In Express: use async wrapper to forward errors
const asyncHandler = fn => (req, res, next) => Promise.resolve(fn(req, res, next)).catch(next);

router.get('/users', asyncHandler(async (req, res) => {
  const users = await User.findAll();
  res.json(users);
}));
```

### Solution 3: Parallel Async Operations
```javascript
// ❌ Sequential — takes 3 seconds if each takes 1s
async function loadDashboard() {
  const user    = await getUser();    // 1s
  const posts   = await getPosts();   // 1s
  const friends = await getFriends(); // 1s
  return { user, posts, friends };
}

// ✅ Parallel — takes 1 second total
async function loadDashboard() {
  const [user, posts, friends] = await Promise.all([
    getUser(),
    getPosts(),
    getFriends(),
  ]);
  return { user, posts, friends };
}

// ✅ Promise.allSettled — don't fail if one rejects
const results = await Promise.allSettled([
  getUser(),
  getPosts(),
  getFriends(),
]);
const successful = results
  .filter(r => r.status === 'fulfilled')
  .map(r => r.value);
```

## 🛡️ Prevention

- Enable `no-floating-promises` ESLint rule with TypeScript
- Always add global handler: `process.on('unhandledRejection', console.error)`

---

[← Back to JavaScript Debugging](README.md)
