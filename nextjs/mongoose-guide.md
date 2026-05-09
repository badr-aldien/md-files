---
marp: true
paginate: true
backgroundColor: #ffffff
theme: default
style: |
  section {
    font-family: 'Inter', sans-serif;
    color: #333;
  }
  h1 {
    color: #0070f3;
  }
  code {
    background: #f4f4f4;
    color: #d1105a;
  }
---

# Connecting Mongoose to Next.js (TSX)
### Professional Guide for Full-Stack Developers

---

## 1. Why Mongoose?

- **ODM (Object Data Modeling)**: Provides a straight-forward, schema-based solution to model your application data.
- **Validation**: Built-in schema validation.
- **Type Safety**: Works perfectly with TypeScript to ensure your data follows the rules.
- **Middleware**: Hooks for pre/post-save logic.

---

## 2. Installation

First, install Mongoose in your Next.js project:

```bash
npm install mongoose
```

And if you are using TypeScript (recommended), you usually don't need extra types as they are included in the main package now.

---

## 3. Environment Setup

Never hardcode your connection string! Add it to `.env.local`:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/myDatabase
```

---

## 4. The Connection Utility (Singleton)

In Next.js development, the server restarts frequently. We must prevent creating multiple connections.

```typescript
// src/lib/db.ts
import mongoose from "mongoose";

const MONGODB_URI = process.env.MONGODB_URI!;

if (!MONGODB_URI) {
  throw new Error("Please define the MONGODB_URI environment variable");
}

let cached = (global as any).mongoose;

if (!cached) {
  cached = (global as any).mongoose = { conn: null, promise: null };
}

async function dbConnect() {
  if (cached.conn) return cached.conn;

  if (!cached.promise) {
    cached.promise = mongoose.connect(MONGODB_URI).then((m) => m);
  }
  cached.conn = await cached.promise;
  return cached.conn;
}

export default dbConnect;
```

---

## 5. Defining a Model (TSX/TS)

Create a schema and a model. Use `mongoose.models` to avoid re-compiling the model on every hot-reload.

```typescript
// src/models/Todo.ts
import mongoose, { Schema, Document } from "mongoose";

export interface ITodo extends Document {
  title: string;
  completed: boolean;
}

const TodoSchema = new Schema({
  title: { type: String, required: true },
  completed: { type: Boolean, default: false },
});

export default mongoose.models.Todo || 
       mongoose.model<ITodo>("Todo", TodoSchema);
```

---

## 6. Usage in a Server Action

```tsx
// src/app/actions.ts
"use server";
import dbConnect from "@/lib/db";
import Todo from "@/models/Todo";

export async function addTodo(formData: FormData) {
  await dbConnect(); // Ensure DB is connected
  
  const title = formData.get("title");
  
  const newTodo = await Todo.create({
    title,
    completed: false
  });

  return JSON.parse(JSON.stringify(newTodo));
}
```

---

## 7. Summary

1. **Install** mongoose.
2. **Setup** `.env.local` with your URI.
3. **Create** a singleton connection helper (`dbConnect`).
4. **Define** your Schemas and Models.
5. **Connect** inside your Server Actions or Route Handlers before querying.

---

# Happy Coding! 🚀
## **[badrsoliman.com](https://www.badrsoliman.com)**
