---
marp: true
paginate: true
---

# JavaScript - Day 4

### DOM Manipulation & Events

##### Badr Aldien Soliman

---

## 1. Element Selectors

```html
<h1 id="mainTitle">Main Title</h1>
<h2 class="subTitle">Sub Title 1</h2>
<h2 class="subTitle">Sub Title 2</h2>
<p>Some paragraph text here...</p>
```

```js
// Select by ID
let title = document.getElementById('mainTitle');
title.style.color = 'blue';

// Select by class name
let firstSubtitle = document.getElementsByClassName('subTitle')[0];
firstSubtitle.style.fontWeight = 'bold';

// Select by tag name
let firstParagraph = document.getElementsByTagName('p')[0];
firstParagraph.style.background = 'lightyellow';
```

---

## 2. Incrementing & Decrementing Values

```html
<h2>Counter: <span id="counter">0</span></h2>
<button onclick="increment()">+</button>
<button onclick="decrement()">-</button>
```

```js
function increment() {
  let counter = document.getElementById('counter');
  counter.innerText = Number(counter.innerText) + 1;
}

function decrement() {
  let counter = document.getElementById('counter');
  let currentValue = Number(counter.innerText);
  if (currentValue > 0) {
    counter.innerText = currentValue - 1;
  }
}
```

---

## 3. Selecting Multiple Elements

```js
function highlightTitles() {
  // Select all elements with class "title"
  const titles = document.getElementsByClassName('title');

  // Loop using index
  for (let i = 0; i < titles.length; i++) {
    titles[i].style.color = 'blue';
    titles[i].style.textTransform = 'uppercase';
  }

  // Loop using for...of
  for (let title of titles) {
    title.style.borderBottom = '2px solid black';
  }
}
```

---

## 4. innerText vs innerHTML

```js
// Treats the value as plain text: tags are displayed literally
document.getElementById('header').innerText = '<h1>Hello World</h1>';

// Treats the value as HTML: tags are rendered by the browser
document.getElementById('header').innerHTML = '<h1>Hello World</h1>';
```

> Use `innerText` when working with plain text.
> Use `innerHTML` when you need to inject actual HTML elements.

---

## 5. Event Handling

```html
<button id="btn1">Click Me!</button>
```

```js
function displayHello(event) {
  // event.target refers to the element that was clicked
  event.target.innerText = 'Hello World!';
}

document.getElementById('btn1').addEventListener('click', displayHello);
```

> `addEventListener` keeps your HTML and JavaScript separate: preferred over `onclick`.

---

## 6. Forms & Input Handling

### Without a Form Tag

```html
<input type="text" id="username" placeholder="Enter your name" />
<input type="email" id="email" placeholder="Enter your email" />
<button onclick="showFormData()">Submit</button>
<p id="output"></p>
```

```js
function showFormData() {
  const username = document.getElementById('username').value;
  const email = document.getElementById('email').value;
  document.getElementById('output').innerText =
    `Hello ${username}, your email is ${email}`;
}
```

---

### With a Form Tag

```html
<form id="myForm">
  <input type="text" id="username" placeholder="Enter your name" />
  <input type="email" id="email" placeholder="Enter your email" />
  <button type="submit">Submit</button>
</form>
<p id="output"></p>
```

```js
function showFormData(event) {
  // Prevent the page from refreshing on submit
  event.preventDefault();
  const username = document.getElementById('username').value;
  const email = document.getElementById('email').value;
  document.getElementById('output').innerText =
    `Hello ${username}, your email is ${email}`;
}

document.getElementById('myForm').addEventListener('submit', showFormData);
```

---

## 7. Creating & Inserting Elements

```html
<input type="text" id="itemInput" placeholder="Add an item" />
<button onclick="addItem()">Add</button>
<ul id="itemList"></ul>
```

```js
function addItem() {
  const input = document.getElementById('itemInput');

  // Create a new <li> element
  const li = document.createElement('li');
  li.innerText = input.value;

  // Append it to the list
  document.getElementById('itemList').appendChild(li);

  // Clear the input field
  input.value = '';
}
```

---

## 8. Adding & Reading Attributes

📖 [MDN: Element.setAttribute](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)

When you open it, look for how to:

- **Set** an attribute: `setAttribute(name, value)`
- **Get** an attribute: `getAttribute(name)`
- **Set directly** via property: `img.src`, `img.alt`, `input.disabled`

---

## Key Concepts Review

- **`getElementById`**: select one element by its ID
- **`getElementsByClassName`**: select multiple elements by class
- **`innerText`**: set or get plain text content
- **`innerHTML`**: set or get HTML content
- **`addEventListener`**: attach events without mixing JS into HTML
- **`event.preventDefault()`**: stop the browser's default behavior
- **`createElement`**: create a new HTML element from scratch
- **`appendChild`**: insert a new element into the page

---

### Self Study

- Practice selecting elements with `querySelector` and `querySelectorAll`
- Experiment with more DOM events: `mouseover`, `keyup`
- Explore removing elements with `removeChild`

---

# The DOM is just a tree. Learn to climb it.

## **[badrsoliman.com](https://www.badrsoliman.com)**
