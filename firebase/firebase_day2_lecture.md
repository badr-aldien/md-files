# Day 2 - Firebase Advanced Operations

### Badr Aldien Soliman

---

## 1. Fetching a Single Document (getDoc & Realtime)

To fetch a single document from Firestore, you can use `getDoc()` for a one-time read or `onSnapshot()` for real-time updates.

```javascript
import { doc, getDoc, onSnapshot } from "firebase/firestore";

// Create a reference to a specific document
const docRef = doc(db, "students", "student1");

// Option 1: One-time fetch (realtime)
onSnapshot(docRef, (doc) => {
  console.log(doc.data(), doc.id);
});
```

**How it works:**

- `doc(db, collectionName, documentId)` creates a reference to a specific document
- `getDoc()` fetches the document once (one-time read)
- `onSnapshot()` listens for real-time changes to that specific document
- Whenever the document is updated in Firebase, `onSnapshot()` automatically updates your local data

---

## 2. Updating Documents in Firestore

To update an existing document, use the `updateDoc()` function. You can create a form similar to the add/delete forms from Day 1.

**index.html:**

```html
<form class="update">
  <label for="id">Document ID:</label>
  <input type="text" name="id" required />

  <label for="name">Name:</label>
  <input type="text" name="name" />

  <label for="age">Age:</label>
  <input type="number" name="age" />

  <label for="grade">Grade:</label>
  <input type="text" name="grade" />

  <button>Update Student</button>
</form>
```

```javascript
import { doc, updateDoc } from "firebase/firestore";

// update student
const updateStudentForm = document.querySelector(".update");
updateStudentForm.addEventListener("submit", (e) => {
  e.preventDefault();

  const docRef = doc(db, "students", updateStudentForm.id.value);

  updateDoc(docRef, {
    name: updateStudentForm.name.value,
    age: Number(updateStudentForm.age.value),
    grade: updateStudentForm.grade.value,
  }).then(() => {
    updateStudentForm.reset();
  });
});
```

**How it works:**

- `updateDoc(docRef, data)` updates specific fields in an existing document
- Only the fields you provide will be updated; other fields remain unchanged

---

## 3. Setup Firebase Authentication

### Step 1: Enable Email/Password Authentication

