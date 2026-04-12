---
marp: true
paginate: true
---

# JavaScript - Day 5

### APIs, JSON, Fetching Data & Storage

##### Badr Aldien Soliman

---

## 1. What is an API?

**API** stands for Application Programming Interface.

It allows two applications to talk to each other.

> Think of an API like a waiter in a restaurant:
>
> - **You** (the client) ask for food
> - **The waiter** (API) takes your order to the kitchen (server)
> - The kitchen prepares it and the waiter brings it back

**Example**: A weather app doesn't store weather data itself: it fetches it from a weather service API.

---

## 2. JSON

**JSON** stands for JavaScript Object Notation.

A lightweight format for storing and transporting data: commonly used when a server sends data to a web page.

```json
{
  "name": "Alice",
  "age": 25,
  "isStudent": false,
  "skills": ["JavaScript", "HTML", "CSS"]
}
```

> Syntax looks like a JS object, but keys and string values must always use **double quotes**.

---

### JSON in JavaScript

```js
let user = { name: 'Bob', age: 30 };

// Convert object → JSON string
let jsonString = JSON.stringify(user);

// Convert JSON string → object
let obj = JSON.parse(jsonString);
```

| Method                | What it does                              |
| --------------------- | ----------------------------------------- |
| `JSON.stringify(obj)` | Convert a JS object to a JSON string      |
| `JSON.parse(jsonStr)` | Convert a JSON string back to a JS object |

---

### Common HTTP Status Codes

| Code  | Status                | Meaning                            |
| ----- | --------------------- | ---------------------------------- |
| `200` | OK                    | Request was successful             |
| `301` | Moved Permanently     | Resource moved to a new URL        |
| `401` | Unauthorized          | Authentication required or failed  |
| `404` | Not Found             | Resource doesn't exist             |
| `500` | Internal Server Error | Something went wrong on the server |

---

## 3. Fetching Data with XHR

```js
function getData() {
  let xhr = new XMLHttpRequest();

  xhr.open('GET', 'https://jsonplaceholder.typicode.com/users');

  xhr.onload = function () {
    if (xhr.status === 200) {
      let users = JSON.parse(xhr.responseText);
      let output = '';
      for (let user of users) {
        output += `<p>${user.name} - ${user.email}</p>`;
      }
      document.getElementById('output').innerHTML = output;
    }
  };

  xhr.send();
}
```

---

### XHR Ready States

Every XHR request goes through a series of states tracked by `readyState`:

| Value | State            | Description                                             |
| ----- | ---------------- | ------------------------------------------------------- |
| `0`   | UNSENT           | XHR client created, `open()` not called yet             |
| `1`   | OPENED           | `open()` has been called                                |
| `2`   | HEADERS_RECEIVED | `send()` has been called, headers and status available  |
| `3`   | LOADING          | Response body is being received                         |
| `4`   | DONE             | Operation complete: data transfer successful or failed |

---

## 4. Web Storage

### localStorage vs sessionStorage vs Cookies

| Feature                       | localStorage | sessionStorage       | Cookies                |
| ----------------------------- | ------------ | -------------------- | ---------------------- |
| Persists after tab close?     | ✅ Yes       | ✅ While tab is open | ✅ Until expiration    |
| Persists after browser close? | ✅ Yes       | ❌ No                | ✅ Depends on settings |
| Size limit                    | ~5–10 MB     | ~5 MB                | ~4 KB                  |

---

### localStorage

Stores data with no expiration: stays even after the browser is closed.

```js
// Save data
localStorage.setItem('username', 'Alice');

// Get data
localStorage.getItem('username');

// Remove one item
localStorage.removeItem('username');

// Clear everything
localStorage.clear();
```

---

### sessionStorage

Same as `localStorage` but cleared when the tab is closed.

```js
// Save data for the current session
sessionStorage.setItem('theme', 'dark');

// Get data
sessionStorage.getItem('theme');
```

---

### Cookies

Small pieces of data stored in the browser and **sent with every request to the server**.

Commonly used for authentication and tracking.

```js
// Setting a cookie client-side
document.cookie = 'username=Bob; expires=Fri, 31 Dec 2025 23:59:59 GMT; path=/';
```

> In most real applications, cookies are managed by the **server**, not the client.

---

## Key Concepts Review

- **API**: a bridge that lets two applications communicate
- **JSON**: a text format for exchanging data between client and server
- **`JSON.stringify()`**: convert an object to a JSON string
- **`JSON.parse()`**: convert a JSON string back to an object
- **XHR**: the original way to fetch data from an API in JavaScript
- **`readyState`**: tracks the current stage of an XHR request
- **`localStorage`**: persistent browser storage, survives browser restarts
- **`sessionStorage`**: temporary storage, cleared when the tab closes
- **`Cookies`**: small browser-stored data, sent to the server with every request

---

### Self Study

- Explore the modern `fetch()` API and how it replaces XHR
- Learn about `async` / `await` for handling asynchronous requests
- Research the difference between `readyState` and `onload`
- Practice reading and writing to `localStorage` with real data

---

# Data is just text until you give it meaning.

## **[badrsoliman.com](https://www.badrsoliman.com)**
