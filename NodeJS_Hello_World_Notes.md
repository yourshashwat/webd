# 🚀 Getting Started with Node.js – "Hello World" + Core Concepts

## 🎬 1. Introduction to the Video
This is your **first hands-on experience** writing Node.js code.
The goal is to build a simple "Hello World" project and understand how Node.js differs from browser-based JavaScript.

---

## 🗂️ 2. Project Setup: Folder & File

### 🧾 Step-by-step:
1. **Create a new folder**, e.g. `nodejs-practice/`.
2. Inside it, create a subfolder for the first project, e.g. `01-hello-world/`.
3. Open the project folder in a code editor like **VS Code**.
4. Create a new file: `hello.js`.

---

## 🖥️ 3. Writing & Running Your First Node.js Code

### ✍️ Code:
```js
console.log("Hey there!");
```

### ▶️ Run it:
Open the **integrated terminal** in VS Code and type:
```bash
node hello.js
```
You should see:
```
Hey there!
```

---

## 🧠 4. Node.js ≠ Browser JavaScript

### 🧪 Example:
```js
console.log(window);
```
Output:
```
ReferenceError: window is not defined
```

### 🔍 Why?
- In **browsers**, you get global objects like `window`, `document`, `alert`, etc.
- In **Node.js**, those don’t exist.

| Feature | Browser JS | Node.js |
|--------|-------------|---------|
| `window` | ✅ Available | ❌ Not available |
| `alert()` | ✅ Works | ❌ Error |
| `console.log()` | ✅ | ✅ |
| `document.getElementById` | ✅ | ❌ |
| File system (`fs`) | ❌ | ✅ |

---

## 📦 5. The Role of npm and `package.json`

### 🔧 What is npm?
- **npm = Node Package Manager**  
Used to manage dependencies, scripts, versioning, etc.

### 🔄 Initialize a Node project:
Run:
```bash
npm init
```
You'll be prompted for package name, version, entry point, etc.

### 📁 This creates: `package.json`
A **config file** for your Node.js project.

#### Example:
```json
{
  "name": "hello-world",
  "version": "1.0.0",
  "main": "hello.js",
  "scripts": {
    "start": "node hello.js"
  }
}
```

---

## 🏃‍♂️ 6. Custom Scripts in `package.json`

Instead of running `node hello.js`, just run:
```bash
npm start
```

### ✅ Why use scripts?
You can predefine startup processes like DB connections or pre-run cleanups.

---

## 📘 7. Why Node.js is Server-Side

Node.js does not support UI-related features like HTML/CSS rendering.
It is optimized for:
- File handling
- Cryptography
- API handling
- Server logic

### 🔐 Bonus Modules in Node.js:
- `fs` (File System)
- `http` (Server)
- `crypto` (Encryption/Hashing)

---

## ✅ 8. Summary Cheat Sheet

| Concept | Purpose |
|--------|---------|
| `node filename.js` | Run JS file in terminal |
| `console.log()` | Print to console |
| `npm init` | Create `package.json` |
| `npm start` | Run the `"start"` script |
| `package.json` | Config file for scripts, dependencies |
| Node.js | Server-side JS runtime using V8 |
| Browser JS | Client-side JS with DOM APIs |

---

## 💡 Extra Wisdom Nuggets

- Always use clear folder names for tracking your projects.
- Think of Node.js as **backend JS**, not a JS replacement.
- `package.json` is the **heart of any Node.js project**.
- Skip prompts by using:
```bash
npm init -y
```

---

## 📌 What's Missing in Node (but exists in browsers)?

| Browser Feature | In Node.js |
|----------------|------------|
| `document`, `alert()` | ❌ Not available |
| DOM manipulation | ❌ |
| CSS/HTML rendering | ❌ |
| File System, Crypto, HTTP | ✅ ✅ ✅ |

---

## 📘 Suggested Next Topics

- Built-in modules: `fs`, `path`, `http`
- Installing packages: `express`, `nodemon`
- Understanding event loop & async behavior