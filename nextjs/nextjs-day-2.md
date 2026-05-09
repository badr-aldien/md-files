---
marp: true
paginate: true
backgroundColor: #f5f5f5
---

# Next.js Fundamentals - Day 2

### Badr Aldien Soliman

---

## 1. Dynamic Routing

Not all pages have a fixed URL. What about `/blog/1` or `/users/marwan`? 
We handle this using **Dynamic Routes** (folder names with brackets `[]`).

---

### Creating a Dynamic Route

If we want a URL like `/blog/[slug]`:

📁 **Structure:** `app/blog/[slug]/page.tsx`

```tsx
// ⚠️ In Next.js 15+, `params` is a Promise!
export default async function BlogPost({ params }) {
  // 1. You must await the params
  const { slug } = await params;
  
  // 2. Decode the URI if it contains non-English characters (like Arabic)
  const decodedSlug = decodeURIComponent(slug);

  return (
    <div>
      <h1>Blog Post Name: {decodedSlug}</h1>
      <p>This page handles ANY string dynamically!</p>
    </div>
  );
}
```

---

## 2. Search Params (`searchParams`)

While `params` handles the URL path, **`searchParams`** handles query strings like: 
`/users?name=Leanne`.

---

### Practical Example: Filtering a List
You can use `searchParams` to filter data fetched from an API.

```tsx
// app/blog/page.tsx
export default async function BlogPage({ searchParams }) {
  // 1. Get the 'name' from the URL (e.g., /users?name=abdulatif)
  const query = await searchParams;
  const searchName = query.name?.toLowerCase();

  // 2. Fetch the data
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  const users = await res.json();

  // 3. Filter the data based on the search query
  const filteredUsers = searchName 
    ? users.filter(u => u.name.toLowerCase().includes(searchName))
    : users;
}
```

---

## 3. Programmatic Routing

Sometimes you need to navigate from a button click or after a form submission. Next.js handles this differently depending on where the code runs.

### Client-Side: `useRouter`
Use this inside Client Components (e.g., inside `onClick`).

```tsx
"use client";
import { useRouter } from 'next/navigation'; // ⚠️ NOT next/router!

export default function DashboardButton() {
  const router = useRouter();
  
  return (
    <button onClick={() => router.push('/dashboard')}>
      Go to Dashboard
    </button>
  );
}
```

---

### Server-Side: `redirect`
Use this inside Server Components or Server Actions (e.g., if a user is not found).

```tsx
import { redirect } from 'next/navigation';

export default async function Profile({ params }) {
  const { slug } = await params;
  const user = await fetchUser(slug);
  
  if (!user) {
    redirect('/not-found'); // Instantly redirects!
  }

  return <h1>{user.name}</h1>;
}
```

---

## 4. Environment Variables (`.env`)

Next.js has built-in support for environment variables to keep secrets safe.

### 🛡️ `.env.local`
Store sensitive keys (like DB passwords) here. This file should **never** be pushed to GitHub.

### 🌐 Server vs. Client Variables
- **Private (Default)**: Variables like `API_KEY` are only accessible on the server.
- **Public**: To use a variable in a Client Component, it MUST start with `NEXT_PUBLIC_`.

```bash
# .env.local
DATABASE_URL=secret_url      # Only server can see this
NEXT_PUBLIC_ANALYTICS=123    # Client can see this too
```

---

## 5. Data Fetching & SSR

In Next.js, Data Fetching is synonymous with **Server-Side Rendering (SSR)**.

### What is SSR?
Instead of sending an empty HTML file to the browser (like standard React), Next.js fetches data and generates the HTML **on the server for every request**.

### Why use SSR?
- **Speed**: The page arrives fully built; the user doesn't see a loading screen for the initial data.
- **SEO**: Search engine bots see the actual content immediately.
- **Security**: You can fetch from your database directly without exposing API keys to the browser.

---

### SSR Fetching Example
Simply make your component `async` and `fetch` directly.

