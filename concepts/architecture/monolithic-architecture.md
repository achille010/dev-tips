# Monolithic Architecture

##  Definition

A **monolith** is an application where all components — UI, business logic, and data access — are unified into a single codebase and deployed as one unit.

##  Characteristics

```
┌─────────────────────────────┐
│         Monolith            │
│  ┌─────────┐ ┌──────────┐   │
│  │   UI    │ │ Business │   │
│  │  Layer  │ │  Logic   │   │
│  └─────────┘ └──────────┘   │
│  ┌──────────────────────┐   │
│  │    Data Access Layer │   │
│  └──────────────────────┘   │
└──────────────┬──────────────┘
               │
          [Database]
```

##  When Monoliths Win

- **Early-stage startups** — ship fast, iterate quickly
- **Small teams (< 10 devs)** — complexity overhead of microservices isn't worth it
- **Simple domains** — not every app is Amazon
- **Proven reliability** — many large systems (Etsy, Stack Overflow) run on monoliths

##  Well-Structured Monolith

```
src/
├── modules/
│   ├── users/
│   │   ├── user.model.js
│   │   ├── user.service.js
│   │   ├── user.controller.js
│   │   └── user.routes.js
│   ├── products/
│   └── orders/
├── shared/          # Cross-cutting concerns
│   ├── middleware/
│   ├── utils/
│   └── database/
└── app.js
```

A well-structured "modular monolith" provides most of the organizational benefits of microservices without the operational complexity.

##  Further Reading

- [Microservices](microservices.md)
- [Event-Driven Architecture](event-driven-architecture.md)

---

[← Back to Architecture](../README.md) | [← Back to Concepts](../../README.md)
