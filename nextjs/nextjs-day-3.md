---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Next.js Fundamentals - Day 3

### Badr Aldien Soliman

---

## 1. Mongoose & Next.js

Mongoose is the industry-standard ODM for MongoDB. In Next.js, we must handle connections carefully to avoid creating multiple instances during development.

---

### The Connection Utility
We use a **Singleton** pattern to reuse the database connection.

```typescript
import mongoose from "mongoose";

export default async function dbConnect() {
  if (mongoose.connection.readyState >= 1) return;

  try {
    await mongoose.connect(process.env.MONGODB_URI);
    console.log("Connected to MongoDB!");
  } catch (err) {
    console.error("MongoDB Connection Error: ", err);
  }
}
```

---

### Defining a Model
Always check if the model already exists to prevent errors during hot-reloads.

```typescript
// models/Task.ts
import mongoose from "mongoose";

const TaskSchema = new mongoose.Schema({
  title: { type: String, required: true },
  done: { type: Boolean, default: false },
});

export default mongoose.models.Task || mongoose.model("Task", TaskSchema);
```

---

## 2. Server Actions (The Mutation Power)

Server Actions allow you to run server-side code (like database queries) directly from your forms without building separate API routes.

---

### Example: Creating a Task

```tsx
// app/actions.ts
"use server";
import { dbConnect } from "@/lib/db";
import Task from "@/models/Task";
import { revalidatePath } from "next/cache";

export async function addTask(formData: FormData) {
  await dbConnect();
  const title = formData.get("title");

  await Task.create({ title });
  
  revalidatePath("/"); // Tells Next.js to refresh the UI immediately!
}
```

---

### Using Actions in the UI
The form calls the action directly. It even works if JavaScript is disabled!

```tsx
// app/page.tsx
import { addTask } from "./actions";

export default function Page() {
  return (
    <form action={addTask}>
      <input name="title" placeholder="New task..." required />
      <button type="submit">Add Task</button>
    </form>
  );
}
```

---

## Summary Workflow

1. **Database**: Connect via a Singleton `dbConnect` and define your **Mongoose** models.
2. **Mutations**: Use **Server Actions** for all database changes. It's faster and more secure than API routes.
3. **Synchronization**: Use `revalidatePath()` inside actions to update the UI instantly.

---


## 🛠️ Lab Task: The Mongoose Todo List

Build a Todo application that persists data to MongoDB.

### Requirements:
1. **Schema**: Create a `Task` model with `title` and `completed` (boolean).
2. **Add**: Implement a form and a Server Action to create new tasks.
3. **Delete**: Add a "Delete" button next to each task that triggers a Server Action.
4. **Toggle**: Add a checkbox that toggles the `completed` status in the database.

---

# Next.js is the cool React 🕶️

## **[badrsoliman.com](https://www.badrsoliman.com)**
