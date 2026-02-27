# Linked Lists

##  Definition

A **linked list** is a linear data structure where elements (nodes) are stored in non-contiguous memory locations. Each node contains a **value** and a **pointer** (reference) to the next node. Unlike arrays, linked lists don't require contiguous memory.

**Types:**
- **Singly Linked**: Each node points to the next node
- **Doubly Linked**: Each node points to both next and previous nodes
- **Circular Linked**: The last node points back to the first node

##  Why It Matters

Linked lists shine when:
- You need frequent insertions/deletions at the front (O(1) vs O(n) for arrays)
- Memory size is unknown in advance
- Implementing stacks, queues, and hash table chaining

##  How It Works

### Singly Linked List Structure
```
Head
 ↓
[10 | •]→[20 | •]→[30 | •]→[40 | null]
```

### Time Complexities

| Operation        | Linked List | Array |
|------------------|-------------|-------|
| Access by index  | O(n)        | O(1)  |
| Insert at front  | O(1)        | O(n)  |
| Insert at end    | O(n)*       | O(1)* |
| Insert at middle | O(n)        | O(n)  |
| Delete at front  | O(1)        | O(n)  |
| Search           | O(n)        | O(n)  |

*O(1) if tail pointer maintained

##  Examples

### Example 1: Singly Linked List (JavaScript)
```javascript
class ListNode {
  constructor(val, next = null) {
    this.val = val;
    this.next = next;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  prepend(val) {
    this.head = new ListNode(val, this.head);
    this.size++;
  }

  append(val) {
    const node = new ListNode(val);
    if (!this.head) { this.head = node; }
    else {
      let curr = this.head;
      while (curr.next) curr = curr.next;
      curr.next = node;
    }
    this.size++;
  }

  delete(val) {
    if (!this.head) return;
    if (this.head.val === val) { this.head = this.head.next; return; }
    let curr = this.head;
    while (curr.next && curr.next.val !== val) curr = curr.next;
    if (curr.next) curr.next = curr.next.next;
  }

  toArray() {
    const result = [];
    let curr = this.head;
    while (curr) { result.push(curr.val); curr = curr.next; }
    return result;
  }
}

const ll = new LinkedList();
ll.append(10); ll.append(20); ll.append(30);
ll.prepend(5);
console.log(ll.toArray()); // [5, 10, 20, 30]
ll.delete(20);
console.log(ll.toArray()); // [5, 10, 30]
```

### Example 2: Reversing a Linked List (Python)
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverse_list(head):
    prev = None
    curr = head
    while curr:
        nxt = curr.next  # save next
        curr.next = prev # reverse pointer
        prev = curr      # advance prev
        curr = nxt       # advance curr
    return prev          # new head

# Build: 1 → 2 → 3 → 4 → 5
head = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))

# Reverse: 5 → 4 → 3 → 2 → 1
head = reverse_list(head)
curr = head
while curr:
    print(curr.val, end=' → ')
    curr = curr.next
```

### Example 3: Detect a Cycle (Floyd's Tortoise & Hare)
```python
def has_cycle(head):
    """Detect cycle using two pointers."""
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next       # moves 1 step
        fast = fast.next.next  # moves 2 steps
        if slow is fast:       # met → cycle exists
            return True
    return False
```

##  Common Misconceptions

1. **"Linked lists are always better than arrays"** — Arrays have O(1) random access; linked lists require O(n) traversal for indexed access.
2. **"Linked lists save memory"** — Each node stores a pointer in addition to the value, increasing per-element memory overhead.
3. **"Doubly linked lists are always preferred"** — They use more memory and are more complex to maintain. Use singly linked lists when you only need forward traversal.

##  Further Reading

- [Arrays and Lists](arrays-and-lists.md)
- [Stacks and Queues](stacks-and-queues.md)
- [Trees and Graphs](trees-and-graphs.md)

---

[← Back to Data Structures](../README.md) | [← Back to Concepts](../../README.md)
