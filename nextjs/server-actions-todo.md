---
marp: true
paginate: true
backgroundColor: #f0f4f8
theme: default
style: |
  section {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  h1 {
    color: #1a202c;
    border-bottom: 3px solid #3182ce;
  }
  .compare {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
---

# Server Actions vs. Traditional APIs
### Building a Todo List in Next.js

---

## The "Old" Way: API Routes

To create a Todo, you would traditionally:
1. Create a Client Component.
2. Create an API Route (`app/api/todo/route.ts`).
3. Use `fetch()` or `axios` to send data.
4. Handle loading and error states manually.

---

### Example: Traditional API Route

```typescript
// app/api/todo/route.ts
export async function POST(req: Request) {
  const { title } = await req.json();
  const newTodo = await db.todo.create({ data: { title } });
  return Response.json(newTodo);
}
```

```tsx
// Client Component
const handleSubmit = async (e) => {
  e.preventDefault();
  await fetch('/api/todo', {
    method: 'POST',
    body: JSON.stringify({ title }),
  });
  router.refresh(); // Manually refresh to see changes
};
```

---

## The "New" Way: Server Actions

Next.js Server Actions allow you to call server-side functions directly from your components (even Client ones).

**Benefits:**
- **Zero API Boilerplate**: No need to define URL endpoints.
- **Type Safety**: End-to-end types without extra effort.
- **Progressive Enhancement**: Works even if JavaScript is disabled!
- **Automatic Revalidation**: Use `revalidatePath()` to update the UI instantly.

---

### Example: Server Action

```typescript
// app/actions.ts
"use server";
import { revalidatePath } from "next/cache";

export async function createTodo(formData: FormData) {
  const title = formData.get("title");
  await db.todo.create({ data: { title } });
  
  revalidatePath("/"); // Update the list automatically!
}
```

```tsx
// Any Component (Server or Client)
<form action={createTodo}>
  <input name="title" />
  <button type="submit">Add Todo</button>
</form>
```

---

## Comparison Summary

| Feature | API Routes | Server Actions |
| :--- | :--- | :--- |
| **Setup** | Requires Route Handler file | Just a function with `"use server"` |
| **Calling** | `fetch('/api/...')` | Direct function call or `<form action>` |
| **Security** | Manual Auth checks | Function-level Auth |
| **Cache** | Manual `router.refresh()` | `revalidatePath()` or `revalidateTag()` |
| **JS Disabled**| Fails (unless using standard form) | **Works out of the box** |

---

## Which one should you use?

- **Use Server Actions** for 99% of your app's internal logic (forms, mutations, deletions). It's faster to write and easier to maintain.
- **Use API Routes** only if you need to provide a public API for **other applications** or external services to consume.

---

# Master the Action! ⚡
## **[badrsoliman.com](https://www.badrsoliman.com)**
