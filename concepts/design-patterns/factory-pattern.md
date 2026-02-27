# Factory Pattern

##  Definition

The **Factory** pattern provides an interface for creating objects without specifying the exact class of object that will be created. It delegates the instantiation logic to subclasses or a factory function.

**Variants:**
- **Simple Factory** — a static method that creates objects
- **Factory Method** — a method in subclasses that creates objects
- **Abstract Factory** — a family of related factories

##  Why It Matters

Factories decouple creation from usage:
- Add new types without changing existing code (Open/Closed Principle)
- Centralize complex initialization logic
- Enable dependency injection and testing
- Create platform-specific objects

##  Examples

### Example 1: Simple Factory (JavaScript)
```javascript
class Animal {
  constructor(name) { this.name = name; }
  speak() { throw new Error('speak() must be implemented'); }
}

class Dog extends Animal {
  speak() { return `${this.name}: Woof!`; }
}

class Cat extends Animal {
  speak() { return `${this.name}: Meow!`; }
}

class Bird extends Animal {
  speak() { return `${this.name}: Tweet!`; }
}

// Factory function
function createAnimal(type, name) {
  const animals = { dog: Dog, cat: Cat, bird: Bird };
  const AnimalClass = animals[type.toLowerCase()];
  if (!AnimalClass) throw new Error(`Unknown animal type: ${type}`);
  return new AnimalClass(name);
}

const dog  = createAnimal('dog', 'Rex');
const cat  = createAnimal('cat', 'Whiskers');
const bird = createAnimal('bird', 'Tweety');

console.log(dog.speak());  // Rex: Woof!
console.log(cat.speak());  // Whiskers: Meow!
console.log(bird.speak()); // Tweety: Tweet!
```

### Example 2: Factory Method (Python)
```python
from abc import ABC, abstractmethod

class Button(ABC):
    @abstractmethod
    def render(self): pass

    @abstractmethod
    def on_click(self): pass

class WindowsButton(Button):
    def render(self):
        return "<button style='windows'>Click me</button>"
    def on_click(self):
        return "Windows click event"

class MacButton(Button):
    def render(self):
        return "<button style='mac'>Click me</button>"
    def on_click(self):
        return "Mac click event"

class Dialog(ABC):
    @abstractmethod
    def create_button(self) -> Button: pass  # Factory Method

    def render(self):
        button = self.create_button()
        return f"Dialog: {button.render()}"

class WindowsDialog(Dialog):
    def create_button(self):
        return WindowsButton()

class MacDialog(Dialog):
    def create_button(self):
        return MacButton()

# Usage
import platform
os_type = platform.system()
dialog = WindowsDialog() if os_type == 'Windows' else MacDialog()
print(dialog.render())
```

##  Common Misconceptions

1. **"Factory and Constructor are the same"** — Constructors always create instances of the same class. Factories can return subclasses, cached objects, or even mock objects.
2. **"Factory pattern adds unnecessary complexity"** — For one or two types, it's overkill. But as the number of types grows, factories become invaluable.

##  Further Reading

- [Singleton Pattern](singleton-pattern.md)
- [Strategy Pattern](strategy-pattern.md)
- [SOLID Principles](../principles/solid-principles.md)

---

[← Back to Design Patterns](../README.md) | [← Back to Concepts](../../README.md)
