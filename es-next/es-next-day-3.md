---
marp: true
paginate: true
---

# ES Next: Day 3

### Badr Aldien Soliman

---

## 1. Callback Hell & Promise

A `Callback Hell` is a situation where we have nested callbacks, which makes the code hard to read and maintain.

- **Callback** is a function that is passed as an argument to another function and is executed after the other function completes.

---

### Callback Hell

```javascript
function hell(win) {
  // for listener purpose
  return function () {
    loadLink(win, REMOTE_SRC + '/assets/css/style.css', function () {
      loadLink(win, REMOTE_SRC + '/lib/async.js', function () {
        loadLink(win, REMOTE_SRC + '/lib/easyXDM.js', function () {
          loadLink(win, REMOTE_SRC + '/lib/json2.js', function () {
            loadLink(win, REMOTE_SRC + '/lib/underscore.min.js', function () {
              loadLink(win, REMOTE_SRC + '/lib/backbone.min.js', function () {
                loadLink(win, REMOTE_SRC + '/dev/base_dev.js', function () {
                  loadLink(win, REMOTE_SRC + '/assets/js/deps.js', function () {
                    loadLink(
                      win,
                      REMOTE_SRC + '/src/' + win.loader_path + '/loader.js',
                      function () {
                        async.eachSeries(SCRIPTS, function (src, callback) {
                          loadScript(win, BASE_URL + src, callback);
                        });
                      },
                    );
                  });
                });
              });
            });
          });
        });
      });
    });
  };
}
```

---

### The Promise Story

A `Promise` is a placeholder for a future value.

- **Pending**: Waiting for result.
- **Fulfilled**: Success!
- **Rejected**: Error!

---

### Promise States

```javascript
const myPromise = new Promise((resolve, reject) => {
  const success = true;
  if (success) {
    resolve('Operation Successful');
  } else {
    reject('Operation Failed');
  }
});
```

---

### Handling Promises

```javascript
fetchData()
  .then((data) => console.log(data))
  .catch((err) => console.error(err))
  .finally(() => console.log('Done'));
```

---

## 2. Async and Await

Syntactic sugar to write asynchronous code that looks synchronous.

```javascript
async function getData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

---

## 4. Promise Static Methods

- `Promise.all([p1, p2])`: Waits for all to succeed.
- `Promise.allSettled([p1, p2])`: Waits for all to finish.
- `Promise.race([p1, p2])`: Returns the first one to settle.

---

## 3. Fetch API and CRUD

Standard way to make network requests.

### CRUD Operations

- **GET**: Read data.
- **POST**: Create data.
- **UPDATE (PUT/PATCH)**: Modify data.
- **DELETE**: Remove data.

---

### Fetch Example (POST)

```javascript
fetch(url, {
  method: 'POST',
  body: JSON.stringify(userData),
  headers: { 'Content-Type': 'application/json' },
})
  .then((res) => res.json())
  .then((data) => console.log(data));
```

---

## 5. Modern Operator additions

### Optional Chaining (`?.`)

Short-circuits if a property doesn't exist.
`const city = user?.address?.city;`

### Nullish Coalescing (`??`)

Returns RHS only if LHS is `null` or `undefined`.
`const name = user.nickname ?? 'Guest';`

---

## 6. The Event Loop

JavaScript is **single-threaded**, meaning it executes one command at a time. The **Event Loop** allows JS to perform non-blocking I/O operations.

### Key Components:

- **Call Stack**: Tracks function calls (LIFO).
- **Web APIs**: Provided by the browser (e.g., `setTimeout`, `fetch`, `DOM`).
- **Callback/Task Queue**: Queue for macrotasks (e.g., `setTimeout`).
- **Microtask Queue**: Higher priority queue (e.g., `Promises`).

---

### Execution Order Example

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout callback');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise callback');
});

console.log('End');
```

---

# Happy coding!

## **[badrsoliman.com](https://www.badrsoliman.com)**
