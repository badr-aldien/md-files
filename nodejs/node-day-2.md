---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Node.js Fundamentals - Day 2

### Badr Aldien Soliman

---

## 1. Clients & Servers

### IP Addresses & Domains

- **Hosts**: Computers connected to the internet that "host" websites.
- **IP Address**: A unique numerical label (like a physical address) for every host (e.g., `172.217.10.14`).
- **Domain Names**: Human-readable names (e.g., `google.com`) that are associated with specific IP addresses.

---

### Creating a Server

We use the built-in `http` module to create a server that "listens" for browser requests.

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  console.log('request made');
});

// Port number and host name
server.listen(3000, 'localhost', () => {
  console.log('listening for requests on port 3000');
});
```

---

### Requests & Responses

The callback function in `createServer` gives us two vital objects:

- **req (Request)**: Contains information about the incoming request (URL, method, headers).
- **res (Response)**: Used to send data back to the browser.

> **Important**: Every time you make a change to your server code, you must restart the file in the terminal.

---

### Sending a Response

To send data back, we must set a **Response Header** so the browser knows what kind of data we are sending.

**Option 1: Plain Text**

```javascript
res.setHeader('Content-Type', 'text/plain');
res.write('hello, students');
res.end();
```

---

**Option 2: HTML Content**

```javascript
res.setHeader('Content-Type', 'text/html');
res.write('<h1>Hello, World!</h1>');
res.write('<p>Keep learning Node.js</p>');
res.end();
```

---

### Sending an HTML File

Instead of writing HTML line by line, we can read a file from the file system and send it back.

```javascript
const fs = require('fs');

fs.readFile('./ , (err, data) => {
  if (err) {
    console.log(err);
    res.end();
  } else {
    // If it's just one file, we can pass data directly to end()
    res.end(data);
  }
});
```

---

## 2. Basic Routing

Routing allows us to send different content based on the URL requested by the user.

```javascript
let path = './views/';

switch (req.url) {
  case '/':
    path += 'index.html';
    res.statusCode = 200; // Success
    break;
  case '/about':
    path += 'about.html';
    res.statusCode = 200; // Success
    break;
  default:
    path += '404.html';
    res.statusCode = 404; // Not Found
    break;
}
```

---

### Status Codes

Status codes tell the browser what happened to the request:

- **200**: OK (Success)
- **301**: Resource moved (Redirect)
- **404**: Not Found (Error)
- **500**: Internal Server Error

---

### Redirection

Sometimes a page has moved, and we want to "redirect" the user to a new URL.

```javascript
case '/about-me':
  res.statusCode = 301;
  res.setHeader('Location', '/about');
  res.end();
  break;
```

---

### Handling POST Requests

By default, most requests are `GET`. To handle a `POST` request (like a form submission) in raw Node.js, we check the `req.method`.

```javascript
if (method === 'GET' && url === '/users') {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify(users));
  return;
}
```

---

### Handling the request body

If we're receiving it as

```bash
  { "name": "John Doe" }
```

```javascript
if (method === 'POST' && url === '/users') {
  let body = '';
  req.on('data', chunk => (body += chunk));
  req.on('end', () => {
    const { name } = JSON.parse(body);
    users.push(name);
    res.writeHead(201, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(users));
  });
  return;
}
```

---

## 3. NPM & NVM

### What is NPM?

NPM (Node Package Manager) is a tool that allows us to install third-party packages (code written by others) into our projects.

### What is NVM?

NVM (Node Version Manager) is a tool used to install and switch between different versions of Node.js on your machine. This is vital when working on multiple projects that require different Node versions.

---

### Initializing NPM

To start using packages in your project, you must initialize it:

```bash
npm init
```

_This will ask you several questions about your project._

**Shortcut (accept all defaults):**

```bash
npm init -y
```

---

## 4. Dependencies & Nodemon

### Installing Packages

```bash
npm install express
```

### Nodemon

Nodemon is a tool that automatically restarts your server whenever you save a file. No more manual restarts!

**Install globally:**

```bash
npm install -g nodemon
```

---

## 5. Project Files & Folders

When you install packages, three important things appear:

1.  **`node_modules/`**: A folder containing all the code for the packages you installed. **Never edit this!**
2.  **`package.json`**: The "manifest" of your project. It lists your project's name, version, and dependencies.
3.  **`package-lock.json`**: Records the exact version of every package installed to ensure consistency across different machines.

---

### Inside `package.json`: Scripts

You can define custom commands in the `scripts` section:

```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```

Now you can run your app using:

```bash
npm run dev
```

---

## Summary Workflow

1. **HTTP & Servers**: Create servers and manage the req/res cycle (GET/POST).
2. **Routing & Redirects**: Handle different URLs and status codes.
3. **NPM & NVM**: Manage packages and Node versions.
4. **Dependencies**: Install and use third-party packages like Nodemon.
5. **Organization**: Understand `package.json` scripts and `node_modules`.

---

# May your bugs be shallow

## **[badrsoliman.com](https://www.badrsoliman.com)**
