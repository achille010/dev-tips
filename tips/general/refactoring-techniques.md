# Refactoring Techniques

## 🎯 Problem

Your codebase has accumulated complexity — functions that are too long, logic that's duplicated, or modules that are too tightly coupled. You need to improve the code without breaking anything.

## ✨ Solution

Refactor in small, safe steps. "Refactoring" means changing the internal structure without changing external behavior. Always have tests before refactoring.

## 💻 Example

### Extract Function
```javascript
// ❌ Before: one large function
function generateInvoice(order) {
  const subtotal = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
  const discount = order.coupon ? subtotal * order.coupon.percentage / 100 : 0;
  const tax = (subtotal - discount) * 0.08;
  const shipping = subtotal > 100 ? 0 : 9.99;
  const total = subtotal - discount + tax + shipping;

  const lines = order.items.map(item =>
    `${item.name} x${item.qty} @$${item.price} = $${item.price * item.qty}`
  ).join('\n');

  return `Invoice #${order.id}\n${lines}\nSubtotal: $${subtotal}\nDiscount: -$${discount}\nTax: $${tax}\nShipping: $${shipping}\nTotal: $${total}`;
}

// ✅ After: extracted, focused functions
function calculateSubtotal(items) {
  return items.reduce((sum, item) => sum + item.price * item.qty, 0);
}

function calculateDiscount(subtotal, coupon) {
  return coupon ? subtotal * coupon.percentage / 100 : 0;
}

function calculateTax(taxableAmount, rate = 0.08) {
  return taxableAmount * rate;
}

function calculateShipping(subtotal, threshold = 100, cost = 9.99) {
  return subtotal > threshold ? 0 : cost;
}

function formatLineItems(items) {
  return items.map(item =>
    `${item.name} x${item.qty} @$${item.price} = $${item.price * item.qty}`
  ).join('\n');
}

function generateInvoice(order) {
  const subtotal = calculateSubtotal(order.items);
  const discount = calculateDiscount(subtotal, order.coupon);
  const tax      = calculateTax(subtotal - discount);
  const shipping = calculateShipping(subtotal);
  const total    = subtotal - discount + tax + shipping;

  return [
    `Invoice #${order.id}`,
    formatLineItems(order.items),
    `Subtotal: $${subtotal}`,
    `Discount: -$${discount}`,
    `Tax: $${tax}`,
    `Shipping: $${shipping}`,
    `Total: $${total}`,
  ].join('\n');
}
```

### Replace Conditional with Polymorphism
```python
# ❌ Before: switch statement on type
def calculate_area(shape):
    if shape.type == 'circle':
        return 3.14 * shape.radius ** 2
    elif shape.type == 'rectangle':
        return shape.width * shape.height
    elif shape.type == 'triangle':
        return 0.5 * shape.base * shape.height
    # Adding new shapes requires modifying this function!

# ✅ After: each class handles its own calculation (OCP)
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float: pass

class Circle(Shape):
    def __init__(self, radius): self.radius = radius
    def area(self): return 3.14159 * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, w, h): self.width, self.height = w, h
    def area(self): return self.width * self.height

# Adding new shape → just add a new class, no existing code changes
```

## 📝 Explanation

### Common Refactoring Patterns
| Pattern | When to Use |
|---------|-------------|
| Extract Function | Function > 20 lines or does multiple things |
| Extract Variable | Complex expression used multiple times |
| Rename | Name doesn't reveal intent |
| Move Method | Method uses another class's data more than its own |
| Replace Magic Number | Unexplained numeric literals |
| Replace Conditional with Polymorphism | Long if/switch on type |

### The Refactoring Process
1. **Ensure tests pass** (baseline)
2. **Make one small change**
3. **Run tests** — must still pass
4. **Repeat**

## 🔗 Related Tips

- [Code Organization](code-organization.md)
- [Testing Tips](testing-tips.md)

---

[← Back to General Tips](README.md)
