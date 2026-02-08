---
marp: true
theme: gaia
paginate: true
---

# Introduction to SASS/SCSS

### Badr Aldien Soliman

---

## 1. What is SASS/SCSS?

SASS (Syntactically Awesome Style Sheets) is a CSS preprocessor that extends CSS with powerful features like variables, nesting, mixins, and functions.

**SCSS vs SASS:**

- **SCSS** – Uses curly braces `{}` and semicolons `;` (like CSS)
- **SASS** – Uses indentation (no braces or semicolons)

---

## Why SASS/SCSS?

- ✅ Write less, do more
- ✅ Better code organization
- ✅ Easier to maintain large stylesheets
- ✅ Reusable components and styles
- ✅ Compiles to standard CSS for browsers

---

## 2. SASS Setup

### Step 1: Install SASS

You need Node.js installed on your computer first.

1. Open your terminal and run:

   ```bash
   npm install -g sass
   ```

2. Verify installation:
   ```bash
   sass --version
   ```

---

### Step 2: Project Structure

Create your project folder with this structure:

```
my-project/
├── scss/
│   └── style.scss
├── css/
│   └── style.css (generated)
└── index.html
```

---

### Step 3: Compile SASS to CSS

Run this command in your terminal:

```bash
sass --watch scss/style.scss:css/style.css
```

**What does this do?**

- `--watch` monitors your SCSS file for changes
- Automatically compiles SCSS to CSS whenever you save
- Creates the CSS file in the specified location

---

### Alternative: VS Code Extension

You can also use the "Live Sass Compiler" extension in VS Code:

1. Install the extension from VS Code marketplace
2. Click "Watch Sass" in the bottom status bar
3. SCSS files will compile automatically on save

---

## 3. Variables

Variables let you store values that you can reuse throughout your stylesheet.

### Single Values

```scss
$primary-color: #3498db;
$font-stack: 'Helvetica Neue', Arial, sans-serif;
$base-padding: 16px;

body {
  font-family: $font-stack;
  color: $primary-color;
}
```

---

### Using Variables

```scss
.button {
  background-color: $secondary-color;
  padding: $base-padding;
  border-radius: $border-radius;
}
```

---

### Lists (Arrays)

```scss
$colors: #e74c3c #3498db #2ecc71 #f39c12;

.box-1 {
  background-color: nth($colors, 1); // #e74c3c
}

.box-2 {
  background-color: nth($colors, 2); // #3498db
}
```

---

## 4. Nesting

Nesting allows you to write CSS in a hierarchical structure, making it easier to read and maintain.

### Basic Nesting

```scss
#title-1 {
  color: $primary-color;
  font-size: 24px;

  div {
    color: $secondary-color;
    padding: 10px;
  }
}
```

---

### Compiled Output

```css
#title-1 {
  color: #3498db;
  font-size: 24px;
}

#title-1 div {
  color: #2ecc71;
  padding: 10px;
}
```

---

### Nesting with Classes

```scss
.card {
  background: white;
  padding: 20px;

  .card-header {
    font-size: 20px;
    font-weight: bold;
  }

  .card-body {
    margin-top: 10px;

    p {
      line-height: 1.6;
    }
  }
}
```

---

## 5. Pseudo-classes and Parent Selector (&)

The `&` symbol references the parent selector, perfect for pseudo-classes and modifiers.

---

### Pseudo-classes

```scss
.button {
  background-color: $primary-color;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  p &:hover {
    background-color: $hover-color;
  }

  &:active {
    transform: scale(0.98);
  }
}
```

---

### Pseudo-elements

```scss
.input {
  position: relative;

  &::placeholder {
    color: #999;
  }

  &::before {
    content: '*';
    color: red;
    position: absolute;
    left: -10px;
  }
}
```

---

## 6. Import & Partials (Code Organization)

Break your styles into smaller, maintainable files using partials and imports.

---

### File Structure

```
scss/
├── _variables.scss
├── _mixins.scss
├── _buttons.scss
├── _cards.scss
└── style.scss
```

> **Note:** Partial files start with an underscore `_` and won't be compiled individually.

---

### \_variables.scss

```scss
// _variables.scss
$primary-color: #3498db;
$secondary-color: #2ecc71;
$font-stack: 'Helvetica Neue', Arial, sans-serif;
$base-padding: 16px;
```

