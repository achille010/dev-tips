# KISS Principle

## 📖 Definition

**KISS (Keep It Simple, Stupid)** is a design principle stating that most systems work best if they are kept simple rather than made complicated. Simplicity should be a key goal, and unnecessary complexity should be avoided.

Originated in the U.S. Navy in 1960, popularized in software by Kelly Johnson.

## 🎯 Why It Matters

Complex code:
- Is harder to understand and onboard new developers
- Is harder to test and debug
- Breaks more often and in unexpected ways
- Takes longer to maintain and extend

## 💻 Examples

### Over-Engineering vs Simple Solution
```javascript
// ❌ Over-engineered: unnecessary abstraction
class NumberEvenChecker {
  constructor(numberToCheck) {
    this.number = numberToCheck;
  }
  
  performEvenCheck() {
    return this.executeModuloOperation() === 0;
  }
  
  executeModuloOperation() {
    return this.number % this.numberDivisor();
  }
  
  numberDivisor() {
    return 2;
  }
}

const checker = new NumberEvenChecker(4);
console.log(checker.performEvenCheck()); // true

// ✅ KISS: one line
const isEven = n => n % 2 === 0;
console.log(isEven(4)); // true
```

### Simple Routing vs Complex Framework
```python
# ✅ KISS for a simple 3-page internal tool
from http.server import HTTPServer, BaseHTTPRequestHandler

class SimpleHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        if self.path == '/':
            self.send_response(200)
            self.end_headers()
            self.wfile.write(b'Hello, World!')
        elif self.path == '/health':
            self.send_response(200)
            self.end_headers()
            self.wfile.write(b'OK')
        else:
            self.send_response(404)
            self.end_headers()

# Don't add Express/FastAPI just because they exist
# Use them when complexity justifies it
```

## ⚠️ Common Misconceptions

1. **"Simple means naive or poorly designed"** — Simple code can be highly sophisticated. Simplicity takes skill; complexity is the easy default.
2. **"KISS means avoid all abstractions"** — Appropriate abstraction reduces cognitive complexity. KISS means *unnecessary* complexity, not all complexity.

## 📚 Further Reading

- [DRY Principle](dry-principle.md)
- [YAGNI Principle](yagni-principle.md)

---

[← Back to Principles](../README.md) | [← Back to Concepts](../../README.md)
