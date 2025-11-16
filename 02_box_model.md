# Module 2: The Box Model

## Understanding the Box Model

Every HTML element is essentially a rectangular box. The CSS box model describes how these boxes are structured and how their size is calculated.

The box model consists of four parts (from inside to outside):

1. **Content** - The actual content (text, images, etc.)
1. **Padding** - Space between content and border
1. **Border** - A line around the padding
1. **Margin** - Space outside the border (between elements)

```
+----------------------------------+
|           Margin                 |
|  +--------------------------+    |
|  |        Border            |    |
|  |  +-------------------+   |    |
|  |  |     Padding       |   |    |
|  |  |  +------------+   |   |    |
|  |  |  |  Content   |   |   |    |
|  |  |  +------------+   |   |    |
|  |  +-------------------+   |    |
|  +--------------------------+    |
+----------------------------------+
```

## Content Area

The content area contains your actual content - text, images, etc.

```css
div {
  width: 300px;
  height: 200px;
}
```

## Padding

Padding creates space **inside** the element, between the content and the border.

### Padding Syntax

**All sides:**

```css
padding: 20px;  /* 20px on all sides */
```

**Vertical and horizontal:**

```css
padding: 10px 20px;  /* 10px top/bottom, 20px left/right */
```

**Individual sides (clockwise from top):**

```css
padding: 10px 15px 20px 25px;  /* top right bottom left */
```

**Individual properties:**

```css
padding-top: 10px;
padding-right: 15px;
padding-bottom: 20px;
padding-left: 25px;
```

**Example:**

```css
.box {
  padding: 20px;
  background-color: lightblue;
}
```

## Border

The border goes around the padding and content.

### Border Properties

**Shorthand:**

```css
border: 2px solid black;
/* width style color */
```

**Individual properties:**

```css
border-width: 2px;
border-style: solid;  /* solid, dashed, dotted, double, none */
border-color: black;
```

**Individual sides:**

```css
border-top: 1px solid red;
border-right: 2px dashed blue;
border-bottom: 3px dotted green;
border-left: 4px double orange;
```

**Border Radius (rounded corners):**

```css
border-radius: 10px;  /* All corners */
border-radius: 10px 20px 30px 40px;  /* top-left, top-right, bottom-right, bottom-left */
```

**Example:**

```css
.card {
  border: 2px solid #333;
  border-radius: 8px;
  padding: 20px;
}
```

## Margin

Margin creates space **outside** the element, between it and other elements.

### Margin Syntax

**All sides:**

```css
margin: 20px;
```

**Vertical and horizontal:**

```css
margin: 10px 20px;  /* 10px top/bottom, 20px left/right */
```

**Individual sides:**

```css
margin: 10px 15px 20px 25px;  /* top right bottom left */
```

**Individual properties:**

```css
margin-top: 10px;
margin-right: 15px;
margin-bottom: 20px;
margin-left: 25px;
```

**Centering with auto:**

```css
.container {
  width: 800px;
  margin: 0 auto;  /* Centers horizontally */
}
```

### Margin Collapse

When two vertical margins meet, they collapse into a single margin (the larger of the two).

```css
.box1 {
  margin-bottom: 20px;
}

.box2 {
  margin-top: 30px;
}
/* Space between boxes will be 30px, not 50px */
```

## Width and Height

Control the size of the content area.

```css
.box {
  width: 300px;
  height: 200px;
}
```

**Percentage values:**

```css
.container {
  width: 80%;  /* 80% of parent element */
}
```

**Min and max:**

```css
.responsive-box {
  width: 100%;
  max-width: 600px;  /* Won't exceed 600px */
  min-height: 200px; /* Won't be smaller than 200px */
}
```

## Box-Sizing Property

By default, width and height only apply to the content area. Padding and border are added on top, making elements larger than expected.

### content-box (default)

```css
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  /* Actual width = 300 + 40 (padding) + 4 (border) = 344px */
}
```

### border-box (recommended)

Width includes padding and border.

```css
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  /* Actual width = 300px (includes padding and border) */
}
```

**Best practice - apply to all elements:**

```css
* {
  box-sizing: border-box;
}
```

## Practical Examples

### Card Component

```css
.card {
  width: 300px;
  padding: 20px;
  margin: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

### Button

```css
.button {
  padding: 10px 20px;
  border: 2px solid #007bff;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  margin: 5px;
}
```

### Container

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
```

## Display Property Basics

Different elements have different default display values that affect the box model.

**Block elements** (take full width):

```css
div, p, h1, section {
  display: block;
}
```

**Inline elements** (only take necessary width):

```css
span, a, strong {
  display: inline;
}
```

**Note:** Width and height don’t work on inline elements. Vertical padding/margin may not work as expected.

**Inline-block** (best of both):

```css
.box {
  display: inline-block;
  width: 200px;  /* Now works! */
}
```

## Exercises

### Exercise 1: Box Model Exploration

Create a div with:

- Width: 400px
- Padding: 30px
- Border: 5px solid blue
- Margin: 20px
- Calculate the total space it takes up

### Exercise 2: Card Layout

Create three card components side by side with:

- Fixed width (250px)
- Padding inside
- Borders with rounded corners
- Margins between cards
- Different background colors

### Exercise 3: Centering

Create a centered container with:

- Max width of 800px
- Centered horizontally on the page
- Padding on all sides
- A border

### Exercise 4: Border Styles

Create four boxes demonstrating different border styles:

- Solid
- Dashed
- Dotted
- Double

### Exercise 5: Box-Sizing

Create two boxes with the same width value:

- One with `box-sizing: content-box`
- One with `box-sizing: border-box`
- Add padding and border to both
- Observe the difference in actual size

## Challenge Project: Product Card Grid

Create a grid of 6 product cards with:

- Each card has an image placeholder (use background-color)
- Product name (heading)
- Price
- Description
- Proper padding, margins, and borders
- Rounded corners
- Cards should be evenly spaced
- Use `box-sizing: border-box` for all elements
- Responsive max-width container

**Requirements:**

- Clean box model usage
- Consistent spacing
- Cards should look professional
- Use margin: 0 auto to center the container

## Common Mistakes to Avoid

1. **Forgetting box-sizing:** Always set `box-sizing: border-box`
1. **Margin collapse confusion:** Remember vertical margins collapse
1. **Inline element sizing:** Can’t set width/height on inline elements
1. **Padding vs Margin:** Padding has background color, margin doesn’t

## Key Takeaways

- Every element is a box with content, padding, border, and margin
- `box-sizing: border-box` makes sizing more predictable
- Padding creates space inside, margin creates space outside
- Margins can collapse vertically
- Use browser DevTools to visualize the box model

-----

**Previous Module:** [Module 1 - CSS Fundamentals](module-01-fundamentals.md)  
**Next Module:** [Module 3 - Typography](module-03-typography.md)

## Additional Resources

- [MDN Box Model Guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
- [CSS-Tricks Box Sizing](https://css-tricks.com/box-sizing/)
