

### 🚀 Introduction to Middleware in Express.js

* Middleware is one of the **core building blocks** of Express.js.
* It sits between the **incoming client request** and the **final route handler**.
* You can perform processing on the request before it reaches the final route.

---

### 🧠 What is Middleware?

Middleware is a **function** in Express that has access to:

```js
(req, res, next)
```

* `req` — Incoming request object
* `res` — Response object
* `next` — Function to pass control to the **next middleware** in the chain

It can:

* Execute **any code**
* Modify the `req` and `res` objects
* **End** the request-response cycle
* **Call `next()`** to pass control to the next middleware

---

### 🔁 Request Flow with Middleware

```
Client --> Middleware 1 --> Middleware 2 --> Route Handler --> Response
           (can modify or end here)
```

![image](https://github.com/user-attachments/assets/289bb3d0-3b0e-4d9e-a95c-d9d76b6cf6a8)


* Middlewares run **sequentially**.
* If any middleware doesn't call `next()` or `res.end()`, the request hangs.
* You can create **custom** or use **third-party** middleware.

---

### 🧪 Example: Custom Middleware

```js
const express = require('express');
const app = express();

// Middleware 1
app.use((req, res, next) => {
  console.log("Hello from Middleware 1");
  req.myUserName = "Piyush Garg"; // modifying request
  next();
});

// Middleware 2
app.use((req, res, next) => {
  console.log("Hello from Middleware 2");
  console.log("User from Middleware 1:", req.myUserName);
  next();
});

// Route Handler
app.get('/users', (req, res) => {
  console.log("In Route Handler");
  res.send(`Welcome, ${req.myUserName}`);
});

app.listen(8000, () => console.log("Server running on port 8000"));
```

![image](https://github.com/user-attachments/assets/3584f89f-081a-4bd8-b6c6-bd65eb6c0b5d)

---

### 📝 Common Use Cases of Middleware

* Parsing request bodies (e.g. `express.urlencoded()`)
* Validating user inputs
* Checking authentication/authorization
* Logging and monitoring
* Setting custom headers
* Serving static files

---

### 📦 Built-in & Third-party Middleware Examples

* `express.json()` — parse JSON body
* `express.urlencoded()` — parse form data
* `morgan` — logging requests
* `cors` — enable CORS
* `helmet` — enhance API security

---

### 📄 Logging with Middleware (Practical Example)

```js
const fs = require('fs');
app.use((req, res, next) => {
  const log = `${new Date().toISOString()} - ${req.method} - ${req.url}\n`;
  fs.appendFile("log.txt", log, (err) => {
    if (err) console.log(err);
  });
  next();
});
```

* Creates or appends a `log.txt` file
* Logs every request method and path

---

### 🧠 Tips

* Middleware makes your code **modular and reusable**.
* Always call `next()` unless you’re ending the cycle.
* Middlewares can be stacked to handle complex logic step-by-step.

---

### ✅ Summary

* Middleware is a function with `req`, `res`, and `next`.
* Can **modify**, **terminate**, or **forward** the request.
* Use it to add logic between request and final route handler.
* Supports built-in, third-party, and custom middleware.

---

**Next Up:** Explore **built-in and third-party middleware** like `cors`, `helmet`, `morgan` etc.
