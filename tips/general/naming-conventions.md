# Naming Conventions

##  Problem

Your codebase uses inconsistent naming — some variables are `camelCase`, some `snake_case`, some abbreviated (`usr`, `btn`), others fully spelled out. New developers struggle to follow the logic.

##  Solution

Adopt a consistent naming convention per language/context and apply it uniformly. Choose names that reveal intent.

##  Example

### General Rules (Language-Agnostic)
```
❌ Bad names:     x, d, temp, data, obj, thing, mgr, helper
✅ Good names:    userAge, createdAt, cartItemCount, httpResponse
```

**Names should answer:**
- **What it stores** (not how it's stored)
- **What it does** (for functions/methods)
- **What it means** in this context

### By Language

#### JavaScript / TypeScript
```javascript
// Variables and functions: camelCase
const userAge = 25;
const isAuthenticated = true;
function calculateTax(amount) {}

// Classes: PascalCase
class UserAuthService {}
class HttpClient {}

// Constants: SCREAMING_SNAKE_CASE
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.example.com';

// Private members (convention): _prefix
class User {
  _passwordHash;  // or #passwordHash (JS private field)
}

// React components: PascalCase
function UserProfileCard() {}

// Files: kebab-case
// user-profile-card.jsx
// auth.service.js
// api-client.ts
```

#### Python
```python
# Variables and functions: snake_case
user_age = 25
is_authenticated = True
def calculate_tax(amount): ...

# Classes: PascalCase
class UserAuthService: ...

# Constants: SCREAMING_SNAKE_CASE
MAX_RETRY_COUNT = 3
API_BASE_URL = 'https://api.example.com'

# Private (convention): _prefix
class User:
    def __init__(self):
        self._password_hash = None  # "protected"
        self.__secret = None        # name-mangled (stronger private)

# Files: snake_case
# user_auth_service.py
# calculate_tax.py
```

### Boolean Naming
```javascript
// Use is/has/can/should prefix for booleans
const isLoggedIn = true;
const hasPermission = false;
const canEdit = user.role === 'admin';
const shouldRedirect = !isLoggedIn;

// ❌ Ambiguous:
const login = true;       // Is this a function or a state?
const permission = false; // Which permission?
```

### Function Naming
```javascript
// Functions should be verb + noun
function getUser(id) {}       // Retrieve
function createOrder(data) {} // Create
function deletePost(id) {}    // Destroy
function validateEmail(email) {} // Check
function formatDate(date) {}  // Transform
function parseJSON(str) {}    // Convert
function notifyUser(msg) {}   // Side effect

// ❌ Nouns as function names (confusing)
function userInfo() {}
function dataCleaner() {}
```

##  Explanation

### Naming Checklist
- [ ] Pronounceable (you'll say it in code review)
- [ ] Searchable (not `e`, `d`, `temp`)
- [ ] Self-describing (no comments needed)
- [ ] Consistent with project conventions
- [ ] Appropriate length (not too short or long)

##  Related Tips

- [Code Organization](code-organization.md)
- [Documentation Tips](documentation-tips.md)

---

[← Back to General Tips](README.md)
