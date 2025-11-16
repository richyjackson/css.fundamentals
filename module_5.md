# Module 5: Layout Basics

## Introduction to CSS Layout

Layout is how we arrange elements on a page. Before Flexbox and Grid (covered in later modules), understanding these fundamental layout properties is essential.

## The Display Property

The `display` property is one of the most important layout properties. It determines how an element behaves and interacts with other elements.

### Block Elements

Block elements take up the full width available and start on a new line.

```css
div, p, h1, h2, section, article, header, footer {
  display: block;
}
```

**Characteristics:**

- Takes up full width of container
- Starts on a new line
- Can have width and height
- Respects all margin and padding

```css
.block-element {
  display: block;
  width: 50%;
  margin: 20px 0;
}
```

### Inline Elements

Inline elements only take up as much width as needed and don’t start on a new line.

```css
span, a, strong, em, img {
  display: inline;
}
```

**Characteristics:**

- Only takes necessary width
- Stays on same line with other inline elements
- Cannot have width or height set
- Vertical padding/margin may not work as expected

```css
.inline-element {
  display: inline;
  /* width: 200px; - This won't work! */
  padding: 0 10px;  /* Horizontal padding works */
}
```

### Inline-Block

Combines the best of both worlds.

```css
.inline-block-element {
  display: inline-block;
  width: 200px;      /* Works now! */
  height: 100px;     /* Works now! */
  margin: 10px;      /* Works fully */
  vertical-align: top;
}
```

**Characteristics:**

- Stays on same line with other inline/inline-block elements
- Can have width and height
- Respects all margin and padding

**Common use case - horizontal navigation:**

```css
.nav-item {
  display: inline-block;
  padding: 10px 20px;
  margin: 0 5px;
}
```

### None

Removes element from page entirely.

```css
.hidden {
  display: none;  /* Element doesn't take up any space */
}
```

**Note:** Different from `visibility: hidden` which hides but preserves space.

## The Position Property

Position controls how elements are positioned within the document flow.

### Static (Default)

Normal document flow. Elements appear in order they’re written in HTML.

```css
.element {
  position: static;  /* Default - rarely needs to be specified */
}
```

### Relative

Positioned relative to its normal position. The element still occupies its original space in the document flow.

```css
.relative-box {
  position: relative;
  top: 20px;     /* Moves down 20px from normal position */
  left: 30px;    /* Moves right 30px from normal position */
}
```

**Key points:**

- Original space is preserved
- Other elements aren’t affected
- Often used as a positioning context for absolute children

### Absolute

Removed from normal flow and positioned relative to nearest positioned ancestor (or viewport if none).

```css
.container {
  position: relative;  /* Creates positioning context */
}

.absolute-box {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

**Key points:**

- Removed from document flow
- Doesn’t affect other elements
- Positioned relative to nearest positioned ancestor
- Great for overlays, tooltips, dropdown menus

**Common pattern - corner badge:**

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: red;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
}
```

### Fixed

Positioned relative to viewport. Stays in place when scrolling.

```css
.fixed-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: white;
  z-index: 1000;
}
```

**Common uses:**

- Fixed headers/navigation
- Floating action buttons
- Cookie notices
- Chat widgets

### Sticky

Hybrid of relative and fixed. Acts relative until scroll threshold, then becomes fixed.

```css
.sticky-nav {
  position: sticky;
  top: 0;
  background: white;
}
```

**Note:** Requires a threshold (top, bottom, left, or right) to work.

## Z-Index

Controls stacking order of positioned elements (only works with positioned elements: relative, absolute, fixed, sticky).

```css
.bottom-layer {
  position: relative;
  z-index: 1;
}

.middle-layer {
  position: absolute;
  z-index: 10;
}

.top-layer {
  position: fixed;
  z-index: 100;
}
```

**Higher values appear on top:**

- Negative values are possible
- Default is `auto` (0)
- Common practice: use increments of 10 or 100

## Float and Clear

**Note:** Float is largely replaced by Flexbox/Grid, but still useful for text wrapping around images.

### Float

```css
.float-left {
  float: left;
  margin-right: 20px;
}

.float-right {
  float: right;
  margin-left: 20px;
}
```

**Text wrapping example:**

```css
img {
  float: left;
  margin: 0 20px 20px 0;
}
```

### Clear

