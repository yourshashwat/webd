# Express.js Beginner Notes

## 📌 Why Express.js?

Before using Express.js, developers used the built-in `http` module in Node.js to create servers. But this approach had problems:

- You had to manually handle different **routes** (e.g., `/`, `/about`).
- You needed to manually handle different **HTTP methods** (GET, POST, etc.).
- Parsing **URLs**, **headers**, and **query parameters** required external packages like `url`.
- The server code became long, repetitive, and hard to read.

**Express.js** solves all of these issues by providing an easy-to-use interface to build web servers.

---

## ⚙️ What is Express.js?

> A fast, unopinionated, and minimalist web framework for Node.js.

It simplifies how we build and manage servers in Node. Internally, it still uses the `http` module but handles everything behind the scenes.

---

## 🧱 Setting Up Express.js

### Step 1: Install Express

```bash
npm install express
```

### Step 2: Import and Initialize

```js
const express = require('express');
const app = express();
```

### Step 3: Define Routes

```js
app.get('/', (req, res) => {
  res.send('Hello from Home Page');
});

app.get('/about', (req, res) => {
  res.send('Hello from About Page');
});
```

### Step 4: Start Server

```js
app.listen(8000, () => {
  console.log("Server running on port 8000");
});
```

---

## 🧠 Key Concepts

### ✅ Clean and Modular Code

Express removes the need for manually creating handler functions and registering routes manually.

### ✅ Built-in Routing

Express provides `.get()`, `.post()`, `.put()`, `.delete()` methods for different HTTP methods.

### ✅ Built-in Query Handling

Express allows easy access to query parameters:

```js
app.get('/about', (req, res) => {
  res.send(`Hello ${req.query.name}`);
});
// Access: /about?name=Piyush
```

### ✅ No More Need for 'url' Package

All query parsing is built-in to Express. You can remove the `url` package.

---

## 🧹 Express vs HTTP Module

| Feature      | HTTP Module           | Express.js              |
| ------------ | --------------------- | ----------------------- |
| Routing      | Manual                | Built-in                |
| HTTP Methods | Manual handling       | Clean, built-in methods |
| Query Params | Requires `url` module | Built-in parsing        |
| Readability  | Messy, boilerplate    | Clean, readable         |

---

## 🚀 Summary

- Express.js makes Node.js server development faster, cleaner, and easier.
- It handles routing, methods, and parameters internally.
- It allows you to create readable, modular server code.
- In upcoming tutorials, dynamic routes and patterns will be covered.

---

## 💡 Sample Code

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello from Home Page');
});

app.get('/about', (req, res) => {
  const name = req.query.name;
  res.send(`Hello ${name}`);
});

app.listen(8000, () => {
  console.log("Server is running on port 8000");
});
```

---

## ✅ Conclusion

Use Express.js instead of the raw `http` module because:

- It gives cleaner structure
- Handles routing and parameters out-of-the-box
- Saves time and effort

➡️ From now on, server-side code will be written using Express.js.

---

Happy coding! 🚀

