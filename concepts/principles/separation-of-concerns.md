# Separation of Concerns

##  Definition

**Separation of Concerns (SoC)** is a design principle for separating a program into distinct sections, where each section addresses a separate **concern** — a set of related responsibilities or information. A concern is any aspect of a program's functionality.

##  Why It Matters

SoC enables:
- **Independent development** — teams work on different concerns simultaneously
- **Independent testing** — test business logic without UI
- **Replaceability** — swap database without changing business rules
- **Comprehensibility** — understand one part without knowing everything

##  Examples

### MVC as Separation of Concerns
```
Model       → Data and business rules
View        → Presentation / UI
Controller  → Connects model and view, handles user input
```

### Layered Architecture (Node.js/Express)
```javascript
// ❌ Mixed concerns: routes, business logic, DB all tangled
app.post('/register', async (req, res) => {
  const { email, password } = req.body;
  if (!email.includes('@')) return res.status(400).json({ error: 'Bad email' });
  const hash = await bcrypt.hash(password, 10);
  const user = await db.query('INSERT INTO users(email,password) VALUES($1,$2)',
    [email, hash]);
  const token = jwt.sign({ id: user.id }, process.env.SECRET);
  res.json({ token });
});

//  Separated concerns:

// routes/auth.js — HTTP concern
router.post('/register', authController.register);

// controllers/authController.js — Orchestration concern
async function register(req, res) {
  try {
    const user = await authService.register(req.body);
    res.status(201).json({ success: true, userId: user.id });
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
}

// services/authService.js — Business logic concern
async function register({ email, password }) {
  validateEmail(email);
  validatePassword(password);
  const existing = await userRepository.findByEmail(email);
  if (existing) throw new Error('Email already registered');
  const hash = await bcrypt.hash(password, 10);
  return userRepository.create({ email, passwordHash: hash });
}

// repositories/userRepository.js — Data access concern
async function create(data) {
  return db.query('INSERT INTO users(email,password_hash) VALUES($1,$2) RETURNING *',
    [data.email, data.passwordHash]);
}
```

### CSS: Separation of Content and Presentation
```html
<!-- ❌ Mixed: HTML + styles + behavior -->
<p style="color:red;font-size:18px;" onclick="alert('clicked')">
  Important message
</p>

<!--  Separated concerns -->
<!-- HTML: structure/content -->
<p class="alert-message" id="importantMsg">Important message</p>

<!-- CSS: presentation -->
<style>
.alert-message { color: red; font-size: 18px; }
</style>

<!-- JS: behavior -->
<script>
document.getElementById('importantMsg').addEventListener('click', () => alert('clicked'));
</script>
```

##  Common Misconceptions

1. **"SoC means one file per concern"** — SoC is about logical separation; physical file organization is just one approach.
2. **"SoC always means more files and layers"** — For small scripts, one file is perfectly appropriate. Apply SoC proportional to system complexity.

##  Further Reading

- [MVC Architecture](../architecture/mvc-architecture.md)
- [SOLID Principles](solid-principles.md)

---

[← Back to Principles](../README.md) | [← Back to Concepts](../../README.md)
