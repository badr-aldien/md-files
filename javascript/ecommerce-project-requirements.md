---
marp: true
paginate: true
theme: gaia
---



## 1. Project Overview

Build a simple, functional E-commerce landing page using HTML, CSS, and Vanilla JavaScript.

**Objective:**
- Implement core UI components.
- Manage user authentication state.
- Create conditional navigation and access control.

---

## 2. Core UI Components

### 🏗️ Required Sections
1. **Navbar**: Navigation for all pages/actions.
2. **Product Grid**: Display items available for "purchase".
3. **Footer**: Simple contact/info section.

---

## 3. Navbar Requirements

The Navbar must dynamically change based on whether the user is **Logged In** or **Logged Out**.

| Feature | Logged Out | Logged In |
| :--- | :---: | :---: |
| **Home** | ✅ | ✅ |
| **About** | ✅ | ✅ |
| **Cart** | ✅ | ✅ |
| **Profile** | ❌ | ✅ |
| **Login/Register** | ✅ | ❌ |

---

## 4. Authentication (Auth)

### 🔐 Features
- **Registration**: Form with validation (Email, Password).
- **Login**: Validate credentials against stored user data.
- **Validation Rules**: 
    - Email must be valid format.
    - Password must be at least 6 characters.

---

## 5. Authorization & Access Control

### 🛂 Navigation Guards
- **Profile Page**: Only accessible if `isLoggedIn === true`.
- **Registration Page**: If `isLoggedIn === true`, redirect the user back to Home (they shouldn't register again).

---

## 6. Cart & Purchasing

### 🛍️ Interactions
- **Add to Cart**: All users (Logged In or Guest) can add products to the cart.
- **Purchase/Checkout**: 
    - If user is **Logged In**: Proceed to checkout.
    - If user is **Guest**: Show an alert/modal saying *"Please log in to complete your purchase"*.




