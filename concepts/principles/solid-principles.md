# SOLID Principles

## 📖 Definition

**SOLID** is an acronym for five design principles that make software more maintainable, flexible, and scalable. Coined by Robert C. Martin ("Uncle Bob").

| Letter | Principle | Short Description |
|--------|-----------|-------------------|
| **S** | Single Responsibility | A class should have one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subclasses must be substitutable for their base classes |
| **I** | Interface Segregation | Many specific interfaces > one general interface |
| **D** | Dependency Inversion | Depend on abstractions, not concretions |

## 🎯 Why It Matters

SOLID violations cause:
- **God classes** that do everything
- **Fragile code** that breaks unexpectedly
- **Rigid code** that's hard to extend
- **Untestable code** with too many dependencies

## 💻 Examples

### S — Single Responsibility Principle
```python
# ❌ Violates SRP: one class handles data + formatting + saving
class Report:
    def generate_data(self):   ...
    def format_as_pdf(self):   ...
    def format_as_html(self):  ...
    def save_to_database(self):...
    def send_by_email(self):   ...

# ✅ Each class has one responsibility
class ReportData:
    def generate(self): ...

class ReportFormatter:
    def to_pdf(self, data): ...
    def to_html(self, data): ...

class ReportRepository:
    def save(self, report): ...

class ReportMailer:
    def send(self, report, recipient): ...
```

### O — Open/Closed Principle
```javascript
// ❌ Violates OCP: must modify class to add new discount type
class OrderCalculator {
  calculateDiscount(order) {
    if (order.type === 'vip') return order.total * 0.2;
    if (order.type === 'member') return order.total * 0.1;
    if (order.type === 'new_user') return order.total * 0.05;
    return 0;
    // Adding a new type requires modifying this method!
  }
}

// ✅ OCP: extend by adding new strategy, not modifying existing code
class VIPDiscount    { calculate(total) { return total * 0.2; } }
class MemberDiscount { calculate(total) { return total * 0.1; } }
class NewUserDiscount{ calculate(total) { return total * 0.05; } }

class OrderCalculator {
  constructor(discountStrategy) { this.strategy = discountStrategy; }
  calculateDiscount(order) { return this.strategy.calculate(order.total); }
}
```

### L — Liskov Substitution Principle
```python
# ❌ Violates LSP: Square breaks Rectangle's contract
class Rectangle:
    def set_width(self, w):  self.width = w
    def set_height(self, h): self.height = h
    def area(self): return self.width * self.height

class Square(Rectangle):  # Bad inheritance!
    def set_width(self, w):
        self.width = self.height = w  # breaks Rectangle expectations!
    def set_height(self, h):
        self.width = self.height = h

# ✅ LSP: use composition or a common interface
class Shape:
    def area(self): pass

class Rectangle(Shape):
    def __init__(self, w, h): self.w, self.h = w, h
    def area(self): return self.w * self.h

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side * self.side
```

### I — Interface Segregation Principle
```typescript
// ❌ Violates ISP: forces classes to implement unused methods
interface Worker {
  work(): void;
  eat(): void;
  sleep(): void;
}

// ✅ ISP: split into focused interfaces
interface Workable { work(): void; }
interface Eatable  { eat(): void;  }
interface Sleepable{ sleep(): void;}

class Human implements Workable, Eatable, Sleepable {
  work()  { console.log('Working'); }
  eat()   { console.log('Eating');  }
  sleep() { console.log('Sleeping');}
}

class Robot implements Workable {
  work() { console.log('Processing...'); }
  // No need to implement eat() or sleep()!
}
```

### D — Dependency Inversion Principle
```javascript
// ❌ Violates DIP: high-level module depends on low-level detail
class NotificationService {
  constructor() {
    this.emailer = new GmailClient(); // concrete dependency
  }
  notify(message) { this.emailer.send(message); }
}

// ✅ DIP: depend on abstraction
class NotificationService {
  constructor(mailer) { // inject the abstraction
    this.mailer = mailer;
  }
  notify(message) { this.mailer.send(message); }
}

class GmailClient   { send(msg) { /* ... */ } }
class SendGridClient{ send(msg) { /* ... */ } }

// Swap implementations without changing NotificationService
const service = new NotificationService(new SendGridClient());
```

## ⚠️ Common Misconceptions

1. **"SOLID must always be followed"** — Over-applying SOLID creates unnecessary abstraction. Use principles as guidelines, not rules.
2. **"DIP means use dependency injection frameworks"** — DIP is about direction of dependencies; DI is one implementation.

## 📚 Further Reading

- [DRY Principle](dry-principle.md)
- [Design Patterns](../design-patterns/)

---

[← Back to Principles](../README.md) | [← Back to Concepts](../../README.md)
