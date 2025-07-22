# CSS

---

## 1. CSS Selectors

| Selector                | Example            | Description                                  |
|-------------------------|--------------------|----------------------------------------------|
| Element                 | `div`              | All `<div>` elements                         |
| Class                   | `.box`             | All elements with class "box"                |
| ID                      | `#header`          | The element with id "header"                 |
| Attribute               | `input[type="text"]` | Input elements of type text                  |
| Descendant              | `ul li`            | All `<li>` inside `<ul>`                     |
| Child                   | `ul > li`          | Direct children `<li>` of `<ul>`             |
| Adjacent Sibling        | `h2 + p`           | First `<p>` immediately after `<h2>`         |
| General Sibling         | `h2 ~ p`           | All `<p>` after an `<h2>` sibling            |
| Pseudo-class            | `a:hover`          | `<a>` elements on hover                      |
| Pseudo-element          | `p::first-line`    | First line of all `<p>` elements             |

---

## 2. CSS Specificity & Cascade

- **Inline style** > **ID selector** > **Class/Attribute/Pseudo-class selector** > **Element/Pseudo-element selector** > **Universal selector**
- Later rules override earlier ones if specificity is equal.

---

## 3. Box Model

```
+-----------------------+
|   Margin              |
|  +-----------------+  |
|  |   Border        |  |
|  | +-----------+   |  |
|  | | Padding   |   |  |
|  | | +-----+   |   |  |
|  | | | Box |   |   |  |
|  | | +-----+   |   |  |
|  | +-----------+   |  |
|  +-----------------+  |
+-----------------------+
```
- `width` = content width  
- `box-sizing: border-box;` includes padding & border in width

---

## 4. Positioning

| Property      | Values         | Description                              |
|---------------|---------------|------------------------------------------|
| `position`    | `static`      | Default, normal flow                     |
|               | `relative`    | Relative to itself (can use top/right)   |
|               | `absolute`    | Relative to nearest positioned ancestor  |
|               | `fixed`       | Relative to viewport                     |
|               | `sticky`      | Scrolls until a threshold, then fixes    |
| `top/right/bottom/left` | px/%/em | Offsets with positioned elements         |
| `z-index`     | number        | Stacking order                           |

---

## 5. Display & Visibility

- `display: block | inline | inline-block | flex | grid | none`
- `visibility: visible | hidden | collapse`
- `opacity: 0` (transparent but clickable)

---

## 6. Flexbox

```css
.container {
  display: flex;
  flex-direction: row; /* or column */
  justify-content: space-between; /* main axis */
  align-items: center; /* cross axis */
  flex-wrap: wrap;
  gap: 20px;
}
.child {
  flex: 1 1 200px; /* grow shrink basis */
  align-self: flex-start;
}
```

| Property                  | Description                        |
|---------------------------|------------------------------------|
| `flex-direction`          | row, column                        |
| `justify-content`         | flex-start, center, space-between  |
| `align-items`             | flex-start, center, stretch        |
| `flex-wrap`               | wrap, nowrap                       |
| `flex`                    | grow shrink basis                  |
| `align-self`              | Override align-items per child     |

---

## 7. CSS Grid

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto 200px;
  gap: 10px;
  grid-template-areas:
    "header header header"
    "sidebar main main";
}
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
```

| Property                  | Example/Values      | Description                      |
|---------------------------|--------------------|----------------------------------|
| `grid-template-columns`   | `1fr 2fr`          | Column sizes (fractional units)  |
| `grid-template-rows`      | `100px auto`       | Row sizes                        |
| `grid-area`               | `header`           | Assign area                      |
| `gap`                     | `20px`             | Space between rows/columns       |
| `place-items`             | `center`           | Align items both axes            |

---

## 8. Colors & Backgrounds

- Colors: `hex`, `rgb()`, `rgba()`, `hsl()`, `hsla()`, color names
- `background: color url("img.jpg") repeat center/cover no-repeat;`
- `background-size: cover | contain`
- `background-blend-mode: multiply | overlay | screen | ...`

---

## 9. Typography

- `font-family: "Roboto", Arial, sans-serif;`
- `font-size: 1rem | 16px | large | ...`
- `font-weight: 400 | bold | ...`
- `line-height: 1.5`
- `letter-spacing`, `word-spacing`
- `text-align: left | center | right | justify`
- `text-transform: uppercase | capitalize | lowercase`
- `text-shadow: 2px 2px 4px #000;`

---

## 10. Transitions & Animations

**Transition Example:**
```css
button {
  transition: background 0.3s ease, color 0.3s;
}
button:hover {
  background: #222;
  color: #fff;
}
```

**Animation Example:**
```css
@keyframes slidein {
  from { transform: translateX(-100%); }
  to   { transform: translateX(0); }
}
.element {
  animation: slidein 1s forwards;
}
```

---

## 11. Media Queries (Responsive Design)

```css
@media (max-width: 600px) {
  .container { flex-direction: column; }
  .sidebar { display: none; }
}
```

- `max-width`, `min-width`, `orientation`, `hover`, `prefers-color-scheme`...

---

## 12. Common CSS Functions

- `calc(100% - 80px)`
- `var(--main-color)`
- `clamp(1rem, 2vw, 2rem)`
- `rgba(255, 0, 0, 0.5)` (red, 50% opacity)
- `linear-gradient(90deg, #333, #eee)`

---

## 13. Common Pseudo-classes & Pseudo-elements

| Selector           | Description                          |
|--------------------|--------------------------------------|
| `:hover`           | On mouse hover                       |
| `:active`          | While being clicked                  |
| `:focus`           | When focused (e.g. input)            |
| `:nth-child(2n)`   | Every even child                     |
| `:first-child`     | First child                          |
| `:last-child`      | Last child                           |
| `::before`         | Insert content before element        |
| `::after`          | Insert content after element         |
| `::placeholder`    | Style input placeholder text         |

---

## 14. Useful CSS Snippets

**Center an element**
```css
.parent {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

**Responsive image**
```css
img {
  max-width: 100%;
  height: auto;
  display: block;
}
```

**Hide scrollbar (Webkit browsers)**
```css
.element::-webkit-scrollbar {
  display: none;
}
```

**Text overflow ellipsis**
```css
.ellipsis {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

---

## 15. Advanced Topics

- **Custom Properties (CSS Variables):**
  ```css
  :root { --main-color: #3498db; }
  .btn { background: var(--main-color); }
  ```

- **Selectors Level 4:**
  - `:is(.a, .b)`, `:where()`, `:not()`
  - `[type^="text"]` (attribute starts with)

- **Logical Properties:**
  - `margin-inline-start`, `padding-block-end`, etc.

- **Backdrop Filter (frosted glass):**
  ```css
  .glass {
    backdrop-filter: blur(6px) brightness(0.7);
    background: rgba(255,255,255,0.2);
  }
  ```

- **Container Queries:**
  ```css
  @container (max-width: 400px) {
    .card { font-size: 1rem; }
  }
  ```

---

## 16. Debugging Tools

- Browser DevTools: Elements, Styles, Computed, Network
- `outline: 2px solid red;` for debugging layouts
- CSS linting tools (stylelint)

---

## 17. Resources & References

- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [CSS Tricks](https://css-tricks.com/)
- [Flexbox Froggy](https://flexboxfroggy.com/)
- [Grid Garden](https://cssgridgarden.com/)
- [Smashing Magazine CSS](https://www.smashingmagazine.com/category/css/)
- [Can I use](https://caniuse.com/)

---

**Happy Styling!** 🎨
