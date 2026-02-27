# Error: CORS Errors

##  The Error

```
Access to fetch at 'http://api.example.com/data' from origin 'http://localhost:3000'
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present
on the requested resource.
```

##  Common Causes

1. **Server doesn't send CORS headers** — most common cause
2. **Wrong origin in allowed list** — typo or mismatch
3. **Preflight OPTIONS not handled** — missing OPTIONS handler
4. **Credentials + wildcard** — `credentials: include` with `*` origin is invalid

##  Quick Fix

CORS errors only happen in browsers. The server must explicitly allow the frontend's origin.

```javascript
// Node.js/Express — add CORS headers
const cors = require('cors');

app.use(cors({
  origin: 'http://localhost:3000',    // your frontend URL
  credentials: true                   // allow cookies/auth
}));
```

##  Detailed Solution

### Solution 1: Express with cors package
```javascript
const cors = require('cors');

// Allow all origins (development only!)
app.use(cors());

// Allow specific origins (production)
app.use(cors({
  origin: ['https://yourdomain.com', 'http://localhost:3000'],
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'OPTIONS'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
}));

// Handle preflight for all routes
app.options('*', cors());
```

### Solution 2: Manual Headers (any server)
```javascript
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', 'http://localhost:3000');
  res.header('Access-Control-Allow-Methods', 'GET,POST,PUT,DELETE,OPTIONS');
  res.header('Access-Control-Allow-Headers', 'Content-Type,Authorization');
  res.header('Access-Control-Allow-Credentials', 'true');
  if (req.method === 'OPTIONS') return res.sendStatus(200);
  next();
});
```

### Solution 3: Proxy in Development (no server changes)
```javascript
// vite.config.js
export default {
  server: {
    proxy: {
      '/api': {
        target: 'http://api.example.com',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
    },
  },
};

// webpack devServer:
devServer: {
  proxy: { '/api': 'http://api.example.com' }
}
```

##  Prevention

- Never use `Access-Control-Allow-Origin: *` with `credentials: true`
- In production, whitelist only known trusted origins
- Consider using a same-domain API to avoid CORS entirely

##  Related Errors

- [Async/Await Issues](async-await-issues.md)
- [Module Not Found](module-not-found.md)

---

[← Back to JavaScript Debugging](README.md)
