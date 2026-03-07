---
marp: true
theme: gaia
paginate: true
---

<!-- _class: lead -->

# Node.js vs Browser JavaScript

### Badr Aldien Soliman

---

## 🌎 Same Language, Different Worlds

JavaScript is just a language. But where it runs (the **Runtime**) changes everything.

> **Runtime:** The environment that provides the tools, libraries, and APIs for code to execute.

| Feature         | 🌐 Browser JS        | 🚀 Node.js                 |
| :-------------- | :------------------- | :------------------------- |
| **Target**      | Targeted for Users   | Targeted for Servers/Tools |
| **Environment** | Lives in the Sandbox | System Access              |
| **Nature**      | Visual & Interactive | Performance & Scalability  |

---

| Feature           | Browser JavaScript         | Node.js                      |
| :---------------- | :------------------------- | :--------------------------- |
| **Global Object** | `window` / `document`      | `global` / `process`         |
| **Main Use Case** | User Interaction (UI)      | Server-side Backend          |
| **File System**   | 🚫 No direct access        | ✅ Full access (`fs` module) |
| **Environment**   | The Client (User's device) | The Server / Local Machine   |
| **Modules**       | ES Modules (`import`)      | CommonJS (`require`) & ESM   |

---

## 📦 The Global Objects

In the browser, everything hangs off the **Window**. In Node, it's the **Global**.

### Browser

```javascript
console.log(window);
// Contains: alert(), localStorage, document
```

### Node.js

```javascript
console.log(global);
// Contains: __dirname, __filename, process, Buffer
```

---

## 🛠️ Different Toolkits (APIs)

The runtime dictates what you can actually _do_.

### Browser APIs

- **DOM** (Document Object Model)
- **Fetch API**
- **Web Storage** (LocalStorage)
- **Geolocation**

---

### Node.js Modules

- **fs** (File System)
- **http** (Server creation)
- **path** (File path helpers)
- **os** (Operating system info)

---

## 🏎️ The Engine: V8

Both run on the **V8 Engine** (developed by Google for Chrome).

- **Browser:** V8 is wrapped in layers of security and visual APIs.
- **Node.js:** Ryan Dahl took V8, added a C++ library (Libuv) for I/O, and brought high-performance JS to the server.

> "Node.js allows JavaScript to be a first-class citizen in the server world."

---

<!-- _class: lead -->

# Ready to Build?

## Let's start our Node.js journey!
