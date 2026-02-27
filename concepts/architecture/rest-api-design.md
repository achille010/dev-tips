# REST API Design

## 📖 Definition

**REST (Representational State Transfer)** is an architectural style for distributed hypermedia systems. A RESTful API exposes resources via HTTP and uses standard HTTP methods to perform CRUD operations.

The six REST constraints: **Client-Server, Stateless, Cacheable, Uniform Interface, Layered System, Code on Demand (optional)**.

## 🎯 Why It Matters

REST is the dominant API style for web services because:
- Uses existing HTTP infrastructure
- Human-readable URLs
- Stateless → easy to scale horizontally
- Works with any client (browser, mobile, IoT)

## 🔍 Core Concepts

### Resources and URLs
```
Resource: Users
Collection:  GET    /users          ← list all users
Single item: GET    /users/{id}     ← get one user
Create:      POST   /users          ← create user (body has data)
Update:      PUT    /users/{id}     ← replace user
Partial:     PATCH  /users/{id}     ← partial update
Delete:      DELETE /users/{id}     ← delete user
```

### HTTP Status Codes
| Code | Meaning | When to Use |
|------|---------|-------------|
| 200 | OK | Successful GET, PATCH |
| 201 | Created | Successful POST |
| 204 | No Content | Successful DELETE |
| 400 | Bad Request | Invalid input |
| 401 | Unauthorized | Not authenticated |
| 403 | Forbidden | Not authorized |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate resource |
| 422 | Unprocessable | Validation failed |
| 500 | Internal Error | Server bug |

## 💻 Examples

### RESTful Express API
```javascript
const express = require('express');
const router = express.Router();

// GET /api/users — list users
router.get('/', async (req, res) => {
  const { page = 1, limit = 20, sort = 'createdAt' } = req.query;
  const users = await User.find()
    .sort(sort)
    .skip((page - 1) * limit)
    .limit(parseInt(limit));
  res.json({ data: users, page, limit });
});

// GET /api/users/:id — get one
router.get('/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  if (!user) return res.status(404).json({ error: 'User not found' });
  res.json({ data: user });
});

// POST /api/users — create
router.post('/', async (req, res) => {
  const user = new User(req.body);
  await user.save();
  res.status(201).json({ data: user });
});

// PATCH /api/users/:id — partial update
router.patch('/:id', async (req, res) => {
  const user = await User.findByIdAndUpdate(
    req.params.id, req.body, { new: true, runValidators: true }
  );
  if (!user) return res.status(404).json({ error: 'User not found' });
  res.json({ data: user });
});

// DELETE /api/users/:id
router.delete('/:id', async (req, res) => {
  await User.findByIdAndDelete(req.params.id);
  res.status(204).send();
});
```

### API Versioning
```
/api/v1/users   ← stable version
/api/v2/users   ← new version with breaking changes
```

## ⚠️ Common Misconceptions

1. **"REST requires JSON"** — REST is format-agnostic. XML, YAML, or even plain text are valid.
2. **"REST is the same as CRUD"** — REST maps nicely to CRUD, but it's about resource state, not database operations.
3. **"REST is outdated — use GraphQL"** — REST and GraphQL serve different needs. REST excels for simple resource-based APIs; GraphQL for complex, client-driven queries.

## 📚 Further Reading

- [MVC Architecture](mvc-architecture.md)
- [Microservices](microservices.md)

---

[← Back to Architecture](../README.md) | [← Back to Concepts](../../README.md)
