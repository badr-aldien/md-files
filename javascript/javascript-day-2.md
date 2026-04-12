---
marp: true
paginate: true
---

# JavaScript - Day 2

### Objects, Arrays, Strings & Math

##### Badr Aldien Soliman

---

## 1. JavaScript Objects

### What is an Object?

A collection of **key-value pairs**: used to group related data together.

```js
var user = {
  name: 'Ahmed',
  age: 30,
  address: 'Qena',
};
```

Think of it like a form: each field has a label (key) and a value.

---

### Ways to Create Objects

**Object Literal**: the most common way:

```js
var user = {
  name: 'Ahmed',
  age: 30,
  address: 'Qena',
};
```

**Constructor Function**: a blueprint for creating multiple similar objects:

```js
function Person(name, age, address) {
  this.name = name;
  this.age = age;
  this.address = address;
}

var person = new Person('Ahmed', 27, 'Qena');
```

---

### Accessing Object Properties

```js
// Get a property using dot notation
user.name;

// Get a property using bracket notation
user['name'];
```

Both do the same thing. Bracket notation is useful when the key is stored in a variable.

---

### Updating, Adding & Deleting

```js
// Update an existing property
user.name = 'Omar';

// Add a new property
user['birthYear'] = 1998;

// Remove a property entirely
delete user.address;
```

---

### Nested Objects & Methods

```js
var person = {
  name: 'Ali',
  birthYear: 1998,
  getAge: function () {
    return 2025 - this.birthYear;
  },
  children: {
    firstChild: 'Ahmed',
    secondChild: 'Omar',
  },
};

// Access a nested property
person.children.secondChild;

// Call a method on the object
person.getAge();
```

---

## 2. Arrays in JavaScript

### What is an Array?

An array stores **multiple values** in a single variable, in an ordered list.

```js
let fruits = ['Apple', 'Banana', 'Mango'];
```

Each item has an **index** starting from `0`:

| Index | Value      |
| ----- | ---------- |
| `0`   | `"Apple"`  |
| `1`   | `"Banana"` |
| `2`   | `"Mango"`  |

---

### Accessing & Modifying

```js
// Read the first item
console.log(fruits[0]);

// Replace the second item
fruits[1] = 'Orange';
```

---

### Array Methods: Adding & Removing

```js
// Add an item to the end
fruits.push('Grapes');

// Remove the last item
fruits.pop();

// Add an item to the start
fruits.unshift('Kiwi');

// Remove the first item
fruits.shift();
```

---

### Array Methods: Inspecting & Reordering

```js
// Get the number of items
fruits.length;

// Reverse the order of items
fruits.reverse();
```

---

### Looping Through an Array

```js
let colors = ['red', 'green', 'blue'];

for (let i = 0; i < colors.length; i++) {
  // Print each color one by one
  console.log(colors[i]);
}
```

---

## 3. Strings in JavaScript

📖 **Reference**: [MDN String Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

When you open it, look for methods that help you:

- **Inspect**: how long is the string? what's at position X?
- **Search**: does it contain a word? where does it appear?
- **Transform**: change case, remove spaces, replace words

> Getting comfortable reading documentation is one of the most important skills you'll build as a developer.

---

> 💡 **Practice idea**: Take a full name and format it so the first letter is uppercase and the rest are lowercase.

---

## 4. Math Object

### Rounding

```js
// Round to the nearest whole number
Math.round(4.6); // → 5

// Always round up
Math.ceil(4.1); // → 5

// Always round down
Math.floor(4.9); // → 4
```

---

### Calculating

```js
// Remove the negative sign
Math.abs(-7);

// Raise a number to a power
Math.pow(2, 3);

// Get the square root
Math.sqrt(16);
```

---

### Utilities

```js
// Get the largest value
Math.max(1, 5, 3);

// Get the smallest value
Math.min(1, 5, 3);

// Generate a random decimal between 0 and 1
Math.random(); // → e.g. 0.482...
```

---

### Generating a Random Number in a Range

To get a random whole number between `1` and `10`:

```js
let random = Math.floor(Math.random() * 10) + 1;
```

> `Math.random()` → decimal between `0` and `1`
> Multiply by `10` → range becomes `0` to `9.99...`
> `Math.floor()` → strips the decimal → `0` to `9`
> Add `1` → final range is `1` to `10` ✅

---

## Key Concepts Review

- **Object**: A group of related key-value pairs
- **Array**: An ordered list of values, accessed by index
- **Method**: A function stored inside an object or built into a type
- **Index**: The position of an item in an array (starts at `0`)
- **`this`**: Refers to the object the method belongs to
- **`Math`**: A built-in object with useful mathematical tools

---

# Growth happens one error at a time.

## **[badrsoliman.com](https://www.badrsoliman.com)**
