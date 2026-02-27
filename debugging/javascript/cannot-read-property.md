# Error: Cannot read property / Cannot read properties of undefined

## 🔴 The Error

```
TypeError: Cannot read properties of undefined (reading 'name')
TypeError: Cannot read property 'name' of null
TypeError: Cannot read property 'map' of undefined
```

## 🤔 Common Causes

1. **Async data not loaded yet** — rendering before data arrives
2. **Missing null check** — assuming a value exists when it might not
3. **Wrong API response shape** — expecting `data.user` but getting `data`
4. **Typo in property name** — accessing `user.naem` instead of `user.name`

## ⚡ Quick Fix

Add a null/undefined check before accessing the property:
```javascript
// Before
console.log(user.name);

// After
console.log(user?.name);        // Optional chaining
console.log(user && user.name); // Short-circuit (ES5)
```

## 🔧 Detailed Solution

### Solution 1: Optional Chaining (?.)
```javascript
// ❌ Crashes if user is null/undefined
const name = user.name;
const city = user.address.city;
const count = items.length;

// ✅ Safe with optional chaining
const name  = user?.name;
const city  = user?.address?.city;
const count = items?.length ?? 0;

// With function calls
const result = obj?.method?.();

// With arrays
const first = arr?.[0]?.name;
```

### Solution 2: Default Values with Nullish Coalescing
```javascript
const name   = user?.name ?? 'Anonymous';
const items  = response?.data?.items ?? [];
const count  = data?.total ?? 0;
```

### Solution 3: Async Data — Loading State
```jsx
// React: show loading until data arrives
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchUser(userId)
      .then(setUser)
      .finally(() => setLoading(false));
  }, [userId]);

  if (loading) return <p>Loading...</p>;
  if (!user)   return <p>User not found</p>;

  // Now safe to access user.name
  return <h1>{user.name}</h1>;
}
```

## 🛡️ Prevention

- Use TypeScript to catch null-related errors at compile time
- Always initialize state with sensible defaults
- Validate API responses before using them

---

[← Back to JavaScript Debugging](README.md)
