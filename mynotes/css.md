## ❖ Cascading Style Sheets (CSS)

### 1. **What is a CSS rule?**

A **CSS rule** (or rule set) consists of a **selector** and a **declaration block**:

```css
selector {
  property1: value1;
  property2: value2;
  /* … */
}
```

* **Selector**: Targets the HTML element(s) you want to style (e.g., `p`, `.button`, `#header`).
* **Declarations**: Inside the `{}`, each **property** (e.g., `color`, `margin`) is paired with a **value** (`blue`, `10px`). Multiple declarations are separated by semicolons.

**Example:**

```css
.button {
  background-color: #007bff;
  color: white;
  padding: 0.5em 1em;
}
```

**Follow-up Questions:**

* How do compound selectors work (e.g., `.nav .item`)?
* What is the difference between a rule and an at-rule (e.g., `@media`)?

---

### 2. **What is CSS reset, and why should we use it?**

A **CSS reset** is a small set of CSS rules that “resets” or **normalizes** browser default styles, providing a consistent baseline across different browsers.

* **Problem:** Browsers apply their own default margins, paddings, font-sizes, etc., leading to inconsistencies.
* **Solution:** A reset (or normalize.css) zeroes out or standardizes these defaults.

**Example Reset Snippet:**

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

**Why use it?**

* Ensures all browsers start from the same point.
* Reduces cross-browser quirks.
* Simplifies layout work by removing unexpected spacing.

**Follow-up Questions:**

* What’s the difference between a reset stylesheet and Normalize.css?
* Does resetting everything to zero have performance implications?

---

### 3. **What is the meaning of the word “Cascade”? Describe it.**

The “Cascade” in CSS describes **how conflicting style rules are resolved** based on:

1. **Origin & Importance**

   * Browser defaults < User-defined < !important
2. **Specificity**

   * Inline styles > IDs > classes/attributes/pseudo-classes > elements/pseudo-elements
3. **Source Order**

   * Later rules override earlier ones when specificity is equal.

**Example:**

```html
<p class="lead" id="intro">Hello CSS!</p>
```

```css
p { color: blue; }              /* specificity 1 */
.lead { color: green; }         /* specificity 10 */
#intro { color: red; }          /* specificity 100 */
```

Result: the paragraph is **red** because the ID rule wins.

**Follow-up Questions:**

* How does `!important` affect the cascade?
* What’s the exact point calculation for compound selectors?

---

### 4. **What are the two types of elements in HTML?**

In CSS context we often distinguish:

1. **Block-level elements**

   * Start on a new line and stretch to full width by default.
   * Examples: `<div>`, `<p>`, `<h1>`–`<h6>`, `<ul>`, `<section>`.
2. **Inline elements**

   * Do not start on a new line; only take up as much width as necessary.
   * Examples: `<span>`, `<a>`, `<img>`, `<strong>`, `<em>`.

(Note: HTML5 introduced more semantic grouping, but from a CSS layout standpoint, block vs. inline still matters.)

**Follow-up Questions:**

* What are inline-block elements?
* How do you convert an inline element into a block with CSS?

---

### 5. **Describe types of measurement units in CSS**

CSS supports several unit types, mainly divided into **absolute** and **relative** units:

* **Absolute units** (fixed size, not responsive):

  * `px` (pixels)
  * `pt` (points; 1pt = 1/72 inch)
  * `cm`, `mm`, `in` (physical measurements)
* **Relative units** (scale based on context):

  * `em` (relative to the font-size of the element)
  * `rem` (relative to the root element’s font-size)
  * `%` (percentage relative to the parent’s property)
  * `vw`, `vh` (1% of viewport width/height)
  * `vmin`, `vmax` (min/max of viewport dimensions)
  * `ch` (width of the “0” character)
  * `ex` (height of the “x” character)

**Follow-up Questions:**

* When would you choose `rem` over `em`?
* What’s the difference between `vw` and `%` for width?

---

### 6. **Describe the difference between absolute and relative positions**

* **`position: absolute;`**

  * Removed from the normal document flow.
  * Positioned relative to the nearest **positioned ancestor** (`relative`, `absolute`, `fixed`, or `sticky`); otherwise, the viewport.
  * Doesn’t reserve space in the layout.

* **`position: relative;`**

  * Remains in the normal flow.
  * Offsets (`top`, `left`, etc.) move the element **visually**, but its original spot still occupies space.

