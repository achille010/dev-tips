# Sorting Algorithms

## 📖 Definition

A **sorting algorithm** arranges elements of a list in a particular order (ascending, descending, or custom). Sorting is one of the most fundamental operations in computer science, enabling efficient searching, merging, and data presentation.

## 🎯 Why It Matters

Sorting is a prerequisite for:
- Binary search (requires sorted data)
- Database query optimization (ORDER BY)
- Finding duplicates or closest pairs
- Data visualization and reporting

## 🔍 Common Sorting Algorithms

### Comparison Table

| Algorithm      | Best    | Average  | Worst    | Space  | Stable |
|----------------|---------|----------|----------|--------|--------|
| Bubble Sort    | O(n)    | O(n²)    | O(n²)    | O(1)   | ✅     |
| Selection Sort | O(n²)   | O(n²)    | O(n²)    | O(1)   | ❌     |
| Insertion Sort | O(n)    | O(n²)    | O(n²)    | O(1)   | ✅     |
| Merge Sort     | O(n log n)| O(n log n)| O(n log n)| O(n) | ✅     |
| Quick Sort     | O(n log n)| O(n log n)| O(n²)  | O(log n)| ❌   |
| Heap Sort      | O(n log n)| O(n log n)| O(n log n)| O(1)| ❌   |
| Counting Sort  | O(n+k)  | O(n+k)   | O(n+k)   | O(k)   | ✅     |

## 💻 Examples

### Merge Sort (JavaScript)
```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left  = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;
  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) result.push(left[i++]);
    else result.push(right[j++]);
  }
  return [...result, ...left.slice(i), ...right.slice(j)];
}

console.log(mergeSort([38, 27, 43, 3, 9, 82, 10]));
// [3, 9, 10, 27, 38, 43, 82]
```

### Quick Sort (Python)
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left   = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right  = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

print(quicksort([3, 6, 8, 10, 1, 2, 1]))
# [1, 1, 2, 3, 6, 8, 10]
```

### Insertion Sort (Good for nearly-sorted data)
```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    const current = arr[i];
    let j = i - 1;
    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current;
  }
  return arr;
}
```

## ⚠️ Common Misconceptions

1. **"Quick sort is always fastest"** — Quick sort is O(n²) worst case (bad pivot). For reliability, use merge sort or Timsort (Python's default).
2. **"Stable sort doesn't matter"** — It matters when sorting objects by multiple keys. An unstable sort may scramble previous orderings.
3. **"Built-in sort is always the best choice"** — Usually yes, but for specialized cases (nearly sorted, tiny arrays), a custom algorithm may win.

## 📚 Further Reading

- [Searching Algorithms](searching-algorithms.md)
- [Big-O Notation](big-o-notation.md)
- [Dynamic Programming](dynamic-programming.md)

---

[← Back to Algorithms](../README.md) | [← Back to Concepts](../../README.md)
