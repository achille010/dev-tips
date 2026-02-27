# Hash Tables

## 📖 Definition

A **hash table** (also called a hash map, dictionary, or associative array) is a data structure that maps **keys to values** using a **hash function**. It provides average O(1) time for insertions, deletions, and lookups.

## 🎯 Why It Matters

Hash tables power some of the most critical features in software:
- Database indexing
- Caching and memoization
- Counting frequencies
- Detecting duplicates
- Implementing sets

## 🔍 How It Works

### The Hash Function
A hash function converts a key into an array index (bucket):

```
key → hash(key) → index → value
"name" → 3829462 % 16 → 6 → "Alice"
```

### Collision Resolution

**1. Chaining** — Each bucket holds a linked list:
```
Bucket 4: ["dog" → "canine"] → ["log" → "wood"] → null
```

**2. Open Addressing (Linear Probing)** — On collision, move to the next empty slot:
```
If bucket[h(k)] is taken, try bucket[h(k)+1], bucket[h(k)+2] ...
```

### Load Factor
`load_factor = n / capacity`

When load factor exceeds ~0.75, the table resizes (doubles) and rehashes all entries.

**Time Complexities:**

| Operation | Average | Worst (all collide) |
|-----------|---------|---------------------|
| Insert    | O(1)    | O(n)               |
| Delete    | O(1)    | O(n)               |
| Search    | O(1)    | O(n)               |

## 💻 Examples

### Example 1: JavaScript (Object / Map)
```javascript
// Object as hash map (string keys only)
const phoneBook = {};
phoneBook['Alice'] = '555-1234';
phoneBook['Bob']   = '555-5678';

console.log(phoneBook['Alice']); // '555-1234'
delete phoneBook['Bob'];

// Map (any key type)
const map = new Map();
map.set(42, 'age');
map.set([1,2], 'array-key');
console.log(map.get(42)); // 'age'
console.log(map.size);    // 2

// Frequency counter pattern
const text = 'hello world';
const freq = {};
for (const char of text) {
  freq[char] = (freq[char] || 0) + 1;
}
// { h:1, e:1, l:3, o:2, ' ':1, w:1, r:1, d:1 }
```

### Example 2: Python (dict)
```python
# Python dicts are hash tables
phone_book = {
    'Alice': '555-1234',
    'Bob':   '555-5678'
}

# Access
print(phone_book.get('Alice', 'Not found'))  # '555-1234'
print(phone_book.get('Carol', 'Not found'))  # 'Not found'

# Iterate
for name, number in phone_book.items():
    print(f"{name}: {number}")

# Counting with Counter
from collections import Counter
words = ['cat', 'dog', 'cat', 'bird', 'dog', 'cat']
counts = Counter(words)  # {'cat': 3, 'dog': 2, 'bird': 1}

# Dictionary comprehension
squares = {x: x**2 for x in range(1, 6)}
```

### Example 3: Java (HashMap)
```java
import java.util.HashMap;

HashMap<String, Integer> scores = new HashMap<>();
scores.put("Alice", 95);
scores.put("Bob", 82);
scores.put("Charlie", 91);

// Access
System.out.println(scores.get("Alice")); // 95
System.out.println(scores.getOrDefault("Dave", 0)); // 0

// Iterate
for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Check existence
if (scores.containsKey("Bob")) {
    scores.put("Bob", scores.get("Bob") + 5); // increment
}
```

## ⚠️ Common Misconceptions

1. **"Hash tables always have O(1) lookup"** — Average case yes, but worst case is O(n) when all keys collide into the same bucket.
2. **"The order of keys is preserved"** — Traditional hash maps don't guarantee order. Python dicts maintain insertion order since 3.7, but that's an implementation detail.
3. **"Any object can be a key"** — Keys must be **hashable** (immutable). Mutable objects like Python lists can't be dict keys.

## 📚 Further Reading

- [Arrays and Lists](arrays-and-lists.md)
- [Dynamic Programming](../algorithms/dynamic-programming.md)

---

[← Back to Data Structures](../README.md) | [← Back to Concepts](../../README.md)
