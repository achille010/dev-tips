# Big-O Notation

##  Definition

**Big-O notation** describes the upper bound of an algorithm's time or space complexity as a function of the input size **n**. It answers: *"How does performance scale as input grows?"*

It captures the **dominant term** and **ignores constants** — because at large scale, constants don't matter:
- O(2n) → O(n)
- O(n² + n) → O(n²)
- O(500) → O(1)

##  Why It Matters

Two algorithms that both "work" can differ by millions of operations for large inputs. Choosing the right algorithm determines whether your software is fast or unusable at scale.

## Complexity Classes (Best to Worst)

| Complexity | Name          | n=10    | n=100      | n=1,000,000  |
|-----------|---------------|---------|------------|--------------|
| O(1)      | Constant      | 1       | 1          | 1            |
| O(log n)  | Logarithmic   | 3       | 7          | 20           |
| O(n)      | Linear        | 10      | 100        | 1,000,000    |
| O(n log n)| Linearithmic  | 33      | 664        | 20,000,000   |
| O(n²)     | Quadratic     | 100     | 10,000     | 10¹²         |
| O(2ⁿ)     | Exponential   | 1,024   | 10³⁰       | 💀            |
| O(n!)     | Factorial     | 3628800 | 9.3×10¹⁵⁷ | 💀💀          |

##  Examples

### Identifying Complexity
```javascript
// O(1) — constant: index access, hash map lookup
function getFirst(arr) {
  return arr[0];
}

// O(n) — linear: single loop
function findMax(arr) {
  let max = arr[0];
  for (const num of arr) {
    if (num > max) max = num;
  }
  return max;
}

// O(n²) — quadratic: nested loops
function hasDuplicate(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) return true;
    }
  }
  return false;
}

// O(n log n) — merge sort
function mergeSort(arr) { /* ... see sorting-algorithms.md */ }

// O(log n) — binary search
function binarySearch(arr, target) { /* ... see searching-algorithms.md */ }
```

### Space Complexity
```javascript
// O(1) space — only uses fixed variables
function sum(arr) {
  let total = 0;
  for (const n of arr) total += n;
  return total;
}

// O(n) space — creates array proportional to input
function doubled(arr) {
  return arr.map(x => x * 2);
}

// O(n) space — recursion call stack
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1); // n stack frames
}
```

### Improving Complexity
```python
# O(n²) — check all pairs for duplicates
def has_duplicate_slow(arr):
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] == arr[j]:
                return True
    return False

# O(n) — use a hash set
def has_duplicate_fast(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return True
        seen.add(num)
    return False
```

##  Common Misconceptions

1. **"O(1) means fast"** — O(1) means *constant*, not necessarily fast. A constant 10 million operations is still O(1) but very slow.
2. **"Always optimize for the best Big-O"** — Constant factors matter for small inputs. O(n²) with tiny constants can beat O(n log n) for n < 100.
3. **"Big-O is about worst case"** — Not always. Big-O is an upper bound notation. We also use Omega (Ω) for lower bound and Theta (Θ) for tight bound.

##  Further Reading

- [Sorting Algorithms](sorting-algorithms.md)
- [Searching Algorithms](searching-algorithms.md)
- [Dynamic Programming](dynamic-programming.md)

---

[← Back to Algorithms](../README.md) | [← Back to Concepts](../../README.md)
