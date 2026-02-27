# Decorator Pattern

##  Definition

The **Decorator** pattern attaches additional responsibilities to an object dynamically. It provides a flexible alternative to subclassing for extending functionality by wrapping objects in decorator objects.

##  Why It Matters

Decorators let you add/compose behavior without modifying existing classes:
- HTTP middleware (authentication, logging, rate limiting)
- Python's `@` decorator syntax
- Java I/O streams (BufferedReader wraps FileReader)
- UI component enhancements

##  Examples

### Example 1: Coffee Shop (JavaScript)
```javascript
// Base component
class Coffee {
  cost()        { return 1.00; }
  description() { return 'Basic Coffee'; }
}

// Base decorator
class CoffeeDecorator {
  constructor(coffee) { this.coffee = coffee; }
  cost()        { return this.coffee.cost(); }
  description() { return this.coffee.description(); }
}

// Concrete decorators
class Milk extends CoffeeDecorator {
  cost()        { return this.coffee.cost() + 0.25; }
  description() { return this.coffee.description() + ', Milk'; }
}

class Sugar extends CoffeeDecorator {
  cost()        { return this.coffee.cost() + 0.10; }
  description() { return this.coffee.description() + ', Sugar'; }
}

class Espresso extends CoffeeDecorator {
  cost()        { return this.coffee.cost() + 0.75; }
  description() { return this.coffee.description() + ', Espresso shot'; }
}

// Compose at runtime
let order = new Coffee();
order = new Milk(order);
order = new Sugar(order);
order = new Espresso(order);

console.log(order.description()); // Basic Coffee, Milk, Sugar, Espresso shot
console.log(`$${order.cost().toFixed(2)}`); // $2.10
```

### Example 2: Python Function Decorators
```python
import time
import functools

def timer(func):
    """Measure function execution time."""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper

def log_calls(func):
    """Log function calls."""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with {args}, {kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

# Stack decorators — applied bottom-up
@timer
@log_calls
def slow_add(a, b):
    time.sleep(0.1)
    return a + b

slow_add(3, 5)
# Calling slow_add with (3, 5), {}
# slow_add returned 8
# slow_add took 0.1001s
```

##  Common Misconceptions

1. **"Decorator is just inheritance"** — Inheritance is static; decorators compose dynamically at runtime and can wrap any object implementing the same interface.
2. **"Python @decorators are the GoF Decorator pattern"** — Python decorators are a language feature for wrapping functions; they're related but not the same formal pattern.

##  Further Reading

- [Strategy Pattern](strategy-pattern.md)
- [Observer Pattern](observer-pattern.md)
- [SOLID Principles](../principles/solid-principles.md)

---

[← Back to Design Patterns](../README.md) | [← Back to Concepts](../../README.md)
