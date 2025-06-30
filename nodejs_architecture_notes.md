
### 🚀 Introduction

- Explains the **architecture of Node.js**, its **internal working**, and why **non-blocking operations** are important.

---
![image](https://github.com/user-attachments/assets/5007187d-9ed9-4d9a-a0cc-44c5f9e06aec)

### 🔄 Basic Architecture of Node.js

1. **Client** sends a request to the **server** (running Node.js).
2. Request is added to the **Event Queue**.
3. **Event Loop** watches the Event Queue continuously.
4. Requests follow **FIFO (First In First Out)** principle.

---
![image](https://github.com/user-attachments/assets/cc907567-9943-40ba-8936-5dc90cd18455)


### ⚙️ Role of Event Loop

- Constantly checks if there are pending requests.
- Picks requests **one by one** from the Event Queue.
- Checks if request is **blocking** or **non-blocking**:
  - **Non-blocking (asynchronous)**: Processes immediately and returns response.
  - **Blocking (synchronous)**: Passed to the **Thread Pool**.

---

### 🧵 Thread Pool

- A pool of **worker threads** to handle **blocking operations**.
- If a thread is available, it gets assigned to the task.
- Once the task completes, thread returns the result and becomes free.
- Default number of threads = **4**.
- Can increase based on number of CPU cores.

---

### ⚠️ Scalability Issue

- If all threads are busy, new blocking requests must wait.
- Leads to performance bottlenecks if too many **blocking operations** exist.
- Hence, always write **non-blocking code** when possible.

---

### 🧪 Code Example: Blocking vs Non-blocking

#### Blocking Code (Synchronous)

```js
const fs = require("fs");
const data = fs.readFileSync("contacts.txt", "utf-8");
console.log(data);
console.log("2");
```

- Output:
  - First file contents
  - Then "2"
- Thread is **blocked** during file read.

#### Non-blocking Code (Asynchronous)

```js
const fs = require("fs");
fs.readFile("contacts.txt", "utf-8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
console.log("2");
```

- Output:
  - First "2"
  - Then file contents
- Other code can execute while file is being read.

---

### 🖥️ Checking CPU Cores for Thread Pool

```js
const os = require("os");
console.log(os.cpus().length);
```

- Returns number of CPU cores.
- Thread pool can be increased up to this number.

---

### ✅ Key Takeaways

- Always prefer **non-blocking operations**.
- Blocking code leads to **thread starvation**.
- Node.js handles concurrency through **Event Loop** + **Thread Pool**.

---

### 🧠 Tips

- Use async methods (`fs.readFile`, DB queries, etc.).
- Avoid `sync` methods in production (e.g., `readFileSync`).
- Optimize for performance by writing **asynchronous, event-driven** code.

---

**Conclusion**

- Understanding Node.js architecture is critical for writing scalable applications.
- Focus on **non-blocking patterns** to fully utilize Node's strengths.

---

