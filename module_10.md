# Module 10: Advanced Selectors

## Introduction

Advanced selectors allow you to target elements with precision, reducing the need for extra classes and making your CSS more powerful and maintainable.

## Combinators

Combinators define relationships between selectors.

### Descendant Combinator (space)

Selects elements inside another element (any level deep).

```css
/* All <p> inside <article> */
article p {
  color: gray;
}

/* All <a> inside <nav> inside <header> */
header nav a {
  color: white;
}
```

### Child Combinator (>)

Selects direct children only (one level deep).

```css
/* Only <p> that are direct children of <article> */
article > p {
  font-size: 1.2rem;
}

/* Only <li> that are direct children of <ul> */
ul > li {
  list-style-type: disc;
}
```

**Difference:**

```html
<article>
  <p>Selected by both article p and article > p</p>
  <div>
    <p>Selected by article p but NOT article > p</p>
  </div>
</article>
```

### Adjacent Sibling Combinator (+)

Selects element immediately after another (same parent).

```css
/* <p> immediately following <h2> */
h2 + p {
  font-weight: bold;
  font-size: 1.1em;
}

/* <img> immediately following <p> */
p + img {
  margin-top: 20px;
}
```

```html
<h2>Heading</h2>
<p>This paragraph is selected (first after h2)</p>
<p>This paragraph is NOT selected</p>
```

### General Sibling Combinator (~)

Selects all siblings after an element (same parent).

```css
/* All <p> that come after <h2> */
h2 ~ p {
  color: gray;
}
```

```html
<h2>Heading</h2>
<p>Selected</p>
<div>Not a paragraph</div>
<p>Also selected</p>
<p>Also selected</p>
```

## Attribute Selectors

Target elements based on their attributes.

### Basic Attribute Presence

```css
/* Has title attribute */
[title] {
  cursor: help;
}

/* Has href attribute */
a[href] {
  color: blue;
}

/* Has disabled attribute */
input[disabled] {
  opacity: 0.5;
}
```

### Exact Attribute Value

```css
/* Exact match */
[type="text"] {
  border: 1px solid blue;
}

[class="button"] {
  /* Exact class (rarely used, use .button instead) */
}
```

### Contains Word (space-separated)

```css
/* Class list contains "primary" */
[class~="primary"] {
  background: blue;
}
```

```html
<!-- Both matched -->
<button class="button primary">Match</button>
<button class="primary button">Match</button>
```

### Starts With

```css
/* href starts with "https" */
a[href^="https"] {
  color: green;
}

/* href starts with "mailto:" */
a[href^="mailto:"]::before {
  content: "📧 ";
}

/* Class starts with "icon-" */
[class^="icon-"] {
  display: inline-block;
  width: 20px;
  height: 20px;
}
```

### Ends With

```css
/* href ends with ".pdf" */
a[href$=".pdf"]::after {
  content: " (PDF)";
}

/* href ends with ".zip" */
a[href$=".zip"]::after {
  content: " ⬇";
}

/* src ends with ".jpg" */
img[src$=".jpg"] {
  border: 2px solid blue;
}
```

### Contains Substring

```css
/* href contains "google" */
a[href*="google"] {
  color: red;
}

/* Class contains "btn" anywhere */
[class*="btn"] {
  padding: 10px 20px;
}
```

### Starts With or Followed by Hyphen

```css
/* lang="en" or lang="en-US" or lang="en-GB" */
[lang|="en"] {
  font-family: Arial;
}
```

### Case-Insensitive Matching

```css
/* Case-insensitive (i flag) */
a[href*="google" i] {
  /* Matches google, Google, GOOGLE, etc. */
}

input[type="email" i] {
  /* Works even if type="EMAIL" */
}
```

## Pseudo-Classes

Select elements based on their state or position.

### User Action Pseudo-Classes

```css
/* Mouse hover */
a:hover {
  color: red;
}

/* Keyboard focus */
input:focus {
  border-color: blue;
  outline: 2px solid blue;
}

/* Mouse click (active) */
button:active {
  transform: scale(0.95);
}

/* Visited link */
a:visited {
  color: purple;
}
```

### Form State Pseudo-Classes

```css
/* Checked checkbox/radio */
input:checked {
  accent-color: green;
}

input:checked + label {
  font-weight: bold;
}

/* Disabled input */
input:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Enabled input */
input:enabled {
  border-color: green;
}

/* Required field */
input:required {
  border-left: 3px solid red;
}

/* Optional field */
input:optional {
  border-left: 3px solid gray;
}

/* Valid input */
input:valid {
  border-color: green;
}

/* Invalid input */
input:invalid {
  border-color: red;
}

/* In range (for number inputs) */
input:in-range {
  border-color: green;
}

/* Out of range */
input:out-of-range {
  border-color: red;
}

/* Read-only */
input:read-only {
  background: #f0f0f0;
}
```

