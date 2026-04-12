---
marp: true
theme: default
paginate: true
backgroundColor: #f0f2f5
---

# JavaScript Day 5 Tasks

---

## Assignment 1: Fetch and List Products (XHR)

Create a button that, when clicked, fetches product data from the following API:
`https://itireact-native-day3.vercel.app/products`

**Requirements:**

- Use `XMLHttpRequest` to get the data.
- Once the data is successfully fetched (status 200), parse the JSON.
- Display each product's **title**, **price**, **thumbnail**, **images** (gallery), **colors**, and **description** in a clean, vertical list on the page.
- **BONUS**: A details button for each product that, when clicked, displays the product's details in a modal/page.

---

## Assignment 2: Persistent Counter

Develop a simple counter application with two buttons: "Count Up" and "Reset".

**Requirements:**

- The count should be displayed in a large font.
- Use `localStorage` to save the current count.
- When the page is **refreshed**, the count should not reset to 0; it should load the last saved value from `localStorage`.

---

## Assignment 3: XHR Ready State Logger

Perform a basic XHR request and use the `onreadystatechange` event to track every status change of the request.

- Print each `readyState` value (1, 2, 3, 4) in the console as it happens.
- Once `readyState` reaches **4**, display the JSON response in a `div` on the page.

---

## Assignment 4: User Settings Persistence

Create a dropdown (Select) with two themes: **"Classic Light"** and **"Dracula Dark"**.

**Requirements:**

- When a user selects a theme, apply the corresponding CSS styles immediately.
- Use `localStorage` to save the user's theme preference.
- On page load, check if a theme is saved and automatically apply it.
