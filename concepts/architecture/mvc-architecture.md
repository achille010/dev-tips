# MVC Architecture

##  Definition

**MVC (Model-View-Controller)** separates an application into three interconnected components: **Model** (data/business logic), **View** (UI/presentation), and **Controller** (input handler/orchestrator).

##  Examples

### Node.js/Express MVC
```
src/
├── models/         # Data + business rules
│   └── User.js
├── views/          # Templates (if server-side rendering)
│   └── user.ejs
├── controllers/    # Request handlers
│   └── userController.js
└── routes/         # URL → controller mapping
    └── userRoutes.js
```

```javascript
// models/User.js (Model)
class User {
  static async findById(id) { return db.users.find(u => u.id === id); }
  static async create(data) { return db.users.push({ id: Date.now(), ...data }); }
}

// controllers/userController.js (Controller)
async function getUser(req, res) {
  const user = await User.findById(req.params.id);
  if (!user) return res.status(404).render('error', { msg: 'Not found' });
  res.render('user', { user }); // passes data to View
}

// routes/userRoutes.js (Router → Controller)
router.get('/users/:id', userController.getUser);
```

##  When to Use MVC

- Web applications with server-side rendering
- REST APIs (View becomes JSON response)
- Application frameworks: Rails, Laravel, Django, ASP.NET MVC

##  Further Reading

- [REST API Design](rest-api-design.md)
- [Separation of Concerns](../principles/separation-of-concerns.md)

---

[← Back to Architecture](../README.md) | [← Back to Concepts](../../README.md)
