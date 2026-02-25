---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Node.js & Express - Day 2

### Badr Aldien Soliman

---

## 1. NPM & NVM

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

## 2. Dependencies & Nodemon

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

## 3. Project Files & Folders

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

## 4. Introduction to Express

Express is a fast, unopinionated, minimalist web framework for Node.js. It makes creating servers much easier.

### Basic Setup

```javascript
const express = require('express');

// Create an instance of an express app
const app = express();

// Listen for requests
app.listen(3000);
```

---

### Handling Requests

Express makes handling different URLs (routing) much cleaner than using the `http` module.

```javascript
app.get('/', (req, res) => {
  // Express automatically sets Content-Type and Status Code!
  res.send('<h1>Home Page</h1>');
});

app.get('/about', (req, res) => {
  res.send('<p>About Page</p>');
});
```

---

## 5. Routing & Sending Files

To send an actual HTML file, we use `res.sendFile()`.

```javascript
app.get('/', (req, res) => {
  // We must provide an absolute path
  res.sendFile('./views/index.html', { root: __dirname });
});
```

- **`__dirname`**: Provides the absolute path to the current directory.
- **`{ root: __dirname }`**: Tells Express exactly where to look for the relative path provided.

---

## 6. Redirects & 404s

### Redirecting Users

If a URL has changed, Express makes it simple to point users elsewhere.

```javascript
app.get('/about-us', (req, res) => {
  res.redirect('/about');
});
```

---

### Handling 404 Errors (The Catch-All)

We use `app.use()` to handle any request that didn't match the routes above.

```javascript
// This MUST be at the bottom of the file
app.use((req, res) => {
  res.status(404).sendFile('./views/404.html', { root: __dirname });
});
```

> **Crucial Note**: Unlike `app.get()`, `app.use()` will fire for every single request. If it reaches this point, it means no previous routes matched, so we manually set `res.status(404)`.

---

## 7. Middleware

### What is Middleware?

Middleware is code that runs on the server between receiving a request and sending a response. It has access to the `req` and `res` objects.

**Order Matters**: Middleware runs in the order it is defined in your code (top to bottom).

---

### Using `app.use()` & `next()`

If we write our own middleware, we must call the `next()` function, or the browser will hang (it won't know to move to the next route/middleware).

```javascript
app.use((req, res, next) => {
  console.log('New request made:');
  console.log('Host: ', req.hostname);
  console.log('Path: ', req.path);
  console.log('Method: ', req.method);
  next(); // Passes control to the next function
});
```

---

### Static Files (Built-in Middleware)

By default, Express blocks access to files in your project (like CSS or images) for security. We use `express.static` to make a folder "public".

```javascript
// Everything inside the 'public' folder is now accessible
app.use(express.static('public'));
```

**Now in your HTML, you can link CSS simply:**
`<link rel="stylesheet" href="/styles.css">`

---

### Third-Party Middleware: Morgan

Instead of writing our own logger, we can use **Morgan**.

1.  **Install**: `npm install morgan`
2.  **Usage**:

```javascript
const morgan = require('morgan');

// 'dev' is a predefined logging format
app.use(morgan('dev'));
```

---

## 8. POST Requests & Arrays

To handle `POST` requests and store data in a simple array.

### Middleware

Express needs this to "parse" the request body:

```javascript
app.use(express.json());
```

---

### GET & POST Example

```javascript
let blogs = ['First Blog', 'Second Blog'];

// GET: Read all blogs
app.get('/blogs', (req, res) => {
  res.json(blogs);
});

// POST: Add a new blog
app.post('/blogs', (req, res) => {
  blogs.push(req.body.title);
  res.status(201).json(blogs);
});
```

> **Comparison**: Unlike raw Node.js where we manually listened for 'data' events, Express (with middleware) does the hard work for us and gives us a clean `req.body` object.

---

## 9. MVC & Controllers

As your project grows, your `app.js` will become cluttered. We use **Controllers** to separate the logic from the route definitions.

### 1. The Controller (`blogController.js`)

We define all the logic for our routes here.

---

```javascript
const blog_all = (req, res) => {
  console.log('GET all blogs');
  res.send('All blogs');
};

const blog_create = (req, res) => {
  console.log('POST a new blog');
  res.send('Blog created');
};

const blog_update = (req, res) => {
  console.log('UPDATE a blog');
  res.send('Blog updated');
};

const blog_delete = (req, res) => {
  console.log('DELETE a blog');
  res.send('Blog deleted');
};

module.exports = { blog_all, blog_create, blog_update, blog_delete };
```

---

### 2. The Router (`blogRoutes.js`)

We use `express.Router()` to connect the URLs to the controller functions.

```javascript
const express = require('express');
const router = express.Router();
const controller = require('../controllers/blogController');

router.get('/', controller.blog_all);
router.post('/', controller.blog_create);
router.patch('/:id', controller.blog_update);
router.delete('/:id', controller.blog_delete);

module.exports = router;
```

---

### 3. Server Setup (`app.js`)

```javascript
const blogRoutes = require('./routes/blogRoutes');

// Use the router for all /blogs routes
app.use('/blogs', blogRoutes);
```

---

## Summary Workflow

1. **Setup**: Use `npm init -y` and install `nodemon`.
2. **Organization**: Understand `package.json` scripts and `node_modules`.
3. **Express**: Initialize the app and listen on a port.
4. **Routing**: Use `app.get()` with `res.send()` or `res.sendFile()`.
5. **Middleware**: Use `app.use()` for logging, static files, or third-party tools.
6. **Finalize**: Add redirects and a 404 catch-all at the bottom.
7. **POST Data**: Use `app.post()` and body-parsing middleware.
8. **Arrays**: Store and retrieve data using simple arrays.
9. **MVC**: Organize code using Controllers and Express Router.

---

# Read the error again

## **[badrsoliman.com](https://www.badrsoliman.com)**
