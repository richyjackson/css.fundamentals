# Module 6: Flexbox

## Introduction to Flexbox

Flexbox (Flexible Box Layout) is a one-dimensional layout system designed for distributing space and aligning items in rows or columns. It’s perfect for navigation bars, card layouts, and centering elements.

## Flexbox Concepts

### Main Axis vs Cross Axis

Flexbox works along two axes:

- **Main Axis:** Direction items flow (horizontal by default)
- **Cross Axis:** Perpendicular to main axis (vertical by default)

```
flex-direction: row (default)
Main Axis →
Items: [1] [2] [3]
       ↓ Cross Axis

flex-direction: column
Items: [1]
       [2]  ↓ Main Axis
       [3]
→ Cross Axis
```

### Parent (Flex Container) vs Children (Flex Items)

```html
<div class="container">  <!-- Flex Container -->
  <div>Item 1</div>      <!-- Flex Item -->
  <div>Item 2</div>      <!-- Flex Item -->
  <div>Item 3</div>      <!-- Flex Item -->
</div>
```

## Creating a Flex Container

```css
.container {
  display: flex;
}
```

All direct children automatically become flex items.

## Flex Container Properties

These properties go on the parent container.

### flex-direction

Controls the direction of the main axis.

```css
flex-direction: row;            /* Default - left to right */
flex-direction: row-reverse;    /* Right to left */
flex-direction: column;         /* Top to bottom */
flex-direction: column-reverse; /* Bottom to top */
```

**Example:**

```css
.horizontal-layout {
  display: flex;
  flex-direction: row;
}

.vertical-layout {
  display: flex;
  flex-direction: column;
}
```

### justify-content

Aligns items along the **main axis**.

```css
justify-content: flex-start;    /* Default - at start */
justify-content: flex-end;      /* At end */
justify-content: center;        /* Centered */
justify-content: space-between; /* Equal space between items */
justify-content: space-around;  /* Equal space around items */
justify-content: space-evenly;  /* Equal space everywhere */
```

**Visual:**

```
flex-start:    [1][2][3]____________
center:        ______[1][2][3]______
flex-end:      ____________[1][2][3]
space-between: [1]______[2]______[3]
space-around:  __[1]____[2]____[3]__
space-evenly:  ___[1]___[2]___[3]___
```

### align-items

Aligns items along the **cross axis**.

```css
align-items: stretch;     /* Default - fill container height */
align-items: flex-start;  /* Align to top/start */
align-items: flex-end;    /* Align to bottom/end */
align-items: center;      /* Center vertically */
align-items: baseline;    /* Align text baselines */
```

**Perfect centering:**

```css
.centered {
  display: flex;
  justify-content: center;  /* Center horizontally */
  align-items: center;      /* Center vertically */
  height: 100vh;
}
```

### flex-wrap

Controls whether items wrap to new lines.

```css
flex-wrap: nowrap;        /* Default - single line */
flex-wrap: wrap;          /* Wrap to multiple lines */
flex-wrap: wrap-reverse;  /* Wrap in reverse order */
```

**Example - responsive grid:**

```css
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  width: 300px;
}
```

### align-content

Aligns multiple lines (only works with `flex-wrap: wrap`).

```css
align-content: stretch;       /* Default */
align-content: flex-start;
align-content: flex-end;
align-content: center;
align-content: space-between;
align-content: space-around;
```

### gap

Space between flex items (modern browsers).

```css
.container {
  display: flex;
  gap: 20px;              /* 20px between all items */
  gap: 20px 40px;         /* 20px rows, 40px columns */
  row-gap: 20px;          /* Only between rows */
  column-gap: 40px;       /* Only between columns */
}
```

### flex-flow (Shorthand)

Combines `flex-direction` and `flex-wrap`.

```css
flex-flow: row wrap;
/* Same as:
   flex-direction: row;
   flex-wrap: wrap; */
```

## Flex Item Properties

These properties go on the children (flex items).

### flex-grow

How much an item grows relative to others (proportional growth).

```css
.item {
  flex-grow: 0;  /* Default - don't grow */
  flex-grow: 1;  /* Grow to fill space */
  flex-grow: 2;  /* Grow twice as much as items with flex-grow: 1 */
}
```

**Example - flexible layout:**

```css
.sidebar {
  flex-grow: 1;  /* Takes 1 part of available space */
}

.main-content {
  flex-grow: 2;  /* Takes 2 parts of available space (twice sidebar) */
}
```

### flex-shrink

How much an item shrinks when space is limited.

```css
flex-shrink: 1;  /* Default - can shrink */
flex-shrink: 0;  /* Don't shrink */
flex-shrink: 2;  /* Shrink twice as much */
```

### flex-basis

Initial size of item before growing/shrinking.

```css
flex-basis: auto;    /* Default - based on content */
flex-basis: 200px;   /* Start at 200px */
flex-basis: 50%;     /* Start at 50% of container */
flex-basis: 0;       /* Ignore content size */
```

### flex (Shorthand)

Combines `flex-grow`, `flex-shrink`, and `flex-basis`.

```css
/* flex: grow shrink basis */
flex: 1;           /* flex: 1 1 0 - commonly used */
flex: 1 0 200px;   /* Grow, don't shrink, start at 200px */
flex: 0 0 auto;    /* Don't grow or shrink - fixed size */
```

