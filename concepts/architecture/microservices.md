# Microservices

##  Definition

**Microservices** is an architectural style that structures an application as a collection of small, independent services, each running in its own process and communicating through well-defined APIs (typically HTTP/REST or message queues).

##  Microservices vs Monolith

| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| Deployment | Single unit | Each service independently |
| Scaling | Scale everything | Scale individual services |
| Tech stack | Usually uniform | Each service can differ |
| Communication | In-process | Network calls |
| Complexity | Initially simpler | Higher operational complexity |
| Fault isolation | One bug can crash all | Failures are contained |

##  Example Structure

```
e-commerce-platform/
├── services/
│   ├── user-service/        # Port 3001 - auth, profiles
│   ├── product-service/     # Port 3002 - catalog, search
│   ├── order-service/       # Port 3003 - cart, checkout
│   ├── payment-service/     # Port 3004 - billing
│   └── notification-service/# Port 3005 - emails, SMS
├── api-gateway/             # Single entry point → routes to services
└── docker-compose.yml       # Orchestration
```

```yaml
# docker-compose.yml
version: '3.8'
services:
  api-gateway:
    build: ./api-gateway
    ports: ["80:80"]
    depends_on: [user-service, product-service]

  user-service:
    build: ./services/user-service
    environment:
      DB_URL: postgres://user_db/users
    ports: ["3001:3001"]

  product-service:
    build: ./services/product-service
    ports: ["3002:3002"]

  user_db:
    image: postgres:15
    environment:
      POSTGRES_DB: users
```

##  Common Misconceptions

1. **"Always use microservices for scalability"** — Start with a monolith, split into microservices when scaling or team boundaries demand it (Martin Fowler's "MonolithFirst").
2. **"Microservices = Docker containers"** — They're complementary. Microservices is an architecture; containers are a deployment mechanism.

##  Further Reading

- [Monolithic Architecture](monolithic-architecture.md)
- [MVC Architecture](mvc-architecture.md)
- [CI/CD Pipelines](../../guides/deployment/ci-cd-pipelines.md)

---

[← Back to Architecture](../README.md) | [← Back to Concepts](../../README.md)