### Structural Pseudo-Classes

#### :first-child and :last-child

```css
/* First child of parent */
li:first-child {
  font-weight: bold;
}

/* Last child of parent */
li:last-child {
  border-bottom: none;
}

/* First <p> that is first child */
p:first-child {
  margin-top: 0;
}
```

#### :nth-child()

```css
/* Specific position */
li:nth-child(3) {
  /* 3rd li */
}

/* Odd elements (1, 3, 5, ...) */
tr:nth-child(odd) {
  background: #f9f9f9;
}

/* Even elements (2, 4, 6, ...) */
tr:nth-child(even) {
  background: white;
}

/* Every 3rd element */
li:nth-child(3n) {
  /* 3rd, 6th, 9th, ... */
}

/* Every 3rd starting from 2nd */
li:nth-child(3n+2) {
  /* 2nd, 5th, 8th, ... */
}

/* First 3 elements */
li:nth-child(-n+3) {
  /* 1st, 2nd, 3rd */
}
```

#### :nth-last-child()

Same as nth-child but counts from the end.

```css
/* 2nd from last */
li:nth-last-child(2) {
  color: red;
}

/* Last 3 elements */
li:nth-last-child(-n+3) {
  font-weight: bold;
}
```

#### :nth-of-type()

Like nth-child but only counts specific element types.

```css
/* 2nd <p> element (ignores other elements) */
p:nth-of-type(2) {
  font-size: 1.2em;
}

/* Odd <div> elements */
div:nth-of-type(odd) {
  background: gray;
}
```

#### :only-child

```css
/* Element that is the only child */
li:only-child {
  list-style: none;
}
```

#### :only-of-type

```css
/* Only <p> among siblings */
p:only-of-type {
  text-align: center;
}
```

#### :empty

```css
/* Elements with no children (not even text) */
div:empty {
  display: none;
}

/* Style empty table cells */
td:empty::before {
  content: "—";
}
```

### Negation Pseudo-Class

```css
/* All <input> except type="submit" */
input:not([type="submit"]) {
  border: 1px solid gray;
}

/* All <li> except first */
li:not(:first-child) {
  margin-top: 10px;
}

/* All elements except .special */
p:not(.special) {
  color: gray;
}

/* Multiple negations */
button:not(.primary):not(.secondary) {
  background: gray;
}
```

### Other Useful Pseudo-Classes

```css
/* Root element (html) */
:root {
  --primary-color: blue;
}

/* Target of URL fragment */
:target {
  background: yellow;
}

/* Element in its default state */
:default {
  border: 2px solid blue;
}
```

## Pseudo-Elements

Create and style virtual elements.

### ::before and ::after

Insert content before or after element content.

```css
.quote::before {
  content: """;
  font-size: 2em;
  color: gray;
}

.quote::after {
  content: """;
  font-size: 2em;
  color: gray;
}

/* Icon before links */
.external-link::after {
  content: " ↗";
}

/* Decorative elements */
.heading::before {
  content: "";
  display: inline-block;
  width: 30px;
  height: 3px;
  background: blue;
  margin-right: 10px;
}
```

**Note:** `content` property is required, even if empty.

### ::first-letter

```css
/* Drop cap */
p::first-letter {
  font-size: 3em;
  font-weight: bold;
  float: left;
  margin-right: 5px;
  line-height: 1;
}
```

### ::first-line

```css
p::first-line {
  font-weight: bold;
  color: blue;
}
```

### ::selection

Style highlighted/selected text.

```css
::selection {
  background: yellow;
  color: black;
}

p::selection {
  background: lightblue;
}
```

### ::placeholder

Style input placeholder text.

```css
input::placeholder {
  color: #999;
  font-style: italic;
}
```

### ::marker

Style list item markers.

```css
li::marker {
  color: red;
  font-weight: bold;
}

ul::marker {
  content: "→ ";
}
```

## Selector Specificity

Understanding how CSS determines which rule wins.

### Specificity Hierarchy

1. Inline styles: `style="..."`
1. IDs: `#id`
1. Classes, attributes, pseudo-classes: `.class`, `[attr]`, `:hover`
1. Elements, pseudo-elements: `div`, `::before`

### Calculating Specificity

Count each type: (inline, IDs, classes, elements)

```css
/* (0, 0, 1, 0) */
.button { }

/* (0, 1, 0, 0) */
#header { }

/* (0, 0, 1, 1) */
div.container { }

/* (0, 1, 1, 1) */
#header .nav a { }

/* (0, 0, 2, 2) */
div.container .button:hover { }

/* (0, 1, 2, 3) */
header #nav ul li.active a { }
```

Higher specificity wins. If equal, last rule wins.

### !important (Use Sparingly!)

```css
.text {
  color: blue !important;  /* Overrides almost everything */
}
```

