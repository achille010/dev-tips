# Error: IndentationError

##  The Error

```
IndentationError: unexpected indent
IndentationError: expected an indented block
TabError: inconsistent use of tabs and spaces in indentation
```

##  Common Causes

1. **Mixed tabs and spaces** — most common cause of `TabError`
2. **Wrong indentation level** — indented too much or too little
3. **Missing block body** — empty `if/for/while` block without `pass`
4. **Copy-paste with different indentation**

##  Quick Fix

```bash
# Convert all tabs to spaces (4 spaces per tab)
expandtabs file.py > fixed.py

# Check for mixed tabs/spaces
python -m py_compile file.py

# Or use autopep8 to auto-fix
pip install autopep8
autopep8 --in-place file.py
```

##  Detailed Solution

### Solution 1: Use Spaces (Not Tabs) Consistently
```python
# ❌ Mixed tabs and spaces (TabError)
def greet(name):
	print("Hello")      # ← tab
    print(name)         # ← spaces

#  All spaces (4 per level is PEP 8 standard)
def greet(name):
    print("Hello")
    print(name)
```

### Solution 2: Empty Blocks Need `pass`
```python
# ❌ Syntax error — block can't be empty
def future_feature():

for item in items:

#  Use pass as placeholder
def future_feature():
    pass

for item in items:
    pass
```

### Solution 3: Configure Your Editor
```
VSCode settings (settings.json):
"editor.tabSize": 4,
"editor.insertSpaces": true,
"editor.detectIndentation": false,
"[python]": {
    "editor.tabSize": 4,
    "editor.insertSpaces": true
}
```

##  Prevention

- Configure your editor to use spaces for Python
- Use a linter: `flake8` or `pylint`
- Format with `black`: `pip install black && black file.py`

---

[← Back to Python Debugging](README.md)
