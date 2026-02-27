# Functional Programming

## 📖 Definition

**Functional Programming (FP)** is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing state or mutable data. Programs are built by composing **pure functions**.

Core principles:
- **Pure functions** — same input always returns same output, no side effects
- **Immutability** — data is never modified; new versions are created
- **First-class functions** — functions are values that can be passed and returned
- **Higher-order functions** — functions that take/return functions

## 🎯 Why It Matters

Functional code is:
- **Predictable** — pure functions are easy to reason about
- **Testable** — no hidden state to account for
- **Parallelizable** — immutable data = no race conditions
- **Composable** — small functions combine into complex behavior

## 💻 Examples

### Example 1: Core FP Concepts (JavaScript)
```javascript
// Pure function: no side effects, deterministic
const add = (a, b) => a + b;
const double = x => x * 2;
const square = x => x * x;

// Immutability: never mutate, create new
const original = [1, 2, 3, 4, 5];
const doubled = original.map(double);    // [2, 4, 6, 8, 10]
const evens   = original.filter(n => n % 2 === 0); // [2, 4]
const sum     = original.reduce(add, 0); // 15
// original is unchanged: [1, 2, 3, 4, 5]

// Higher-order functions
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);
const pipe    = (...fns) => x => fns.reduce((v, f) => f(v), x);

const transform = pipe(double, square, x => x - 1);
console.log(transform(3)); // ((3*2)^2) - 1 = 35

// Currying: partial application
const multiply = a => b => a * b;
const triple = multiply(3);
console.log([1, 2, 3, 4].map(triple)); // [3, 6, 9, 12]
```

### Example 2: Avoiding Side Effects (Python)
```python
# Impure — modifies outer state (avoid)
total = 0
def add_to_total(n):
    global total
    total += n  # side effect!
    return total

# Pure — no side effects
def running_total(numbers):
    return sum(numbers)

# FP-style data transformation
from functools import reduce

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

result = (
    list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4, 6, 8, 10]
    |> list(map(lambda x: x ** 2, ...))           # [4, 16, 36, 64, 100]
)

# Using functools
squared_evens = list(map(lambda x: x**2, filter(lambda x: x%2==0, numbers)))
print(squared_evens)  # [4, 16, 36, 64, 100]

total = reduce(lambda acc, x: acc + x, squared_evens, 0)
print(total)  # 220
```

### Example 3: Memoization (Pure Function Optimization)
```javascript
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const expensiveCalculation = memoize((n) => {
  console.log(`Computing for ${n}...`);
  return n * n * n;
});

console.log(expensiveCalculation(5));  // Computing for 5... 125
console.log(expensiveCalculation(5));  // 125 (cached!)
console.log(expensiveCalculation(3));  // Computing for 3... 27
```

## ⚠️ Common Misconceptions

1. **"FP means no loops"** — FP favors recursion and higher-order functions over loops, but that's about style, not a hard rule.
2. **"FP is only for academics"** — React (hooks), Redux, Elm, and Haskell are mainstream FP-influenced tools used in production daily.
3. **"Pure functions eliminate all side effects"** — Side effects (I/O, network) are necessary. FP isolates side effects rather than eliminating them entirely.

## 📚 Further Reading

- [Object-Oriented Programming](object-oriented-programming.md)
- [Declarative vs Imperative](declarative-vs-imperative.md)

---

[← Back to Paradigms](../README.md) | [← Back to Concepts](../../README.md)