## Practical Examples

### Zebra Striped Table

```css
table tr:nth-child(even) {
  background: #f9f9f9;
}

table tr:hover {
  background: #e9e9e9;
}
```

### Breadcrumb Navigation

```css
.breadcrumb li:not(:last-child)::after {
  content: " / ";
  margin: 0 5px;
  color: gray;
}
```

### Custom Checkbox

```css
input[type="checkbox"] {
  display: none;
}

input[type="checkbox"] + label::before {
  content: "";
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 2px solid gray;
  margin-right: 10px;
  vertical-align: middle;
}

input[type="checkbox"]:checked + label::before {
  background: blue;
  border-color: blue;
}
```

### Form Validation Styling

```css
input:valid {
  border-color: green;
}

input:valid + .feedback::before {
  content: "✓";
  color: green;
}

input:invalid:not(:placeholder-shown) {
  border-color: red;
}

input:invalid:not(:placeholder-shown) + .feedback::before {
  content: "✗";
  color: red;
}
```

### Link Icons by Type

```css
a[href^="http"]::after {
  content: " 🔗";
}

a[href^="mailto:"]::before {
  content: "📧 ";
}

a[href$=".pdf"]::after {
  content: " (PDF)";
}
```

## Exercises

### Exercise 1: Combinators

Create a navigation menu where:

- All links in nav are styled one way
- Direct child links are styled differently
- Hover effects on links

### Exercise 2: Nth-child

Create a list where:

- Odd items have gray background
- Even items have white background
- First item is bold
- Last item has no border

### Exercise 3: Attribute Selectors

Style different types of links:

- External links (https)
- Email links (mailto)
- PDF links (.pdf)
- Each with different icons/styling

### Exercise 4: Form States

Create a form with styling for:

- Focus states
- Valid/invalid inputs
- Required fields indicator
- Disabled inputs

### Exercise 5: Pseudo-Elements

Create styled content using ::before and ::after:

- Quote marks around quotes
- Decorative elements on headings
- Custom list markers

## Challenge Project: Advanced Blog Layout

Create a blog post layout demonstrating advanced selectors:

**Typography:**

- First paragraph after headings is larger
- Drop cap on first paragraph of article
- Custom quote styling with ::before/::after

**Lists:**

- Custom markers with ::marker or ::before
- Different styles for nested lists (>)
- Breadcrumb with separator using :not(:last-child)

**Links:**

- Different icons for external, email, PDF links
- Hover/focus/active states
- Visited link styling

**Forms:**

- Newsletter signup with validation styling
- Custom checkbox/radio using :checked
- Focus indicators
- Error messages for :invalid

**Tables:**

- Zebra striping with :nth-child
- Hover effects on rows
- Different styling for first/last rows

**Comments Section:**

- Highlight :target comment when linked
- Author comments styled differently
- Nested comments with >

**Requirements:**

- Use at least 10 different advanced selectors
- No extra classes where selectors can be used
- Proper specificity management
- Clean, maintainable code
- Professional appearance

## Best Practices

1. **Keep specificity low:** Easier to override later
1. **Use classes over IDs:** Better for reusability
1. **Avoid !important:** Last resort only
1. **Be specific but not too specific:** Balance maintainability
1. **Use meaningful selectors:** Self-documenting code

## Common Mistakes to Avoid

1. **Over-qualifying selectors:** `div.button` instead of `.button`
1. **Too specific selectors:** Hard to override
1. **Relying on structure:** HTML might change
1. **Forgetting :not() complexity:** Can get confusing
1. **Abusing !important:** Creates maintenance nightmares

## Key Takeaways

- Combinators: descendant (space), child (>), sibling (+, ~)
- Attribute selectors: target elements by attributes
- Pseudo-classes: target states and positions
- Pseudo-elements: create virtual elements
- Specificity: IDs > classes > elements
- Advanced selectors reduce need for extra classes
- Balance power with maintainability

-----

**Previous Module:** [Module 9 - Transitions and Animations](module-09-transitions-animations.md)

## Additional Resources

- [MDN Selectors Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [Specificity Calculator](https://specificity.keegan.st/)
- [CSS Diner Game](https://flukeout.github.io/) - Learn selectors through gameplay

-----

## 🎉 Congratulations!

You’ve completed all 10 modules of CSS learning! You now have a solid foundation in:

- CSS fundamentals and selectors
- Box model and typography
- Colors and backgrounds
- Layout systems (Flexbox and Grid)
- Responsive design
- Animations and transitions
- Advanced selectors

**Next Steps:**

1. Build real projects to practice
1. Explore CSS frameworks (Bootstrap, Tailwind)
1. Learn CSS preprocessors (Sass, Less)
1. Study CSS architecture (BEM, SMACSS)
1. Keep up with new CSS features

Keep coding and creating! 🚀
