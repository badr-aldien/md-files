---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Mongoose & Schemas - Day 4

### Badr Aldien Soliman

---

## 1. Introduction to Mongoose

Mongoose is an **ODM** (Object Data Modeling) library for MongoDB and Node.js. It manages relationships between data, provides schema validation, and is used to translate between objects in code and the representation of those objects in MongoDB.

### Why use Mongoose?

- **Schemas**: Defines the structure of your documents.
- **Validation**: Ensures data follows specific rules before saving.
- **Consistency**: Helps maintain a predictable data structure.

---

## 2. Installation & Connection

First, install the mongoose package in your project:

```bash
npm install mongoose
```

### Connecting to MongoDB

We use `mongoose.connect()` to establish a connection to our database.

```javascript
const mongoose = require('mongoose');

const dbURI = 'mongodb://localhost:27017/my_database';

mongoose
  .connect(dbURI)
  .then(() => console.log('Connected to DB'))
  .catch(err => console.log('Connection error:', err));
```

---

## 3. What is a Schema?

While MongoDB is schemaless (you can put any data in any collection), Mongoose allows us to define a **Schema**.

A Schema defines the **shape** and **structure** of the documents inside a particular collection. It maps to a MongoDB collection and defines the types of data allowed.

---

## 4. Creating a Schema & Model

It is best practice to keep your schemas in a separate folder (e.g., `models/`).

**`models/User.js`**

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// 1. Define the Schema
const userSchema = new Schema({
  name: String,
  age: Number,
});

// 2. Create and Export the Model
// 'User' will automatically look for a collection named 'users'
module.exports = mongoose.model('User', userSchema);
```

---

## 5. Using the Model

Once exported, we can use the model in our main file to interact with the database.

### Method 1: New Instance & Save

```javascript
const User = require('./models/User');

const newUser = new User({
  name: 'John Doe',
  age: 25,
});

newUser
  .save()
  .then(result => console.log('User Saved:', result))
  .catch(err => console.log(err));
```

---

### Method 2: Model.create() (One-liner)

Instead of creating an instance first, we can do it all in one step:

```javascript
User.create({
  name: 'Jane Smith',
  age: 30,
})
  .then(result => console.log('User Created:', result))
  .catch(err => console.log(err));
```

---

## 6. Deep Dive: Schema Data Types

Schemas can handle much more than just strings and numbers. Let's expand our `User` schema.

```javascript
const userSchema = new Schema({
  name: String,
  email: String,
  hobbies: [String], // Array of strings
  address: {
    // Nested object
    city: String,
    zip: Number,
  },
  createdAt: {
    type: Date,
    default: Date.now,
  },
  updatedAt: Date,
});
```

### 🚀 The Better Way: `{ timestamps: true }`

Instead of manually defining `createdAt` and `updatedAt`, Mongoose can handle this for you. Simply pass an options object as the second argument.

```javascript
const userSchema = new Schema(
  {
    name: String,
    email: String,
  },
  { timestamps: true }, // Automatically adds createdAt & updatedAt
);
```

---

### Complex Schemas: Nested Schemas

If a nested object is complex, it's better to define it as its own schema first.

```javascript
const addressSchema = new Schema({
  city: String,
  street: String,
  zip: Number,
});

const userSchema = new Schema({
  name: String,
  address: addressSchema, // Using nested schema
});
```

---

## 7. Handling Type Errors

Mongoose performs **casting**. If you try to save a `String` into a field defined as a `Number`, Mongoose will try to convert it. If it fails, it throws a **ValidationError**.

```javascript
try {
  await User.create({ age: 'Not A Number' });
} catch (error) {
  console.log('Error caught:', error.message);
  // Output: User validation failed: age: Cast to Number failed...
}
```

---

## 8. Schema Validation

We can pass an object to define rules like `required`, `lowercase`, and `immutable`.

```javascript
const userSchema = new Schema({
  username: {
    type: String,
    required: true,
    lowercase: true,
    minLength: 3,
  },
  registeredAt: {
    type: Date,
    immutable: true, // Cannot be changed once set
    default: () => Date.now(),
  },
});
```

---

### Number & String Validation

- **Numbers**: `min`, `max`.
- **Strings**: `minLength`, `maxLength`, `enum` (only allowed values).

```javascript
const productSchema = new Schema({
  price: {
    type: Number,
    min: 1,
    max: 1000,
  },
  category: {
    type: String,
    enum: ['Electronics', 'Books', 'Clothing'],
  },
});
```

---

## 9. Custom Validators

If built-in validators aren't enough, you can write your own manual validation logic.

```javascript
const userSchema = new Schema({
  age: {
    type: Number,
    validate: {
      validator: function (v) {
        return v % 2 === 0; // Only allow even numbers
      },
      message: props => `${props.value} is not an even number!`,
    },
  },
});
```

---

## 10. Basic Queries

Querying in Mongoose is **asynchronous**, so we always use `async/await` (or `.then()`).

### `findById(id)`

Fetches a single document by its `_id`.

```javascript
const user = await User.findById('60d5ec123...');
```

---

### `find({})`

Returns an **array** of all documents matching the criteria. Passing an empty object `{}` returns all documents in the collection.

```javascript
// Find all users named 'John'
const users = await User.find({ name: 'John' });

