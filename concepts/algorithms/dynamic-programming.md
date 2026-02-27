# Dynamic Programming

##  Definition

**Dynamic Programming (DP)** is an optimization technique that solves complex problems by breaking them into overlapping subproblems, solving each subproblem only once, and storing results for reuse. It's applicable when a problem has:
1. **Optimal substructure** — optimal solution contains optimal solutions to subproblems
2. **Overlapping subproblems** — same subproblems are solved multiple times

##  Why It Matters

DP turns exponential algorithms into polynomial ones:
- Fibonacci: O(2^n) → O(n)
- Shortest path: naive O(n!) → Dijkstra O(E log V)
- Sequence alignment in bioinformatics
- Resource allocation and scheduling

##  Two Approaches

### Top-Down: Memoization (Recursion + Cache)
```
fib(5) → fib(4) + fib(3)
          ↓         ↓
        fib(3)+fib(2)  fib(2)+fib(1)
          ↓
       [Cache hit! fib(2) already computed]
```

### Bottom-Up: Tabulation (Iterative)
```
dp[0] = 0
dp[1] = 1
dp[2] = dp[1] + dp[0] = 1
dp[3] = dp[2] + dp[1] = 2
dp[4] = dp[3] + dp[2] = 3
dp[5] = dp[4] + dp[3] = 5
```

##  Examples

### Example 1: Fibonacci (JavaScript)
```javascript
// Memoization (top-down)
function fibMemo(n, memo = new Map()) {
  if (n <= 1) return n;
  if (memo.has(n)) return memo.get(n);
  const result = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
  memo.set(n, result);
  return result;
}

// Tabulation (bottom-up, O(n) time, O(1) space)
function fibTab(n) {
  if (n <= 1) return n;
  let prev = 0, curr = 1;
  for (let i = 2; i <= n; i++) {
    [prev, curr] = [curr, prev + curr];
  }
  return curr;
}

console.log(fibTab(50)); // 12586269025 (milliseconds!)
```

### Example 2: 0/1 Knapsack (Python)
```python
def knapsack(weights, values, capacity):
    """
    Given items with weights and values and a capacity,
    find the maximum value that fits in the knapsack.
    """
    n = len(weights)
    # dp[i][w] = max value using first i items with capacity w
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            # Don't take item i
            dp[i][w] = dp[i-1][w]
            # Take item i if it fits
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i][w],
                               dp[i-1][w - weights[i-1]] + values[i-1])

    return dp[n][capacity]

weights = [2, 3, 4, 5]
values  = [3, 4, 5, 6]
capacity = 8
print(knapsack(weights, values, capacity))  # 10
```

### Example 3: Longest Common Subsequence (JavaScript)
```javascript
function lcs(s1, s2) {
  const m = s1.length, n = s2.length;
  const dp = Array.from({ length: m + 1 }, () => Array(n + 1).fill(0));

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (s1[i-1] === s2[j-1]) dp[i][j] = dp[i-1][j-1] + 1;
      else dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
    }
  }
  return dp[m][n];
}

console.log(lcs('ABCBDAB', 'BDCAB')); // 4 (BCAB or BDAB)
```

##  Common Misconceptions

1. **"DP is just recursion with memoization"** — Memoization is one implementation. Tabulation (bottom-up) is equally valid and often more space-efficient.
2. **"DP always requires a 2D table"** — Many DP problems (Fibonacci, climbing stairs) only need O(1) or O(n) space.
3. **"Greedy algorithms are a subset of DP"** — Greedy makes locally optimal choices; DP explores all subproblems. They're distinct techniques.

##  Further Reading

- [Recursion](recursion.md)
- [Big-O Notation](big-o-notation.md)

---

[← Back to Algorithms](../README.md) | [← Back to Concepts](../../README.md)
