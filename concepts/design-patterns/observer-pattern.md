# Observer Pattern

##  Definition

The **Observer** pattern defines a one-to-many dependency between objects. When one object (the **subject/publisher**) changes state, all its dependents (**observers/subscribers**) are notified and updated automatically.

Also known as: **Publisher-Subscriber**, **Event Listener**

##  Why It Matters

Observer decouples the subject from its observers:
- Event systems (DOM events, Node.js EventEmitter)
- MVC/MVVM frameworks (React state, Vue reactivity)
- Real-time notifications (WebSockets)
- Stock ticker / news feeds

##  Examples

### Example 1: Event Emitter (JavaScript)
```javascript
class EventEmitter {
  constructor() {
    this.events = {};
  }

  on(event, listener) {
    if (!this.events[event]) this.events[event] = [];
    this.events[event].push(listener);
    return this; // allows chaining
  }

  off(event, listener) {
    if (!this.events[event]) return;
    this.events[event] = this.events[event].filter(l => l !== listener);
  }

  emit(event, ...args) {
    if (!this.events[event]) return;
    this.events[event].forEach(listener => listener(...args));
  }
}

// Usage
const store = new EventEmitter();

const logChange = (state) => console.log('Log:', JSON.stringify(state));
const renderUI  = (state) => console.log('UI updated:', state.count);

store.on('stateChange', logChange);
store.on('stateChange', renderUI);

store.emit('stateChange', { count: 1 });
// Log: {"count":1}
// UI updated: 1

store.off('stateChange', logChange);
store.emit('stateChange', { count: 2 });
// UI updated: 2  (logChange was removed)
```

### Example 2: Stock Ticker (Python)
```python
from abc import ABC, abstractmethod

class Observer(ABC):
    @abstractmethod
    def update(self, symbol: str, price: float): pass

class StockMarket:
    def __init__(self):
        self._observers = []
        self._prices = {}

    def subscribe(self, observer: Observer):
        self._observers.append(observer)

    def unsubscribe(self, observer: Observer):
        self._observers.remove(observer)

    def set_price(self, symbol: str, price: float):
        self._prices[symbol] = price
        self._notify(symbol, price)

    def _notify(self, symbol: str, price: float):
        for observer in self._observers:
            observer.update(symbol, price)

class AlertSystem(Observer):
    def __init__(self, threshold):
        self.threshold = threshold
    def update(self, symbol, price):
        if price > self.threshold:
            print(f"🚨 ALERT: {symbol} hit ${price:.2f}!")

class Dashboard(Observer):
    def update(self, symbol, price):
        print(f" Dashboard: {symbol} = ${price:.2f}")

market = StockMarket()
market.subscribe(Dashboard())
market.subscribe(AlertSystem(threshold=150))

market.set_price('AAPL', 145.50)
market.set_price('AAPL', 152.00)
#  Dashboard: AAPL = $152.00
#  ALERT: AAPL hit $152.00!
```

##  Common Misconceptions

1. **"Observer and Pub/Sub are identical"** — In Observer, subjects know their observers. In Pub/Sub, publishers and subscribers are decoupled via a message broker.
2. **"Observers always receive all events"** — You can filter: observers can check event data and ignore irrelevant updates.

##  Further Reading

- [Strategy Pattern](strategy-pattern.md)
- [Event-Driven Architecture](../architecture/event-driven-architecture.md)

---

[← Back to Design Patterns](../README.md) | [← Back to Concepts](../../README.md)