**Example:**

```css
.container { position: relative; }
.child {
  position: absolute;
  top: 10px;
  left: 20px;
}
```

**Follow-up Questions:**

* How do `top: auto` and `bottom: auto` differ?
* What’s stacking context and how do positions affect it?

---

### 7. **What is the default position of an element?**

By default, every element has:

```css
position: static;
```

* **`static`** means it’s in the normal document flow.
* **`top`, `right`, `bottom`, `left`** properties do **not** apply.

To use offsets or stacking, you must switch to `relative`, `absolute`, `fixed`, or `sticky`.

**Follow-up Questions:**

* Can you transition an element from `static` to another positioning?
* Does `static` create a new stacking context?

---

### 8. **How does the box model help in web designing and what are its areas?**

Every HTML element is a **rectangular box**, governed by the **CSS box model**:

```
+---------------------------+
|        Margin             |
|  +---------------------+  |
|  |     Border          |  |
|  |  +---------------+  |  |
|  |  |   Padding     |  |  |
|  |  | +-----------+ |  |  |
|  |  | | Content   | |  |  |
|  |  | +-----------+ |  |  |
|  |  +---------------+  |  |
|  +---------------------+  |
+---------------------------+
```

* **Content box**: The actual content (text, image).
* **Padding**: Space between content and border.
* **Border**: The frame around padding + content.
* **Margin**: Space outside the border, separating boxes.

**Why it helps:**

* Precise control over spacing, borders, and layout.
* Consistent sizing (especially with `box-sizing: border-box;`).

**Follow-up Questions:**

* What’s the difference between `content-box` and `border-box` sizing?
* How do negative margins work?

---

### 9. **How do sticky positions work?**

* **`position: sticky;`** acts like `relative` until a threshold, then like `fixed`.
* Combined with an offset (e.g., `top: 0`), it “sticks” to that spot in its **scroll container** when you scroll past it.

**Example:**

```css
header {
  position: sticky;
  top: 0;
  background: white;
}
```

The header scrolls with the page until it reaches the top of the viewport, then remains fixed there.

**Follow-up Questions:**

* Which parent overflow settings break `position: sticky`?
* Can you use `sticky` horizontally?

---

### 10. **What is the difference between sticky and fixed positions?**

* **`position: fixed;`**

  * Removed from flow and always positioned relative to the viewport.
  * Stays in place even when the page scrolls.
  * Does not require scroll threshold.

* **`position: sticky;`**

  * Behaves like `relative` until it crosses a defined offset in its container, then acts like `fixed`.
  * Only “sticks” within its parent’s scroll area.

**Key Distinction:**

* **Fixed** is always fixed; **Sticky** toggles between relative and fixed based on scroll.

**Follow-up Questions:**

* How do z-index and stacking apply to fixed vs. sticky?
* Are there performance considerations using many sticky elements?

---

### 11. **When should we use `position: relative`?**

Use `position: relative` when you need to **nudge** an element from its normal flow **without removing it**:

* **Offsetting**: You want to move an element **slightly** (e.g., `top: 5px;`) but still have its original spot reserve space.
* **Positioning children**: If you apply `position: absolute` to a child, setting the parent to `position: relative` establishes the parent as the **containing block** for that absolutely-positioned child.
* **Layering**: You need to create a new stacking context for z-index purposes (though note: `position: relative` alone doesn’t always create a new stacking context—`z-index` will).

```css
.card {
  position: relative;
  top: 10px;            /* nudges the card down 10px */
  left: 0;
  z-index: 10;          /* now can layer above other elements */
}
.card .badge {
  position: absolute;   /* positioned relative to .card */
  top: 5px;
  right: 5px;
}
```

**Follow-up Questions:**

* How does `position: relative` interact with `transform: translate()`?
* Can you animate a relative offset?

---

### 12. **What are `em` and `rem`?**

Both are **relative units** tied to font sizes:

* **`em`**

  * Relative to the **font-size of the current element**.
  * Cascading effect: if a parent’s font-size is 20px, `1.5em` on the child equals 30px.
* **`rem`**

  * Relative to the **root element’s** (`<html>`) font-size.
  * Consistent across the document (commonly 16px by default).

