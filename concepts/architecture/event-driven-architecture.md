# Event-Driven Architecture

## 📖 Definition

**Event-Driven Architecture (EDA)** is a software design pattern where components communicate by producing and consuming **events** — notifications that something significant has happened. Producers emit events; consumers react to them asynchronously.

## 🔍 Core Components

```
[Producer] → emits event → [Message Broker] → delivers → [Consumer(s)]
                              (Kafka, RabbitMQ,
                               Redis Pub/Sub)

Example event:
{
  "type": "ORDER_PLACED",
  "orderId": "123",
  "userId": "456",
  "total": 99.99,
  "timestamp": "2025-02-27T12:00:00Z"
}
```

## 💻 Example: Node.js with EventEmitter

```javascript
const EventEmitter = require('events');
const bus = new EventEmitter();

// Producer: Order Service
class OrderService {
  placeOrder(order) {
    // Save to DB...
    console.log(`Order ${order.id} placed`);
    // Emit event — don't care who listens
    bus.emit('ORDER_PLACED', order);
  }
}

// Consumers — react independently
bus.on('ORDER_PLACED', (order) => {
  console.log(`[Email] Sending confirmation to ${order.email}`);
});

bus.on('ORDER_PLACED', (order) => {
  console.log(`[Inventory] Reserving stock for order ${order.id}`);
});

bus.on('ORDER_PLACED', (order) => {
  console.log(`[Analytics] Recording order value: $${order.total}`);
});

// Usage
const orderService = new OrderService();
orderService.placeOrder({ id: 123, email: 'user@example.com', total: 49.99 });
// All three consumers react independently!
```

## 🎯 Benefits

- **Loose coupling** — producer doesn't know about consumers
- **Scalability** — consumers can be scaled independently
- **Resilience** — consumer failures don't affect the producer
- **Audit trail** — events log exactly what happened and when

## ⚠️ Common Misconceptions

1. **"EDA always requires a message broker"** — Simple in-process event emitters are EDA too. Brokers add durability and cross-service capabilities.
2. **"Events replace synchronous APIs"** — Some operations need immediate responses (login, payment verification). Events complement, not replace, synchronous calls.

## 📚 Further Reading

- [Microservices](microservices.md)
- [Observer Pattern](../design-patterns/observer-pattern.md)

---

[← Back to Architecture](../README.md) | [← Back to Concepts](../../README.md)
