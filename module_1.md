# Module 1: CSS Fundamentals

## What is CSS?

CSS (Cascading Style Sheets) is the language used to style and layout web pages. While HTML provides the structure and content, CSS makes it look good by controlling colors, fonts, spacing, positioning, and much more.

## CSS Syntax

CSS follows a simple pattern:

```css
selector {
  property: value;
  another-property: another-value;
}
```

**Example:**

```css
h1 {
  color: blue;
  font-size: 36px;
  text-align: center;
}
```

This rule selects all `<h1>` elements and makes them blue, 36 pixels tall, and centered.

## Three Ways to Add CSS

### 1. Inline CSS (Not Recommended)

CSS written directly in HTML elements using the `style` attribute.

```html
<p style="color: red; font-size: 18px;">This is red text.</p>
```

**Pros:** Quick for testing
**Cons:** Hard to maintain, not reusable, mixes content with presentation

### 2. Internal CSS

CSS written inside a `<style>` tag in the HTML `<head>` section.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      color: red;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <p>This is red text.</p>
</body>
</html>
```

**Pros:** Good for single-page styles
**Cons:** Not reusable across multiple pages

### 3. External CSS (Best Practice)

CSS written in a separate `.css` file and linked to HTML.

**styles.css:**

```css
p {
  color: red;
  font-size: 18px;
}
```

**index.html:**

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <p>This is red text.</p>
</body>
</html>
```

**Pros:** Reusable, maintainable, separates concerns
**Cons:** Requires an extra HTTP request (minimal impact)

## CSS Selectors

### Element Selector

Selects all elements of a specific type.

```css
p {
  color: blue;
}
```

Selects all `<p>` elements.

### Class Selector

Selects elements with a specific class. Use a dot (`.`) before the class name.

```css
.highlight {
  background-color: yellow;
}
```

```html
<p class="highlight">This paragraph is highlighted.</p>
```

### ID Selector

Selects a single element with a specific ID. Use a hash (`#`) before the ID name.

```css
#header {
  font-size: 24px;
}
```

```html
<div id="header">This is the header.</div>
```

**Important:** IDs should be unique on a page. Use classes for styling multiple elements.

### Universal Selector

Selects all elements. Use the asterisk (`*`).

```css
* {
  margin: 0;
  padding: 0;
}
```

## Common CSS Properties

### Text and Font Properties

```css
color: red;                    /* Text color */
font-size: 16px;               /* Text size */
font-family: Arial, sans-serif; /* Font type */
font-weight: bold;             /* Text boldness */
text-align: center;            /* Text alignment */
text-decoration: underline;    /* Text decoration */
line-height: 1.5;              /* Space between lines */
```

### Background Properties

```css
background-color: lightblue;   /* Background color */
background-image: url('image.jpg'); /* Background image */
```

### Spacing Properties

```css
margin: 10px;      /* Space outside element */
padding: 10px;     /* Space inside element */
```

### Border Properties

```css
border: 2px solid black;  /* Border around element */
border-radius: 5px;       /* Rounded corners */
```

## CSS Comments

Comments help you document your code and are ignored by browsers.

```css
/* This is a single-line comment */

/*
  This is a
  multi-line comment
*/

h1 {
  color: blue; /* Inline comment */
}
```

## The Cascade

CSS stands for “Cascading” Style Sheets because styles cascade down from multiple sources. When multiple rules apply to the same element, the browser determines which rule wins based on:

1. **Specificity** - More specific selectors override less specific ones
1. **Source Order** - Later rules override earlier ones (if specificity is equal)
1. **Importance** - `!important` overrides everything (use sparingly!)

**Example:**

```css
p {
  color: blue;  /* Less specific */
}

.intro {
  color: red;   /* More specific - this wins */
}
```

```html
<p class="intro">This text will be red.</p>
```

## Exercises

### Exercise 1: Setup

1. Create an HTML file called `index.html`
1. Create a CSS file called `styles.css`
1. Link the CSS file to your HTML

### Exercise 2: Basic Styling

Create a simple webpage with:

- A heading that is blue and centered
- A paragraph with red text and 18px font size
- A div with a yellow background and 20px padding

### Exercise 3: Classes and IDs

1. Create three paragraphs with different classes
1. Style each class differently (different colors, sizes)
1. Create one div with an ID and give it a border

### Exercise 4: Practice Selectors

Style a webpage with:

- All `<h2>` elements in green
- Elements with class “warning” in red with bold text
- An element with ID “footer” with a gray background

## Challenge Project: Personal Bio Page

Create a personal bio page with the following:

- A header with your name (styled with large, centered text)
- A profile section with a colored background
- Multiple paragraphs about yourself with different styling
- A footer with smaller text
- Use at least 3 different selectors (element, class, ID)
- Use at least 8 different CSS properties

**Requirements:**

- External CSS file
- Clean, readable code with comments
- Proper HTML structure
- Creative color scheme

## Key Takeaways

- CSS controls the visual presentation of HTML
- External CSS files are the best practice
- Selectors target HTML elements for styling
- The cascade determines which styles apply when there are conflicts
- Start with basic properties and build up complexity

-----

**Next Module:** [Module 2 - The Box Model](module-02-box-model.md)

## Additional Resources

- [MDN CSS Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)
- [CSS Selectors Reference](https://www.w3schools.com/cssref/css_selectors.php)
