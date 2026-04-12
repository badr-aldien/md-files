---
marp: true
paginate: true
theme: gaia
---

# Task - Day 4: Bookstore Management System

---

## 1. Database Requirements

Create a **Book** schema in a `models/Book.js` file with the following fields:

- **Title**: String, required, trimmed.
- **Author**: String, required.
- **Price**: Number, minimum of 0.
- **Category**: String, only allowed values are: 'Fiction', 'Non-Fiction', 'Science', 'History'.
- **Stock**: Number, default value of 0.

---

## 2. API Endpoints (Part 1)

Implement the following functionality in your Express application:

1. **Add a New Book**
   - **URL**: `POST /books`

2. **View All Books**
   - **URL**: `GET /books`

---

## 3. API Endpoints (Part 2)

3. **Find a Specific Book**
   - **URL**: `GET /books/:id`

4. **Update Book Details**
   - **URL**: `PUT /books/:id`
5. **Remove a Book**
   - **URL**: `DELETE /books/:id`

---

## 5. Specific Filter (Query)

6. **Filter Books by Category**
   - **URL**: `GET /books?category=Science`
   - Update your "View All Books" logic to allow users to filter books by their category using a **query string**.
   - If a category is specified in the URL, only books matching that category should be returned.

---

## 🚀 Bonus Task: Restock logic

7. **Increment Stock Count**
   - **URL**: `PATCH /books/:id/restock`
   - Create a route that allows you to **add** to the current stock.
   - Example: If the book has 5 copies and you send 10, the new stock should be 15.
   - _Challenge_: Can you do this without sending the total number?
