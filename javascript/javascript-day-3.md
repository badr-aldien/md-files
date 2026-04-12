---
marp: true
paginate: true
---

# JavaScript - Day 3

### Advanced Arrays, Objects & Browser APIs

##### Badr Aldien Soliman

---

## 1. Advanced Array Methods

### splice(): Remove or Insert at a Position

```js
let names = ['Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Frank'];

// Remove 1 element at index 1
names.splice(1, 1);
```

---

### Looping: Traditional vs Modern

```js
// Traditional for loop
for (let i = 0; i < names.length; i++) {
  document.writeln('Hello ' + names[i]);
}

// for...of: cleaner, more readable
for (let username of names) {
  document.writeln('Hello ' + username);
}
```

---

### filter(): Keep Only What Matches

```js
let years = [1995, 1998, 2000, 2002, 2003, 2005];

// Keep only years from 2000 onwards
let newYears = years.filter(function (year) {
  return year >= 2000;
});

// Same thing using an arrow function
let filteredByIndex = years.filter((year, index) => index >= 2);
```

> We'll cover arrow functions properly after functions: for now just notice the shorter syntax.

---

## 2. Working with Arrays of Objects

```js
let products = [
  { id: 101, name: 'iPhone 16', price: 1200, qty: 5 },
  { id: 102, name: 'Samsung Galaxy S24', price: 1000, qty: 8 },
  { id: 103, name: 'Google Pixel 9', price: 900, qty: 6 },
  { id: 104, name: 'OnePlus 12', price: 750, qty: 12 },
  { id: 105, name: 'Oppo Reno 12', price: 600, qty: 15 },
];
```

---

### Displaying & Mapping

```js
// Loop through and display each product name
for (let product of products) {
  document.write(product.name + '<br>');
}

// Extract just the names into a new array
let productNames = products.map(product => product.name);
```

---

## 3. Object Iteration

### for...in: Loop Through an Object's Keys

```js
let product = { id: 101, name: 'iPhone 16', price: 1200, qty: 5 };

for (let key in product) {
  // key is the property name
  // product[key] is the value
}
```

---

## 4. Primitive vs Reference Types

### Primitive Types: Copied by Value

```js
let str1 = 'Alice';
let str2 = str1;

str1 = 'Bob';

// str1 → "Bob"
// str2 → "Alice"  (unaffected)
```

Primitives: `string`, `number`, `boolean`

---

### Reference Types: Copied by Reference

```js
// Arrays: use Array.from() to get an independent copy
let arr1 = ['Alice', 'Bob', 'Charlie'];
let arr2 = Array.from(arr1);

arr1.push('David');
// arr1 has "David": arr2 does not
```

```js
// Objects: use spread (...) to get an independent copy
let person1 = { name: 'Alice', age: 30, address: 'Cairo' };
let person2 = { ...person1 };

person2.name = 'Bob';
// person1.name → "Alice"
// person2.name → "Bob"
```

---

## 5. Browser Object Model (BOM)

The **BOM** gives JavaScript access to the browser itself: not just the page content.

| Object      | What it represents             |
| ----------- | ------------------------------ |
| `window`    | The browser tab/window         |
| `screen`    | The user's physical screen     |
| `navigator` | The browser and device info    |
| `location`  | The current page URL           |
| `history`   | The browser navigation history |

---

### window: Opening & Sizing

```js
// Open a new browser window
open('https://facebook.com', '_blank', 'width=400,height=400');

// Get the browser's outer dimensions
let wd = window.outerWidth;
```

> `outerWidth` includes the browser chrome (tabs, borders)
> `innerWidth` is just the visible page area

---

### screen & navigator

📖 [MDN: Screen](https://developer.mozilla.org/en-US/docs/Web/API/Screen) · [MDN: Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)

When you open them, look for properties that tell you:

- **screen**: physical display size and available area
- **navigator**: browser language, platform, CPU cores, and online status

---

### location & history

📖 [MDN: Location](https://developer.mozilla.org/en-US/docs/Web/API/Location) · [MDN: History](https://developer.mozilla.org/en-US/docs/Web/API/History)

When you open them, look for:

- **location**: reading and changing the current page URL
- **history**: moving forward and backward through visited pages

---

## 6. Document Object Model (DOM)

```js
// Access basic page info
console.log(document.title);
console.log(document.URL);
```

> The DOM represents the page content as a tree of objects.
> We'll dive much deeper into this in the next session.

---

## 7. Timing Functions

### setTimeout: Run Once After a Delay

```js
// Show an alert after 2 seconds
setTimeout(() => alert('Hello!'), 2000);
```

---

### setInterval & clearInterval: Repeat Until Stopped

```js
function display() {
  document.writeln('hello my friend<br>');
}

// Run display() every 500ms
let counter = setInterval(display, 500);

// Stop it after 5 seconds
setTimeout(function () {
  clearInterval(counter);
}, 5000);
```

---

## Key Concepts Review

- **`splice()`**: remove or insert items at a specific index
- **`filter()`**: create a new array with only matching items
- **`map()`**: transform every item into something new
- **`for...of`**: loop through array values
- **`for...in`**: loop through object keys
- **Primitive**: copied by value, changes don't affect the original
- **BOM**: browser APIs: `window`, `screen`, `navigator`, `location`, `history`
- **Timing**: `setTimeout()`, `setInterval()`, `clearInterval()`

---

### Self Study

- Explore array methods: `map()`, `reduce()`, `forEach()`
- Learn about deep vs shallow copying
- Practice with Browser APIs: `location`, `history`, `document`
- Experiment with timing functions
- Research: sync vs async, and macro vs micro tasks in JS

---

# Now go break something: then fix it.

## **[badrsoliman.com](https://www.badrsoliman.com)**
