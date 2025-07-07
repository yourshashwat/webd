
# HTTP Status Codes Explained with Express.js

This markdown file summarizes key concepts from the Node.js video tutorial on HTTP status codes.

---

## 🔢 Categories of HTTP Status Codes

![image](https://github.com/user-attachments/assets/eadb62bf-ac75-49ec-bdbd-704acfaed0e2)

HTTP status codes are 3-digit numbers categorized by their first digit:

| Category | Range     | Description                       |
|----------|-----------|-----------------------------------|
| 1xx      | 100–199   | Informational responses            |
| 2xx      | 200–299   | Successful responses               |
| 3xx      | 300–399   | Redirection messages               |
| 4xx      | 400–499   | Client error responses             |
| 5xx      | 500–599   | Server error responses             |

---

## ✅ Successful Status Codes (2xx)

| Code | Meaning          | Use Case Example                        |
|------|------------------|-----------------------------------------|
| 200  | OK               | Default success response                |
| 201  | Created          | After successful POST that creates data|
| 202  | Accepted         | Request accepted, but not yet processed|
| 204  | No Content       | Success but no content to return       |

---

## ⚠️ Client Error Codes (4xx)

| Code | Meaning               | Description |
|------|-----------------------|-------------|
| 400  | Bad Request           | Invalid/missing input from client |
| 401  | Unauthorized          | Client not authenticated |
| 403  | Forbidden             | Authenticated but not authorized |
| 404  | Not Found             | Requested resource not found |
| 405  | Method Not Allowed    | HTTP method not supported by route |

Example:
```js
if (!body.first_name || !body.email || !body.last_name) {
  return res.status(400).json({ message: "All fields are required" });
}
```

---

## 💥 Server Error Codes (5xx)

| Code | Meaning                 | Description |
|------|-------------------------|-------------|
| 500  | Internal Server Error   | Server crashed or misconfigured |
| 501  | Not Implemented         | Route/method not yet implemented |
| 503  | Service Unavailable     | Server is temporarily down or overloaded |

---

## 🔁 Redirection Codes (3xx)

| Code | Meaning             | Example Use Case |
|------|---------------------|------------------|
| 301  | Moved Permanently   | URL redirection |
| 302  | Found (Temporary)   | Payment gateways, etc. |

---

## 🛠 Express Example

```js
app.post('/users', (req, res) => {
  const { first_name, last_name, email } = req.body;
  if (!first_name || !last_name || !email) {
    return res.status(400).json({ message: "All fields are required" });
  }
  // Create user logic here...
  return res.status(201).json({ message: "User created" });
});
```

---

## 🔁 Development Tip

Use **nodemon** to avoid restarting server manually after every code change:

```bash
npm install -g nodemon
nodemon index.js
```

---

## 🎯 Summary

- Use `res.status(code).json({...})` to set appropriate HTTP status codes.
- 2xx → Success, 4xx → Client Error, 5xx → Server Error.
- Proper use of status codes improves API clarity and client-side debugging.

---

✍️ Based on a Hindi Node.js Express tutorial from YouTube. Happy coding! 🚀