```css
html { font-size: 16px; }
p {
  font-size: 1.25rem; /* 1.25 × 16px = 20px */
}
p span {
  font-size: 2em;     /* 2 × (20px) = 40px */
}
```

**When to use which?**

* Use `rem` for **global sizing** patterns (fonts, spacing) to maintain consistency.
* Use `em` when an element’s size should **scale with its parent** (e.g., padding inside buttons that grow with text).

**Follow-up Questions:**

* What happens if you change `<body>` font-size—does `rem` change?
* How do `em` and `rem` compare to viewport units (`vw`, `vh`) for responsive typography?

---

### 13. **Explain the difference between Flex and Grid layout**

Both are modern CSS layout systems, but they serve slightly different use-cases:

| Aspect           | Flexbox                                                                  | Grid                                                     |
| ---------------- | ------------------------------------------------------------------------ | -------------------------------------------------------- |
| **Axis**         | One-dimensional (row **or** column at a time)                            | Two-dimensional (rows **and** columns)                   |
| **Use-case**     | Aligning items in a single row/column, distributing space along one axis | Complex layouts: entire page sections or component grids |
| **Container**    | `display: flex;`                                                         | `display: grid;`                                         |
| **Item control** | `justify-content` (main axis), `align-items` (cross axis)                | `grid-template-rows/columns`, `grid-gap`                 |
| **Ordering**     | `order` property to reorder flex items                                   | `grid-area` or line-based placement                      |

**Examples:**

<details>
<summary>Flexbox (horizontal nav)</summary>

```css
.nav {
  display: flex;
  justify-content: space-between;
}
```

</details>

