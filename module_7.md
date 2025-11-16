# Module 7: Grid Layout

## Introduction to CSS Grid

CSS Grid is a two-dimensional layout system that works with rows AND columns simultaneously. It’s perfect for complex layouts, magazine-style designs, and overall page structure.

## Grid vs Flexbox

- **Flexbox:** One-dimensional (row OR column)
- **Grid:** Two-dimensional (rows AND columns)

Use Flexbox for components, Grid for layouts.

## Creating a Grid Container

```css
.container {
  display: grid;
}
```

All direct children automatically become grid items.

## Defining Grid Structure

### grid-template-columns

Defines the columns of your grid.

```css
/* Three equal columns */
.grid {
  display: grid;
  grid-template-columns: 200px 200px 200px;
}

/* Different sizes */
.grid {
  grid-template-columns: 100px 300px 200px;
}

/* Percentage */
.grid {
  grid-template-columns: 25% 50% 25%;
}

/* FR unit (fraction) - flexible */
.grid {
  grid-template-columns: 1fr 2fr 1fr;
  /* Takes available space: 1 part, 2 parts, 1 part */
}

/* repeat() function */
.grid {
  grid-template-columns: repeat(3, 1fr);
  /* Same as: 1fr 1fr 1fr */
}

/* Auto columns */
.grid {
  grid-template-columns: auto auto auto;
  /* Size based on content */
}

/* Mix of units */
.grid {
  grid-template-columns: 200px 1fr 2fr;
  /* Fixed, flexible, more flexible */
}
```

### grid-template-rows

Defines the rows of your grid.

```css
.grid {
  grid-template-rows: 100px 200px 150px;
}

.grid {
  grid-template-rows: repeat(3, 100px);
}

.grid {
  grid-template-rows: 1fr 2fr 1fr;
}

/* Often auto for content-based height */
.grid {
  grid-template-rows: auto auto auto;
}
```

### The FR Unit

The `fr` unit represents a fraction of available space.

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  /* Each column gets 1/3 of space */
}

.grid {
  grid-template-columns: 2fr 1fr;
  /* First column gets 2/3, second gets 1/3 */
}

.grid {
  grid-template-columns: 200px 1fr 1fr;
  /* First: fixed 200px, others share remaining space equally */
}
```

## Gap (Spacing)

Space between grid cells.

```css
gap: 20px;              /* 20px between rows and columns */
gap: 20px 40px;         /* 20px rows, 40px columns */
row-gap: 20px;          /* Only between rows */
column-gap: 40px;       /* Only between columns */

/* Old syntax (still works) */
grid-gap: 20px;
grid-row-gap: 20px;
grid-column-gap: 40px;
```

## Placing Grid Items

### grid-column and grid-row

Control where items are placed and how much space they take.

```css
/* Item starts at column line 1, ends at line 3 (spans 2 columns) */
.item {
  grid-column: 1 / 3;
}

/* Shorthand using span */
.item {
  grid-column: span 2;  /* Spans 2 columns */
}

/* Individual properties */
.item {
  grid-column-start: 1;
  grid-column-end: 3;
}

/* Row placement */
.item {
  grid-row: 1 / 3;  /* Spans 2 rows */
  grid-row: span 2;  /* Spans 2 rows */
}

/* Span to end */
.item {
  grid-column: 1 / -1;  /* From start to end */
}
```

**Grid Lines:**

```
Columns:
     1   2   3   4
   |   |   |   |   |
   | A | B | C |
   |   |   |   |

Item A: grid-column: 1 / 2
Item B: grid-column: 2 / 3
Item C: grid-column: 3 / 4
```

## Grid Template Areas

Named grid areas for intuitive layouts.

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
  gap: 20px;
  min-height: 100vh;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

**Empty cells with dots:**

```css
grid-template-areas:
  "header header header"
  "sidebar main ."
  "footer footer footer";
```

## Alignment

### justify-items

Align items horizontally within their cells.

```css
justify-items: start;    /* Left align */
justify-items: center;   /* Center align */
justify-items: end;      /* Right align */
justify-items: stretch;  /* Default - fill cell */
```

### align-items

Align items vertically within their cells.

```css
align-items: start;    /* Top align */
align-items: center;   /* Center align */
align-items: end;      /* Bottom align */
align-items: stretch;  /* Default - fill cell */
```

### justify-content

Align the entire grid horizontally within container.

```css
justify-content: start;
justify-content: center;
justify-content: end;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

### align-content

Align the entire grid vertically within container.

```css
align-content: start;
align-content: center;
align-content: end;
align-content: space-between;
align-content: space-around;
align-content: space-evenly;
```

### place-items (Shorthand)

```css
place-items: center;        /* Center both ways */
place-items: center start;  /* align-items justify-items */
```

### place-content (Shorthand)

```css
place-content: center;
place-content: center start;
```

### Individual Item Alignment

```css
.item {
  justify-self: center;  /* Horizontal within cell */
  align-self: center;    /* Vertical within cell */
  place-self: center;    /* Both */
}
```

## Auto-Fit and Auto-Fill

Create responsive grids without media queries!

### auto-fill

