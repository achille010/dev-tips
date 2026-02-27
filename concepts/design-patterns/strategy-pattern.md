# Strategy Pattern

## 📖 Definition

The **Strategy** pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets you change the algorithm used by an object at runtime without changing the object itself.

## 🎯 Why It Matters

Strategy eliminates conditional logic for selecting behaviors:
- Sorting algorithms (sort by name, date, or size)
- Payment processing (credit card, PayPal, crypto)
- Compression (zip, gzip, bzip2)
- Authentication (JWT, OAuth, Basic)

## 💻 Examples

### Example 1: Payment Processing (JavaScript)
```javascript
// Strategies
class CreditCardStrategy {
  pay(amount) {
    console.log(`Paying $${amount} with Credit Card`);
  }
}

class PayPalStrategy {
  pay(amount) {
    console.log(`Paying $${amount} via PayPal`);
  }
}

class CryptoStrategy {
  pay(amount) {
    console.log(`Paying $${amount} in Bitcoin`);
  }
}

// Context
class ShoppingCart {
  constructor(paymentStrategy) {
    this.paymentStrategy = paymentStrategy;
    this.items = [];
  }

  setPaymentStrategy(strategy) {
    this.paymentStrategy = strategy;
  }

  addItem(item, price) {
    this.items.push({ item, price });
  }

  checkout() {
    const total = this.items.reduce((sum, i) => sum + i.price, 0);
    this.paymentStrategy.pay(total);
  }
}

const cart = new ShoppingCart(new CreditCardStrategy());
cart.addItem('Laptop', 999);
cart.addItem('Mouse', 49);
cart.checkout(); // Paying $1048 with Credit Card

// Switch strategy at runtime
cart.setPaymentStrategy(new PayPalStrategy());
cart.checkout(); // Paying $1048 via PayPal
```

### Example 2: Sorting Strategy (Python)
```python
from abc import ABC, abstractmethod

class SortStrategy(ABC):
    @abstractmethod
    def sort(self, data: list) -> list: pass

class BubbleSortStrategy(SortStrategy):
    def sort(self, data):
        arr = data.copy()
        for i in range(len(arr)):
            for j in range(len(arr) - i - 1):
                if arr[j] > arr[j+1]:
                    arr[j], arr[j+1] = arr[j+1], arr[j]
        return arr

class QuickSortStrategy(SortStrategy):
    def sort(self, data):
        if len(data) <= 1: return data
        pivot = data[len(data)//2]
        left   = [x for x in data if x < pivot]
        middle = [x for x in data if x == pivot]
        right  = [x for x in data if x > pivot]
        return self.sort(left) + middle + self.sort(right)

class DataProcessor:
    def __init__(self, strategy: SortStrategy):
        self.strategy = strategy

    def set_strategy(self, strategy: SortStrategy):
        self.strategy = strategy

    def process(self, data):
        return self.strategy.sort(data)

data = [64, 34, 25, 12, 22, 11, 90]
processor = DataProcessor(QuickSortStrategy())
print(processor.process(data))  # [11, 12, 22, 25, 34, 64, 90]
```

## ⚠️ Common Misconceptions

1. **"Strategy requires many classes"** — In modern languages, you can use functions/lambdas as strategies instead of full classes.
2. **"Strategy and State patterns are the same"** — State also encapsulates behavior, but the behavioral change is driven by the object's internal state, not client code.

## 📚 Further Reading

- [Factory Pattern](factory-pattern.md)
- [Decorator Pattern](decorator-pattern.md)

---

[← Back to Design Patterns](../README.md) | [← Back to Concepts](../../README.md)
