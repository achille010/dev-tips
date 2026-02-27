# Arrays and Lists

##  Definition

Arrays and lists are the most fundamental data structures — they store collections of elements in sequential order. An **array** is a fixed-size, contiguous block of memory, while a **list** (or dynamic array) can grow or shrink at runtime.

##  Why It Matters

Nearly every program manipulates collections of data. Understanding arrays and lists is essential for:
- Iterating over datasets
- Storing ordered information
- Accessing elements by index in O(1) time

##  How It Works

### Static Arrays
A static array allocates a fixed amount of memory when created. The index maps directly to a memory address, making reads extremely fast.

```
Index:  0    1    2    3    4
Value: [10] [20] [30] [40] [50]
Memory: 0x00 0x04 0x08 0x0C 0x10
```

### Dynamic Arrays (Lists)
Dynamic arrays start with a capacity and double it when full — a process called **resizing**.

**Time Complexities:**

| Operation       | Average | Worst |
|----------------|---------|-------|
| Access by index | O(1)   | O(1)  |
| Search          | O(n)   | O(n)  |
| Insert at end   | O(1)*  | O(n)  |
| Insert at start | O(n)   | O(n)  |
| Delete at end   | O(1)   | O(1)  |
| Delete at start | O(n)   | O(n)  |

*amortized

##  Examples

### Example 1: JavaScript
```javascript
// Static-like array
const fruits = ['apple', 'banana', 'cherry'];
console.log(fruits[1]); // 'banana' - O(1)

// Dynamic operations
fruits.push('date');       // O(1) amortized
fruits.unshift('avocado'); // O(n) - shifts all elements

// Iteration
fruits.forEach((fruit, index) => {
  console.log(`${index}: ${fruit}`);
});

// Slicing (non-destructive)
const citrus = fruits.slice(1, 3); // ['banana', 'cherry']
```

### Example 2: Python
```python
# Python lists are dynamic arrays
numbers = [1, 2, 3, 4, 5]

# Access - O(1)
print(numbers[2])  # 3

# Append - O(1) amortized
numbers.append(6)

# Insert at position - O(n)
numbers.insert(0, 0)

# List comprehension
squares = [x**2 for x in numbers]

# Slicing
even = numbers[::2]  # every other element
```

### Example 3: Java
```java
import java.util.ArrayList;
import java.util.Arrays;

// Fixed-size array
int[] staticArr = {1, 2, 3, 4, 5};

// Dynamic list
ArrayList<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);
list.add(30);
list.remove(1); // removes index 1 (value 20)

System.out.println(list.get(0)); // 10
```

##  Common Misconceptions

1. **"Arrays and lists are the same"** — Arrays are fixed-size with O(1) access; list is an abstract data type that may use arrays or linked lists internally.
2. **"Insertion is always O(1)"** — Only at the end. Inserting at the beginning or middle is O(n) due to shifting.
3. **"Python lists are linked lists"** — False. Python lists are dynamic arrays (similar to Java's ArrayList).

##  Further Reading

- [Hash Tables](hash-tables.md)
- [Linked Lists](linked-lists.md)
- [Big-O Notation](../algorithms/big-o-notation.md)

---

[← Back to Data Structures](../README.md) | [← Back to Concepts](../../README.md)
