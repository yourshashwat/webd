# What is a URL and its Major Components

This tutorial focuses on understanding what a URL (Uniform Resource Locator) is and its various key components. Understanding how URLs work is very important for web server developers.

---

## 1. Definition of a URL


* **Full form of URL:** Uniform Resource Locator.
* **Function:** It specifies the address of a resource on the web (such as a webpage, image, video). It is a user-friendly name that points to a server's IP address.

---

## 2. Key Components of a URL

![image](https://github.com/user-attachments/assets/8805b486-eed6-434d-aa5c-51f126b928b8)


A typical URL like `https://www.example.com/path/to/page?query=value#section` can be broken down into the following components:

### a. Protocol

* **Examples:** `http://`, `https://`, `ws://`
* **Definition:** It is a set of rules that dictates how the browser should communicate with the server.
* **Types:**
    * **HTTP (Hypertext Transfer Protocol):** The original protocol used for transferring data on the web. It is not secure.
    * **HTTPS (Hypertext Transfer Protocol Secure):** The secure version of HTTP. It encrypts all communication between the client and server using an SSL/TLS certificate. It is the most widely used on the web.
    * **WS (WebSocket Protocol):** Used for real-time communication, such as chat applications or live updates.

### b. Domain / Host

* **Examples:** `www.example.com`, `google.com`, `youtube.com`
* **Definition:** This is a user-friendly name for the server's IP address. The DNS (Domain Name System) translates this domain name into its corresponding IP address.
* **Importance:** IP addresses (like `172.217.160.142`) are difficult to remember, so domain names are used.

### c. Port (Often Hidden)

* **Example:** `8000` in `http://localhost:8000`
* **Definition:** It is a number that indicates a specific application or service running on the server.
* **Default Ports:** The default port for HTTP is `80` and for HTTPS is `443`, so they are usually not specified in the URL. If another port is used, it is specified after the domain with a colon (`:`).

### d. Path

* **Examples:** `/`, `/about`, `/contact`, `/projects/tic-tac-toe`
* **Definition:** This is the specific location or file path of the resource on the server.
* **Types:**
    * **Root Path (`/`):** The home page or main entry point of the website.
    * **Nested Paths (`/projects/tic-tac-toe`):** Paths with hierarchical structures, pointing to a specific sub-section or resource.
* **Server Handling:** The server reads this path using `req.url` or `req.path` and responds accordingly.

### e. Query Parameters

* **Examples:** `?user_id=1&name=Piyush`, `?search_query=javascript+tutorial`
* **Definition:** These are additional pieces of information sent to the server via the URL. They are used to filter, sort data, or provide specific information.
* **Structure:**
    * `?` (Question Mark): Indicates the beginning of the query parameters.
    * `key=value`: Each parameter is a key-value pair.
    * `&` (Ampersand): Separates multiple key-value pairs.
* **Example Usage:**
    * Google Search: `https://www.google.com/search?q=javascript+interview+questions`
        * `q` (query) is a key, and `javascript+interview+questions` is its value.
    * YouTube Search: `https://www.youtube.com/results?search_query=javascript`
        * `search_query` is a key, and `javascript` is its value.
* **Parsing in Node.js:** Node.js's built-in `http` module does not directly parse query parameters. For this, an external package like `url` is used, which parses the URL into an object containing a property called `query`.

### f. Fragment / Anchor (Client-Side)

* **Example:** `#section-name`
* **Definition:** This is the part of the URL that points to a specific section or anchor within a webpage.
* **Function:** It instructs the browser to scroll to that specific part of the page.
* **Server Impact:** This part is not sent to the server; it is handled only by the browser.

---

## 3. Handling URLs in Node.js

In the Node.js server created in the previous video, we handled the path using `req.url`. However, `req.url` provides the entire URL string, which may include query parameters.

### a. Using the `url` Package

To parse query parameters separately, you can use the `url` package.

1.  **Install the `url` package:**
    ```bash
    npm install url
    ```
    This will add `url` to your `dependencies` in `package.json` and create a `node_modules` folder containing the package's code. If `node_modules` is accidentally deleted, running `npm install` again will reinstall all dependencies listed in `package.json`.

2.  **Require and parse the URL:**
    ```javascript
    const http = require('http');
    const fs = require('fs');
    const url = require('url'); // Require the url module

    const myServer = http.createServer((req, res) => {
      // Parse the URL
      const myURL = url.parse(req.url, true); // `true` parses query string into an object

      const log = `${Date.now()}: New Request Received on ${myURL.pathname}\n`; // Use pathname for logging

      fs.appendFile('log.txt', log, (err) => {
        if (err) {
          console.error("Error writing to log file:", err);
        }

        // Ignore favicon requests for logging and handling
        if (req.url === '/favicon.ico') return res.end();

        switch (myURL.pathname) { // Use myURL.pathname for routing
          case '/':
            res.end("Hello, this is the Home Page!");
            break;
          case '/about':
            res.end("Hi, I am Piyush Garg!");
            break;
          case '/contact':
            // Access query parameters from myURL.query
            const userName = myURL.query.name || "Guest"; // Get 'name' query param, default to 'Guest'
            const userId = myURL.query.id || "N/A"; // Get 'id' query param
            res.end(`Contact us at example@example.com. Hello ${userName}, your ID is ${userId}`);
            break;
          case '/search':
            const searchQuery = myURL.query.q; // For Google-like search
            res.end(`Searching for: ${searchQuery}`);
            break;
          case '/youtube-search':
            const youtubeQuery = myURL.query.search_query; // For YouTube-like search
            res.end(`YouTube search for: ${youtubeQuery}`);
            break;
          default:
            res.end("404 Not Found");
            break;
        }
      });
    });

    myServer.listen(8000, () => console.log("Server Started!"));
    ```
* **`url.parse(req.url, true)`:** This function parses the URL string. The `true` argument ensures that the query string is also parsed into an object, making it easy to access individual query parameters.
    * `myURL.pathname`: Gives only the path part of the URL (e.g., `/about`, `/`).
    * `myURL.query`: Gives an object containing the parsed query parameters (e.g., `{ name: 'Piyush', id: '1' }`).
* **Handling `favicon.ico`:** Browsers automatically request `favicon.ico`. It's good practice to handle this separately to avoid unnecessary logging or routing.

### b. Practical Application (Google/YouTube Search Example)

* **Google Search URL:** `https://www.google.com/search?q=javascript+interview+questions`
    * Here, `pathname` is `/search` and `query` is `{ q: 'javascript interview questions' }`.
* **YouTube Search URL:** `https://www.youtube.com/results?search_query=javascript`
    * Here, `pathname` is `/results` and `query` is `{ search_query: 'javascript' }`.

By parsing the URL, a server can:
1.  Identify the requested resource (`pathname`).
2.  Extract additional data provided by the client (`query parameters`).
3.  Use this information to interact with a database, fetch data, or generate a dynamic response.

---

## Conclusion

This video provided a comprehensive overview of URLs and their components. Understanding these elements is crucial for building robust web applications. We learned about:
* The definition of a URL and its purpose.
* The key components: Protocol, Domain/Host, Port, Path, Query Parameters, and Fragments.
* How to handle different URL paths and extract query parameters in a Node.js server using the `url` module.
* The importance of using non-blocking operations for efficient server performance.

This foundational knowledge is essential before moving on to more advanced topics like web frameworks (e.g., Express.js) that abstract away much of this low-level URL handling.