Fills row with as many columns as fit, even if empty.

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}
```

### auto-fit

Similar to auto-fill but collapses empty tracks.

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

**When to use:**

- `auto-fill`: Want empty space preserved
- `auto-fit`: Want items to stretch (more common)

## MinMax Function

Set minimum and maximum sizes for tracks.

```css
/* Min 200px, max 1fr */
.grid {
  grid-template-columns: repeat(3, minmax(200px, 1fr));
}

/* Responsive without media queries */
.grid {
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

/* Prevent items from getting too small */
.grid {
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

## Implicit vs Explicit Grid

### Explicit Grid

Rows/columns you define.

```css
.grid {
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 100px 100px;
}
```

### Implicit Grid

Automatically created rows/columns for extra content.

```css
.grid {
  grid-template-columns: 1fr 1fr 1fr;
  /* Only defined columns, rows auto-created */
  
  grid-auto-rows: 150px;  /* Control implicit row height */
}
```

### Auto Flow

Control how auto-placed items flow.

```css
grid-auto-flow: row;     /* Default - fill rows first */
grid-auto-flow: column;  /* Fill columns first */
grid-auto-flow: dense;   /* Fill gaps (can change visual order) */
```

## Common Grid Patterns

### Basic Card Grid

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}
```

### Holy Grail Layout

```css
.layout {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "nav main aside"
    "footer footer footer";
  gap: 20px;
  min-height: 100vh;
}
```

### Magazine Layout

```css
.magazine {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 20px;
}

.featured {
  grid-column: span 4;
  grid-row: span 2;
}

.article {
  grid-column: span 2;
}
```

### Asymmetric Grid

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 200px;
  gap: 10px;
}

.tall {
  grid-row: span 2;
}

.wide {
  grid-column: span 2;
}

.big {
  grid-column: span 2;
  grid-row: span 2;
}
```

### Dashboard Grid

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-auto-rows: minmax(100px, auto);
  gap: 20px;
}

.widget-small {
  grid-column: span 3;
}

.widget-medium {
  grid-column: span 6;
}

.widget-large {
  grid-column: span 12;
}
```

## Practical Examples

### Photo Gallery

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-auto-rows: 200px;
  gap: 10px;
}

.gallery img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.featured {
  grid-column: span 2;
  grid-row: span 2;
}
```

### Responsive Form Layout

```css
.form {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.full-width {
  grid-column: 1 / -1;
}
```

### Sidebar Layout

```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 30px;
  padding: 20px;
}

@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

## Exercises

### Exercise 1: Basic Grid

Create a 3x3 grid with 9 equal boxes. Add 20px gap between cells.

### Exercise 2: Spanning Items

Create a grid where:

- First item spans 2 columns
- Second item spans 2 rows
- Third item spans 2 columns and 2 rows

### Exercise 3: Template Areas

Create a layout using grid-template-areas with header, sidebar, main content, and footer.

### Exercise 4: Responsive Cards

Create a card grid that shows:

- 4 cards per row on desktop
- 2 cards per row on tablet
- 1 card per row on mobile
  Use auto-fit and minmax (no media queries).

### Exercise 5: Photo Gallery

Create a photo gallery where some images are larger (span multiple cells) than others.

## Challenge Project: Complete Website Layout

Create a full website layout with:

- Header spanning full width
- Navigation sidebar (fixed width)
- Main content area with nested grid:
  - Hero section (full width)
  - 3-column feature section
  - 2-column service section
  - Full-width testimonial
- Aside for widgets (fixed width)
- Footer spanning full width
- Must be responsive:
  - Desktop: sidebar + main + aside
  - Tablet: main content full width, sidebar and aside stack below
  - Mobile: everything stacks

**Requirements:**

- Use grid-template-areas
- Nested grids for content sections
- Responsive with media queries
- Proper use of fr units
- Professional spacing with gap
- No fixed heights except where necessary

## Grid vs Flexbox Decision Tree

**Use Grid when:**

- Defining both rows AND columns
- Creating complex layouts
- Items align in two dimensions
- Working with overall page structure

**Use Flexbox when:**

- Creating one-dimensional layouts
- Items align in a single direction
- Building navigation bars
- Creating component layouts

**Use Both:**
Grid for page structure, Flexbox for components within grid cells!

## Common Mistakes to Avoid

1. **Forgetting display: grid:** Essential first step
1. **Overusing grid:** Use Flexbox for simpler component layouts
1. **Not using fr units:** They’re more flexible than percentages
1. **Hardcoding everything:** Use auto-fit/auto-fill for responsiveness
1. **Confusing grid lines:** Lines are numbered, not cells

## Key Takeaways

- Grid is for two-dimensional layouts (rows AND columns)
- Define structure with grid-template-columns/rows
- Use fr units for flexible sizing
- Gap creates space between cells
- grid-template-areas makes complex layouts intuitive
- auto-fit + minmax creates responsive grids without media queries
- Grid for layouts, Flexbox for components
- Can nest grids and flexbox within each other

-----

**Previous Module:** [Module 6 - Flexbox](module-06-flexbox.md)  
**Next Module:** [Module 8 - Responsive Design](module-08-responsive-design.md)

## Additional Resources

- [CSS Tricks Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid by Example](https://gridbyexample.com/)
- [Grid Garden Game](https://cssgridgarden.com/)
- [MDN Grid Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