1. In Firebase Console, go to **"Authentication"** from the left menu
2. Click **"Get started"** (if you haven't enabled it yet)
3. Click on the **"Sign-in method"** tab
4. Click on **"Email/Password"**
5. Toggle **"Enable"** to turn it on
6. Click **"Save"**

### Step 2: Initialize Auth Service in JavaScript

```javascript
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";
import { getAuth } from "firebase/auth";

// Your Firebase configuration (replace with your own)
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
};

// 1. Initialize Firebase
const app = initializeApp(firebaseConfig);

// 2. Initialize Firestore service
const db = getFirestore(app);

// 3. Initialize Auth service
const auth = getAuth(app);
```

---

## 4. Signing Users Up

> **Note:** Firebase Auth uses JWTs for user authentication.

To create new user accounts, use the `createUserWithEmailAndPassword()` function.

**index.html:**

```html
<form class="signup">
  <label for="email">Email:</label>
  <input type="email" name="email" required />

  <label for="password">Password:</label>
  <input type="password" name="password" required />

  <button>Sign Up</button>
</form>
```

```javascript
import { createUserWithEmailAndPassword } from "firebase/auth";

// sign up
const signupForm = document.querySelector(".signup");
signupForm.addEventListener("submit", (e) => {
  e.preventDefault();

  const email = signupForm.email.value;
  const password = signupForm.password.value;

  createUserWithEmailAndPassword(auth, email, password).then((cred) => {
    console.log("user created", cred.user);
    signupForm.reset();
  });
});
```

**How it works:**

- `createUserWithEmailAndPassword(auth, email, password)` creates a new user account
- The function returns a promise with user credentials
- `cred.user` contains the newly created user object with properties like `uid`, `email`, etc.

> **Note:** Firebase automatically logs you in after signing up.

---

## 5. Logging In & Out

To sign in existing users, use the `signInWithEmailAndPassword()` function. To sign out, use the `signOut()` function.

**index.html:**

```html
<form class="login">
  <label for="email">Email:</label>
  <input type="email" name="email" required />

  <label for="password">Password:</label>
  <input type="password" name="password" required />

  <button>Log In</button>
</form>

<button class="logout">Log Out</button>
```

```javascript
import { signInWithEmailAndPassword, signOut } from "firebase/auth";

// log in
const loginForm = document.querySelector(".login");
loginForm.addEventListener("submit", (e) => {
  e.preventDefault();

  const email = loginForm.email.value;
  const password = loginForm.password.value;

  signInWithEmailAndPassword(auth, email, password).then((cred) => {
    console.log("user logged in", cred.user);
    loginForm.reset();
  });
});

// log out
const logoutButton = document.querySelector(".logout");
logoutButton.addEventListener("click", () => {
  signOut(auth).then(() => {
    console.log("user logged out");
  });
});
```

**How it works:**

- `signInWithEmailAndPassword(auth, email, password)` signs in an existing user
- `signOut(auth)` signs out the currently authenticated user
- Both functions return promises that resolve when the operation completes

---

## 6. Monitoring Authentication State (onAuthStateChanged)

To detect when a user signs in or out, use the `onAuthStateChanged()` function. This is useful for showing or hiding UI elements based on authentication status.

```javascript
import { onAuthStateChanged } from "firebase/auth";

onAuthStateChanged(auth, (user) => {
  if (user) {
    console.log("user logged in:", user);
  } else {
    console.log("user logged out");
  }
});
```

**Example: Show/Hide UI Based on Auth State**

```javascript
import { onAuthStateChanged } from "firebase/auth";

onAuthStateChanged(auth, (user) => {
  const loginForm = document.querySelector(".login");
  const signupForm = document.querySelector(".signup");
  const logoutButton = document.querySelector(".logout");

  if (user) {
    // User is signed in
    loginForm.style.display = "none";
    signupForm.style.display = "none";
    logoutButton.style.display = "block";
  } else {
    // User is signed out
    loginForm.style.display = "block";
    signupForm.style.display = "block";
    logoutButton.style.display = "none";
  }
});
```

**How it works:**

- `onAuthStateChanged(auth, callback)` listens for authentication state changes
- The callback function is called whenever the user signs in or out
- The callback receives a `user` object if signed in, or `null` if signed out
- This is useful for updating your UI automatically when authentication state changes

---

## 7. Soft Delete (Flag Instead of Remove)

Soft delete means we mark a document as deleted (e.g., `deleted: true`) instead of removing it with `deleteDoc()`. This makes it easy to restore data later or keep historical records for auditing.

**index.html:**

```html
<form class="soft-delete">
  <label for="id">Document ID:</label>
  <input type="text" name="id" required />

  <button>Soft Delete Student</button>
</form>
```

```javascript
import {
  doc,
  updateDoc,
  query,
  where,
  onSnapshot,
  collection,
  serverTimestamp,
} from "firebase/firestore";

// soft delete student
const softDeleteForm = document.querySelector(".soft-delete");
softDeleteForm.addEventListener("submit", (e) => {
  e.preventDefault();

  const docRef = doc(db, "students", softDeleteForm.id.value);

  updateDoc(docRef, {
    deleted: true,
    deletedAt: serverTimestamp(),
  }).then(() => {
    console.log("student soft deleted");
    softDeleteForm.reset();
  });
});

// query only active students
const studentsQuery = query(
  collection(db, "students"),
  where("deleted", "!=", true)
);

onSnapshot(studentsQuery, (snapshot) => {
  let activeStudents = [];
  snapshot.docs.forEach((doc) => {
    activeStudents.push({ ...doc.data(), id: doc.id });
  });
  console.log("Active students:", activeStudents);
});
```

**How it works:**

- `updateDoc()` adds `deleted` and `deletedAt` fields without removing the document
- `where("deleted", "!=", true)` filters out documents that were marked as deleted
- You can restore a document by updating `deleted` back to `false`

---

## Task: OAuth Signup + Protected CRUD

1. **Add a provider:** enable Google, Facebook, or GitHub under Authentication → Sign-in method, then use the matching SDK helper (e.g., `GoogleAuthProvider` + `signInWithPopup`).
2. **Wire the UI:** add a “Continue with …” button that signs the user in via the provider and reuse the existing logout button.
3. **Gate CRUD actions:** only allow fetching/updating/deleting students when a user is signed in. Disable/hide the forms or show a message until `onAuthStateChanged` reports a user.
4. **Handle UI changes:** show a logout button in your navbar when the user is signed in, and display a “Log in first” message on CRUD pages when no user is authenticated.

> Goal: no authenticated user = no CRUD. Make sure the flow feels seamless before moving on.

---

### Happy coding! [badrsoliman.com](https://www.badrsoliman.com)
