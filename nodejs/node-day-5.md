---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Auth & JWT - Day 5

### Badr Aldien Soliman

---

## 1. Authentication Basics

Authentication is the process of verifying who a user is. In a web app, this usually involves a username and a password.

### Identification vs. Authentication

- **Identification**: Telling the system who you are (e.g., entering your username).
- **Authentication**: Proving you are who you say you are (e.g., entering your password).

---

## 2. Basic User Registration (The Weak Way)

Initially, we might store users in a simple array. However, storing passwords in plain text is a **huge security risk**.

### The Setup

```javascript
const express = require('express');
const app = express();
app.use(express.json());

const users = [];

// GET: See all users (For testing - DON'T do this in production!)
app.get('/users', (req, res) => {
  res.json(users);
});
```

---

```javascript
// POST: Register a user (Weak - no hashing)
app.post('/users', (req, res) => {
  const user = { name: req.body.name, password: req.body.password };
  users.push(user);
  res.status(201).json({
    status: 201,
    message: 'User created successfully',
    data: user,
  });
});
```

---

## 3. Password Hashing with Bcrypt

To secure passwords, we use **Hashing**. A hash is a one-way transformation of data. If a hacker steals your database, they only see the hashes, not the actual passwords.

### Why Bcrypt?

Bcrypt is a library specifically designed for hashing passwords. It is slow by design to prevent "Brute Force" attacks and uses "Salting" to ensure identical passwords have different hashes.

---

### Understanding the Bcrypt String

When you look at a hashed password in your terminal, it looks like this:
`$2b$10$nOUIs5kJ7naTuTFkBy1veuK0kSShXueka4zF7vS8nAL6.0yhV.e2.`

It is actually a **concatenation** of several parts:

- **`$2b$`**: The version of the algorithm.
- **`$10$`**: The cost factor (how many times it was hashed).
- **The Salt**: The next 22 characters.
- **The Hash**: The final 31 characters (the "scrambled" password).

**Note**: The salt is stored in plain text inside the hash so that Bcrypt knows which salt to use when you try to log in later!

---

### Installation

```bash
npm install bcrypt
```

---

## 4. Registering with Hashing

We use `bcrypt.hash()` to scramble the password before storing it.

```javascript
const bcrypt = require('bcrypt');

app.post('/users', async (req, res) => {
  try {
    // Generate a hash (10 is the 'salt rounds' or cost factor)
    const hashedPassword = await bcrypt.hash(req.body.password, 10);

    const user = { name: req.body.name, password: hashedPassword };
    users.push(user);
    res.status(201).send();
  } catch {
    res.status(500).send();
  }
});
```

---

## 5. Logging In (Comparing Passwords)

Since hashes are one-way, we cannot "decrypt" them. To check a password, we must hash the _incoming_ password and compare it to the _stored_ hash using `bcrypt.compare()`.

---

```javascript
app.post('/users/login', async (req, res) => {
  const user = users.find(user => user.name === req.body.name);
  if (user == null) {
    return res.status(400).send('Invalid username or password');
  }
  try {
    if (await bcrypt.compare(req.body.password, user.password)) {
      res.send('Success');
    } else {
      res.send('Invalid username or password');
    }
  } catch {
    res.status(500).send();
  }
});
```

> **Security Tip**: Always use generic error messages for login failures. If you say "User not found," an attacker now knows that specific username exists in your database and can focus on brute-forcing their password (Username Enumeration).

---

## 6. Introduction to JWT

**JWT (JSON Web Token)** is a compact way to securely transmit information between parties as a JSON object. It is most commonly used for **Stateless Authentication**.

### Why JWT?

- **Stateless**: The server doesn't need to store session data. Everything is in the token.
- **Scalable**: Perfect for microservices and APIs.

### Inspecting Tokens

You can visit **[JWT.io](https://jwt.io)** to paste a token and see the data (payload) encoded inside it. **Remember**: JWTs are encoded, not encrypted. Anyone can see the data, but only the server with the secret key can verify it.

---

## 7. Setup & Environment Variables

We need to install the necessary libraries and secure our secret keys.

### Installation

```bash
npm install jsonwebtoken dotenv
```

### What is a `.env` file?

A `.env` file is used to store "Environment Variables" sensitive information like API keys or database passwords that should **never** be pushed to GitHub.

**`.env`**

```env
ACCESS_TOKEN_SECRET=your_generated_secret_here
```

---

## 8. Generating a Secure Secret

You should never just "type" a secret key. Use Node's built-in `crypto` library to generate a random 64-byte hex string.

**Run this in your terminal:**

```bash
node
> require('crypto').randomBytes(64).toString('hex')
```

Copy the resulting long string and paste it into your `.env` file as `ACCESS_TOKEN_SECRET`.

---

## 9. Signing a Token

When a user logs in successfully, we issue them a token containing their information (id, name, etc.).

```javascript
require('dotenv').config();
const jwt = require('jsonwebtoken');

app.post('/users/login', async (req, res) => {
  // ... after bcrypt.compare is successful ...
  const user = { name: req.body.name, isAdmin: req.body.isAdmin || false };

  const accessToken = jwt.sign(user, process.env.ACCESS_TOKEN_SECRET);
  res.json({ accessToken: accessToken });
});
```

---

## 10. Authentication Middleware

We create a middleware function to protect our routes. It checks the `Authorization` header for a `Bearer` token.

```javascript
function authenticateToken(req, res, next) {
  const authHeader = req.headers['authorization'];
  // Use && to check if authHeader exists before splitting
  const token = authHeader && authHeader.split(' ')[1];

  if (token == null) return res.sendStatus(401); // Unauthorized (No token)

  jwt.verify(token, process.env.ACCESS_TOKEN_SECRET, (err, user) => {
    if (err) return res.sendStatus(403); // Forbidden (Invalid token)
    req.user = user;
    next();
  });
}
```

---

## 11. Authorization (Admin Control)

Authorization is checking if a user has **permission** to do something.

```javascript
const products = [
  { id: 1, name: 'Laptop' },
  { id: 2, name: 'Phone' },
];

app.delete('/products/:id', authenticateToken, (req, res) => {
  // Check if the user from the JWT has admin rights
  if (!req.user.isAdmin) {
    return res.status(403).send('Action restricted to Admins only');
  }

  const productId = parseInt(req.params.id);
  // Logic to delete product...
  res.send(`Product ${productId} deleted by ${req.user.name}`);
});
```

---

## Summary Workflow

1. **Bcrypt**: Hash passwords on register and compare them on login.
2. **Setup**: Install `jsonwebtoken` and `dotenv`.
3. **Secrets**: Generate a secure secret for your access tokens.
4. **Sign**: Issue an access token on successful login.
5. **Verify**: Use middleware to protect routes by verifying the token using `jwt.verify`.
6. **Authorize**: Check the decoded user information to grant or deny access.

---

## 12. Self-Study: Refresh Tokens

The problem with typical tokens is that if they are stolen, an attacker has access forever until the token is revoked. To solve this, we use **short-lived Access Tokens** and **long-lived Refresh Tokens**.

### Strategy:

1. **Access Token**: Expires quickly (e.g., 15 minutes). Used for every request.
2. **Refresh Token**: Expires in days/weeks. Used only to get a _new_ Access Token.

---

# Secure the gates

## **[badrsoliman.com](https://www.badrsoliman.com)**