**Common patterns:**

```css
.flexible {
  flex: 1;  /* Grow to fill, can shrink, ignore content size */
}

.fixed {
  flex: 0 0 200px;  /* Fixed 200px width */
}

.content-size {
  flex: 0 0 auto;  /* Based on content, no growing/shrinking */
}
```

### align-self

Override `align-items` for individual item.

```css
.special-item {
  align-self: flex-start;
  align-self: flex-end;
  align-self: center;
  align-self: stretch;
}
```

### order

Change visual order of items (doesn’t affect DOM order).

```css
.item-1 {
  order: 2;  /* Appears second */
}

.item-2 {
  order: 1;  /* Appears first */
}

.item-3 {
  order: 3;  /* Appears third */
}
```

Default order is `0`. Negative values are allowed.

## Common Flexbox Patterns

### Horizontal Navigation

```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
}

.nav-links {
  display: flex;
  gap: 20px;
}
```

### Card Grid

```css
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 0 0 calc(33.333% - 20px);  /* 3 cards per row */
}
```

### Sidebar Layout

```css
.layout {
  display: flex;
  gap: 20px;
}

.sidebar {
  flex: 0 0 250px;  /* Fixed 250px sidebar */
}

.main {
  flex: 1;  /* Takes remaining space */
}
```

### Perfect Centering

```css
.center-box {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

### Equal Height Columns

```css
.columns {
  display: flex;
  gap: 20px;
}

.column {
  flex: 1;
  /* All columns automatically same height */
}
```

### Footer at Bottom

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;  /* Takes up remaining space */
}

footer {
  flex: 0 0 auto;
}
```

### Responsive Navigation

```css
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

@media (max-width: 768px) {
  .nav {
    flex-direction: column;
    align-items: stretch;
  }
}
```

## Practical Examples

### Feature Cards

```css
.features {
  display: flex;
  gap: 30px;
  flex-wrap: wrap;
}

.feature-card {
  flex: 1 1 300px;  /* Grow, shrink, min 300px */
  padding: 30px;
  text-align: center;
  border: 1px solid #ddd;
  border-radius: 8px;
}
```

### Split Screen

```css
.split {
  display: flex;
  height: 100vh;
}

.split-left,
.split-right {
  flex: 1;
  padding: 50px;
}

.split-left {
  background: #667eea;
}

.split-right {
  background: #764ba2;
}
```

### Pricing Table

```css
.pricing {
  display: flex;
  gap: 20px;
  justify-content: center;
}

.pricing-card {
  flex: 0 1 300px;
  padding: 30px;
  border: 2px solid #ddd;
  border-radius: 10px;
  text-align: center;
}

.pricing-card.featured {
  flex-grow: 1.2;
  border-color: #667eea;
  transform: scale(1.05);
}
```

## Exercises

### Exercise 1: Basic Flexbox

Create a container with 5 boxes. Use flexbox to:

1. Arrange them horizontally
1. Center them
1. Add equal spacing between them

### Exercise 2: Navigation Bar

Create a navigation bar with:

- Logo on the left
- Navigation links in the center
- Button on the right
- All vertically centered

### Exercise 3: Card Layout

Create a responsive card grid:

- 3 cards per row on desktop
- 2 cards per row on tablet
- 1 card per row on mobile
- Equal height cards

### Exercise 4: Flexible Columns

Create a 3-column layout:

- Narrow left sidebar (fixed 200px)
- Wide main content (grows to fill)
- Narrow right sidebar (fixed 200px)

### Exercise 5: Vertical Centering

Create a hero section that perfectly centers its content both horizontally and vertically.

## Challenge Project: Complete Dashboard Layout

Create a dashboard layout with:

- Top navigation bar (logo left, nav center, user menu right)
- Sidebar (fixed width, full height)
- Main content area (flexible, takes remaining space)
- Grid of stat cards (responsive, 4 columns on desktop, 2 on tablet, 1 on mobile)
- Footer that sticks to bottom (even with little content)
- All cards should have equal height within their row

**Requirements:**

- Use only Flexbox (no Grid)
- Fully responsive
- No fixed heights except where necessary
- Proper use of flex properties (grow, shrink, basis)
- Clean gap spacing throughout
- Professional appearance

## Common Mistakes to Avoid

1. **Forgetting to set display: flex:** Nothing works without it!
1. **Confusing main axis and cross axis:** `justify-content` is main, `align-items` is cross
1. **Using flex on the container:** Flex properties (grow, shrink, basis) go on items, not container
1. **Overthinking flex shorthand:** `flex: 1` is usually all you need for flexible items

## Key Takeaways

- Flexbox is for one-dimensional layouts (row or column)
- Container properties: display, flex-direction, justify-content, align-items, flex-wrap, gap
- Item properties: flex-grow, flex-shrink, flex-basis (shorthand: flex)
- Perfect for navigation, card layouts, and centering
- Works great with responsive design
- Main axis = direction items flow, Cross axis = perpendicular

-----

**Previous Module:** [Module 5 - Layout Basics](module-05-layout-basics.md)  
**Next Module:** [Module 7 - Grid Layout](module-07-grid-layout.md)

## Additional Resources

- [CSS Tricks Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy Game](https://flexboxfroggy.com/)
- [MDN Flexbox Guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
