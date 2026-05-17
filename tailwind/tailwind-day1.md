---
marp: true
paginate: true
---

# Tailwind CSS - Day 1

### Badr Aldien Soliman

---

## 1. What is Tailwind CSS?

Tailwind is a **utility-first CSS framework**. Instead of writing class names and then styling them in a separate file, you style elements directly using pre-defined classes.

### The core idea:
- Each class does **one thing** - `flex`, `p-4`, `text-xl`
- No context switching between `.jsx` and `.css`
- No naming things - `.card-wrapper-inner-2` is a thing of the past

---

### Tailwind vs. Vanilla CSS

```html
<!-- Vanilla CSS: two files, one class used once -->
<div class="card">Hello</div>
```

```css
.card {
  display: flex;
  padding: 1rem;
  border-radius: 0.5rem;
  background-color: white;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}
```

```html
<!-- Tailwind: everything in one place -->
<div class="flex p-4 rounded-lg bg-white shadow-md">Hello</div>
```

---

## 2. The Spacing Scale

Tailwind uses a consistent numeric scale for spacing. `1 unit = 0.25rem`.

| Class | Value |
| :--- | :--- |
| `p-1` | 0.25rem (4px) |
| `p-2` | 0.5rem (8px) |
| `p-4` | 1rem (16px) |
| `p-8` | 2rem (32px) |
| `p-16` | 4rem (64px) |

The same scale applies to `m-`, `gap-`, `w-`, `h-`, and more. Learn it once, use it everywhere.

---

## 3. Typography & Colors

```html
<!-- Font size -->
<p class="text-sm">Small</p>
<p class="text-base">Base (default)</p>
<p class="text-xl">Extra Large</p>
<p class="text-4xl">4X Large</p>

<!-- Font weight -->
<p class="font-normal">Normal</p>
<p class="font-semibold">Semibold</p>
<p class="font-bold">Bold</p>

<!-- Colors follow a 50–950 shade scale -->
<p class="text-gray-500">Muted text</p>
<p class="text-indigo-600">Brand text</p>
<div class="bg-indigo-100">Light background</div>
```

---

## 4. Layout - Flexbox & Grid

Tailwind gives you flex and grid as single classes.

### Flexbox

```html
<div class="flex items-center justify-between gap-4">
  <span>Left</span>
  <span>Right</span>
</div>
```

### Grid

```html
<div class="grid grid-cols-3 gap-6">
  <div>Card 1</div>
  <div>Card 2</div>
  <div>Card 3</div>
</div>
```

---

## 5. Responsive Design

Tailwind is **mobile-first**. Classes without a prefix apply to all screen sizes. Prefixes apply from that breakpoint **and up**.

| Prefix | Breakpoint |
| :--- | :--- |
| *(none)* | All screens |
| `sm:` | ≥ 640px |
| `md:` | ≥ 768px |
| `lg:` | ≥ 1024px |
| `xl:` | ≥ 1280px |

```html
<p class="text-sm md:text-lg xl:text-2xl">Responsive text</p>
<div class="grid grid-cols-1 md:grid-cols-3 gap-6">...</div>
```

---

## 6. State Variants

Apply styles on hover, focus, or active using prefixes - the same pattern as responsive breakpoints.

```html
<button class="bg-indigo-500 hover:bg-indigo-600 active:scale-95 transition">
  Click me
</button>

<input class="border border-gray-300 focus:border-indigo-500
              focus:ring-2 focus:ring-indigo-200 outline-none
              rounded-md px-3 py-2 transition" />
```

> Variants are **stackable**: `md:hover:bg-indigo-700` is valid.

---

## 7. Transforms & Transitions

Make your UI feel alive with smooth animations and state changes.

---

### Transitions
Control property, duration, and easing.



```html
<button class="transition-all duration-300 ease-in-out hover:bg-indigo-600 hover:scale-105">
  Smooth Hover
</button>
```

- `transition-all`, `transition-colors`, `transition-opacity`
- `duration-150`, `duration-300`, `duration-500`
- `ease-linear`, `ease-in`, `ease-out`, `ease-in-out`

---

### Transforms
Scale, rotate, and translate elements.

- `scale-95`, `scale-100`, `scale-105`
- `rotate-3`, `rotate-12`, `rotate-45`
- `translate-x-2`, `-translate-y-4`

---

## 8. Real-World Patterns

This is where Tailwind really pays off. Let's build patterns you'll use on **every project**.

---

### Pattern 1: Max-Width Layout Wrapper

Every website needs a centered container with a max width. This is the skeleton of every page.

```html
<div class="max-w-7xl mx-auto px-4">
  <!-- All your page content goes here -->
</div>
```

- `max-w-7xl` → caps width at 1280px
- `mx-auto` → centers it horizontally
- `px-4` → adds horizontal padding on small screens

> **Pro Tip:** Wrap your entire layout in this inside `layout.tsx` so every page inherits it automatically.

---

### Pattern 2: Responsive Navbar

A navbar that shows links on desktop and hides them on mobile.

```html
<nav class="bg-white shadow-sm">
  <div class="max-w-7xl mx-auto px-4 flex items-center justify-between h-16">

    <span class="font-bold text-xl">Logo</span>

    <!-- Desktop links: hidden on mobile, visible on md+ -->
    <ul class="hidden md:flex items-center gap-8 text-gray-600">
      <li><a href="#" class="hover:text-indigo-600 transition">Home</a></li>
      <li><a href="#" class="hover:text-indigo-600 transition">About</a></li>
      <li><a href="#" class="hover:text-indigo-600 transition">Contact</a></li>
    </ul>

  </div>
</nav>
```

---

### Pattern 3: Loading Spinner

A pure CSS spinner using Tailwind's animation utilities.

```html
<div class="flex items-center justify-center h-screen">
  <div class="w-10 h-10 border-4 border-indigo-200 border-t-indigo-600
              rounded-full animate-spin"></div>
</div>
```

- `border-4` → the ring thickness
- `border-indigo-200` → the faint background arc
- `border-t-indigo-600` → the colored spinning arc
- `animate-spin` → Tailwind's built-in 1s linear infinite rotation

---

### Pattern 5: Card with Hover Overlay

Using the `group` utility to reveal an overlay when the parent is hovered.

```html
<div class="relative overflow-hidden rounded-xl cursor-pointer group">

  <img src="/photo.jpg" class="w-full h-64 object-cover" />

  <!-- Invisible by default, visible on group hover -->
  <div class="absolute inset-0 bg-black/50 opacity-0
              group-hover:opacity-100 transition-opacity duration-300
              flex items-center justify-center">
    <span class="text-white font-bold text-lg">View Project</span>
  </div>

</div>
```

---

## Summary

| Pattern | Key Classes |
| :--- | :--- |
| Max-width wrapper | `max-w-7xl mx-auto px-4` |
| Responsive navbar | `hidden md:flex` |
| Loading spinner | `animate-spin`, `border-t-{color}` |
| Card hover overlay | `group`, `group-hover:opacity-100` |

---

## 🛠️ Lab Task: Put It All Together

Build a **profile page** using only Tailwind - no external CSS.

### Requirements:
1. **Wrapper**: Use the max-width layout wrapper pattern.
2. **Navbar**: Logo on the left, links on the right. Hidden on mobile.
3. **Cards**: A responsive grid of 3 project cards with a hover overlay.
4. **Interactions**: Use transitions and transforms for smooth hover effects.


---

# Style is just one class away 🎨

## **[badrsoliman.com](https://www.badrsoliman.com)**
