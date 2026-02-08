---
marp: true
theme: gaia
paginate: true
---

# Bootstrap

### Badr Aldien Soliman

---

## 1. Introduction to Bootstrap

Bootstrap is a powerful CSS framework that helps us build responsive, mobile-first websites quickly and efficiently.

---

## 2. Bootstrap Setup

Before we dive into the components, make sure you have Bootstrap properly linked in your HTML document.

You can either:

- Download Bootstrap files
- Use the CDN links

---

## 3. The Bootstrap Grid System

Bootstrap uses a **three-level deep structure** for its grid system:

1. **Container** - The wrapper that contains your content
2. **Rows** - Horizontal groups of columns
3. **Columns** - The actual content containers

---

## The 12-Column System

Bootstrap divides each row into **12 equal columns**.

Here's how it works:

- `col-6` takes up 6 out of 12 columns (50% of the screen width)
- `col-4` takes up 4 out of 12 columns (33.33% of the screen width)
- `col-12` takes up the full width

---

## Important Rule

**If you add more than 12 columns in a single row, the extra columns will wrap to the next line.**

---

## Special Column Classes

- `col` (without a number) - Takes whatever space is left, even if it's less than one column
- `col-auto` - Adjusts its width based on the content inside

---

## Breakpoints and Responsive Columns

Bootstrap uses breakpoints to create responsive designs:

```html
<div class="col-sm-6 col-md-4 col-lg-3">Content</div>
```

**The syntax is:** `col-(breakpoint)-(1-12)`

---

## Offset Classes

Offsets create empty space to the left of a column. Use offset classes on the same line as your column class:

```html
<div class="col-6 offset-3">This column is centered</div>
```

This creates empty space equivalent to 3 columns on the left side.

---

## Row Columns

You can control how columns behave within a row using `row-cols` classes:

```html
<div class="container">
  <div class="row row-cols-2">
    <div class="col"><div class="box"></div></div>
    <div class="col"><div class="box"></div></div>
    <div class="col"><div class="box"></div></div>
    <div class="col"><div class="box"></div></div>
  </div>
</div>
```

**The syntax:** `row-cols-(breakpoint)-(number)`

---

## Gaps (Gutters)

Control spacing between columns and rows:

- `g-x-(1-5)` - Horizontal gaps
- `g-y-(1-5)` - Vertical gaps
- `g-(1-5)` - Both horizontal and vertical gaps

You can also use breakpoints with gaps: `g-md-3`, `g-lg-4`, etc.

---

## Nested Rows

You can nest a row inside a column for more complex layouts:

```html
<div class="container">
  <div class="row">
    <div class="col-8">
      <div class="row">
        <div class="col-6">Nested content</div>
        <div class="col-6">Nested content</div>
      </div>
    </div>
  </div>
</div>
```

---

## Important Rule for Nesting

**Always nest rows inside columns for proper alignment.**

Removing the column wrapper will break the expected behavior.

---

## 4. Bootstrap Tables

Creating responsive tables with Bootstrap is straightforward:

```html
<table class="table">
  <thead>
    <tr>
      <th>Header</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data</td>
    </tr>
  </tbody>
</table>
```

---

## Table Themes

Bootstrap provides **8 different color themes** that can be applied to tables, rows, or cells:

- `table-primary`
- `table-secondary`
- `table-success`
- `table-danger`
- `table-warning`

---

## Additional Table Classes

- `table-striped` - Adds zebra-striping to table rows
- `table-hover` - Enables hover state on table rows
- `table-responsive` - Makes tables scroll horizontally on smaller screens
- `table-responsive-(breakpoint)` - Stop responsiveness at specific breakpoint

---

## Table Groups

Use specific classes for table sections:

- `table-group-divider` - Adds a divider between table sections
- Classes can be applied to `<thead>` and `<tbody>` elements

---

## 5. Bootstrap Forms

Bootstrap provides extensive form styling and validation features.

---

## Basic Form Elements

```html
<form>
  <div class="mb-3">
    <label class="form-label">Email</label>
    <input type="email" class="form-control" />
  </div>
  <div class="mb-3">
    <label class="form-label">Country</label>
    <select class="form-select">
      <option>Choose...</option>
    </select>
  </div>
</form>
```

---

## More Form Elements

```html
<div class="mb-3">
  <label class="form-label">Range</label>
  <input type="range" class="form-range" />
</div>

<div class="mb-3">
  <label class="form-label">Color</label>
  <input type="color" class="form-control form-control-color" />
</div>
```

---

## Form Control Sizes

Change input sizes using:

- `form-control-lg` - Large inputs
- `form-control-sm` - Small inputs

---

## Form States

- `disabled` - Disables the input
- `readonly` - Makes the input read-only

---

## Form Validation

Bootstrap provides visual feedback for form validation:

- `is-valid` - Green styling for valid inputs
- `is-invalid` - Red styling for invalid inputs

---

## JavaScript Form Validation

```javascript
// Add novalidate to form tag to prevent browser validation
form = document.querySelector('form');

form.addEventListener('submit', (e) => {
  if (!form.checkValidity()) {
    e.preventDefault();
  }
  form.classList.add('was-validated');
});
```

---

## Validation Approach

This approach:

1. Uses `novalidate` on the form tag to disable browser validation
2. Handles validation through JavaScript
3. Adds the `was-validated` class to trigger Bootstrap's validation styles

---

# Happy coding!

## **[badrsoliman.com](https://www.badrsoliman.com)**
