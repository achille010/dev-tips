# Error: Merge Conflicts

##  The Error

```
CONFLICT (content): Merge conflict in src/app.js
Automatic merge failed; fix conflicts and then commit the result.
```

##  Common Causes

1. **Two branches modified the same line** — most common
2. **File renamed on one branch, modified on another**
3. **File deleted on one branch, modified on another**

##  Quick Fix

Conflicts are **not emergencies** — they're git asking for your decision. Open the conflicting file, choose the correct code, then complete the merge.

##  Detailed Solution

### Step 1: Understand the Conflict Markers
```
const API_URL = 'http://localhost:3000';
```

The conflict is between **HEAD** (your current branch) and the **incoming branch**.

### Step 2: Resolve the Conflict
```bash
# Option A: Keep YOUR version
git checkout --ours   src/app.js

# Option B: Keep THEIR version  
git checkout --theirs src/app.js

# Option C: Manually edit the file
# Remove conflict markers, keep the code you want:
const API_URL = process.env.API_URL || 'http://localhost:3000';
```

### Step 3: Complete the Merge
```bash
# After resolving all conflicts:
git add src/app.js
git merge --continue
# or just:
git commit  # git generates a merge commit message
```

### Using VS Code for Conflicts
VS Code shows a visual diff with buttons:
- **Accept Current Change** — keep your version
- **Accept Incoming Change** — keep their version
- **Accept Both Changes** — keep both
- **Compare Changes** — side-by-side view

### Aborting a Merge
```bash
git merge --abort  # cancel the entire merge, restore to pre-merge state
```

##  Prevention

- **Pull frequently** — small conflicts are easier than large ones
- **Keep branches short-lived** — the longer a feature branch lives, the more divergence
- **Communicate** — let teammates know if you're refactoring shared files

---

[← Back to Git Debugging](README.md)
