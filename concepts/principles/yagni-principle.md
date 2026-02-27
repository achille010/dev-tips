# YAGNI Principle

##  Definition

**YAGNI (You Aren't Gonna Need It)** is a principle of Extreme Programming (XP) that states: always implement things when you actually need them, **never when you just foresee that you might need them**.

Coined by Ron Jeffries, it's a safeguard against over-engineering.

##  Why It Matters

Speculative features:
- Add maintenance burden for code never used
- Increase complexity for future developers
- Waste time that could be spent on real features
- Often implement requirements incorrectly (requirements change!)

##  Examples

### YAGNI in API Design
```javascript
// ❌ YAGNI violation: "we might need these later"
class UserService {
  async getUser(id) { /* ... */ }
  async getUsersByAge(minAge, maxAge) { /* maybe needed? */ }
  async getUsersByCountry(country) { /* possibly useful? */ }
  async getUsersBySubscriptionLevel(level) { /* just in case */ }
  async exportUsersToCSV() { /* someone might ask for this */ }
  async archiveInactiveUsers(days) { /* future feature? */ }
}

//  YAGNI: implement only what's currently required
class UserService {
  async getUser(id) { /* ← actually needed now */ }
  async createUser(data) { /* ← actually needed now */ }
}
// Add more when stakeholders request them with real requirements
```

### YAGNI in Database Design
```sql
-- ❌ Future-proofing overkill
CREATE TABLE users (
    id BIGINT PRIMARY KEY,
    username VARCHAR(50),
    email VARCHAR(100),
    -- "might need social login later"
    google_id VARCHAR(100),
    github_id VARCHAR(100),
    facebook_id VARCHAR(50),
    -- "might need preferences later"
    preferred_currency CHAR(3),
    preferred_language CHAR(5),
    newsletter_topic_1 VARCHAR(50),
    newsletter_topic_2 VARCHAR(50)
);

--  Add columns when requirements are confirmed
CREATE TABLE users (
    id BIGINT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT NOW()
);
-- Add social_logins table and preferences table when actually needed
```

##  Common Misconceptions

1. **"YAGNI means no forward planning"** — YAGNI targets *implementation*, not *design*. You can design extensible systems without implementing unused features.
2. **"YAGNI and DRY conflict"** — They complement each other. DRY: don't repeat what you have now. YAGNI: don't add what you don't have yet.

##  Further Reading

- [KISS Principle](kiss-principle.md)
- [DRY Principle](dry-principle.md)
- [SOLID Principles](solid-principles.md)

---

[← Back to Principles](../README.md) | [← Back to Concepts](../../README.md)
