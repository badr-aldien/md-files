# Node.js — Day 2 Task

**Goal:** Build a persistent Book Management API using Express and the MVC pattern.

---

## The Scenario

You are building a **Book Management API**. All books must be saved to and retrieved from a `books.json` file.

---

## Project Structure

Your project MUST follow this structure:

```
book-manager/
├── data/
│   └── books.json      ← Your "database"
├── controllers/
│   └── bookController.js
├── routes/
│   └── bookRoutes.js
├── app.js
└── package.json
```

---

## Functional Requirements

### 1. Data Persistence

- All book data must reside in `data/books.json`.
- The file should stay updated after every "Create", "Update", or "Delete" operation.

### 2. API Endpoints

Your API should handle the following routes under the `/api/books` prefix:

| Method     | Endpoint | Description                                         |
| :--------- | :------- | :-------------------------------------------------- |
| **GET**    | `/`      | Retrieve the full list of books from the JSON file. |
| **POST**   | `/`      | Add a new book (with a unique ID) to the file.      |
| **PATCH**  | `/:id`   | Update the details of a specific book by its ID.    |
| **DELETE** | `/:id`   | Remove a specific book from the file by its ID.     |

### 3. Server Logic

- Use **Express Router** to manage your routes.
- Implement a **404 Catch-all** middleware for any undefined routes.
- Ensure the server can parse incoming JSON data in the request body.

### 4. Middleware Task

- Create a custom **Logger Middleware** that prints the HTTP method and request URL (e.g., `GET /api/books`) to the console for every request.

---

## Expected Testing Flow

1. **Create:** Add a book like `{"title": "The Hobbit", "author": "J.R.R. Tolkien"}`.
2. **Read:** Fetch the list to see your new book with its generated ID.
3. **Update:** Change the title or author of that specific book.
4. **Delete:** Remove the book and verify it is gone from both the API response and the `books.json` file.
