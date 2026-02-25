---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Node.js Fundamentals - Day 1

### Badr Aldien Soliman

---

## 1. The Global Object

In the browser, the top-level object is `window`. In Node.js, it is `global`.

### Common Global Properties:

- `global`: The global namespace.
- `__dirname`: Absolute path to the directory containing the current file.
- `__filename`: Absolute path to the current file itself.

---

### Timers (Also Global)

```javascript
// Runs once after 3 seconds
setTimeout(() => {
  console.log('3 seconds passed');
}, 3000);

// Runs every 1 second
const interval = setInterval(() => {
  console.log('1 second tick');
}, 1000);

// Stop the interval after 5 seconds
setTimeout(() => clearInterval(interval), 5000);
```

---

## 2. Modules & Require

Node.js uses a module system where every file is treated as a separate module.

### Why use Modules?

- **Encapsulation**: Keep variables private to the file.
- **Organization**: Break large projects into smaller pieces.
- **Reusability**: Use the same logic in different parts of the app.

---

### Exporting and Importing

**`people.js` (The Module)**

```javascript
const people = ['yoshi', 'ryu', 'chun-li'];
const ages = [20, 25, 30];

module.exports = {
  people,
  ages,
};
```

**`app.js` (The Consumer)**

```javascript
const { people, ages } = require('./people');

console.log(people); // ['yoshi', 'ryu', 'chun-li']
```

---

## 3. The File System (fs)

Node.js has a built-in module called `fs` to interact with files.

### Reading Files

```javascript
const fs = require('fs');

fs.readFile('./docs/blog1.txt', (err, data) => {
  if (err) {
    console.log(err);
  }
  console.log(data.toString());
});
```

_Note: `readFile` is asynchronous and doesn't block the rest of the code._

---

### Writing Files

```javascript
fs.writeFile('./docs/blog1.txt', 'hello, world', () => {
  console.log('file was written');
});

// If the file doesn't exist, it creates it!
fs.writeFile('./docs/blog2.txt', 'new text here', () => {
  console.log('new file created');
});
```

---

### Working with Directories

**Creating a folder:**

```javascript
if (!fs.existsSync('./assets')) {
  fs.mkdir('./assets', err => {
    if (err) console.log(err);
    console.log('folder created');
  });
}
```

**Deleting a folder:**

```javascript
if (fs.existsSync('./assets')) {
  fs.rmdir('./assets', err => {
    if (err) console.log(err);
    console.log('folder deleted');
  });
}
```

---

### Deleting Files

```javascript
if (fs.existsSync('./docs/deleteme.txt')) {
  fs.unlink('./docs/deleteme.txt', err => {
    if (err) console.log(err);
    console.log('file deleted');
  });
}
```

---

## 4. Streams & Buffers

### What are Buffers?

A small "waiting area" for data being moved from one place to another. Data is gathered until it fills the buffer, then sent.

### What are Streams?

Streams allow us to start using data before it has finished loading. Think of it like a "flowing" pipe of data.

---

### Read Streams

`createReadStream` reads data in "chunks".

```javascript
const fs = require('fs');

const readStream = fs.createReadStream('./docs/blog3.txt', {
  encoding: 'utf8',
});

readStream.on('data', chunk => {
  console.log('--- NEW CHUNK ---');
  console.log(chunk);
});
```

---

### Write Streams

`createWriteStream` sends data to a file in chunks.

```javascript
const writeStream = fs.createWriteStream('./docs/blog4.txt');

writeStream.write('\nNEW CHUNK OF DATA\n');
writeStream.write('Hello again!');
```

---

### The Power of Pipes

Piping is a way to take data from a read stream and "pipe" it directly into a write stream.

```javascript
const readStream = fs.createReadStream('./docs/blog3.txt');
const writeStream = fs.createWriteStream('./docs/blog4.txt');

// This does exactly what the manual read/write does, but faster!
readStream.pipe(writeStream);
```

---

## 5. Clients & Servers

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

## 6. Basic Routing

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

## Summary Workflow

1. **Globals**: Variables available everywhere (`__dirname`, `__filename`).
2. **Modules**: Split code into files using `require` and `module.exports`.
3. **FS Module**: Manage files and folders (Async vs Sync).
4. **Streams**: Handle large data efficiently using chunks.
5. **HTTP & Servers**: Create servers and manage the req/res cycle (GET/POST).
6. **Routing & Redirects**: Handle different URLs and status codes.

---

# May your bugs be shallow

## **[badrsoliman.com](https://www.badrsoliman.com)**
