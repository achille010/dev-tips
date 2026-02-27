# Security Best Practices

## 🎯 Problem

Security is often treated as an afterthought. Vulnerabilities like injection attacks, broken authentication, and exposed secrets end up in production code and cause breaches.

## ✨ Solution

Build security in from the start. Follow the principle of least privilege, validate all input, never trust the client, and keep secrets secret.

## 💻 Example

### Input Validation & Sanitization
```javascript
// ❌ Vulnerable to SQL injection
const user = await db.query(
  `SELECT * FROM users WHERE email = '${req.body.email}'`
);

// ✅ Parameterized queries (node-postgres example)
const user = await db.query(
  'SELECT * FROM users WHERE email = $1',
  [req.body.email]
);

// ❌ Vulnerable to XSS
document.getElementById('output').innerHTML = userInput;

// ✅ Use textContent or DOM methods
document.getElementById('output').textContent = userInput;
// Or if you need HTML: use a library like DOMPurify
import DOMPurify from 'dompurify';
element.innerHTML = DOMPurify.sanitize(userInput);
```

### Authentication & Passwords
```javascript
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');

// ❌ Never store plaintext passwords
users.create({ email, password });

// ✅ Hash passwords with bcrypt (cost factor 12+)
const salt = await bcrypt.genSalt(12);
const hash = await bcrypt.hash(password, salt);
users.create({ email, passwordHash: hash });

// Verify
const match = await bcrypt.compare(inputPassword, user.passwordHash);

// JWT: use short expiry + refresh tokens
const accessToken = jwt.sign(
  { userId: user.id, role: user.role },
  process.env.JWT_SECRET,   // ← store in environment variable!
  { expiresIn: '15m' }      // ← short expiry
);
```

### Environment Variables & Secrets
```bash
# ❌ Never hardcode secrets
const API_KEY = 'sk-abc123-real-key-here';

# ✅ Use environment variables
const API_KEY = process.env.STRIPE_API_KEY;

# ✅ .env file (never commit to git!)
STRIPE_API_KEY=sk-test-...
JWT_SECRET=long-random-string-here
DATABASE_URL=postgres://...

# ✅ Commit an EXAMPLE file
# .env.example (safe to commit)
STRIPE_API_KEY=your_key_here
JWT_SECRET=your_secret_here
DATABASE_URL=postgres://user:pass@localhost:5432/dbname
```

### Security Headers (Express)
```javascript
const helmet = require('helmet');
app.use(helmet()); // Sets many security headers automatically:
// Content-Security-Policy, X-Frame-Options, X-XSS-Protection, etc.

// CORS: be explicit about allowed origins
const cors = require('cors');
app.use(cors({
  origin: ['https://yourdomain.com', 'https://app.yourdomain.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  credentials: true
}));
```

## 📝 Explanation

### OWASP Top 10 Quick Reference
1. **Injection** → Use parameterized queries
2. **Broken Auth** → bcrypt passwords, short JWT expiry
3. **Sensitive Data Exposure** → HTTPS everywhere, no secrets in code
4. **XXE** → Disable XML external entities
5. **Broken Access Control** → Verify authorization on every request
6. **Security Misconfiguration** → Helmet, disable debug in prod
7. **XSS** → Sanitize output, Content Security Policy
8. **Insecure Deserialization** → Validate deserialized data
9. **Vulnerable Dependencies** → `npm audit`, Dependabot
10. **Insufficient Logging** → Log security events, don't log passwords

## 🔗 Related Tips

- [Error Handling](error-handling.md)
- [Performance Optimization](performance-optimization.md)

---

[← Back to General Tips](README.md)
