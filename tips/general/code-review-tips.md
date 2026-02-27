# Code Review Tips

##  Problem

Code reviews are either rubber stamps ("LGTM") that miss real issues, or brutal critiques that demoralize contributors. Neither makes the codebase better.

##  Solution

Approach code reviews with curiosity and empathy. Focus on the code, not the person. Use a structured review process.

##  Example

### What to Look For (Reviewer Checklist)

**Correctness**
```
□ Does the code do what the PR description says?
□ Are edge cases handled? (empty inputs, nulls, large values)
□ Are errors handled appropriately?
□ Are there race conditions in async code?
```

**Design**
```
□ Is the change in the right place?
□ Are responsibilities clearly separated?
□ Is the change the simplest that could work?
□ Does it introduce technical debt?
```

**Readability**
```
□ Are names descriptive?
□ Is complex logic commented/documented?
□ Could you understand this cold in 6 months?
```

**Tests**
```
□ Are tests included for new behavior?
□ Do tests test behavior, not implementation?
□ Are edge cases tested?
```

### Giving Feedback Constructively
```markdown
❌ "This is wrong."
✅ "This won't work when the array is empty — consider adding a guard at line 12."

❌ "Why did you do it this way?"
✅ "I'm curious about the choice to use a Map here — would a plain object work too? 
   I don't have a strong preference, just want to understand the reasoning."

❌ "This function is too long."
✅ "This function handles 4 different responsibilities. Would it be reasonable to 
   split out the validation into a separate `validateInput` function? It would 
   make each part easier to test."

# Classify your comments:
# [blocking] — must fix before merge
# [suggestion] — consider this
# [nit] — minor style thing, your call
# [question] — I'm just curious
```

### As the Author (Receiving Reviews)
```markdown
✅ Respond to all comments (even just "done" or "good point, fixed")
✅ Don't take feedback personally — it's about the code
✅ Explain your reasoning if you disagree
✅ Say "good catch!" when reviewers find real bugs
✅ Keep PRs small — < 400 lines is a good target
✅ Write a clear PR description: What, Why, How to test
```

### PR Description Template
```markdown
## What
Brief description of the change.

## Why
Context: what problem does this solve or what feature does this add? 
Link to ticket: Closes #123

## How to Test
1. Start the server
2. Navigate to /users
3. Verify the list loads with pagination controls

## Screenshots (if UI change)
[before] | [after]

## Checklist
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No breaking changes (or documented)
```

##  Related Tips

- [Testing Tips](testing-tips.md)
- [Documentation Tips](documentation-tips.md)

---

[← Back to General Tips](README.md)