---

### \_buttons.scss

```scss
// _buttons.scss
.button {
  background-color: $primary-color;
  color: white;
  padding: $base-padding;
  border: none;
  cursor: pointer;

  &:hover {
    opacity: 0.9;
  }
}
```

---

### style.scss (Main File)

```scss
@import 'variables';
@import 'mixins';
@import 'buttons';
@import 'cards';

body {
  font-family: $font-stack;
  margin: 0;
  padding: 0;
}
```

---

### How it works

- All partials are imported into the main `style.scss` file
- Only `style.scss` is compiled to CSS
- Variables and mixins are available across all files

---

## 7. Mixins (Reusable Styles)

Mixins are reusable blocks of styles that can accept parameters.

---

### Basic Mixin

```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  @include flex-center;
  height: 100vh;
}

.card {
  @include flex-center;
  padding: 20px;
}
```

---

### Mixins with Parameters

```scss
@mixin button-style($bg-color, $text-color, $padding) {
  background-color: $bg-color;
  color: $text-color;
  padding: $padding;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    opacity: 0.8;
  }
}
```

---

### Using Parameterized Mixins

```scss
.btn-primary {
  @include button-style(#3498db, white, 10px 20px);
}

.btn-success {
  @include button-style(#2ecc71, white, 12px 24px);
}

.btn-danger {
  @include button-style(#e74c3c, white, 8px 16px);
}
```

---

### Mixins with Default Parameters

```scss
@mixin box-shadow($x: 0, $y: 2px, $blur: 4px, $color: rgba(0, 0, 0, 0.1)) {
  box-shadow: $x $y $blur $color;
}

.card {
  @include box-shadow; // Uses defaults
}

.modal {
  @include box-shadow(0, 4px, 8px, rgba(0, 0, 0, 0.2));
}
```

---

## 8. For Loops

SCSS provides `@for` loops to repeat styles and generate multiple classes dynamically.

---

### Basic @for Loop

```scss
@for $i from 1 through 5 {
  .margin-#{$i} {
    margin: #{$i}px;
  }
}
```

---

**Compiled Output:**

```css
.margin-1 {
  margin: 1px;
}
.margin-2 {
  margin: 2px;
}
.margin-3 {
  margin: 3px;
}
.margin-4 {
  margin: 4px;
}
.margin-5 {
  margin: 5px;
}
```

---

### Generating Multiple Classes

```scss
$colors: #e74c3c, #3498db, #2ecc71, #f39c12, #9b59b6;

@for $i from 1 through length($colors) {
  .box-#{$i} {
    background-color: nth($colors, $i);
    padding: 20px;
    margin-bottom: 10px;
  }
}
```

---

### Creating Responsive Utilities

```scss
// Generate spacing utilities (0, 4, 8, 12, 16, 20)
@for $i from 0 through 5 {
  .p-#{$i} {
    padding: #{$i * 4}px;
  }

  .m-#{$i} {
    margin: #{$i * 4}px;
  }
}
```

---

## 9. Functions

SASS provides built-in functions and allows you to create custom ones.

---

### Built-in Functions

```scss
$base-color: #3498db;

.box {
  background-color: $base-color;
  border-color: darken($base-color, 10%);
  color: lighten($base-color, 40%);
}

.overlay {
  background-color: rgba($base-color, 0.5); // Add transparency
}
```

---

### Custom Functions

```scss
@function calculate-rem($pixels) {
  @return $pixels / 16 * 1rem;
}

.heading {
  font-size: calculate-rem(24);
  margin-bottom: calculate-rem(16);
}
```

---

## 9. Extend & Inheritance

Share styles between selectors using `@extend`.

```scss
.message {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.message-success {
  @extend .message;
  background-color: #d4edda;
  border-color: #c3e6cb;
}
```

---

## 10. Operators

SASS supports mathematical operations in your styles.

> **Note:** In newer versions of Sass, the `/` operator for division is deprecated.

```scss
@use 'sass:math';

$base-size: 16px;

.column {
  width: math.div(100%, 3); // 33.333%
  margin-right: math.div($base-size, 2); // 8px
}
```

---

# Happy coding!

## **[badrsoliman.com](https://www.badrsoliman.com)**
