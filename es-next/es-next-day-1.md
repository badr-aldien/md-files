---
marp: true
paginate: true
---

# ES Next: Day 1

### Badr Aldien Soliman

---

## 1. Introduction to ES6+

![ES Next](esnext.png)

---

**ECMAScript** is the standard for JavaScript.

- **ES6 (ES2015)** was a massive update that changed how we write JS.
- Since then, yearly updates bring new "sugary" features.
- "ES Next" refers to the latest versions and upcoming features.

---

## 2. Using let and const

In the past, we only had `var`.

### Why avoid `var`?

- Function-scoped (not block-scoped).
- Hoisting can lead to weird bugs.
- Can be redeclared.

---

### Block Scoping with let & const

```javascript
if (true) {
  var framework = 'AngularJS';
  let library = 'React';
}

console.log(framework); // "AngularJS"
console.log(library); // ReferenceError
```

- **`let`**: Use for variables that will change.
- **`const`**: Use for constants.
- Both are **Block Scoped**.

---

## 3. Arrow Functions

A shorter way to write functions.

### Syntax & Implicit Return

```javascript
// Traditional
function add(a, b) {
  return a + b;
}

// Arrow
const add = (a, b) => a + b;
```

---

### `this` Binding

Arrow functions do not have their own `this`. They capture `this` from the surrounding code (lexical scope).

### Default Parameters

Initialize functions with default values if no value is passed.

```javascript
const greet = (name = 'Guest') => `Hello, ${name}!`;
greet(); // "Hello, Guest!"
```

---

## 4. Destructuring

Extraction of data from arrays and objects into distinct variables.

### Object & Array Destructuring

```javascript
const user = { name: 'Badr', age: 30 };
const { name } = user;

const colors = ['red', 'green'];
const [first] = colors;
```

`Note: Default parameters can be used & variables can be overridden`
`Note: Destructuring can be used in function parameters`

---

## 5. Rest Parameter and Spread Operator

### Spread Operator (`...`)

"Unpacks" elements from an array or object.

```javascript
const arr2 = [...arr1, 4, 5];
```

### Rest Parameter (`...`)

"Packs" multiple arguments into a single array.

```javascript
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
```

---

## 6. Built-in Methods

Commonly used array methods for transformation and searching.

- `map`, `filter`, `reduce`
- `find`, `findIndex`
- `every`, `some`
- `splice`, `slice`

---

### Transform & Search

```javascript
const nums = [1, 2, 3, 4];

const doubled = nums.map((n) => n * 2);
const even = nums.filter((n) => n % 2 === 0);
const firstEven = nums.find((n) => n % 2 === 0);
```

---

## 7. Loops

### Traditional vs Modern

1. **`for` loop**: The classic way.
2. **`for...of`**: Iterate over iterable objects (arrays, strings).
3. **`.forEach()`**: A method for executing a function on each element.

```javascript
const items = ['a', 'b', 'c'];

for (const item of items) {
  console.log(item);
}

items.forEach((item) => console.log(item));
```

---

# Happy coding!

## **[badrsoliman.com](https://www.badrsoliman.com)**
