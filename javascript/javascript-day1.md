# Day 1 - Introduction to JavaScript

### Eng. Badr Aldien Soliman

---

## 1. Introduction to JavaScript

JavaScript makes web pages interactive.
Runs in the browser and can be added to HTML using <script> tag.

```html
<script>
  "use strict"; // Recommended for cleaner code
  console.log("Hello from JavaScript");
</script>
```

**Comments:**

```javascript
// This is a single-line comment
/* This is a multi-line comment */
```

---

## 2. Basic I/O in JavaScript

**Alert:** Show a message to the user.

```javascript
alert("This is an alert message");
```

**Prompt:** Get input from the user.

```javascript
let answer = prompt("Type something here");
```

**Console Log:** Display output for debugging.

```javascript
console.log("User entered:", answer);
```

**Document Write:** Write directly to the page (simple demo only).

```javascript
document.write("This text appears on the page");
```

---

## 3. Variables and Data Types

Declare variables using let (can change) or const (fixed).

```javascript
let age = 20;
const country = "Egypt";
```

Basic types: string, number, boolean.
Combine values:

```javascript
let name = "Ali";
let greeting = "Hello " + name;
console.log(greeting);
```

```javascript
// var: can be redeclared (bad practice)
var x = 10;
var x = 20;
console.log(x); // 20
```

```javascript
// let: cannot be redeclared in the same scope
let y = 10;
// let y = 20; //
❌ SyntaxError
```

```javascript
// const: cannot be redeclared or reassigned
const z = 10;
// z = 20; //
❌ TypeError
```

```javascript
let name = "Badr";
console.log(typeof name); // output: string
```

---

## 4. Functions

Functions group code into reusable blocks.

```javascript
function sayHello() {
  console.log("Hello!");
}
sayHello();
```

Functions with parameters and return values:

```javascript
function multiply(a, b) {
  return a * b;
}
let result = multiply(3, 4);
console.log(result);
```

---

## 5. Arithmetic Operators

**Addition (+)** – Adds two values.

```javascript
let sum = 5 + 3;
console.log(sum); // 8
```

**Subtraction (-)** – Subtracts one value from another.

```javascript
let difference = 10 - 4;
console.log(difference); // 6
```

**Multiplication (\*)** – Multiplies two values.

```javascript
let product = 6 * 7;
console.log(product); // 42
```

**Division (/)** – Divides one value by another.

```javascript
let quotient = 20 / 5;
console.log(quotient); // 4
```

**Modulus (%)** – Returns the remainder of a division.

```javascript
let remainder = 10 % 3;
console.log(remainder); // 1
```

**Exponentiation (**)\*\* – Raises the first number to the power of the second.

```javascript
let power = 2 ** 3;
console.log(power); // 8
```

**Increment (++)** – Increases value by 1.

```javascript
let a = 5;
a++;
console.log(a); // 6
```

**Decrement (--)** – Decreases value by 1.

```javascript
let b = 5;
b--;
console.log(b); // 4
```

---

## 6. Conditional Statements

**If / Else**

```javascript
let number = 5;
if (number > 0) {
  console.log("Positive");
} else {
  console.log("Not positive");
}
```

**Ternary Operator**

```javascript
let status = number > 0 ? "Positive" : "Non-positive";
console.log(status);
```

**Switch Example**

```javascript
let day = "Monday";
switch (day) {
  case "Monday":
    console.log("Start of the week");
    break;
  case "Friday":
    console.log("Weekend is near!");
    break;
  default:
    console.log("Midweek");
}
```

---

## 7. Loops

**For Loop**

```javascript
for (let i = 1; i <= 5; i++) {
  console.log("Count:", i);
}
```

**While Loop**

```javascript
let count = 1;
while (count <= 3) {
  console.log("Count is", count);
  count++;
}
```

Self-study: Explore other types of loops in JavaScript like do...while and for...in /
for...of.

---

## 8. Comparison & Logical Operators

Comparison: >, <, >=, <=, ==, ===, !=, !==
Logical: && (AND), || (OR)

```javascript
let temp = 28;
if (temp > 20 && temp < 30) {
  console.log("Comfortable weather");
}
```

---

### Happy coding! [badrsoliman.com](https://www.badrsoliman.com)
