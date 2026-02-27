# Testing Tips

## 🎯 Problem

Tests are either missing entirely, or they test implementation details so closely that every refactor breaks them, making tests a burden rather than a safety net.

## ✨ Solution

Test behavior, not implementation. Apply the testing pyramid (many unit tests, fewer integration, few E2E). Keep tests isolated, fast, and deterministic.

## 💻 Example

### Unit Testing (JavaScript/Jest)
```javascript
// ❌ Testing implementation (brittle)
test('calls calculateDiscount with 0.1', () => {
  const spy = jest.spyOn(service, 'calculateDiscount');
  service.processOrder(order);
  expect(spy).toHaveBeenCalledWith(0.1);
});

// ✅ Testing behavior (robust)
test('10% member discount applied correctly', () => {
  const order = { total: 100, memberType: 'member' };
  const result = service.processOrder(order);
  expect(result.total).toBe(90); // tested the outcome
});

// ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
// Well-structured test: AAA pattern
describe('UserService', () => {
  describe('createUser', () => {
    it('should hash the password before saving', async () => {
      // Arrange
      const userData = { email: 'test@example.com', password: 'plaintext' };
      const savedUsers = [];
      const mockRepo = { save: (u) => savedUsers.push(u) };
      const service = new UserService(mockRepo);

      // Act
      await service.createUser(userData);

      // Assert
      expect(savedUsers[0].password).not.toBe('plaintext');
      expect(savedUsers[0].password).toMatch(/^\$2[aby]/); // bcrypt hash
    });

    it('should throw ValidationError for invalid email', async () => {
      const service = new UserService(mockRepo);
      await expect(
        service.createUser({ email: 'notanemail', password: 'pass123' })
      ).rejects.toThrow(ValidationError);
    });
  });
});
```

### Test Coverage Philosophy
```
Unit tests     ████████████████████████████ 70%
Integration    ████████████              20%
E2E            ████                       10%
```

### Test Naming
```javascript
// Bad: describes what it does
it('createUser test');

// Good: describes what should happen under what condition
it('should return 404 when user does not exist');
it('should throw ValidationError when email format is invalid');
it('should send confirmation email after successful registration');
```

## 📝 Explanation

### Testing Anti-Patterns to Avoid
- **Testing implementation** — mock internals rarely; test outcomes
- **Shared mutable state between tests** — always reset state in `beforeEach`
- **Tests that depend on order** — every test should be independent
- **Slow tests** — mock external services (DB, APIs); unit tests should be < 5ms

## 🔗 Related Tips

- [Code Review Tips](code-review-tips.md)
- [Error Handling](error-handling.md)

---

[← Back to General Tips](README.md)
