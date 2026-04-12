---
marp: true
paginate: true
---

# CSS3 & HTML5 - Day 3

### Badr Aldien Soliman

---

## 1. Advanced Typography & Fonts

Customizing text is a core part of CSS3.

### Web Fonts (`@font-face`)
Allows you to use any font on your website, even if the user doesn't have it installed.

```css
@font-face {
  font-family: 'MyCustomFont';
  src: url('myfont.woff2') format('woff2');
}

body {
  font-family: 'MyCustomFont', sans-serif;
}
```

---

### Google Fonts
The easier way to add modern typography.

```html
<!-- Include this in your <head> -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
```

---

## 2. CSS Transforms

Transforms allow you to move, rotate, and scale elements without disturbing the original flow of the document.

---

### a. Rotate
Rotates an element by a specified angle (degrees).
- Positive values: Clockwise
- Negative values: Counter-clockwise

```css
.box:hover {
  transform: rotate(45deg);
}
```

---

### b. Scale
Changes the size of an element (1 = 100%).
- `scale(2)`: Twice as big.
- `scale(0.5)`: Half the size.

```css
.box:hover {
  transform: scale(1.2); /* 20% larger */
}
```

---

### c. Translate
Moves an element from its current position along the X and Y axes.

```css
.box:hover {
  transform: translate(20px, 10px); /* Move 20px right, 10px down */
}

/* Tip: Moving vertically only */
.box:hover {
  transform: translateY(-10px);
}
```

---

## 3. CSS Transitions

Transitions make the transforms feel "smooth" instead of instantaneous.

### Basic Properties:
- `transition-property`: e.g., `transform` or `background-color`.
- `transition-duration`: e.g., `0.3s`.
- `transition-timing-function`: e.g., `ease` or `linear`.

---

```css
.box {
  background-color: #3498db;
  transition: all 0.5s ease;
}

.box:hover {
  background-color: #f1c40f;
  transform: rotate(10deg) scale(1.1);
}
```

---

## 4. CSS Animations

Animations are for continuous or multi-step movements using `@keyframes`.

```css
@keyframes bounce {
  from { transform: translateY(0); }
  to { transform: translateY(-50px); }
}

.ball {
  background: red;
  border-radius: 50%;
  animation: bounce 1s infinite alternate;
}
```
---

#### Key Animation Properties:
- `animation-name`: Link to the `@keyframes`.
- `animation-duration`: How long it takes.
- `animation-iteration-count`: `infinite` for loops.
- `animation-direction`: `alternate` to play forward then backward.

---

## 5. Accessibility (ARIA) & Semantic SEO

HTML5 isn't just for visuals; it's for everyone.

- **`role` attribute**: Defines the element's purpose (e.g., `role="button"`).
- **`aria-label`**: Provides a text label for screen readers.
- **`aria-hidden="true"`**: Hides decorative symbols from screen readers.

### Why it matters?
1. **Accessibility**: Helps people with disabilities (screen readers).
2. **SEO**: Search engines prefer semantic and accessible HTML.

---

## Key Day 3 Terms Review

- **Transform**: Change shape, size, or position.
- **Rotate**: Twist elements in 2D space.
- **Scale**: Enlarge or shrink elements.
- **Translate**: Move elements on X and Y axes.
- **Transition**: Smoothly animate property changes.
- **`@keyframes`**: Custom animation steps.
- **ARIA**: Accessible Rich Internet Applications.

---

# Bringing the web to life

## **[badrsoliman.com](https://www.badrsoliman.com)**
