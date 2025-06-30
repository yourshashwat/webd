**Detailed Notes from the Video on Creating a Basic HTTP Server in Node.js**

---

### 🌐 Introduction

- This is the beginning of a video series.
- In this video, a basic HTTP web server will be created using **Node.js**.
- It's a beginner-level tutorial with fundamental concepts for anyone new to backend development.

---

### 🔨 Project Setup

1. Create an empty folder and name it (e.g., `server`).
2. Open the folder in a code editor (e.g., VS Code).
3. Open the terminal inside the folder.
4. Run the command:
   ```bash
   npm init
   ```
   - Accept all defaults by pressing `Enter` or typing `yes`.
   - This generates a `package.json` file.
5. Create a new file named:
   ```bash
   index.js
   ```
   - This will be the **entry point** of the server.
   - Naming the main file `index.js` is a best practice.

---

### 🔄 Importing Core HTTP Module

```js
const http = require('http');
```

- The `http` module is built-in to Node.js and does not need to be installed.

---

### ⚖️ Creating the Server

```js
const server = http.createServer((req, res) => {
  console.log("New request received");
  res.end("Hello from Server");
});
```

- `http.createServer()` creates a server object.
- Takes a callback with two parameters:
  - `req`: contains the request details.
  - `res`: used to send response back to the client.
- `res.end()` sends the final response.

---

### ⛔ Listening on a Port

```js
server.listen(8000, () => {
  console.log("Server started on port 8000");
});
```

- The server listens on **port 8000**.
- You can open `http://localhost:8000` in the browser to interact with the server.

---

### 📃 Logging Requests

```js
console.log("New request received");
```

- Every time a user hits the server, this message is logged.

---

### ⌚ Logging Timestamps

```js
const fs = require('fs');
fs.appendFile("log.txt", `${new Date().toISOString()} - New Request\n`, () => {});
```

- Every request is logged into a file `log.txt`.
- Used `appendFile` instead of `appendFileSync` to avoid blocking the event loop.

---

### 📊 Request Object

- The `req` object contains:
  - URL path: `req.url`
  - Headers: `req.headers`
  - HTTP version, method, etc.

Example:
```js
console.log(req.url);
console.log(req.headers);
```

---

### 🔄 Sending Different Responses Based on URL

```js
switch(req.url) {
  case "/":
    res.end("This is Home Page");
    break;
  case "/about":
    res.end("I am Piyush Garg");
    break;
  default:
    res.end("404 Not Found");
}
```

- A simple routing mechanism based on `req.url`.

---

### 🧩 URL Structure Explained

**URL (Uniform Resource Locator)** is made of several parts:

1. **Protocol**: `http`, `https`, or others like `ws` (WebSocket)
2. **Domain**: Human-readable name (e.g., `google.com`)
3. **Path**: Specific route after the domain (e.g., `/about`, `/contact`)
4. **Query Parameters**: Extra data after `?` (e.g., `?user=john&id=3`)

You can extract components using:
```js
const url = require('url');
const myUrl = url.parse(req.url, true);
```

- `myUrl.pathname` gives the path
- `myUrl.query` gives the key-value pairs in the query string

---

### 📌 Nested Paths

You can use nested routes like:
- `/projects/1`
- `/projects/2`
- `/blog/post-5`

This allows more structured routing.

---

### 🧮 Parsing Query Parameters

Example:
```
/about?user=piyush&id=2
```

Use the `url` module to extract query params:
```js
const url = require('url');
const parsedUrl = url.parse(req.url, true);
const query = parsedUrl.query;
console.log(query.user); // 'piyush'
```

---

### 🧠 Example Application Logic Using Query Params

You can personalize responses:
```js
if (parsedUrl.pathname === '/about') {
  res.end(`Hey ${parsedUrl.query.user}`);
}
```

---

### 📦 Installing External URL Parsing Package

Install if needed:
```bash
npm install url
```

But usually the `url` module is built into Node.js.

---

### 💻 Full Server Code

```js
const http = require('http');
const fs = require('fs');
const url = require('url');

const server = http.createServer((req, res) => {
  const myUrl = url.parse(req.url, true);
  const pathname = myUrl.pathname;
  const query = myUrl.query;

  fs.appendFile("log.txt", `${new Date().toISOString()} - ${req.url}\n`, () => {});

  if (pathname === "/") {
    res.end("This is Home Page");
  } else if (pathname === "/about") {
    res.end(`Hey ${query.user || "there"}`);
  } else {
    res.end("404 Not Found");
  }
});

server.listen(8000, () => {
  console.log("Server started on port 8000");
});
```

---

### ✨ Summary

- Created a simple HTTP server in Node.js.
- Used core module `http` to handle requests and responses.
- Implemented routing with `switch-case` and `pathname`.
- Parsed query parameters using `url` module.
- Logged all requests with timestamps.
- Introduced real-world use cases like URL parsing and nested routing.

---

**End of Notes**

