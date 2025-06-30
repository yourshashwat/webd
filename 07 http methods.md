# 🌐 HTTP Methods - Notes

HTTP methods are used to communicate between a **client (like a browser)** and a **server** in web development. Each method tells the server what action to perform on a resource.

---

## 📌 Common HTTP Methods

![image](https://github.com/user-attachments/assets/770abb13-54ad-437c-a901-c209123b8fe7)



### 1. **GET**
- ✅ **Used to retrieve data** from the server.
- ❌ Does **not modify** any data.
- 🔒 Safe and **idempotent** (same result if called multiple times).
- 📦 Data sent via **URL query parameters**.

**Example:**  
`GET /products` → Fetches list of all products.

---

### 2. **POST**
- 📝 **Used to send data** to the server to create a new resource.
- 🔄 Not idempotent (sending twice creates duplicates).
- 📤 Data sent in the **body** of the request.

**Example:**  
`POST /users` with body `{ "name": "Alice" }` → Creates a new user.

---

### 3. **PUT**
- 🛠️ Used to **update or replace** an existing resource.
- 🧹 Completely **replaces the resource**.
- ✅ Idempotent.

**Example:**  
`PUT /users/1` with full user data → Replaces user with ID 1.

---

### 4. **PATCH**
- 🔧 Used to **partially update** a resource.
- ✅ More efficient than PUT if only a few fields need changes.
- 🔁 Might not be idempotent depending on the use case.

**Example:**  
`PATCH /users/1` with `{ "email": "new@mail.com" }` → Only email is updated.

---

### 5. **DELETE**
- ❌ **Used to delete** a resource.
- ✅ Idempotent (deleting multiple times has the same effect).

**Example:**  
`DELETE /users/1` → Deletes user with ID 1.

---

![ChatGPT Image Jul 1, 2025, 01_59_40 AM](https://github.com/user-attachments/assets/d48b47de-1f06-4418-ab78-ab1b1a61ac3e)


## 🔍 Comparison Table

| Method  | Action           | Data Sent In | Idempotent | Safe | Typical Use Case              |
|---------|------------------|--------------|------------|------|-------------------------------|
| GET     | Retrieve         | URL          | ✅         | ✅   | Getting a product list        |
| POST    | Create           | Request Body | ❌         | ❌   | Submitting a form             |
| PUT     | Update (replace) | Request Body | ✅         | ❌   | Updating an entire user       |
| PATCH   | Update (partial) | Request Body | ⚠️ Depends | ❌   | Updating just one field       |
| DELETE  | Delete           | URL          | ✅         | ❌   | Removing a record             |

---

## 🧠 Tips to Remember
- Use **GET** only for fetching data.
- Use **POST** for creating **new** items.
- Use **PUT** for replacing, and **PATCH** for partial updates.
- Use **DELETE** when you want to remove something.
- GET requests can be bookmarked, others usually cannot.

---

## 📦 Bonus: Safe vs Idempotent

- **Safe methods**: Do **not change data** (like GET).
- **Idempotent methods**: Can be **called multiple times** without different outcomes (like PUT, DELETE).

---

