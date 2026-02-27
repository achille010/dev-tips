# Object-Oriented Programming

## 📖 Definition

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes code around **objects** — entities that bundle both **data** (attributes/properties) and **behavior** (methods/functions). OOP models real-world entities and their interactions.

The four pillars of OOP are: **Encapsulation, Abstraction, Inheritance, and Polymorphism**.

## 🎯 Why It Matters

OOP is the dominant paradigm in software engineering because it:
- Maps naturally to real-world concepts
- Promotes code reuse through inheritance
- Hides complexity through encapsulation
- Makes large codebases maintainable

## 🔍 The Four Pillars

### 1. Encapsulation — Hide Internal State
Bundle data and methods together; restrict direct access to internal state.

### 2. Abstraction — Show Only What's Necessary
Expose a simple interface, hide complex implementation details.

### 3. Inheritance — Reuse and Extend
Child classes inherit properties and methods from parent classes.

### 4. Polymorphism — Many Forms
Different classes respond to the same method name in different ways.

## 💻 Examples

### Example 1: All Four Pillars (Python)
```python
from abc import ABC, abstractmethod

# Abstraction: abstract class defines interface
class Shape(ABC):
    def __init__(self, color):
        self._color = color  # Encapsulation: protected attribute

    @property
    def color(self):
        return self._color

    @abstractmethod
    def area(self) -> float: pass   # Abstraction: abstract method

    def describe(self):             # Shared behavior
        return f"A {self._color} {type(self).__name__} with area {self.area():.2f}"

# Inheritance: Circle and Rectangle inherit from Shape
class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self._radius = radius

    def area(self):                 # Polymorphism: own implementation
        import math
        return math.pi * self._radius ** 2

class Rectangle(Shape):
    def __init__(self, color, width, height):
        super().__init__(color)
        self._width, self._height = width, height

    def area(self):                 # Polymorphism: different implementation
        return self._width * self._height

# Polymorphism in action
shapes = [Circle('red', 5), Rectangle('blue', 4, 6)]
for shape in shapes:
    print(shape.describe())
# A red Circle with area 78.54
# A blue Rectangle with area 24.00
```

### Example 2: OOP in JavaScript (ES6+)
```javascript
class BankAccount {
  #balance;  // Private field (Encapsulation)
  #owner;

  constructor(owner, initialBalance = 0) {
    this.#owner = owner;
    this.#balance = initialBalance;
  }

  // Abstraction: simple interface hides implementation
  deposit(amount) {
    this.#validate(amount);
    this.#balance += amount;
    return this;
  }

  withdraw(amount) {
    this.#validate(amount);
    if (amount > this.#balance) throw new Error('Insufficient funds');
    this.#balance -= amount;
    return this;
  }

  get balance() { return this.#balance; }
  get owner()   { return this.#owner; }

  #validate(amount) {  // Private method
    if (amount <= 0) throw new Error('Amount must be positive');
  }

  toString() {
    return `${this.#owner}'s account: $${this.#balance.toFixed(2)}`;
  }
}

// Inheritance
class SavingsAccount extends BankAccount {
  #interestRate;

  constructor(owner, balance, interestRate) {
    super(owner, balance);
    this.#interestRate = interestRate;
  }

  applyInterest() {
    this.deposit(this.balance * this.#interestRate);
    return this;
  }
}

const savings = new SavingsAccount('Alice', 1000, 0.05);
savings.deposit(500).applyInterest();
console.log(savings.toString()); // Alice's account: $1575.00
```

## ⚠️ Common Misconceptions

1. **"OOP is always the best paradigm"** — OOP excels at modeling entities with shared behavior, but functional programming is often better for data transformation pipelines.
2. **"Inheritance should always be used for code reuse"** — Favor **composition over inheritance**. Inheritance creates tight coupling; composition is more flexible.
3. **"Everything must be an object"** — Over-engineering simple functions into class hierarchies adds unnecessary complexity.

## 📚 Further Reading

- [Functional Programming](functional-programming.md)
- [SOLID Principles](../principles/solid-principles.md)
- [Design Patterns](../design-patterns/)

---

[← Back to Paradigms](../README.md) | [← Back to Concepts](../../README.md)
