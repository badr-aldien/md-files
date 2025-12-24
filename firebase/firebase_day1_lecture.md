# Day 1 - Introduction to Firebase

### Badr Aldien Soliman

---

## 1. What is Firebase?

Firebase is a Backend-as-a-Service (BaaS) platform by Google that provides ready-to-use backend services for web and mobile applications.

**Key Features:**

- **Firestore Database** – Real-time NoSQL database
- **Authentication** – User sign-in and management
- **Hosting** – Deploy web apps quickly
- **Storage** – Store files like images and videos
- **Cloud Functions** – Run backend code without servers

**Why Firebase?**

- ✅ No backend coding required
- ✅ Real-time data synchronization
- ✅ Scalable and secure
- ✅ Fast development and deployment
- ✅ Free tier available for learning and small projects

---

## 2. Firebase Setup

### Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"**
3. Enter project name (e.g., "my-first-firebase-app")
4. Follow the setup wizard (disable Google Analytics for simplicity)
5. Click **"Create project"**

### Step 2: Register Your Web App

1. In your Firebase project, click the **Web icon** (`</>`)
2. Give your app a nickname (e.g., "My Web App")
3. Click **"Register app"**

---

## 3. Create a Vanilla JavaScript Project (or Library/Framework), With or Without Vite

To quickly start a modern JavaScript project, use [Vite](https://vitejs.dev/), which is a build tool and bundler.

**Steps:**

1. Open your terminal and run:

   ```bash
   npm create vite@latest my-firebase-app -- --template vanilla
   cd my-firebase-app
   npm install
   ```

2. To start your project, run:
   ```bash
   npm run dev
   ```

**What is a Bundler?**  
A bundler (like Vite) combines your code and dependencies into files that browsers can use. It makes development faster and easier with modern features.

---

## 4. Initialize Firebase in JavaScript

```javascript
// Import Firebase modules from npm package
import { initializeApp } from "firebase/app";

// Your Firebase configuration (replace with your own)
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
```

## 5. Setup Firestore Database

### Step 1: Enable Firestore

1. In Firebase Console, go to **"Firestore Database"** from the left menu
2. Click **"Create database"**
3. Choose **"Start in test mode"** (for development only)
4. Select a location (choose closest to you)
5. Click **"Enable"**

### Step 2: Create a Collection Manually

1. Click **"Start collection"**
2. Enter collection ID: `students`
3. Click **"Next"**
4. Add the first document:
   - Document ID: `student1` (or leave auto-generated)
   - Add fields:
     - Field: `name` | Type: `string` | Value: `Ali Ahmed`
     - Field: `age` | Type: `number` | Value: `20`
     - Field: `grade` | Type: `string` | Value: `A`
5. Click **"Save"**
6. Add more documents if you like (e.g., `student2`, `student3`)

---

## 6. Setup Firestore in JavaScript

```javascript
import { initializeApp } from "firebase/app";
import { getFirestore, collection, doc } from "firebase/firestore";

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

// 3. Initialize collection reference
const studentsCollection = collection(db, "students");

console.log("Firebase initialized successfully!");
```

---

## 7. Fetching All Documents in the Collection

To fetch all documents from the `students` collection:

```javascript
import { getDocs } from "firebase/firestore";

let students = [];

// Fetching data inside the collection
getDocs(studentsCollection)
  .then((snapshot) => {
    snapshot.docs.forEach((doc) => {
      students.push({ ...doc.data(), id: doc.id });
    });
    console.log(students);
  })
  .catch((err) => console.error(err));
```

---

## 8. Adding/Deleting in Firestore

**index.html:**

```html
<form class="add">
  <label for="name">Name:</label>
  <input type="text" name="name" required />

  <label for="age">Age:</label>
  <input type="number" name="age" required />

  <label for="grade">Grade:</label>
  <input type="text" name="grade" required />

  <button>Add Student</button>
</form>

<form class="delete">
  <label for="id">Document ID:</label>
  <input type="text" name="id" required />

  <button>Delete Student</button>
</form>
```

```javascript
// add new student
const addStudentForm = document.querySelector(".add");
addStudentForm.addEventListener("submit", (e) => {
  e.preventDefault();

  addDoc(colRef, {
    name: addStudentForm.name.value,
    age: Number(addStudentForm.age.value),
    grade: addStudentForm.grade.value,
  }).then(() => {
    addStudentForm.reset();
  });
});

// delete student
const deleteStudentForm = document.querySelector(".delete");
deleteStudentForm.addEventListener("submit", (e) => {
  e.preventDefault();

  const docRef = doc(db, "students", deleteStudentForm.id.value);

  deleteDoc(docRef).then(() => {
    deleteStudentForm.reset();
  });
});
```

---

## 8. Realtime Collection Data (onSnapshot)

```javascript
// Listen for real-time updates on the "students" collection
onSnapshot(colRef, (snapshot) => {
  let students = [];
  snapshot.docs.forEach((doc) => {
    students.push({ ...doc.data(), id: doc.id });
  });
  console.log("Current students:", students);
});
```

**How it works:**

- `onSnapshot()` listens to changes in the collection
- Whenever data is added, updated, or deleted in Firebase, the UI updates automatically
- No need to refresh the page!

---

## 9. Firestore Queries (Filtering and Sorting)

You can use Firestore's query capabilities to filter and sort documents in your collections.

> **Note:**  
> Combining multiple query clauses (like `where` and `orderBy`) may require a Firestore composite index.

```javascript
// Import Firestore query helpers
import { query, where, orderBy, onSnapshot } from "firebase/firestore";
```

**Example 1: Get all students in grade "A"**

```javascript
const q1 = query(colRef, where("grade", "==", "A"));

onSnapshot(q1, (snapshot) => {
  let studentsInGradeA = [];
  snapshot.docs.forEach((doc) => {
    studentsInGradeA.push({ ...doc.data(), id: doc.id });
  });
  console.log("Students in grade A:", studentsInGradeA);
});
```

**Example 2: Get all students older than 16**

```javascript
const q2 = query(colRef, where("age", ">", 16));

onSnapshot(q2, (snapshot) => {
  let studentsOlderThan16 = [];
  snapshot.docs.forEach((doc) => {
    studentsOlderThan16.push({ ...doc.data(), id: doc.id });
  });
  console.log("Students older than 16:", studentsOlderThan16);
});
```

**Example 3: Get all students in grade "B" and order them by age**

```javascript
const q3 = query(colRef, where("grade", "==", "B"), orderBy("age"));

onSnapshot(q3, (snapshot) => {
  let studentsInGradeB = [];
  snapshot.docs.forEach((doc) => {
    studentsInGradeB.push({ ...doc.data(), id: doc.id });
  });
  console.log("Students in grade B, ordered by age:", studentsInGradeB);
});
```

**Example 4: Order students by server timestamp**

To use server timestamps for record creation, add your documents with a `createdAt` field using Firestore's `serverTimestamp`. Import it like this:

```javascript
import { serverTimestamp, addDoc } from "firebase/firestore";
```

Then, when adding a document:

```javascript
addDoc(colRef, {
  name: "New Student",
  age: 22,
  grade: "C",
  createdAt: serverTimestamp(),
});
```

Now you can query and order by `createdAt`:

```javascript
const q4 = query(colRef, orderBy("createdAt", "desc"));

onSnapshot(q4, (snapshot) => {
  let studentsByTime = [];
  snapshot.docs.forEach((doc) => {
    studentsByTime.push({ ...doc.data(), id: doc.id });
  });
  console.log("Students ordered by creation time:", studentsByTime);
});
```

**Explanation:**

- `where(field, operator, value)` filters documents based on specific criteria.
- `orderBy(field)` sorts the returned documents.
- `query()` lets you combine multiple clauses.
- `onSnapshot()` listens for real-time updates based on the query.

---

## Summary

✅ Learned what Firebase is and why it's useful  
✅ Set up a Firebase project and Firestore database  
✅ Created a collection manually in Firebase Console  
✅ Initialized Firebase in vanilla JavaScript  
✅ Fetched data by ID using `getDoc()`  
✅ Added data using `addDoc()`  
✅ Deleted data using `deleteDoc()`  
✅ Implemented real-time updates with `onSnapshot()`

---

## Tasks/Exercises

### Exercise 1: Setup

- Create a collection called `employees` in Firestore
- Add at least 3 documents with fields: `name`, `department`, `salary`, `rating`

### Exercise 2: Display Employees

- Use `onSnapshot()` to listen for real-time updates on the `employees` collection
- Display all employees on the webpage in a list format

### Exercise 3: Add and Delete Forms

- Create an HTML form to add new employees (name, department, salary, rating)
- Create an HTML form to delete employees by document ID
- Use `addDoc()` and `deleteDoc()` to perform the operations

### Exercise 4: Queries

- Filter employees with rating >= 4
- Sort employees by salary (ascending)
- Create a combined query: employees with rating >= 4, ordered by salary

### Exercise 5: Timestamps

- Add `createdAt` when creating new employees
- Query employees ordered by `createdAt` in descending order (newest first)

### Exercise 6: Complete Employee Management App

Create a complete app with a good UI and:

- Real-time display of all employees
- Add and delete employee forms
- Filter employees by rating (dropdown)
- Sort button to sort employees by different criteria (salary, rating, creation date)
- Display employee count
- Show loading states while fetching data

---

### Happy coding! [badrsoliman.com](https://www.badrsoliman.com)
