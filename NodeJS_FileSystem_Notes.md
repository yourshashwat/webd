
# Node.js `fs` Module — Notes

## 📘 Introduction
- The `fs` module in Node.js allows you to interact with the file system.
- It is a **built-in module** — no need to install it.
- Loaded using:
  ```js
  const fs = require('fs');
  ```

---

## 🧾 Basic File Operations

### 1. Creating/Writing a File (Sync & Async)

```js
// Synchronous
fs.writeFileSync('./test.txt', 'Hey there!');
```
- Creates `test.txt` and writes content synchronously.
- Overwrites content if file already exists.

```js
// Asynchronous
fs.writeFile('./test.txt', 'This is async write', (err) => {
  if (err) console.error(err);
});
```
- Uses a **callback** function.
- Does not block execution.

---

### 2. Reading a File

```js
// Synchronous
const data = fs.readFileSync('./contacts.txt', 'utf-8');
console.log(data);
```

```js
// Asynchronous
fs.readFile('./contacts.txt', 'utf-8', (err, data) => {
  if (err) console.error(err);
  else console.log(data);
});
```
> 🔸 `readFileSync` returns data directly.  
> 🔸 `readFile` expects a callback.

---

### 3. Appending to a File

```js
fs.appendFileSync('./test.txt', '\nNew line');
```

```js
fs.appendFile('./test.txt', '\nAnother line', (err) => {
  if (err) console.error(err);
});
```

✅ Useful for creating logs (e.g., `log.txt` with time, IP, etc.).

---

### 4. Copying a File

```js
fs.copyFileSync('./test.txt', './test_copy.txt');
```

---

### 5. Deleting a File

```js
fs.unlinkSync('./test_copy.txt');
```

---

### 6. File Status/Metadata

```js
const stats = fs.statSync('./test.txt');
console.log(stats);
console.log('Is file:', stats.isFile());
console.log('Is directory:', stats.isDirectory());
```

---

## 📁 Directory Operations

### Creating Directories

```js
fs.mkdir('./myFolder', { recursive: true }, (err) => {
  if (err) console.error(err);
});
```

> `recursive: true` creates nested folders like `'./a/b/c'`.

---

## 🔄 Sync vs Async: Key Differences

| Feature            | Sync                      | Async                         |
|--------------------|---------------------------|-------------------------------|
| Blocking?          | Yes (halts execution)     | No (continues other tasks)    |
| Returns value?     | Yes                       | No (uses callback)            |
| Recommended for?   | Small scripts/testing     | Production apps               |

> 📌 Blocking vs Non-blocking execution is **crucial** for backend developers.  
> Learn about the **Event Loop**, **threads**, and **Node.js architecture** in the next video.

---

## 📝 Summary
- The `fs` module provides complete control over file/directory operations.
- Every method has both **sync** and **async** variants.
- Prefer **async methods** in real-world apps to avoid blocking the event loop.
- Logging, file manipulation, and monitoring are common real-world use cases.
