# Performance Optimization

## 🎯 Problem

Your application feels slow. Pages take forever to load, API calls pile up, and users are leaving. You need to identify and fix performance bottlenecks.

## ✨ Solution

Profile first, then optimize. Focus on the biggest wins: reduce network requests, cache aggressively, and avoid unnecessary work.

## 💻 Example

### Frontend Performance
```javascript
// ❌ N+1 fetches: fetches each user separately
const posts = await getPosts();
for (const post of posts) {
  post.author = await getUser(post.authorId); // N separate API calls!
}

// ✅ Batch fetch: one query
const posts = await getPosts();
const authorIds = [...new Set(posts.map(p => p.authorId))];
const authors = await getUsers(authorIds); // one query
const authorMap = Object.fromEntries(authors.map(a => [a.id, a]));
posts.forEach(p => p.author = authorMap[p.authorId]);

// ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

// Debounce expensive operations (React example)
import { useState, useEffect, useCallback } from 'react';

function useDebounce(value, delay = 300) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const id = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(id);
  }, [value, delay]);
  return debounced;
}

function SearchBar() {
  const [query, setQuery] = useState('');
  const debouncedQuery = useDebounce(query, 300);

  useEffect(() => {
    if (debouncedQuery) fetchSearchResults(debouncedQuery);
  }, [debouncedQuery]); // Only fires 300ms after user stops typing

  return <input onChange={e => setQuery(e.target.value)} />;
}
```

### Backend/Database
```sql
-- ❌ Full table scan every request
SELECT * FROM orders WHERE email = 'user@example.com';

-- ✅ Add an index on frequently queried columns
CREATE INDEX idx_orders_email ON orders(email);

-- ❌ SELECT * fetches unused columns
SELECT * FROM users;

-- ✅ SELECT only what you need
SELECT id, name, email FROM users;
```

```javascript
// In-memory caching example (Node.js)
const cache = new Map();

async function getCachedUser(id) {
  const key = `user:${id}`;
  if (cache.has(key)) {
    return cache.get(key); // serve from cache
  }
  const user = await db.findUser(id);
  cache.set(key, user);
  // Clear cache after 5 minutes
  setTimeout(() => cache.delete(key), 5 * 60 * 1000);
  return user;
}
```

## 📝 Explanation

### Performance Checklist
- [ ] Profile before optimizing (measure, don't guess)
- [ ] Fix N+1 query problems first (biggest impact)
- [ ] Add database indexes on filtered/sorted columns
- [ ] Implement caching (Redis, in-memory) for repeated queries
- [ ] Use pagination instead of returning all records
- [ ] Lazy load images and non-critical JavaScript
- [ ] CDN for static assets

## 🔗 Related Tips

- [Security Best Practices](security-best-practices.md)
- [Testing Tips](testing-tips.md)

---

[← Back to General Tips](README.md)
