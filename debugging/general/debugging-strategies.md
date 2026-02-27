# Debugging Strategies

##  Problem

A bug exists but you don't know where or why. You're adding `console.log` statements randomly and spending hours on something that structured debugging would solve in minutes.

##  Solution

Apply a systematic debugging process. Bugs always have a cause; systematic investigation finds it faster than random changes.

##  Example

### The Scientific Method for Debugging

```
1. Observe the bug     → "User can't log in, gets 401"
2. Reproduce it        → reliably recreate the conditions
3. Form a hypothesis   → "JWT secret might be wrong in env"
4. Test the hypothesis → check env vars, log the secret length
5. Fix or refute       → adjust, test again
6. Verify the fix      → run tests, confirm bug is gone
7. Prevent recurrence  → add a test that catches this
```

### Binary Search Debugging (Divide and Conquer)
```javascript
// Bug somewhere in a chain of operations
// Don't trace every line — bisect!

function processOrder(order) {
  const validated = validate(order);         // Step 1
  const priced    = applyPricing(validated); // Step 2
  const taxed     = applyTax(priced);        // Step 3
  const shipped   = addShipping(taxed);      // Step 4
  return shipped;
}

// Add a log in the middle
function processOrder(order) {
  const validated = validate(order);
  const priced    = applyPricing(validated);
  console.log('After pricing:', JSON.stringify(priced)); // ← bisect here
  const taxed     = applyTax(priced);
  const shipped   = addShipping(taxed);
  return shipped;
}
// If priced looks correct → bug is in step 3 or 4
// If priced looks wrong   → bug is in step 1 or 2
// Narrow down from there
```

### Rubber Duck Debugging
```
Explain the problem out loud to someone (or a rubber duck).
The act of articulating the problem often reveals the solution.

"So this function is supposed to... wait, I never call setUser() 
after the fetch completes! That's why the state is always null."
```

### Tool Chain
```bash
# Structured logging (better than random console.logs)
# Add context: what function, what data
console.log('[processOrder] Input:', JSON.stringify(order));
console.log('[applyPricing] Output:', price);

# Node.js built-in debugger
node --inspect-brk app.js
# Then open Chrome → chrome://inspect

# VS Code debugging (launch.json)
{
  "type": "node",
  "request": "launch",
  "name": "Debug App",
  "program": "${workspaceFolder}/app.js",
  "console": "integratedTerminal"
}
# Set breakpoints, step through code interactively
```

##  Explanation

### Common Debugging Mistakes
1. **Random changes** — "maybe this will fix it" without understanding why
2. **Not reproducing first** — fixing something that might not be the issue
3. **Changing too many things at once** — makes it hard to know what worked
4. **Not checking assumptions** — "I know X is true" (verify it anyway)

##  Further Reading

- [Reading Stack Traces](reading-stack-traces.md)
- [Using Debuggers](using-debuggers.md)

---

[← Back to General Debugging](README.md)