<details>
<summary>Grid (two-dimensional card layout)</summary>

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);  
  grid-gap: 16px;
}
```

</details>

**Follow-up Questions:**

* Can you nest Flex inside Grid and vice versa?
* When does using both together make sense?

---

### 14. **How many selectors are there in CSS? Explain their usage one by one with examples.**

CSS selectors fall into several categories. Here’s an overview with examples:

1. **Type (Element) Selector**

   * Targets by tag name.

   ```css
   p { color: blue; }
   ```
2. **Class Selector**

   * Targets elements with a given class.

   ```css
   .button { padding: 8px 16px; }
   ```
3. **ID Selector**

   * Targets a unique element with that ID.

   ```css
   #header { background: gray; }
   ```
4. **Attribute Selector**

   * Targets elements with specified attributes.

   ```css
   input[type="text"] { border: 1px solid #ccc; }
   ```
5. **Universal Selector**

   * Targets **all** elements.

   ```css
   * { box-sizing: border-box; }
   ```
6. **Pseudo-class Selector**

   * Targets elements in a special state.

   ```css
   a:hover { text-decoration: underline; }
   ```
7. **Pseudo-element Selector**

   * Targets parts of an element.

   ```css
   p::first-line { font-weight: bold; }
   ```
8. **Descendant Selector**

   * Targets elements nested inside another.

   ```css
   .nav a { color: white; }
   ```
9. **Child Selector**

   * Only immediate children.

   ```css
   ul > li { list-style: none; }
   ```
10. **Adjacent Sibling Selector**

    * Targets an element immediately preceded by another.

    ```css
    h2 + p { margin-top: 0; }
    ```
11. **General Sibling Selector**

    * Targets all siblings after another.

    ```css
    h2 ~ p { color: gray; }
    ```
12. **Group Selector**

    * Combines multiple selectors.

    ```css
    h1, h2, h3 { font-family: sans-serif; }
    ```
13. **Negation Selector**

    * Excludes specific elements.

    ```css
    input:not([type="submit"]) { background: #f9f9f9; }
    ```

**Follow-up Questions:**

* Which selectors are most specific?
* How do you write an attribute selector for “starts with” or “contains”?

---

### 15. **Explain how the cascades are resolved step by step**

When multiple CSS rules target the same element/property, the browser follows these steps:

1. **Importance & Origin**

   * User `!important` > Author `!important` > Author normal > User normal > Browser defaults.
2. **Specificity Calculation**

   * Count ID selectors (×100), class/attribute/pseudo-class selectors (×10), element/pseudo-element selectors (×1).
   * Higher total wins.
3. **Source Order**

   * If specificity and importance tie, **later** rules override **earlier** ones in the stylesheet or document.
4. **Inline Styles**

   * Treated with high specificity (same as IDs) but still subject to `!important` rules.

**Example Conflict:**

```html
<p id="intro" class="lead">Welcome!</p>
```

```css
p { color: blue; }               /* specificity 0-0-1 */
.lead { color: green; }          /* 0-1-0 */
#intro { color: red; }           /* 1-0-0 */
p.lead { color: orange; }        /* 0-1-1 = 11 */
```

* The `#intro` rule (100) outweighs `p.lead` (11), so the text is **red**.

**Follow-up Questions:**

* How do user stylesheets interact with author styles?
* Can specificity ever be “too high” or problematic?

---

### 16. **What is a transition?**

A **CSS transition** animates property changes **smoothly** over time.

* **Properties:** Which CSS properties to animate (e.g., `width`, `background-color`).
* **Duration:** How long the transition lasts.
* **Timing-function:** How the intermediate values are calculated (`ease`, `linear`, etc.).
* **Delay:** Time before the transition starts.

```css
button {
  transition: background-color 0.3s ease-in-out 0s;
}
button:hover {
  background-color: darkblue;
}
```

On hover, `background-color` will gradually shift to dark blue over 0.3 seconds.

**Follow-up Questions:**

* Can you transition between `display: none` and `display: block`?
* How do you chain multiple transitions?

---

### 17. **What are keyframes in CSS?**

**Keyframes** define **complex animations** by specifying **intermediate steps**:

```css
@keyframes slideIn {
  0%   { transform: translateX(-100%); }
  50%  { transform: translateX(10%); }
  100% { transform: translateX(0); }
}

.box {
  animation: slideIn 1s ease-out forwards;
}
```

* **`@keyframes name`**: Declare sequence.
* **Percentages or from/to**: Define start (0%/from) and end (100%/to) states, plus any in-between.
* **`animation` shorthand**: Combine name, duration, timing, delay, iteration count, direction.

**Follow-up Questions:**

* How do you pause and resume CSS animations?
* What’s the difference between `animation-fill-mode` values?

---

### 18. **Explain about media queries and write down a media query for 320px–375px devices**

**Media queries** apply CSS only when certain conditions (viewport width, resolution, orientation) are met:

```css
@media (min-width: 320px) and (max-width: 375px) {
  body {
    font-size: 14px;
  }
  .container {
    padding: 1rem;
  }
}
```

* **`@media`**: Starts the query.
* **Conditions**: `min-width`, `max-width`, `orientation`, etc.
* **Block**: Styles inside only apply when conditions are true.

**Follow-up Questions:**

* What’s the difference between `max-width` and `max-device-width`?
* How do you write queries for high-DPI (Retina) screens?

---

### 19. **Explain CSS inheritance with an example**

**Inheritance** means certain CSS properties set on a parent element are **inherited** by its children (unless overridden).

* **Inherited properties**: `color`, `font-family`, `line-height`, `visibility`.
* **Non-inherited**: `margin`, `padding`, `border`, `width`, `height`.

```css
article {
  color: #333;
  font-family: Georgia, serif;
}
article p {
  /* No color specified—inherits #333 */
}
article p a {
  color: blue;   /* overrides inherited color */
}
```

In this example, all `<p>` and `<a>` inside `<article>` start with `#333`, but links override to blue.

**Follow-up Questions:**

* How do you disable inheritance for a property?
* What’s the `all: initial` declaration?

---

### 20. **Explain how the browser performs the rendering process of a web page**

1. **Parsing HTML → DOM Tree**

   * Browser reads HTML and builds the **Document Object Model**.
2. **Parsing CSS → CSSOM**

   * CSS (external, internal, inline, user-agent) is parsed into the **CSS Object Model**.
3. **Constructing Render Tree**

   * Combines DOM + CSSOM, discarding hidden elements (`display: none`), and computes styles.
4. **Layout (Reflow)**

   * Calculates the size and position of each render-tree node.
5. **Painting**

   * Fills in pixels: colors, text, images, borders.
6. **Compositing**

   * Layers are combined, accounting for stacking contexts, transforms, and opacity.

This pipeline is why:

* Changes to CSS can trigger **repaints** or **reflows** (expensive).
* Minimizing layout thrashing and batching DOM/CSS changes can improve performance.

**Follow-up Questions:**

* What’s the difference between repaint and reflow?
* How do tools like Chrome DevTools help profile rendering?

---