// Using operators in find
const results = await User.find({
  age: { $gt: 18 },
  email: { $exists: true },
});
```

---

## 11. Deleting Documents

### `deleteOne` & `deleteMany`

- `deleteOne()`: Deletes the first document that matches the criteria.
- `deleteMany()`: Deletes all documents that match.

```javascript
await User.deleteOne({ name: 'John' });
```

---

### ⚠️ Warning: Validation & Middleware

Avoid using methods like `findOneAndDelete`, `findOneAndUpdate`, or `updateMany` unnecessarily.

> **Note**: These methods **do not** trigger Mongoose schema validation by default. You can enable validation by passing `{ runValidators: true }`, and return the updated document with `{ new: true }`.
>
> ```javascript
> await User.findOneAndUpdate(
>   { name: 'John' },
>   { age: 30 },
>   { new: true, runValidators: true },
> );
> ```

---

## 12. Chainable Query Building

Mongoose provides a powerful, readable way to build queries using `.where()`.

```javascript
const users = await User.where('age')
  .gt(18)
  .lt(65)
  .where('name')
  .equals('Badr')
  .limit(5) // Limit results to 5
  .select('name age') // Only return 'name' and 'age' fields
  .exec(); // Executes the query
```

---

## 13. Integration with Express

Using Mongoose with Express allows you to create APIs that interact with your database.

### `POST`: Create a Record

```javascript
app.post('/users', async (req, res) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json(user);
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
});
```

---

### `PUT`: Update a Record

We use `findByIdAndUpdate` with `{ runValidators: true }` to ensure schema rules are followed during updates.

```javascript
app.put('/users/:id', async (req, res) => {
  try {
    const user = await User.findByIdAndUpdate(req.params.id, req.body, {
      new: true, // Return the modified document
      runValidators: true,
    });
    res.status(200).json(user);
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
});
```

---

## 14. Middleware: `pre` hooks

Mongoose middleware (pre-hooks) allow you to run functions **before** certain events like saving or validating.

### `pre('validate')`

Runs before the document is validated against the schema. Good for formatting data (e.g., trimming strings).

```javascript
userSchema.pre('validate', function (next) {
  this.name = this.name.trim(); // 'this' refers to the document
  next();
});
```

---

### `pre('save')`

Runs before the document is saved to the database. Practical for updating timestamp fields or logic before saving.

> **Note**: For `createdAt` and `updatedAt`, use the built-in `{ timestamps: true }` option instead of manual hooks.

```javascript
userSchema.pre('save', function (next) {
  this.updatedAt = Date.now();
  next();
});
```

---

## Summary Workflow

1. **Install**: Use `npm install mongoose`.
2. **Connect**: Use `mongoose.connect()`.
3. **Define Schema**: Specify structure and validation rules.
4. **Export Model**: Use `mongoose.model()`.
5. **Save Data**: Use `.save()` or `Model.create()`.
6. **Queries**: Use `findById`, `find`, and `findOne`.
7. **Deletion**: Use `deleteOne` or `deleteMany`.
8. **Query Builder**: Use `.where()` to chain methods.
9. **Express Integration**: Use models inside routes for REST APIs (POST, PUT, GET, DELETE).
10. **Middleware**: Use `.pre()` hooks for logic before saving/validating.

---

# Trust the Schema

## **[badrsoliman.com](https://www.badrsoliman.com)**
