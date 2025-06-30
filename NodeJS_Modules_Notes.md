# 🧱 Node.js Modules & Modular Programming – Detailed Notes

## 📌 What This Covers:
- What are modules in Node.js?
- How to use `require()` and `module.exports`
- Custom module creation and usage
- Built-in modules in Node.js
- Modular programming best practices

---

## 📁 1. Setting the Context

You can run your Node.js project using:
```bash
npm start
```
This command will trigger whatever script is set under the `"start"` property in your `package.json` file.

If you're prompted to update npm, you can do that later using:
```bash
npm install -g npm
```

---

## 🧩 2. What Are Modules?

A **module** is just a JS file that encapsulates code — functions, variables, logic — that can be **imported into other files**.

### 🔍 Example:

**hello.js:**
```js
const math = require('./math');
console.log(math.add(2, 4));
```

**math.js:**
```js
function add(a, b) {
  return a + b;
}

module.exports = { add };
```

- `require('./math')`: Imports local module
- `module.exports = { add }`: Exposes the function

---

## ⚠️ 3. Common Mistakes

| Mistake | Why it Fails |
|--------|--------------|
| `require('math')` | Tries to find installed/built-in package, not local |
| `require('./math')` | ✅ Correct |
| Not using `module.exports` | Imported file returns `{}` (empty object) |
| Overwriting `module.exports` multiple times | Only last assignment is preserved |

---

## ✍️ 4. Multiple Exports

### ✅ Recommended:
```js
function add(a, b) { return a + b; }
function subtract(a, b) { return a - b; }

module.exports = { add, subtract };
```

**OR use `exports`:**
```js
exports.add = (a, b) => a + b;
exports.subtract = (a, b) => a - b;
```

### 🧪 Use with destructuring:
```js
const { add, subtract } = require('./math');
console.log(add(2, 4));
console.log(subtract(10, 3));
```

---

## 🧠 5. Behind the Scenes

- `require()` is **Node.js-specific** (not available in browser JavaScript)
- If you give just the package name (e.g. `fs`, `http`), Node searches built-in modules
- If you give `./filename`, Node looks in current project directory

---

## 🛠️ 6. Built-in Modules in Node.js

| Module | Purpose |
|--------|---------|
| `fs` | File system operations (read/write files) |
| `http` | Create web servers |
| `crypto` | Encrypt, hash, secure data |
| `os` | Access system info (RAM, platform, CPUs) |
| `path` | Work with file paths |

Use like:
```js
const fs = require('fs');
```

---

## 🧵 7. Default vs Named Exports

| Method | When to Use |
|--------|-------------|
| `module.exports = functionName` | Default export (single export) |
| `module.exports = { fn1, fn2 }` | Named export (multiple exports) |
| `exports.fn = function() {}` | Cleaner for multiple functions |

If you overwrite `module.exports`, other previous exports will be lost.

---

## 🧪 8. Good Practices

✅ Keep each module focused on one concern (e.g. math logic, API handling).  
✅ Use `exports` for readable multiple-function exports.  
✅ Use `module.exports` when exporting a single value or object.  
✅ Use relative paths for local modules: `./filename`.

---

## 🔚 Summary Cheat Sheet

| Feature | Purpose |
|--------|---------|
| `require()` | Import a module |
| `module.exports` | Export from a module |
| `exports.name = ...` | Named export |
| `require('fs')` | Built-in module |
| `require('./math')` | Local module |
| `npm start` | Run `start` script from `package.json` |

---

## 🎁 Bonus: Built-in Module Access

In VS Code, type `require('')` and trigger autocomplete with `Ctrl+Space` (or `Cmd+Space` on Mac) to see all built-in Node.js modules.

---

## 🎯 Coming Up Next

You'll soon use these concepts to build:
- File handlers (`fs`)
- HTTP servers (`http`)
- Encryption apps (`crypto`)

Stay tuned! 📚