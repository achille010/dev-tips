# Declarative vs Imperative Programming

##  Definition

- **Imperative**: Describes **HOW** to do something — explicit step-by-step instructions
- **Declarative**: Describes **WHAT** you want — the system figures out how

##  Why It Matters

Understanding this distinction helps you choose the right tool:
- SQL, HTML, CSS, React JSX → declarative
- C, Python loops, shell scripts → imperative
- Most real-world code mixes both

##  Examples

### Same Problem, Two Styles
```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Imperative — HOW: loop, check, accumulate
const evenSquaresImperative = [];
for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] % 2 === 0) {
    evenSquaresImperative.push(numbers[i] * numbers[i]);
  }
}

// Declarative — WHAT: filter even, map to square
const evenSquaresDeclarative = numbers
  .filter(n => n % 2 === 0)
  .map(n => n * n);

// Both produce: [4, 16, 36, 64, 100]
```

### SQL (Declarative)
```sql
-- WHAT: "Give me customers who ordered > 3 times"
-- HOW: The database engine decides (index scan, hash join, etc.)
SELECT name, email
FROM customers
WHERE id IN (
    SELECT customer_id
    FROM orders
    GROUP BY customer_id
    HAVING COUNT(*) > 3
);
```

### React JSX (Declarative UI)
```jsx
// Declarative: describe WHAT the UI should look like
function UserList({ users, filter }) {
  return (
    <ul>
      {users
        .filter(u => u.active === filter)
        .map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
    </ul>
  );
}
// React handles the HOW (DOM diffing, updates)
```

##  Common Misconceptions

1. **"Declarative is always better"** — Declarative abstractions can hide performance issues. Sometimes you need imperative control (tight loops, memory management).
2. **"You must choose one style"** — All modern languages support both. Use declarative for clarity where possible, imperative when you need fine-grained control.

##  Further Reading

- [Functional Programming](functional-programming.md)
- [Object-Oriented Programming](object-oriented-programming.md)

---

[← Back to Paradigms](../README.md) | [← Back to Concepts](../../README.md)
