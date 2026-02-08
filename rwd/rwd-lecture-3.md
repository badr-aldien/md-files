---
marp: true
theme: default
paginate: true
---

# Bootstrap Components

### Badr Aldien Soliman

---

## 1. Bootstrap Buttons

Bootstrap provides a comprehensive button system with various styles and states.

---

## Basic Button Classes

```html
<button class="btn btn-primary">Primary Button</button>
<a href="#" class="btn btn-success">Success Link</a>
<button class="btn btn-link">Link Style Button</button>
```

---

## Button Themes

Bootstrap includes **8 different button themes:**

- `btn-primary`
- `btn-success`
- `btn-danger`
- `btn-warning`
- `btn-info`
- `btn-light`
- `btn-dark`

---

## Button Sizes

- `btn-lg` - Large buttons
- `btn-sm` - Small buttons
- Default size (no additional class needed)

---

## Outline Buttons

Use `btn-outline-*` for outlined button styles:

```html
<button class="btn btn-outline-primary">Outlined Primary</button>
<button class="btn btn-outline-danger">Outlined Danger</button>
```

---

## Disabled Buttons

```html
<button class="btn btn-primary" disabled>Disabled Button</button>
```

---

## Button Groups

Group buttons together using `btn-group`:

```html
<div class="btn-group">
  <button class="btn btn-outline-primary">Left</button>
  <button class="btn btn-outline-primary">Middle</button>
  <button class="btn btn-outline-primary">Right</button>
</div>
```

---

## Vertical Button Groups

For vertical button groups:

```html
<div class="btn-group-vertical">
  <button class="btn btn-outline-primary">Top</button>
  <button class="btn btn-outline-primary">Middle</button>
  <button class="btn btn-outline-primary">Bottom</button>
</div>
```

---

## 2. Bootstrap Alerts

Alerts provide contextual feedback messages for typical user actions.

---

## Basic Alert Structure

```html
<div class="alert alert-primary">A simple primary alert—check it out!</div>
```

---

## Alert Themes

Use any of the **8 Bootstrap themes** with alerts:

- `alert-primary`
- `alert-secondary`
- `alert-success`
- `alert-danger`
- `alert-warning`
- `alert-info`
- `alert-light`
- `alert-dark`

---

## Dismissible Alerts

Create closeable alerts:

```html
<div class="alert alert-warning alert-dismissible">
  <strong>Warning!</strong> This alert can be dismissed.
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

## Alert Animations

Add smooth animations to alerts:

```html
<div class="alert alert-success alert-dismissible fade show">
  <strong>Success!</strong> This alert has a fade animation.
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

## 3. Bootstrap Cards

Cards are flexible content containers with multiple variants and options.

---

## Basic Card Structure

```html
<div class="card">
  <img src="..." class="card-img-top" alt="..." />
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <h6 class="card-subtitle mb-2 text-muted">Card subtitle</h6>
    <p class="card-text">Card content goes here.</p>
  </div>
</div>
```

---

## Card Image Positions

- `card-img-top` - Image at the top
- `card-img-bottom` - Image at the bottom
- `card-img` - Full-width image with overlay

---

## Card Image Overlay

```html
<div class="card">
  <img src="..." class="card-img" alt="..." />
  <div class="card-img-overlay">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Text overlay on image.</p>
  </div>
</div>
```

---

## Card Header and Footer

```html
<div class="card">
  <div class="card-header">Featured</div>
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Card content</p>
  </div>
  <div class="card-footer text-muted">2 days ago</div>
</div>
```

---

## Card Groups

Stack multiple cards together:

```html
<div class="card-group">
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Card 1</h5>
      <p class="card-text">Content for card 1</p>
    </div>
  </div>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Card 2</h5>
      <p class="card-text">Content for card 2</p>
    </div>
  </div>
</div>
```

---

## 4. Bootstrap Modals

Modals are dialog boxes that overlay the current page.

---

## Basic Modal Structure

```html
<div class="modal fade" id="exampleModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Modal title</h5>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="modal"
        ></button>
      </div>
      <div class="modal-body">Modal content goes here...</div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
          Close
        </button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
```

---

## Modal Trigger Button

```html
<button
  type="button"
  class="btn btn-primary"
  data-bs-toggle="modal"
  data-bs-target="#exampleModal"
>
  Launch Modal
</button>
```

**Note:** The modal won't show without a trigger button that links to it using `data-bs-toggle="modal"` and `data-bs-target="#modalId"`.

---

## Modal Animations

Add the `fade` class to the modal for smooth animations:

```html
<div class="modal fade" id="exampleModal">
  <!-- Modal content -->
</div>
```

---

## Modal Customizations

- `modal-dialog-centered` - Vertically center the modal
- `modal-dialog-scrollable` - Make the modal body scrollable

```html
<div class="modal fade" id="exampleModal">
  <div
    class="modal-dialog modal-dialog-centered 
              modal-dialog-scrollable"
  >
    <!-- Modal content -->
  </div>
</div>
```

---

## 5. Bootstrap Navbar

The navbar is a responsive navigation component.

---

## Important Structure Note

Unlike other components, the navbar container structure is different:

- The `.container` goes **inside** the `.navbar`
- There's a separate outer container for the page content
- This allows the navbar background color to span the full width

---

## Basic Navbar Structure

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container">
    <a class="navbar-brand" href="#">Brand Name</a>
    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarNav"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">About</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

---

## Separate Container for Content

```html
<!-- Separate container for page content -->
<div class="container">
  <h1>Page Content</h1>
</div>
```

---

## Navbar Components

- `navbar-brand` - Large, prominent brand/logo text
- `navbar-nav` - Container for navigation links
- `nav-item` - Individual navigation items
- `nav-link` - Navigation link styling (can include `active` class)

---

## Responsive Navbar

- `navbar-expand-(breakpoint)` - Controls when the navbar collapses
- `navbar-toggler` - The hamburger menu button
- `collapse navbar-collapse` - The collapsible navigation content

---

## Navbar Toggle Functionality

The navbar toggler connects to the collapsible content using:

- `data-bs-toggle="collapse"` on the button
- `data-bs-target="#navbarId"` pointing to the collapse element's ID

This creates a responsive navigation that collapses into a hamburger menu on smaller screens.

---

# Happy coding!

## **[badrsoliman.com](https://www.badrsoliman.com)**
