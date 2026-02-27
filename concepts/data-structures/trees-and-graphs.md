# Trees and Graphs

## 📖 Definition

**Trees** and **graphs** are non-linear data structures that represent hierarchical and networked relationships.

- A **tree** is an acyclic, connected graph with a designated root node and parent-child relationships.
- A **graph** is a collection of nodes (vertices) connected by edges, which may contain cycles.

## 🎯 Why It Matters

These structures model real-world relationships:
- **Trees**: File systems, DOM, organization charts, decision trees, BSTs for fast search
- **Graphs**: Social networks, road maps, dependency resolution, web crawling

## 🔍 How It Works

### Tree Terminology
```
        A          ← root
       / \
      B   C        ← internal nodes
     / \   \
    D   E   F      ← leaf nodes

- Height: 2 (longest path from root to leaf)
- Depth of E: 2 (path from root to E)
- Degree of B: 2 (number of children)
```

### Binary Search Tree (BST) Property
Left subtree < Node < Right subtree

```
        8
       / \
      3   10
     / \    \
    1   6    14
       / \
      4   7
```

**BST Complexities:**
| Operation | Average | Worst (degenerate) |
|-----------|---------|---------------------|
| Search    | O(log n)| O(n)               |
| Insert    | O(log n)| O(n)               |
| Delete    | O(log n)| O(n)               |

### Graph Representations
**Adjacency List** (efficient for sparse graphs):
```
A: [B, C]
B: [A, D]
C: [A, D, E]
D: [B, C]
E: [C]
```

**Adjacency Matrix** (efficient for dense graphs):
```
  A B C D E
A[0,1,1,0,0]
B[1,0,0,1,0]
C[1,0,0,1,1]
D[0,1,1,0,0]
E[0,0,1,0,0]
```

## 💻 Examples

### Example 1: Binary Tree Traversals (JavaScript)
```javascript
class TreeNode {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

// Build tree
const root = new TreeNode(8);
root.left = new TreeNode(3);
root.right = new TreeNode(10);
root.left.left = new TreeNode(1);
root.left.right = new TreeNode(6);

// In-order traversal (Left → Root → Right) → sorted for BST
function inOrder(node) {
  if (!node) return;
  inOrder(node.left);
  console.log(node.val);
  inOrder(node.right);
}
// Output: 1, 3, 6, 8, 10

// BFS with queue
function bfs(root) {
  const queue = [root];
  while (queue.length) {
    const node = queue.shift();
    console.log(node.val);
    if (node.left)  queue.push(node.left);
    if (node.right) queue.push(node.right);
  }
}
```

### Example 2: Graph BFS/DFS (Python)
```python
from collections import deque

graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A', 'D', 'E'],
    'D': ['B', 'C'],
    'E': ['C']
}

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)
    order = []
    while queue:
        node = queue.popleft()
        order.append(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return order

def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()
    visited.add(node)
    print(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

print(bfs(graph, 'A'))  # ['A', 'B', 'C', 'D', 'E']
```

## ⚠️ Common Misconceptions

1. **"Trees are a subset of graphs"** — True! A tree is an acyclic undirected connected graph.
2. **"BSTs always give O(log n) search"** — Only for balanced trees. An unbalanced BST degrades to O(n). Use AVL or Red-Black trees for guaranteed O(log n).
3. **"DFS always finds the shortest path"** — BFS finds the shortest path in unweighted graphs. DFS does not guarantee shortest path.

## 📚 Further Reading

- [Linked Lists](linked-lists.md)
- [Sorting Algorithms](../algorithms/sorting-algorithms.md)

---

[← Back to Data Structures](../README.md) | [← Back to Concepts](../../README.md)
