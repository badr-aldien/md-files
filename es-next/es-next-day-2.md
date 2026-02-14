---
marp: true
paginate: true
---

# ES Next: Day 2

### Badr Aldien Soliman

---

## 1. Set and Map

### Set

A collection of **unique** values.

```javascript
const mySet = new Set([1, 2, 2, 3]);

mySet.add(4); // Adds 4
mySet.has(2); // true
mySet.delete(1); // Removes 1
console.log(mySet.size); // 3
mySet.clear(); // Removes all elements
```

---

### Map

A collection of keyed data items. Keys can be of **any type**.

```javascript
const myMap = new Map();

myMap.set('name', 'Badr'); // Sets key 'name' to 'Badr'
myMap.set(1, 'one');
myMap.get('name'); // 'Badr'
myMap.has(1); // true
myMap.delete(1); // Removes key 1
console.log(myMap.size); // 1
myMap.clear(); // Removes all entries
```

---

## 2. Classes (Function Constructor to Classes)

### What is a Class?

Classes are **syntactic sugar** over JavaScript's prototype-based inheritance. They provide a cleaner syntax to create objects and handle inheritance.

---

### Traditional Constructor

```javascript
function Person(name) {
  this.name = name; // Property defined on instance
  this.sayHi = function () {
    console.log('Hi');
  }; // Method on instance
}
Person.prototype.greet = function () {
  console.log(this.name); // Method on prototype
};
```

---

### Class Structure

```javascript
class Animal {
  type = 'Unknown';
}
const pet = new Animal();
```

---

### The Constructor & Properties

The `constructor` is a special method for creating and initializing an object. It runs automatically when `new` is used.

---

```javascript
class Person {
  static type = 'Human'; // Static property
  #id = 123; // Private property (ES2022)

  constructor(name) {
    this.name = name; // Defining properties on the instance

    // Method in constructor -> Added to each INSTANCE
    this.jump = function () {
      console.log('Jumping!');
    };
  }

  // Method in class body -> Added to the PROTOTYPE
  sayHello() {
    console.log(`Hi, I'm ${this.name}`);
  }
}
```

---

### Inheritance

```javascript
class Teacher extends Person {
  constructor(name, subject) {
    super(name); // Must call super() to use 'this' and parent logic
    this.subject = subject;
  }
}
```

---

## 3. Modules

Standard way to share code.

### Exporting & Destructuring Imports

```javascript
// math.js
export const add = (a, b) => a + b;
export const sub = (a, b) => a - b;

// main.js
import { add, sub } from './math.js';
```

---

# Happy coding!

## **[badrsoliman.com](https://www.badrsoliman.com)**
