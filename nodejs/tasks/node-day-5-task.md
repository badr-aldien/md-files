---
marp: true
paginate: true
theme: gaia
---

# Day 5 Assignment: Terminal "Vault" API

---

## **Objective**

Build a professional Node.js REST API for personal task management using in-memory arrays.

### **Core Stack**

- **Runtime**: Node.js & Express
- **Security**: JWT & Bcrypt
- **Storage**: In-memory Arrays (No Mongoose)

---

## **1. Initial Data Structure**

```javascript
const users = [
  { id: 1, name: 'Admin', password: '...', role: 'admin' },
  { id: 2, name: 'John', password: '...', role: 'user' },
];

const tasks = [
  { id: 1, userId: 2, title: 'Learn JWT', completed: false },
  { id: 2, userId: 2, title: 'Auth Middleware', completed: true },
];
```

---

## **2. Project Setup**

- [ ] Initialize standard NPM project.
- [ ] Required Libraries: `express`, `bcrypt`, `jsonwebtoken`, `dotenv`.
- [ ] Environment Variables: Use a `.env` file for your **Secret Keys**.

---

## **3. API Endpoints: Auth**

| Method   | Endpoint      | Access | Responsibility                |
| :------- | :------------ | :----- | :---------------------------- |
| **POST** | `/auth/login` | Public | Validate & issue signed token |

---

## **4. API Endpoints: Tasks (CRUD)**

| Method     | Endpoint     | Access | Responsibility                    |
| :--------- | :----------- | :----- | :-------------------------------- |
| **GET**    | `/tasks`     | User   | Filter `tasks` by `userId`        |
| **POST**   | `/tasks`     | User   | Push new task (link via `userId`) |
| **PATCH**  | `/tasks/:id` | User   | Update OWN task only              |
| **DELETE** | `/tasks/:id` | User   | Filter out OWN task only          |

---

## **5. Professional Constraints**

1. **Architecture**: Implement **Stateless** authentication.
2. **Security**: Ensure no sensitive fields (like password hashes) are returned in responses.
3. **Roles**: Restricted routes must verify user roles from the token.
4. **Resiliency**: Use appropriate HTTP status codes (201, 401, 403, 404).
