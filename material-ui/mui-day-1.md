---
marp: true
paginate: true
backgroundColor: #f5f5f5
theme: default
---

# Material UI for React/Next.js - Day 1

### Badr Aldien Soliman

---


## 1. Setup Environment

### Installing Material UI
```bash
npm install @mui/material @emotion/react @emotion/styled
```

### Key Imports
```tsx
import { Button, Typography } from '@mui/material';
```

---

## 2. Typography

The `Typography` component makes it easy to apply a default set of font weights and sizes to your application.

- **Variants**: `h1` through `h6`, `body1`, `body2`, `subtitle1`, `subtitle2`, `caption`.
- **Props**: `align`, `gutterBottom`, `noWrap`, `color`.
- **Semantic HTML**: Use the `component` prop to change the underlying HTML element while keeping the visual style.

---

## 3. Buttons

MUI provides three main types of buttons:

- **Contained**: High emphasis (e.g., "Submit").
- **Outlined**: Medium emphasis (e.g., "Cancel").
- **Text**: Low emphasis (e.g., "Learn More").

### Features:
- **Sizes**: `small`, `medium`, `large`.
- **Icons**: `startIcon` or `endIcon` props.
- **Icon Buttons**: Use `IconButton` for buttons with only an icon.

---

## 4. TextFields - User Input

The `TextField` wrapper component is a complete form control including a label, input, and help text.

- **Variants**: `outlined` (default), `filled`, `standard`.
- **Props**:
    - `label`: Floating label.
    - `helperText`: Text below the input.
    - `error`: Boolean to toggle error state.
    - `multiline`: For text areas.

---

## 5. Layout Components

### **Stack**
- Manages layout of immediate children along the vertical or horizontal axis.
- Uses `spacing` prop for consistent gaps.

### **Box**
- A wrapper component for all your CSS needs.
- Use the `sx` prop for quick styling.

### **Divider**
- A thin line that groups content in lists and layouts.

---

## 6. AppBar and Toolbar

The `AppBar` displays information and actions relating to the current screen.

- **Positioning**: `fixed`, `absolute`, `sticky`, `static`, `relative`.
- **Toolbar**: Used as a child of AppBar to provide padding and align items horizontally.
- **Integration**: Works perfectly with `IconButton` and `Menu` for navigation.

---

## 7. Tabs

Tabs make it easy to explore and switch between different views.

- **Tabs**: The container for `Tab` components.
- **Tab**: Individual selection items.
- **TabPanel**: Content shown when a specific tab is selected.
- **Options**: Vertical/Horizontal, scrollable, with icons.

---

## 8. ThemeProvider

MUI allows you to customize the look and feel using a theme.

- **createTheme()**: Function to define colors, typography, spacing, etc.
- **ThemeProvider**: Context provider to inject the theme into your app.

```tsx
const theme = createTheme({
  palette: {
    primary: { main: '#1976d2' },
  },
});

<ThemeProvider theme={theme}>
  <App />
</ThemeProvider>
```

---

## Day 1 Task: Multi-step Signup Form

1. Build a **multi-step signup form** using Material UI.
2. Include: text, email, password, select, and checkbox.
3. Use **Zod** for validation on each step.
4. Display errors using `TextField`'s `error` and `helperText`.
5. Add a progress indicator (Tabs or Stepper).
6. Show a “Signup successful!” message on completion.

💡 *Hint: Use Container, Box, and Stack for layout.*