Prevents elements from wrapping around floated elements.

```css
.clear-left {
  clear: left;
}

.clear-right {
  clear: right;
}

.clear-both {
  clear: both;
}
```

### Clearfix Pattern

Contain floated children within parent.

```css
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

## Overflow

Controls what happens when content is larger than its container.

```css
overflow: visible;  /* Default - content overflows */
overflow: hidden;   /* Clips overflowing content */
overflow: scroll;   /* Always shows scrollbars */
overflow: auto;     /* Shows scrollbars only when needed */
```

**Individual axes:**

```css
overflow-x: hidden;
overflow-y: auto;
```

**Common use - scrollable container:**

```css
.scrollable-box {
  height: 300px;
  overflow-y: auto;
  border: 1px solid #ddd;
}
```

## Visibility

Hide elements while preserving their space.

```css
visibility: visible;  /* Default */
visibility: hidden;   /* Hidden but space preserved */
visibility: collapse; /* For table elements */
```

**display vs visibility:**

```css
.removed {
  display: none;      /* Element gone, no space taken */
}

.invisible {
  visibility: hidden; /* Element invisible, space preserved */
}
```

## Practical Layout Patterns

### Centered Container

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}
```

### Card with Badge

```css
.card {
  position: relative;
  padding: 20px;
  border: 1px solid #ddd;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: red;
  color: white;
  padding: 5px 10px;
}
```

### Fixed Header

```css
header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
  background: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  z-index: 1000;
}

main {
  margin-top: 60px; /* Offset for fixed header */
}
```

### Sticky Sidebar

```css
.sidebar {
  position: sticky;
  top: 20px;
  height: fit-content;
}
```

### Overlay Modal

```css
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 30px;
  z-index: 1001;
}
```

### Image with Text Wrap

```css
img.float-left {
  float: left;
  margin: 0 20px 20px 0;
  max-width: 300px;
}
```

## Exercises

### Exercise 1: Display Property

Create a page with:

1. Three block elements (take full width)
1. Three inline elements (on same line)
1. Three inline-block elements (on same line but with width/height)

### Exercise 2: Positioning

Create a container with:

1. A relatively positioned parent
1. An absolutely positioned child in the top-right corner
1. Another absolutely positioned child in the bottom-left corner

### Exercise 3: Fixed Header

Create a page with:

1. Fixed header at top
1. Content below with enough text to scroll
1. Header should stay visible while scrolling

### Exercise 4: Sticky Navigation

Create a page with:

1. Regular content at the top
1. Sticky navigation that sticks to top when scrolled
1. More content below

### Exercise 5: Layering

Create three overlapping boxes with different z-index values to practice stacking order.

## Challenge Project: Blog Layout

Create a blog post layout with:

- Fixed header with navigation (stays visible on scroll)
- Main content area (centered, max-width)
- Floating author image in the article (text wraps around it)
- Sticky table of contents sidebar
- “Back to top” button (fixed position, bottom-right)
- Badge on featured article card (absolute positioned)
- Proper z-index management for all positioned elements

**Requirements:**

- Use at least 4 different position values
- Implement proper layering with z-index
- Float an image with text wrapping
- Center main content with auto margins
- Handle overflow properly in scrollable areas

## Common Mistakes to Avoid

1. **Forgetting position: relative on parent:** Absolute children need a positioned parent
1. **Using float for layout:** Use Flexbox or Grid instead (covered in next modules)
1. **Z-index not working:** Element must be positioned (not static)
1. **Fixed elements without accounting for them:** Add margin/padding to content below fixed headers

## Key Takeaways

- Display controls element box behavior (block, inline, inline-block)
- Position controls element placement (static, relative, absolute, fixed, sticky)
- Z-index controls stacking order of positioned elements
- Float is mainly for text wrapping (use Flexbox/Grid for layout)
- Overflow controls behavior when content exceeds container
- Understanding these basics is crucial before learning Flexbox and Grid

-----

**Previous Module:** [Module 4 - Colors and Backgrounds](module-04-colors-backgrounds.md)  
**Next Module:** [Module 6 - Flexbox](module-06-flexbox.md)

## Additional Resources

- [MDN Position Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- [CSS Layout Cookbook](https://developer.mozilla.org/en-US/docs/Web/CSS/Layout_cookbook)
- [Understanding Z-Index](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index)
