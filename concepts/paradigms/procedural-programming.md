# Procedural Programming

##  Definition

**Procedural Programming** is a paradigm derived from structured programming, based on the concept of the **procedure call**. A program is a sequence of instructions (procedures/functions) that execute in order, operating on shared data.

It's the foundation of C, Pascal, and early BASIC, and remains relevant in scripts, systems programming, and data pipelines.

##  Why It Matters

Procedural code is:
- **Simple and direct** — easy to trace execution flow
- **Efficient** — minimal overhead, great for performance-critical code
- **Universal** — all programmers understand sequential logic
- **C/systems** — OS kernels, embedded systems use procedural style

##  Examples

### Example 1: Classic Procedural Style (C-like JavaScript)
```javascript
// Global/shared state
let playerScore = 0;
let playerLives = 3;
let gameOver    = false;

// Procedures operating on shared state
function collectCoin(value) {
  playerScore += value;
  console.log(`Score: ${playerScore}`);
}

function loseLife() {
  playerLives--;
  if (playerLives <= 0) {
    gameOver = true;
    endGame();
  }
}

function endGame() {
  console.log(`Game Over! Final score: ${playerScore}`);
}

function startGame() {
  console.log('Game started!');
  collectCoin(10);
  collectCoin(20);
  loseLife();
  loseLife();
  loseLife(); // triggers endGame()
}

startGame();
```

### Example 2: Procedural Data Processing (Python)
```python
import csv

def read_csv(filepath):
    rows = []
    with open(filepath, 'r') as f:
        reader = csv.DictReader(f)
        for row in reader:
            rows.append(row)
    return rows

def filter_by_age(data, min_age):
    result = []
    for row in data:
        if int(row['age']) >= min_age:
            result.append(row)
    return result

def calculate_avg_salary(data):
    if not data:
        return 0
    total = 0
    for row in data:
        total += float(row['salary'])
    return total / len(data)

def print_report(data, avg):
    print(f"Found {len(data)} records")
    print(f"Average salary: ${avg:.2f}")
    for row in data:
        print(f"  {row['name']}: ${row['salary']}")

# Main procedure
def main():
    data = read_csv('employees.csv')
    seniors = filter_by_age(data, 30)
    avg = calculate_avg_salary(seniors)
    print_report(seniors, avg)

main()
```

##  Common Misconceptions

1. **"Procedural means spaghetti code"** — With proper function decomposition and module organization, procedural code can be very clean and maintainable.
2. **"OOP replaced procedural programming"** — They coexist. Python and JavaScript are multi-paradigm, and most code mixes procedural and OOP style naturally.
3. **"Procedural doesn't scale"** — Linux kernel, Redis, SQLite — all written in procedural C and scale to billions of users.

##  Further Reading

- [Object-Oriented Programming](object-oriented-programming.md)
- [Functional Programming](functional-programming.md)
- [Declarative vs Imperative](declarative-vs-imperative.md)

---

[← Back to Paradigms](../README.md) | [← Back to Concepts](../../README.md)
