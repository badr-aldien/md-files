---
marp: true
theme: gaia
paginate: true
---

<!-- _class: lead -->

# Next.js vs React

### Badr Aldien Soliman

---

## 🌎 Same Library, Different Worlds

> **Framework:** A structured environment that adds conventions, tooling, and features on top of a library.

| Feature         | ⚛️ React (CRA/Vite)    | 🚀 Next.js                    |
| :-------------- | :--------------------- | :---------------------------- |
| **Target**      | Client-Side Apps       | Full-Stack Web Apps           |
| **Rendering**   | Browser Only (CSR)     | Server + Browser (SSR/SSG)    |
| **Nature**      | UI Library             | Production-Ready Framework    |

---

| Feature            | React (CRA/Vite)           | Next.js                        |
| :----------------- | :------------------------- | :----------------------------- |
| **Routing**        | Manual (React Router)      | ✅ File-Based (built-in)       |
| **Rendering**      | Client-Side Only (CSR)     | SSR, SSG, ISR, CSR             |
| **API Routes**     | 🚫 Not included            | ✅ Built-in (`/app/api/`)      |
| **SEO**            | ⚠️ Limited (client render) | ✅ Excellent (server render)   |


---


## 🛠️ Built-in Superpowers

**Next.js** comes with tools React alone doesn't provide.

### React

- Manual routing setup
- No built-in API layer
- SEO requires extra libraries

---

### Next.js

- **Image Optimization** (`next/image`)
- **Font Optimization** (`next/font`)
- **API Routes** (build backend endpoints)
- **Middleware** (run code before a request)

---

## 🔌 API Routes

Next.js lets you write **backend logic** inside your frontend project.

```
app/
└── api/
    └── users/
        └── route.js   → GET /api/users
```

> No need for a separate Express server for simple backends!

---

## 🏎️ The Engine: React + Server

Next.js is built **on top of React**, but adds a server layer powered by Node.js.

- **React:** Handles component rendering and UI state.
- **Node.js:** Powers the server, API routes, and SSR.
- **Next.js:** Orchestrates both with smart defaults and optimizations.

---

<!-- _class: lead -->

# Ready to Build?
