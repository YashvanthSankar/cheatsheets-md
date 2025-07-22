# HTML

---

## Table of Contents

1. Introduction to HTML
2. HTML Document Structure
3. Text Formatting Tags
4. Links and Images
5. Lists (Ordered & Unordered)
6. Tables
7. Forms and Inputs
8. Semantic HTML
9. Multimedia: Audio and Video
10. Best Practices & Accessibility
11. Final Project

---

## 1: Introduction to HTML

**HTML** stands for *HyperText Markup Language*. It is the standard language for creating web pages and web applications.

- **HTML elements** are building blocks of web pages.
- HTML elements are represented by **tags**.

**Example:**
```html
<p>Hello, world!</p>
```

**Exercise:**  
Write a simple HTML tag that displays your name.

---

## 2: HTML Document Structure

A basic HTML document looks like this:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Web Page</title>
  </head>
  <body>
    <h1>Welcome!</h1>
    <p>This is my first web page.</p>
  </body>
</html>
```

- `<!DOCTYPE html>`: Declares the document as HTML5.
- `<html>`: Root element.
- `<head>`: Contains meta-information, like the title.
- `<title>`: Sets the page title (appears in browser tab).
- `<body>`: Contains visible content.

**Exercise:**  
Create an HTML file with your own title and a welcome message.

---

## 3: Text Formatting Tags

Common tags for text:

- Headings: `<h1>` to `<h6>`
- Paragraph: `<p>`
- Bold: `<strong>`
- Italic: `<em>`
- Line break: `<br>`
- Horizontal rule: `<hr>`

**Example:**
```html
<h1>Main Heading</h1>
<p>This is <strong>important</strong> and <em>emphasized</em> text.</p>
<hr>
```

**Exercise:**  
Write a paragraph using bold and italic text, and add a heading above it.

---

## 4: Links and Images

**Links:**
```html
<a href="https://www.example.com">Visit Example</a>
```

**Images:**
```html
<img src="image.jpg" alt="Description of image">
```

- `href`: URL for links.
- `src`: Image file path.
- `alt`: Alternative text for accessibility.

**Exercise:**  
Add a link to your favorite website and display an image with a descriptive alt text.

---

## 5: Lists (Ordered & Unordered)

**Unordered List:**
```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
</ul>
```

**Ordered List:**
```html
<ol>
  <li>First</li>
  <li>Second</li>
</ol>
```

**Exercise:**  
Create an ordered list of your top 3 favorite movies and an unordered list of your hobbies.

---

## Lesson 6: Tables

**Example:**
```html
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>John</td>
    <td>25</td>
  </tr>
  <tr>
    <td>Jane</td>
    <td>28</td>
  </tr>
</table>
```

- `<table>`: Table container.
- `<tr>`: Table row.
- `<th>`: Table header cell.
- `<td>`: Table data cell.

**Exercise:**  
Make a table with 2 columns: "Country" and "Capital", and add 3 rows.

---

## 7: Forms and Inputs

**Example:**
```html
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name">
  
  <label for="email">Email:</label>
  <input type="email" id="email" name="email">
  
  <input type="submit" value="Submit">
</form>
```

- `<form>`: Form container.
- `<input>`: Input field (types: text, email, password, etc.)
- `<label>`: Label for input.

**Exercise:**  
Create a form with fields for Name, Age, and a Submit button.

---

## 8: Semantic HTML

Semantic tags describe the meaning of content:

- `<header>`: Top section (logo, nav, etc.)
- `<nav>`: Navigation links.
- `<main>`: Main content.
- `<article>`: Self-contained content.
- `<section>`: Thematic grouping.
- `<footer>`: Bottom section.

**Example:**
```html
<header>
  <h1>My Blog</h1>
</header>
<nav>
  <a href="#home">Home</a>
  <a href="#about">About</a>
</nav>
<main>
  <article>
    <h2>First Post</h2>
    <p>Hello!</p>
  </article>
</main>
<footer>
  &copy; 2025 My Blog
</footer>
```

**Exercise:**  
Structure a simple web page using at least three semantic tags.

---

## 9: Multimedia: Audio and Video

**Audio:**
```html
<audio controls>
  <source src="song.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

**Video:**
```html
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
```

**Exercise:**  
Embed an audio file and a video file in your web page.

---

## 10: Best Practices & Accessibility

- Always use `alt` for images.
- Use semantic tags.
- Make forms accessible with `label`.
- Use proper heading order (`h1`, then `h2`, etc.).
- Validate your HTML using [W3C Validator](https://validator.w3.org/).

**Exercise:**  
Review one of your HTML files and improve its accessibility.

---

## Final Project

**Build a personal profile page** that includes:

- Your name and photo
- A short biography
- Links to your social media
- An ordered list of your skills
- A table of your favorite books (title + author)
- A contact form

---

## Additional Resources

- [MDN Web Docs: HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [W3Schools HTML Tutorial](https://www.w3schools.com/html/)
- [HTML Reference](https://htmlreference.io/)

---

**Happy Learning!**