```tsx
export default async function UsersPage() {
  // This happens on the SERVER on every request
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  const users = await res.json();

  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}
```

---

## 6. UI States: Loading

Data fetching takes time. Instead of managing complex loading states, Next.js gives us a special file: **`loading.tsx`**.

While your page.tsx is awaiting data, Next.js will instantly show `loading.tsx`.

**`app/users/loading.tsx`**
```tsx
export default function Loading() {
  // You can put a Skeleton UI or a spinner here
  return <h2>Fetching users... Please wait ⏳</h2>;
}
```

*This works automatically! You don't need to import it into your page.*

---

### `<Suspense />` (Partial Page)
While `loading.tsx` covers the **whole page**, `<Suspense>` allows you to show loading states for **specific components**. This allows the rest of the page to be interactive immediately.

```tsx
import { Suspense } from 'react';
import UserList from './UserList';

export default function Page() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Suspense fallback={<p>Loading users...</p>}>
        <UserList />
      </Suspense>
    </div>
  );
}
```


---

## 7. UI States: Errors & 404s

Just like loading, we handle failures with special files.

### 🚫 `not-found.tsx`
Catches missing pages (404 errors).
```tsx
// app/not-found.tsx
import Link from 'next/link';

export default function NotFound() {
  return (
    <div>
      <h2>Oops! Page Not Found</h2>
      <Link href="/">Return Home</Link>
    </div>
  );
}
```

---

### 💥 `error.tsx`

If your data fetching fails or your component crashes, `error.tsx` catches the error so the rest of the application stays alive.

_Note: Error boundaries must be **Client Components**._

```tsx
"use client"; // Must be a client component

export default function Error({ error, reset }) {
  return (
    <div>
      <h2>Something went wrong! 🥲</h2>
      <button onClick={() => reset()}>Try Again</button>
    </div>
  );
}
```

---

## 8. Data Fetching Strategies

Next.js gives you full control over how your data is cached and updated using the `fetch` API.

```tsx
// 1. Always fresh (SSR)
// Fetches data on every single request.
const response = await fetch(`${baseURL}/products`, { cache: 'no-store' });

// 2. Cached, refresh every hour (ISR)
// Re-fetches in the background after the time expires.
const response = await fetch(`${baseURL}/products`, { next: { revalidate: 3600 } });

// 3. Cached forever (SSG)
// Fetches once at build time and stays cached until next deploy.
const response = await fetch(`${baseURL}/products`, { cache: 'force-cache' });
```

---

## 9. Route Handlers (API Routes)

Next.js is a Full-Stack framework. You don't need a separate Express/Node backend. You can build your APIs directly in the `app` directory.

### How it works:
Instead of `page.tsx`, you create a **`route.ts`** file.

```typescript
// app/api/hello/route.ts
import { NextResponse } from 'next/server';

export async function GET(request: Request) {
  return NextResponse.json({ message: "Hello from the backend!" });
}
```
*Access this via `http://localhost:3000/api/hello`*

---

### Handling POST Requests

```typescript
// app/api/users/route.ts
import { NextResponse } from 'next/server';

export async function POST(request: Request) {
  const body = await request.json(); // Parse the incoming JSON
  
  // Logic to save to database goes here...
  
  return NextResponse.json(
    { message: "User created", user: body }, 
    { status: 201 }
  );
}
```

---

## Summary Workflow

1. **Variables**: Use `params` and `searchParams` to handle dynamic URL data.
2. **Navigation**: Use `useRouter` on the client and `redirect` on the server.
3. **Setup**: Keep secrets safe in `.env` and use `NEXT_PUBLIC_` for the browser.
4. **Data**: Use **SSR** (async/await) to fetch data directly on the server.
5. **Feedback**: Handle loading and errors effortlessly with special files.
6. **Optimization**: Use **ISR** to keep your cached data fresh.
---

# May your bugs be shallow

## **[badrsoliman.com](https://www.badrsoliman.com)**
