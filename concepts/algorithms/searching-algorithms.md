# Searching Algorithms

##  Definition

A **searching algorithm** finds an element within a data structure. The two fundamental approaches are **linear search** (O(n), works on unsorted data) and **binary search** (O(log n), requires sorted data).

##  Why It Matters

Efficient searching is at the core of:
- Database queries
- Autocomplete and type-ahead features
- Finding items in sorted lists
- AI game tree searches (minimax, alpha-beta pruning)

##  How It Works

### Linear Search
Check every element from left to right until found.
```
Array: [3, 7, 1, 9, 4, 2, 8]
Find 9:  3 → 7 → 1 → 9 ✓ (4 comparisons)
```

### Binary Search
Requires sorted array. Compare target to middle; eliminate half.
```
Sorted: [1, 3, 5, 7, 9, 11, 13, 15]
Find 7:
  → mid = 7 (index 3), 7 == 7 ✓ (1 comparison!)
Find 1:
  → mid = 7, 1 < 7 → search left half [1,3,5]
  → mid = 3, 1 < 3 → search left half [1]
  → mid = 1, 1 == 1 ✓ (3 comparisons)
```

##  Examples

### Binary Search (Iterative)
```javascript
function binarySearch(arr, target) {
  let left = 0, right = arr.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1; // not found
}

const sorted = [1, 3, 5, 7, 9, 11, 13, 15];
console.log(binarySearch(sorted, 7));  // 3
console.log(binarySearch(sorted, 6));  // -1
```

### Binary Search (Recursive)
```python
def binary_search(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
    if left > right:
        return -1
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, right)
    else:
        return binary_search(arr, target, left, mid - 1)

arr = [2, 4, 6, 8, 10, 12, 14]
print(binary_search(arr, 10))  # 4
```

### Ternary Search (for unimodal functions)
```python
def ternary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        third = (right - left) // 3
        mid1 = left + third
        mid2 = right - third
        if arr[mid1] == target: return mid1
        if arr[mid2] == target: return mid2
        if target < arr[mid1]:
            right = mid1 - 1
        elif target > arr[mid2]:
            left = mid2 + 1
        else:
            left, right = mid1 + 1, mid2 - 1
    return -1
```

##  Common Misconceptions

1. **"Binary search is complex to implement"** — It's surprisingly easy to get wrong (off-by-one errors). Always verify your mid calculation: `mid = left + (right - left) // 2` avoids integer overflow.
2. **"Linear search is always bad"** — For tiny arrays (< 10 elements) or unsorted data, linear search is perfectly fine.
3. **"Binary search only works for numbers"** — It works for any comparable, sorted sequence: strings, dates, custom objects.

##  Further Reading

- [Sorting Algorithms](sorting-algorithms.md)
- [Big-O Notation](big-o-notation.md)

---

[← Back to Algorithms](../README.md) | [← Back to Concepts](../../README.md)
