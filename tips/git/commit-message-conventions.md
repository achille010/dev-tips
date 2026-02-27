# Commit Message Conventions

##  Problem

Inconsistent, vague commit messages make `git log` useless. Messages like "fix stuff", "WIP", or "asdf" tell teammates (and future-you) nothing about what changed or why.

##  Solution

Follow the **Conventional Commits** specification. It provides a structured format that makes history readable, enables automated changelogs, and communicates intent clearly.

##  Example

### The Format
```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

### Types
| Type       | When to Use                            |
|------------|----------------------------------------|
| `feat`     | New feature                            |
| `fix`      | Bug fix                                |
| `docs`     | Documentation only                     |
| `style`    | Formatting (no code logic change)      |
| `refactor` | Code change (not feature, not bug fix) |
| `test`     | Adding or updating tests               |
| `chore`    | Build process, dependency updates      |
| `perf`     | Performance improvement                |
| `ci`       | CI configuration changes               |
| `revert`   | Reverts a previous commit              |

### Real Examples
```bash
# Feature
feat(auth): add JWT refresh token support

# Bug fix with body
fix(checkout): prevent double-submission on payment

Payment form was not being disabled after first submit,
causing duplicate charges in rare edge cases.

Closes #234

# Breaking change
feat(api)!: change /users endpoint to return paginated response

BREAKING_CHANGE: Response is now { data: [] , meta: { page, total } }
instead of a plain array.

# Docs
docs(contributing): add section on coding standards

# Chore
chore(deps): bump axios from 1.2.0 to 1.3.1
```

##  Explanation

### Subject Line Rules
1. **Imperative mood**: "Add feature" not "Added feature"
2. **Lowercase**: `feat` not `Feat`
3. **No period at end**: `fix: resolve bug` not `fix: resolve bug.`
4. **~72 characters max**

### Why Conventions Matter
- `git log --oneline` becomes a readable changelog
- Tools like `semantic-release` automate version bumping from commit types
- Code reviewers instantly understand scope from message structure
- `feat:` bumps minor version, `fix:` bumps patch, `!` bumps major

##  Related Tips

- [Interactive Rebase](interactive-rebase.md)
- [Undo Mistakes](undo-mistakes.md)

---

[← Back to Git Tips](README.md)
