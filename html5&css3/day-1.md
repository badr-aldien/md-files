---
marp: true
paginate: true
---

# HTML5 - Day 1

### Badr Aldien Soliman

---

## 1. Introduction to HTML5

HTML5 is the latest version of the HyperText Markup Language. 

It provides a more semantic way to structure web pages and includes built-in support for multimedia and advanced features.

### Simplified Syntax
The Doctype and Charset are much simpler now:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>HTML5 Page</title>
</head>
```

---

## 2. Semantic Elements

Semantic elements clearly describe their meaning to both the browser and the developer.

| Element      | Description                                      |
| ------------ | ------------------------------------------------ |
| `<header>`   | Defines a header for a document or section      |
| `<nav>`      | Defines a set of navigation links                |
| `<main>`     | Specifies the main content of a document         |
| `<footer>`   | Defines a footer for a document or section      |
| `<section>`  | Defines a section in a document                  |
| `<article>`  | Defines an independent, self-contained content   |
| `<aside>`    | Defines content aside from the page content      |

---

### Semantic Layout Example

```html
<body>
  <header>
    <h1>My Website</h1>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>Post Title</h2>
      <p>Content goes here...</p>
    </article>
  </main>

  <footer>
    <p>&copy; 2024 Badr Aldien</p>
  </footer>
</body>
```

---

## 3. New Form Input Types

HTML5 introduced specialized input types that provide better user experiences and automatic validation.

```html
<!-- Email and URL -->
<input type="email" placeholder="Enter your email" required>
<input type="url" placeholder="Enter website URL">

<!-- Dates and Numbers -->
<input type="date">
<input type="number" min="1" max="100">

<!-- Range and Color -->
<input type="range" min="0" max="10">
<input type="color">
```

---

### New Form Attributes

- **`placeholder`**: Displays a hint in the input field.
- **`required`**: Makes an input field mandatory.
- **`autofocus`**: Focuses the input automatically on page load.
- **`pattern`**: Allows validation using a regular expression.
- **`list`**: Connects an input to a `<datalist>` for suggestions.

```html
<input type="text" list="browsers">
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Edge">
</datalist>
```

---

## 4. Multimedia: Video and Audio

Before HTML5, you needed plugins (like Flash) to play media. Now, it's native.

### Video Element
```html
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
  Your browser does not support the video tag.
</video>
```

---

### Audio Element

```html
<audio controls>
  <source src="music.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

#### Common Attributes:
- `controls`: Displays the play/pause/volume buttons.
- `autoplay`: Starts playing automatically.
- `muted`: Starts the media on mute.
- `loop`: Repeats the media.

---

## 5. Other HTML5 Features

### The `<figure>` and `<figcaption>` Elements
Used to mark up a photo with a caption.

```html
<figure>
  <img src="img_pulpit.jpg" alt="The Pulpit Rock" width="304" height="228">
  <figcaption>Fig.1 - A view of the Pulpit Rock, Norway.</figcaption>
</figure>
```

---

### Progress and Meter
Visual indicators for task completion or scalar measurements.

```html
<!-- Progress Bar -->
<label for="file">Downloading:</label>
<progress id="file" value="70" max="100"> 70% </progress>

<!-- Scalar Gauge -->
<label for="temp">Temperature:</label>
<meter id="temp" min="0" max="100" low="30" high="80" optimum="50" value="65"></meter>
```

---

## Key HTML5 Terms Review

- **Semantic**: Elements that provide meaning (e.g., `<main>`, `<article>`).
- **Validation**: Checking input data automatically (e.g., `type="email"`).
- **Native Media**: Playing audio/video without external tools.
- **Data Attributes**: Custom storage using `data-*` (e.g., `data-user-id`).
- **Web Storage**: `localStorage` and `sessionStorage` for client-side data.

---

# Read the error again

## **[badrsoliman.com](https://www.badrsoliman.com)**
