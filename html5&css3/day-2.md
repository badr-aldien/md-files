---
marp: true
paginate: true
---

# CSS3 - Day 2

### Badr Aldien Soliman

---

## 1. Advanced Selectors

Beyond class and ID selectors, CSS3 provides powerful ways to target elements.

### Pseudo-classes
Target elements in a specific state.
- `:hover`: When the mouse is over the element.
- `:nth-child(n)`: Selects the nth child of its parent.
- `:focus`: When an input element has focus.

---

### Pseudo-elements
Style specific parts of an element.
- `::before`: Insert content before an element.
- `::after`: Insert content after an element.
- `::placeholder`: Style the placeholder text in inputs.

---

### Selector Examples

```css
/* Styling even rows in a table */
tr:nth-child(even) {
  background-color: #f2f2f2;
}

/* Adding an icon before a link */
a::before {
  content: "🔗 ";
}

/* Changing button appearance on hover */
button:hover {
  background-color: #4CAF50;
  cursor: pointer;
}
```

---

## 2. Dynamic Units: rem & em

Modern web pages use relative units to ensure text scales correctly.

- **`em`**: Relative to the font-size of its **parent** element.
- **`rem`**: Relative to the font-size of the **root** (`<html>`) element. 

### Why use `rem`?
It's more consistent. 1rem = usually 16px (the default browser size).

```css
div { font-size: 20px; }
span { font-size: 2em; } /* Becomes 40px */

html { font-size: 16px; }
p { font-size: 2rem; } /* Becomes 32px everywhere */
```

---

## 3. Icons with Font Awesome

Sometimes standard emojis (🔗) aren't enough. Font Awesome provides professional vector icons.

### How to use:
1. Link the CSS file (CDN).
2. Use the `<i>` tag with specific classes.

```html
<!-- Include CDN in <head> -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

<!-- Use icons -->
<i class="fa-solid fa-house"></i>
<i class="fa-brands fa-github"></i>
<i class="fa-solid fa-gear"></i>
```

---

## 4. Visual Effects: Gradients & Shadows

Gradients allow two or more colors to blend into one another.

### CSS Gradients
```css
/* Linear Gradient */
.linear {
  background: linear-gradient(to right, #3498db, #2ecc71);
}

/* Radial Gradient */
.radial {
  background: radial-gradient(circle, white, blue);
}
```

---

### Shadows & Translucency
Add depth and realism to your design.

```css
/* Box Shadow */
.card {
  box-shadow: 10px 10px 15px rgba(0, 0, 0, 0.2);
}

/* Text Shadow */
h1 {
  text-shadow: 2px 2px 4px #000;
}

/* RGBA (Transparency) */
.overlay {
  background-color: rgba(0, 0, 0, 0.5); /* 50% opacity */
}
```

---

## 5. Content Control: Overflow

The `overflow` property controls what happens when content is too big for its container.

- **`hidden`**: The extra content is cut off and invisible.
- **`scroll`**: Always adds scrollbars.
- **`auto`**: Adds scrollbars ONLY if needed.
- **`visible`**: (Default) Content spills out of the container.

```css
.scroll-box {
  width: 200px;
  height: 100px;
  overflow: auto; /* Adds scrollbar only if text is long */
  border: 1px solid black;
}
```

---

## Key Day 2 Terms Review

- **Pseudo-class**: Selects based on state (`:hover`).
- **Pseudo-element**: Targets parts of content (`::after`).
- **rem**: Root-relative unit for consistent scaling.
- **em**: Relative unit based on parent font-size.
- **Font Awesome**: The industry standard for web icons.
*   **Linear Gradient**: Smooth transitions between colors.
*   **Overflow**: Manages content that exceeds box dimensions.

---

# Add some salt & pepper

## **[badrsoliman.com](https://www.badrsoliman.com)**
