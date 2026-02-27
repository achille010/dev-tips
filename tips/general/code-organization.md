# Code Organization

## 🎯 Problem

Your project has grown organically and files are scattered everywhere — components mixed with utilities, business logic inside routes, no clear structure. It's hard to find anything.

## ✨ Solution

Organize files by **feature** rather than **type** for larger projects, and always separate concerns into distinct layers.

## 💻 Example

### By Type (Small Projects)
```
src/
├── components/     # All React components
├── hooks/          # All custom hooks
├── services/       # All API services
├── utils/          # All utility functions
└── pages/          # All pages/routes
```

### By Feature (Large Projects — Recommended)
```
src/
├── features/
│   ├── auth/
│   │   ├── components/         # Auth-specific components
│   │   │   ├── LoginForm.jsx
│   │   │   └── RegisterForm.jsx
│   │   ├── hooks/
│   │   │   └── useAuth.js
│   │   ├── services/
│   │   │   └── auth.service.js
│   │   ├── store/
│   │   │   └── authSlice.js
│   │   └── index.js            # Public API for this feature
│   │
│   ├── users/
│   │   ├── components/
│   │   ├── services/
│   │   └── index.js
│   │
│   └── products/
│       ├── components/
│       ├── services/
│       └── index.js
│
├── shared/                     # Cross-feature utilities
│   ├── components/             # Button, Modal, Input
│   ├── hooks/                  # useLocalStorage, useDebounce
│   └── utils/                  # formatDate, generateId
│
├── pages/                      # Route-level components only
│   ├── Home.jsx
│   ├── Profile.jsx
│   └── Products.jsx
│
└── app/                        # App-level config
    ├── store.js
    ├── router.jsx
    └── App.jsx
```

### The Barrel Export Pattern
```javascript
// features/auth/index.js — public API
export { LoginForm } from './components/LoginForm';
export { useAuth } from './hooks/useAuth';
export { login, logout } from './services/auth.service';

// Usage elsewhere (clean imports)
import { LoginForm, useAuth } from '@/features/auth';
// vs
import LoginForm from '@/features/auth/components/LoginForm';
import { useAuth } from '@/features/auth/hooks/useAuth';
```

## 📝 Explanation

### Rules of Thumb
1. **Co-locate related files** — if you change X and always change Y, they belong together
2. **One export per file** for components (easier to find)
3. **Index files** for public API of a feature
4. **Shared vs feature** — if it's used by 3+ features, it's shared

## 🔗 Related Tips

- [Naming Conventions](naming-conventions.md)
- [Refactoring Techniques](refactoring-techniques.md)

---

[← Back to General Tips](README.md)
