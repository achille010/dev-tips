# DRY Principle

## 📖 Definition

**DRY (Don't Repeat Yourself)** states: *"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."* — Andy Hunt & Dave Thomas, The Pragmatic Programmer.

If you find yourself copying code, there's likely a DRY violation.

## 🎯 Why It Matters

When knowledge is duplicated:
- A bug fix in one place leaves it unfixed in others
- Feature changes must be synchronized across duplicates
- Cognitive overhead increases as you must track all copies

## 💻 Examples

### Violating DRY — Then Fixing It
```javascript
// ❌ DRY violation: validation logic duplicated
function registerUser(email, password) {
  if (!email.includes('@')) throw new Error('Invalid email');
  if (password.length < 8)  throw new Error('Password too short');
  // register...
}

function updateUser(email, password) {
  if (!email.includes('@')) throw new Error('Invalid email');
  if (password.length < 8)  throw new Error('Password too short');
  // update...
}

// ✅ DRY: single source of truth for validation
function validateEmail(email) {
  if (!email.includes('@')) throw new Error('Invalid email');
}

function validatePassword(password) {
  if (password.length < 8) throw new Error('Password too short');
}

function registerUser(email, password) {
  validateEmail(email);
  validatePassword(password);
  // register...
}

function updateUser(email, password) {
  validateEmail(email);
  validatePassword(password);
  // update...
}
```

### DRY in Configuration
```python
# ❌ Magic numbers repeated everywhere
tax_rate = 1.08
price1_with_tax = 10.00 * 1.08
price2_with_tax = 25.00 * 1.08
price3_with_tax = 50.00 * 1.08

# ✅ Single source of truth
TAX_RATE = 1.08

def apply_tax(price):
    return price * TAX_RATE

prices = [10.00, 25.00, 50.00]
prices_with_tax = [apply_tax(p) for p in prices]
```

## ⚠️ Common Misconceptions

1. **"DRY means never copy any code"** — DRY is about *knowledge*, not *code text*. Sometimes similar-looking code represents different concepts and should remain separate.
2. **"DRY abstraction is always better"** — Premature DRY creates wrong abstractions. WET (Write Everything Twice) is sometimes acceptable early on; abstract after the third occurrence.

## 📚 Further Reading

- [SOLID Principles](solid-principles.md)
- [KISS Principle](kiss-principle.md)

---

[← Back to Principles](../README.md) | [← Back to Concepts](../../README.md)
