---
marp: true
paginate: true
---

# JavaScript - Day 1

### Badr Aldien Soliman

---

## 1. Introduction to JavaScript

JavaScript makes web pages interactive.

It runs in the browser and can be added to HTML using the `<script>` tag.

```html
<script>
  'use strict'; // Recommended for cleaner code
  console.log('Hello from JavaScript');
</script>
```

### Comments

```js
// This is a single-line comment

/* This is a
   multi-line comment */
```

---

## 2. Basic I/O in JavaScript

### Alert

Show a message to the user.

```js
alert('This is an alert message');
```

---

### Prompt

Get input from the user.

```js
let answer = prompt('Type something here');
```

### Console Log

Display output for debugging.

```js
console.log('User entered:', answer);
```

### Document Write

Write directly to the page (simple demo only).

```js
document.write('This text appears on the page');
```

---

## 3. Variables and Data Types

Declare variables using `let` (can change) or `const` (fixed).

```js
let age = 20;
const country = 'Egypt';
```

Basic types: `string`, `number`, `boolean`.

```js
let name = 'Ali';
let greeting = 'Hello ' + name;
console.log(greeting);
```

---

### Variable Declaration Comparison

```js
// var: can be redeclared (bad practice)
var x = 10;
var x = 20;
console.log(x); // 20

// let: cannot be redeclared in the same scope
let y = 10;
// let y = 20; // ❌ SyntaxError

// const: cannot be redeclared or reassigned
const z = 10;
// z = 20; // ❌ TypeError
```

### Checking Types

```js
let name = 'Badr';
console.log(typeof name); // output: string
```

---

## 4. Functions

Functions group code into reusable blocks.

```js
function sayHello() {
  console.log('Hello!');
}

sayHello();
```

### Functions with Parameters and Return Values

```js
function multiply(a, b) {
  return a * b;
}

let result = multiply(3, 4);
console.log(result); // 12
```

---

## 5. Arithmetic Operators

| Operator | Name           | Example  | Result |
| -------- | -------------- | -------- | ------ |
| `+`      | Addition       | `5 + 3`  | `8`    |
| `-`      | Subtraction    | `10 - 4` | `6`    |
| `*`      | Multiplication | `6 * 7`  | `42`   |
| `/`      | Division       | `20 / 5` | `4`    |
| `%`      | Modulus        | `10 % 3` | `1`    |
| `**`     | Exponentiation | `2 ** 3` | `8`    |
| `++`     | Increment      | `a++`    | `+1`   |
| `--`     | Decrement      | `b--`    | `-1`   |

---

### Operator Examples

```js
let sum = 5 + 3; // 8
let difference = 10 - 4; // 6
let product = 6 * 7; // 42
let quotient = 20 / 5; // 4
let remainder = 10 % 3; // 1
let power = 2 ** 3; // 8

let a = 5;
a++;
console.log(a); // 6

let b = 5;
b--;
console.log(b); // 4
```

---

## 6. Conditional Statements

### If / Else

```js
let number = 5;

if (number > 0) {
  console.log('Positive');
} else {
  console.log('Not positive');
}
```

### Ternary Operator

```js
let status = number > 0 ? 'Positive' : 'Non-positive';
console.log(status);
```

---

### Switch Statement

```js
let day = 'Monday';

switch (day) {
  case 'Monday':
    console.log('Start of the week');
    break;
  case 'Friday':
    console.log('Weekend is near!');
    break;
  default:
    console.log('Midweek');
}
```

---

## 7. Loops

### For Loop

```js
for (let i = 1; i <= 5; i++) {
  console.log('Count:', i);
}
```

### While Loop

```js
let count = 1;

while (count <= 3) {
  console.log('Count is', count);
  count++;
}
```

> **Self-study**: Explore other loop types: `do...while`, `for...in`, and `for...of`.

---

## 8. Comparison & Logical Operators

### Comparison Operators

`>` , `<` , `>=` , `<=` , `==` , `===` , `!=` , `!==`

### Logical Operators

`&&` (AND) , `||` (OR)

```js
let temp = 28;

if (temp > 20 && temp < 30) {
  console.log('Comfortable weather');
}
```

---

## Key Concepts Review

### Essential JavaScript Terms

- **Variable**: A named container for storing data
- **Function**: A reusable block of code
- **String**: Text data wrapped in quotes
- **Boolean**: A `true` or `false` value
- **Operator**: A symbol that performs an operation
- **Condition**: A check that evaluates to `true` or `false`
- **Loop**: Repeated execution of a block of code

---

# Every bug is a lesson!

## **[badrsoliman.com](https://www.badrsoliman.com)**
