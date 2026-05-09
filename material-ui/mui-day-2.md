---
marp: true
paginate: true
backgroundColor: #f5f5f5
theme: default
---

# Material UI for React/Next.js - Day 2

### Badr Aldien Soliman

---


## 1. Menu and MenuItem

Menus display a list of choices on temporary surfaces.

- **Basics**: Triggered by an element (like a button) and anchored to it.
- **Nested Menus**: Supporting sub-levels of navigation.
- **Keyboard Navigation**: Built-in support for arrow keys and Enter.
- **Context Menus**: Menus triggered by right-click.

---

## 2. Card

Cards contain content and actions about a single subject.

- **CardHeader**: Title, subtitle, and avatar.
- **CardMedia**: Images or videos.
- **CardContent**: The main body text.
- **CardActions**: Buttons or links at the bottom.

**Exercise**: Build a product showcase with cards.

---

## 3. Dialog

Dialogs inform users about a task and can contain critical information or require decisions.

- **Structure**: Title -> Content -> Actions.
- **Modal**: Blocks interaction with the rest of the app until dismissed.
- **Use Cases**: Alerts, form inputs, or confirmations.

**Exercise**: Create a set of dialogs for different use cases.

---

## 4. Container

The container centers your content horizontally. It's the most basic layout element.

- **Fluid**: Scales with the viewport width (`maxWidth` prop).
- **Fixed**: Snaps to discrete breakpoints.
- **Best Practice**: Combine with `Grid` or `Stack` for internal layout.

**Exercise**: Build a responsive page layout using containers.

---

## 5. Accordion

An accordion allows users to toggle the display of sections of content.

- **AccordionSummary**: The header that users click to expand.
- **AccordionDetails**: The expandable content area.
- **Controlled**: Manage the expanded state yourself for more control.

**Exercise**: Create an FAQ section with accordions.

---

## 6. Drawer

Navigation drawers provide access to destinations in your app.

- **Types**:
    - **Temporary**: Overlays the UI.
    - **Permanent**: Always visible on the side.
    - **Persistent**: Can be toggled but pushes content.
- **Positioning**: `left`, `right`, `top`, `bottom`.

**Exercise**: Build a sidebar navigation with a drawer.

---

## 7. Snackbar

Snackbars provide brief messages about app processes at the bottom of the screen.

- **Duration**: Automatically disappears after a set time.
- **Actions**: Can include a "Close" or "Undo" button.
- **Queuing**: Handle multiple notifications efficiently.

**Exercise**: Implement a notification system with snackbars.

---


## Additional Resources

- **Material UI Official Docs**: [mui.com](https://mui.com)
- **Material Design Guidelines**: [m3.material.io](https://m3.material.io)
- **React Hook Form**: [react-hook-form.com](https://react-hook-form.com)
- **Zod**: [zod.dev](https://zod.dev)

---

## Bonus Exercises

- **Breadcrumbs**: Navigation trail for page hierarchy.
- **Pagination**: Navigate large datasets.
- **Stepper**: Step-by-step progress indicator.
- **SpeedDial**: FAB with quick actions.
- **Popover & Popper**: Floating content containers and positioning engine.

