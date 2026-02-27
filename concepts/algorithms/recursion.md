# Recursion

## 📖 Definition

**Recursion** is a programming technique where a function calls itself to solve a smaller version of the same problem. Every recursive solution has:
1. A **base case** — the simplest version of the problem that can be solved directly
2. A **recursive case** — breaking the problem down and calling the function on the smaller version

## 🎯 Why It Matters

Recursion elegantly solves problems with self-similar or tree-like structure:
- Tree/graph traversals
- Sorting (merge sort, quick sort)
- Parsing nested data (JSON, HTML, file systems)
- Mathematical sequences (Fibonacci, factorial)
- Backtracking puzzles (sudoku, N-queens)

## 🔍 How It Works

### Call Stack Visualization

```
factorial(4)
  └── 4 * factorial(3)
        └── 3 * factorial(2)
              └── 2 * factorial(1)
                    └── 1 * factorial(0)
                          └── BASE CASE: 1
                    ← returns 1 * 1 = 1
              ← returns 2 * 1 = 2
        ← returns 3 * 2 = 6
  ← returns 4 * 6 = 24
```

### Tail Recursion
A recursive call is **tail-recursive** if the recursive call is the last operation (no pending multiplication, addition, etc.). Some languages optimize tail recursion to avoid stack overflow.

## 💻 Examples

### Example 1: Classic Recursion (JavaScript)
```javascript
// Factorial
function factorial(n) {
  if (n <= 1) return 1;          // base case
  return n * factorial(n - 1);   // recursive case
}

// Fibonacci (naive - O(2^n))
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}

// Fibonacci (memoized - O(n))
function fibMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
  return memo[n];
}

console.log(factorial(6));    // 720
console.log(fibMemo(40));     // 102334155 (fast!)
```

### Example 2: File System Traversal (Python)
```python
import os

def list_files(directory, indent=0):
    """Recursively list all files in a directory."""
    for item in os.listdir(directory):
        path = os.path.join(directory, item)
        print('  ' * indent + item)
        if os.path.isdir(path):
            list_files(path, indent + 1)  # recurse into subdirectory

list_files('.')
```

### Example 3: Backtracking — N-Queens (Python)
```python
def solve_n_queens(n):
    solutions = []

    def backtrack(row, cols, diag1, diag2, board):
        if row == n:
            solutions.append([''.join(r) for r in board])
            return
        for col in range(n):
            if col in cols or (row - col) in diag1 or (row + col) in diag2:
                continue
            board[row][col] = 'Q'
            backtrack(row + 1,
                      cols | {col},
                      diag1 | {row - col},
                      diag2 | {row + col},
                      board)
            board[row][col] = '.'

    board = [['.' for _ in range(n)] for _ in range(n)]
    backtrack(0, set(), set(), set(), board)
    return solutions

print(f"4-Queens has {len(solve_n_queens(4))} solutions")  # 2
```

## ⚠️ Common Misconceptions

1. **"Recursion is always slower than iteration"** — With memoization (dynamic programming), recursive solutions can match or beat iterative ones. Tail-call optimization makes them equivalent in supporting languages.
2. **"You'll always hit stack overflow"** — For reasonable input sizes and proper base cases, recursion is safe. Most call stacks support thousands of frames.
3. **"All recursive problems need multiple recursive calls"** — Linear recursion (one call per step) is the simplest form and very common.

## 📚 Further Reading

- [Dynamic Programming](dynamic-programming.md)
- [Trees and Graphs](../data-structures/trees-and-graphs.md)
- [Stacks and Queues](../data-structures/stacks-and-queues.md)

---

[← Back to Algorithms](../README.md) | [← Back to Concepts](../../README.md)
