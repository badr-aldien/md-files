---
marp: true
paginate: true
---

# Next.js Fundamentals - Day 1

### Badr Aldien Soliman

---

## 1. Creating a Next.js Project

The easiest way to start is using the official CLI tool.

### Using `npx` (Recommended)

```pwsh
npx create-next-app@latest
```

---

## 2. File-Based Routing

In Next.js, the file system is the router. The `app` directory handles your routes.

### Basic Routing Rules:
- **Folders** define the path (e.g., `app/about/`).
- **`page.tsx`** makes that path accessible to the public.

### Nested Routes:
Creating a folder inside another folder creates nested paths.
- `app/blog/first-post/page.tsx` → `/blog/first-post`

---

### Route Groups:
Folders wrapped in parentheses `( )` are ignored by the URL path. This is great for organizing files or sharing layouts without affecting the URL.

- `app/(auth)/login/page.tsx` → `/login`
- `app/(auth)/register/page.tsx` → `/register`

---

### Absolute Paths (`@/`):
Next.js uses **Import Aliases** to avoid "relative path hell" (`../../../components`).
- The `@/` symbol refers to the root of your project (or the `src` folder if used).

```tsx
// Instead of this:
import Button from '../../../../components/Button';

// Use this:
import Button from '@/components/Button';
```

---

### Creating your first page

Every `page.tsx` must export a default React component.

**`app/about/page.tsx`**
```jsx
const AboutPage = () => {
  return (
    <div>
      <h1>About Us</h1>
      <p>This is the about page content.</p>
    </div>
  );
};

export default AboutPage;
```

---

## 3. Linking Between Pages

To navigate between pages, we use the `<Link>` component instead of the standard `<a>` tag.

### Why `<Link>`?
- **Client-side navigation**: No full page reload.
- **Prefetching**: Next.js preloads the linked page in the background for instant loading.

---

### Using the Link Component

**`app/page.tsx`**
```tsx
import Link from 'next/link';

export default function Home() {
  return (
      <h1>Home Page</h1>
      <ul>
        <li>
          <Link href="/about">About Us</Link>
        </li>
        <li>
          <Link href="/login">Login (Route Group)</Link>
        </li>
      </ul>
  );
}
```

---

## 4. Layouts & Shared UI

A **Layout** is UI that is shared between multiple pages. On navigation, layouts preserve state and do not re-render.

### The Root Layout
Every Next.js project has a `layout.tsx` in the root of the `app` directory. This is where you define the `<html>` and `<body>` tags.

---

### Creating a Shared Navbar
**`app/layout.tsx`**
```tsx
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <nav>Shared Navbar</nav>
        <main>{children}</main>
        <footer>Shared Footer</footer>
      </body>
    </html>
  );
}
```

---

## 5. Server vs. Client Components

This is the most important concept in the App Router. By default, **every component is a Server Component**.

| Feature | Server Component (Default) | Client Component |
| :--- | :--- | :--- |
| **Rendering** | Renders on the server | Renders in the browser |
| **Interactivity** | 🚫 No (No state/effects) | ✅ Yes (onClick, useState) |
| **Performance** | Faster (Less JS sent) | Slower (More JS sent) |

---

### When to use `"use client"`?
If you need **Interactivity** (hooks like `useState`, `useEffect` or event listeners like `onClick`), you MUST add the directive at the very top of your file.

```tsx
"use client"; // This line is required!

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;}
```

---

## 6. Optimization (Images & Fonts)

Next.js handles the "heavy lifting" for performance automatically through dedicated components.

### 🖼️ The Image Component
Prevents **Cumulative Layout Shift (CLS)** and optimizes formats (WebP).

---

```tsx
import Image from 'next/image';

<Image 
  src="/hero.png" 
  width={500} 
  height={300} 
  alt="Hero Image" 
/>
```

> **Pro Tip:** Use `fill` when the image size is unknown, provided the parent has `position: relative`.

---

### 🔠 The Font Component (`next/font`)
Next.js automatically self-hosts Google Fonts. This means **zero layout shift** and better privacy.

**`app/layout.tsx`**
```tsx
import { Inter } from 'next/font/google';

const inter = Inter({ subsets: ['latin'] });

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={inter.className}>
      <body>{children}</body>
    </html>
  );
}
```

---

## 7. Metadata (SEO)

Next.js has a built-in Metadata API to help you optimize your SEO and social sharing.

### Static Metadata
You can export a `metadata` object from any **Server Component** (`layout.tsx` or `page.tsx`).

```tsx
export const metadata = {
  title: 'My Awesome Site',
  description: 'Built with Next.js',
};

export default function Page() {
  return <h1>Hello World</h1>;
}
```

---

## 8. Deployment (Vercel)

Next.js is built by the team at **Vercel**, making deployment incredibly simple. 

### How to Deploy:
1. Push your Next.js code to **GitHub**.
2. Go to [vercel.com](https://vercel.com) and log in with GitHub.
3. Click **Add New -> Project**, select your repository, and click **Deploy**.

> **Magic:** Vercel automatically detects Next.js, builds it, and gives you a live HTTPS URL. It will automatically update whenever you push to the `main` branch!

---

## Summary Workflow

1. **Structure**: Use **Layouts** for shared components and **Route Groups** for organization.
2. **Components**: By default, use **Server Components**. Use `"use client"` only when interactivity is needed.
3. **Optimizations**: Use **Next Image** and **Next Font** to ensure a high Performance score.
4. **SEO**: Use the **Metadata API** for better search visibility.
5. **Deployment**: Deploy to **Vercel** via GitHub to see your site (and test SEO) live!

---

# EAT THE FROG!

## **[badrsoliman.com](https://www.badrsoliman.com)**
