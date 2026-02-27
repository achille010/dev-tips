# Stacks and Queues

## 📖 Definition

- A **stack** is a LIFO (Last In, First Out) data structure — the last item pushed is the first item popped.
- A **queue** is a FIFO (First In, First Out) data structure — the first item enqueued is the first item dequeued.

## 🎯 Why It Matters

Stacks and queues abstract common real-world workflows:
- **Stacks**: Undo/redo, function call stack, balanced parentheses checking, browser history
- **Queues**: Task scheduling, print queues, BFS traversal, message queues

## 🔍 How It Works

### Stack Operations
```
Push 1 → [1]
Push 2 → [1, 2]
Push 3 → [1, 2, 3]
Pop    → [1, 2]  returns 3
Peek   → 2 (view top without removing)
```

**Time Complexities:**
| Operation | Time |
|-----------|------|
| Push      | O(1) |
| Pop       | O(1) |
| Peek/Top  | O(1) |
| Search    | O(n) |

### Queue Operations
```
Enqueue A → [A]
Enqueue B → [A, B]
Enqueue C → [A, B, C]
Dequeue   → [B, C]  returns A
Peek      → B (front without removing)
```

**Time Complexities:**
| Operation | Array-backed | Linked-list |
|-----------|-------------|-------------|
| Enqueue   | O(1)*       | O(1)        |
| Dequeue   | O(n)        | O(1)        |
| Peek      | O(1)        | O(1)        |

*Using a deque or circular buffer avoids the O(n) dequeue

## 💻 Examples

### Example 1: Stack in JavaScript
```javascript
// Array as stack (push/pop at end)
class Stack {
  constructor() { this.items = []; }
  push(item) { this.items.push(item); }
  pop()       { return this.items.pop(); }
  peek()      { return this.items[this.items.length - 1]; }
  isEmpty()   { return this.items.length === 0; }
  size()      { return this.items.length; }
}

// Real use: balanced parentheses
function isBalanced(str) {
  const stack = new Stack();
  const open  = '({[';
  const close = ')}]';
  const match = { ')': '(', '}': '{', ']': '[' };

  for (const ch of str) {
    if (open.includes(ch))  stack.push(ch);
    else if (close.includes(ch)) {
      if (stack.isEmpty() || stack.peek() !== match[ch]) return false;
      stack.pop();
    }
  }
  return stack.isEmpty();
}

console.log(isBalanced('({[hello]})'));  // true
console.log(isBalanced('({[hello}])')); // false
```

### Example 2: Queue in Python
```python
from collections import deque

# deque supports O(1) append and popleft
queue = deque()
queue.append('task1')
queue.append('task2')
queue.append('task3')

print(queue.popleft())  # 'task1'
print(queue[0])         # 'task2' (peek front)

# Priority Queue with heapq
import heapq
pq = []
heapq.heappush(pq, (1, 'high priority'))
heapq.heappush(pq, (3, 'low priority'))
heapq.heappush(pq, (2, 'medium priority'))

while pq:
    priority, task = heapq.heappop(pq)
    print(f"Processing: {task}")
# Output: high → medium → low
```

### Example 3: Stack for Undo/Redo
```javascript
class TextEditor {
  constructor() {
    this.text = '';
    this.undoStack = [];
    this.redoStack = [];
  }

  type(chars) {
    this.undoStack.push(this.text);
    this.redoStack = []; // clear redo on new action
    this.text += chars;
  }

  undo() {
    if (this.undoStack.length === 0) return;
    this.redoStack.push(this.text);
    this.text = this.undoStack.pop();
  }

  redo() {
    if (this.redoStack.length === 0) return;
    this.undoStack.push(this.text);
    this.text = this.redoStack.pop();
  }
}

const editor = new TextEditor();
editor.type('Hello');
editor.type(' World');
console.log(editor.text); // 'Hello World'
editor.undo();
console.log(editor.text); // 'Hello'
editor.redo();
console.log(editor.text); // 'Hello World'
```

## ⚠️ Common Misconceptions

1. **"Stack overflow is only a website"** — Stack overflow happens when the call stack exceeds memory limits, typically from unbounded recursion.
2. **"Queues are always FIFO"** — Priority queues and deques modify the standard FIFO behavior.
3. **"Using an array as a queue is fine"** — `array.shift()` is O(n). Use a deque/linked list for efficient queue operations.

## 📚 Further Reading

- [Arrays and Lists](arrays-and-lists.md)
- [Trees and Graphs](trees-and-graphs.md)
- [Recursion](../algorithms/recursion.md)

---

[← Back to Data Structures](../README.md) | [← Back to Concepts](../../README.md)
