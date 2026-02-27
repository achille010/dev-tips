# Documentation Tips

##  Problem

Undocumented code becomes a mystery to your future self and teammates. You're spending 20 minutes reverse-engineering a function that could have been explained in 3 lines of comments.

##  Solution

Write documentation that explains **why**, not **what** (the code already shows what). Use standardized formats like JSDoc/docstrings, maintain a good README, and keep docs close to the code.

##  Example

### JSDoc (JavaScript)
```javascript
/**
 * Calculates the discounted price for an order item.
 * Discounts are additive (not compounded) up to MAX_DISCOUNT.
 *
 * @param {number} price - Original item price in cents
 * @param {number[]} discountPercentages - List of discount percentages to apply
 * @returns {number} Final price in cents after all discounts
 * @throws {TypeError} If price is negative
 *
 * @example
 * calculateDiscountedPrice(10000, [10, 5]) // 8500 (15% off $100.00)
 */
function calculateDiscountedPrice(price, discountPercentages) {
  if (price < 0) throw new TypeError('Price cannot be negative');
  const totalDiscount = Math.min(
    discountPercentages.reduce((sum, d) => sum + d, 0),
    MAX_DISCOUNT_PERCENTAGE
  );
  return Math.round(price * (1 - totalDiscount / 100));
}
```

### Python Docstrings (Google Style)
```python
def calculate_discounted_price(price: int, discounts: list[float]) -> int:
    """Calculate the final price after applying a list of discounts.

    Discounts are additive (not compounded). The total discount is
    capped at MAX_DISCOUNT_PERCENTAGE to prevent negative prices.

    Args:
        price: Original price in cents (must be non-negative).
        discounts: List of discount percentages to apply.

    Returns:
        Final price in cents after all discounts are applied.

    Raises:
        TypeError: If price is negative.

    Example:
        >>> calculate_discounted_price(10000, [10, 5])
        8500
    """
```

### Comment Best Practices
```javascript
// ❌ Useless comment — restates what code does
// Increment i
i++;

// ❌ Outdated comment — WORSE than no comment
// Returns the user object
function getUsers() { return db.query('SELECT * FROM users'); }

//  Explains WHY (not what)
// Retry up to 3 times — the auth service has intermittent flakiness
// that typically resolves within a second (see issue #482)
const MAX_RETRIES = 3;

//  Explains non-obvious behavior
// Note: We use UTC here because the admin dashboard converts to
// local timezone on the client side (see Dashboard.jsx:47)
const timestamp = new Date().toISOString();

//  TODO with context
// TODO(alice): Remove this workaround after API v3 migration (ETA Q2 2025)
const data = transformLegacyResponse(response);
```

##  Explanation

### What to Document
- **Public API** — always (JSDoc/docstrings)
- **Complex algorithms** — explain the approach, cite the source
- **Workarounds / hacks** — WHY this workaround exists
- **Non-obvious behavior** — side effects, caveats, requirements
- **TODOs** — with context and ticket reference

### What NOT to Document
- Obvious code (`// increment counter`)
- Private implementation details that change often

##  Related Tips

- [Naming Conventions](naming-conventions.md)
- [Code Review Tips](code-review-tips.md)

---

[← Back to General Tips](README.md)
