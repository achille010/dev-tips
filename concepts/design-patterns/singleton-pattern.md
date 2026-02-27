# Singleton Pattern

## 📖 Definition

The **Singleton** pattern ensures a class has **only one instance** and provides a global point of access to it. It's one of the most well-known (and debated) design patterns.

## 🎯 Why It Matters

Use singletons when exactly one object is needed to coordinate actions across a system:
- Database connection pools
- Configuration managers
- Logger instances
- Caches
- Thread pools

## 🔍 How It Works

```
Client A ──→ getInstance() ──→ [Single Instance]
Client B ──→ getInstance() ──→ [same Single Instance]
Client C ──→ getInstance() ──→ [same Single Instance]
```

The constructor is made private (or equivalent), and a static method `getInstance()` returns the same instance every time.

## 💻 Examples

### Example 1: JavaScript
```javascript
class Logger {
  constructor() {
    if (Logger.instance) {
      return Logger.instance;
    }
    this.logs = [];
    Logger.instance = this;
  }

  log(message) {
    const entry = `[${new Date().toISOString()}] ${message}`;
    this.logs.push(entry);
    console.log(entry);
  }

  getLogs() {
    return this.logs;
  }
}

// Usage
const logger1 = new Logger();
const logger2 = new Logger();

logger1.log('Application started');
logger2.log('User logged in');

console.log(logger1 === logger2); // true — same instance!
console.log(logger1.getLogs().length); // 2 — both saw both logs
```

### Example 2: Python (Thread-Safe)
```python
import threading

class DatabaseConnection:
    _instance = None
    _lock = threading.Lock()

    def __new__(cls):
        if cls._instance is None:
            with cls._lock:
                # Double-checked locking
                if cls._instance is None:
                    cls._instance = super().__new__(cls)
                    cls._instance.connection = None
                    cls._instance._connect()
        return cls._instance

    def _connect(self):
        print("Establishing DB connection...")
        self.connection = "DB_CONNECTION_OBJECT"

    def query(self, sql):
        print(f"Executing: {sql}")
        return []

# Usage
db1 = DatabaseConnection()
db2 = DatabaseConnection()
print(db1 is db2)  # True
db1.query("SELECT * FROM users")
```

## ⚠️ Common Misconceptions

1. **"Singletons are just global variables"** — They provide lazy initialization, controlled instantiation, and can be subclassed.
2. **"Singleton is always the right choice for shared resources"** — Singletons make testing harder (shared state between tests). Consider dependency injection instead.
3. **"Singleton guarantees thread safety"** — Not automatically. You must add locking (as shown in Python example) for thread-safe access.

## 📚 Further Reading

- [Factory Pattern](factory-pattern.md)
- [Observer Pattern](observer-pattern.md)

---

[← Back to Design Patterns](../README.md) | [← Back to Concepts](../../README.md)
