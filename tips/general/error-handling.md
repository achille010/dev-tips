# Error Handling

## 🎯 Problem

Your app crashes with an unhelpful "undefined" error, or swallows errors silently and continues in a broken state. Users see white screens; you have no idea what went wrong.

## ✨ Solution

Handle errors explicitly, provide context in error messages, and fail loudly in development while failing gracefully in production.

## 💻 Example

### JavaScript — Try/Catch/Finally
```javascript
// ❌ No error handling — crashes or silent failure
async function getUser(id) {
  const response = await fetch(`/api/users/${id}`);
  const data = await response.json();
  return data;
}

// ✅ Explicit error handling with context
async function getUser(id) {
  if (!id) throw new TypeError('getUser: id is required');

  let response;
  try {
    response = await fetch(`/api/users/${id}`);
  } catch (networkError) {
    throw new Error(`getUser: Network request failed: ${networkError.message}`);
  }

  if (!response.ok) {
    throw new Error(`getUser: API returned ${response.status} ${response.statusText}`);
  }

  try {
    return await response.json();
  } catch (parseError) {
    throw new Error(`getUser: Invalid JSON response: ${parseError.message}`);
  }
}

// Usage with error handling
try {
  const user = await getUser(123);
  renderUser(user);
} catch (err) {
  console.error(err.message);
  showErrorToast('Failed to load user. Please try again.');
}
```

### Custom Error Classes
```javascript
class AppError extends Error {
  constructor(message, { statusCode = 500, code, context } = {}) {
    super(message);
    this.name = this.constructor.name;
    this.statusCode = statusCode;
    this.code = code;
    this.context = context;
  }
}

class NotFoundError extends AppError {
  constructor(resource, id) {
    super(`${resource} with id '${id}' not found`, { statusCode: 404, code: 'NOT_FOUND' });
  }
}

class ValidationError extends AppError {
  constructor(field, message) {
    super(`Validation failed for '${field}': ${message}`, { statusCode: 422, code: 'VALIDATION_ERROR' });
  }
}

// Express global error handler
app.use((err, req, res, next) => {
  const status = err.statusCode || 500;
  const code   = err.code || 'INTERNAL_ERROR';

  console.error(err); // log full error server-side

  res.status(status).json({
    error: { code, message: err.message }
  });
});
```

### Python — Exception Hierarchy
```python
class AppError(Exception):
    """Base application error."""
    def __init__(self, message, code=None):
        super().__init__(message)
        self.code = code

class DatabaseError(AppError):
    """Database-related errors."""

class ValidationError(AppError):
    """Input validation errors."""

def get_user(user_id: int):
    if not user_id:
        raise ValidationError("user_id is required", code="MISSING_FIELD")
    try:
        user = db.query(User).filter_by(id=user_id).first()
        if not user:
            raise AppError(f"User {user_id} not found", code="NOT_FOUND")
        return user
    except SQLAlchemyError as e:
        raise DatabaseError(f"Database query failed: {e}") from e  # chain exceptions

# Usage
try:
    user = get_user(user_id)
except ValidationError as e:
    return jsonify({"error": str(e)}), 422
except DatabaseError as e:
    logger.error(f"DB error: {e}")
    return jsonify({"error": "Service unavailable"}), 503
except AppError as e:
    return jsonify({"error": str(e), "code": e.code}), 404
```

## 📝 Explanation

### Principles
1. **Fail loudly in dev, gracefully in prod** — raise errors during development; show friendly messages to users
2. **Add context** — "Network error" is worse than "getUser: network error for id=123"
3. **Don't swallow errors** — `catch(e) {}` is almost always wrong
4. **Use custom error classes** — allows catch-by-type

## 🔗 Related Tips

- [Testing Tips](testing-tips.md)
- [Security Best Practices](security-best-practices.md)

---

[← Back to General Tips](README.md)
