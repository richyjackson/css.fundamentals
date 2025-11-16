# Module 8: Responsive Design

## Introduction to Responsive Design

Responsive design means creating websites that adapt to different screen sizes and devices. Your site should look great on phones, tablets, laptops, and desktop monitors.

## Viewport Meta Tag

**Critical first step!** Add this to your HTML `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Without this, mobile browsers display pages as if on desktop, then zoom out.

## Responsive Units

### Absolute Units

Fixed size, doesn’t change.

```css
px    /* Pixels - most common absolute unit */
pt    /* Points */
cm    /* Centimeters */
```

### Relative Units

Size relative to something else.

#### EM

Relative to parent element’s font size.

```css
.parent {
  font-size: 16px;
}

.child {
  font-size: 2em;    /* 32px (16 * 2) */
  padding: 1em;      /* 32px (based on own font-size) */
}
```

**Compounding issue:**

```css
.level1 { font-size: 1.2em; }  /* 19.2px if parent is 16px */
.level2 { font-size: 1.2em; }  /* 23px (19.2 * 1.2) */
.level3 { font-size: 1.2em; }  /* 27.6px (23 * 1.2) */
```

#### REM

Relative to root element (html) font size. **Recommended for typography!**

```css
html {
  font-size: 16px;  /* Base size */
}

h1 {
  font-size: 2.5rem;   /* 40px (16 * 2.5) */
}

p {
  font-size: 1rem;     /* 16px */
}

.small {
  font-size: 0.875rem; /* 14px */
}
```

**No compounding with rem:**

```css
.level1 { font-size: 1.2rem; }  /* Always 19.2px */
.level2 { font-size: 1.2rem; }  /* Always 19.2px */
.level3 { font-size: 1.2rem; }  /* Always 19.2px */
```

#### Percentages

Relative to parent element.

```css
.container {
  width: 1200px;
}

.child {
  width: 50%;  /* 600px (50% of 1200px) */
}
```

#### Viewport Units

Relative to viewport (browser window) size.

```css
vw   /* Viewport width - 1vw = 1% of viewport width */
vh   /* Viewport height - 1vh = 1% of viewport height */
vmin /* Smaller of vw or vh */
vmax /* Larger of vw or vh */
```

**Examples:**

```css
.full-screen {
  width: 100vw;
  height: 100vh;
}

.hero {
  height: 80vh;  /* 80% of viewport height */
}

.responsive-text {
  font-size: 5vw;  /* Scales with viewport width */
}
```

**Fluid typography:**

```css
h1 {
  font-size: calc(1.5rem + 2vw);  /* Grows with viewport */
}
```

#### CH Unit

Width of the “0” character. Great for limiting line length!

```css
.article {
  max-width: 65ch;  /* Optimal reading length: 50-75 characters */
}
```

## Media Queries

Apply styles based on device characteristics (usually screen width).

### Basic Syntax

```css
@media (condition) {
  /* CSS rules */
}
```

### Width Queries

```css
/* Mobile first - styles for small screens */
.container {
  width: 100%;
  padding: 10px;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    width: 750px;
    padding: 20px;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    width: 960px;
  }
}

/* Large desktop */
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
```

### Common Breakpoints

```css
/* Mobile: < 576px (no media query needed) */

/* Small devices (landscape phones) */
@media (min-width: 576px) { }

/* Medium devices (tablets) */
@media (min-width: 768px) { }

/* Large devices (desktops) */
@media (min-width: 992px) { }

/* Extra large devices (large desktops) */
@media (min-width: 1200px) { }
```

### Max-Width Queries (Desktop First)

```css
/* Desktop styles first */
.container {
  width: 1200px;
}

/* Tablet */
@media (max-width: 1024px) {
  .container {
    width: 100%;
    padding: 20px;
  }
}

/* Mobile */
@media (max-width: 768px) {
  .container {
    padding: 10px;
  }
}
```

### Range Queries

```css
/* Between 768px and 1024px */
@media (min-width: 768px) and (max-width: 1024px) {
  .container {
    width: 750px;
  }
}
```

### Orientation Queries

```css
/* Portrait (height > width) */
@media (orientation: portrait) {
  .sidebar {
    display: none;
  }
}

/* Landscape (width > height) */
@media (orientation: landscape) {
  .sidebar {
    display: block;
  }
}
```

### Multiple Conditions

```css
@media (min-width: 768px) and (max-width: 1024px) and (orientation: portrait) {
  /* Styles */
}
```

### Media Queries in HTML

```html
<!-- Load different stylesheets for different screens -->
<link rel="stylesheet" href="mobile.css" media="(max-width: 768px)">
<link rel="stylesheet" href="desktop.css" media="(min-width: 769px)">
```

## Mobile-First vs Desktop-First

### Mobile-First (Recommended)

Start with mobile styles, add complexity for larger screens.

```css
/* Mobile (default) */
.nav {
  flex-direction: column;
}

/* Tablet and up */
@media (min-width: 768px) {
  .nav {
    flex-direction: row;
  }
}
```

**Advantages:**

- Faster on mobile (less CSS to override)
- Forces you to prioritize content
- Better performance

### Desktop-First

Start with desktop styles, simplify for smaller screens.

```css
/* Desktop (default) */
.nav {
  flex-direction: row;
}

/* Mobile */
@media (max-width: 768px) {
  .nav {
    flex-direction: column;
  }
}
```

## Responsive Images

### Max-Width for Scalable Images

```css
img {
  max-width: 100%;
  height: auto;
}
```

### Picture Element

Different images for different screens.

```html
<picture>
  <source media="(min-width: 1200px)" srcset="large.jpg">
  <source media="(min-width: 768px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Description">
</picture>
```

### Srcset Attribute

Let browser choose best image.

```html
<img 
  src="image-small.jpg"
  srcset="image-small.jpg 400w,
          image-medium.jpg 800w,
          image-large.jpg 1200w"
  sizes="(max-width: 768px) 100vw, 50vw"
  alt="Responsive image"
>
```

### Object-Fit

Control how images fit containers.

```css
.image-container {
  width: 300px;
  height: 300px;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;     /* Crop to fill */
  object-fit: contain;   /* Fit entire image */
  object-fit: fill;      /* Stretch to fill */
}
```

## Responsive Typography

### Fluid Typography with Clamp

```css
h1 {
  font-size: clamp(1.5rem, 4vw, 3rem);
  /* min: 1.5rem, preferred: 4vw, max: 3rem */
}

p {
  font-size: clamp(1rem, 2vw, 1.25rem);
}
```

### Media Query Approach

```css
h1 {
  font-size: 2rem;
}

@media (min-width: 768px) {
  h1 {
    font-size: 2.5rem;
  }
}

@media (min-width: 1024px) {
  h1 {
    font-size: 3rem;
  }
}
```

### Rem-Based Scale

```css
html {
  font-size: 14px;
}

@media (min-width: 768px) {
  html {
    font-size: 16px;
  }
}

@media (min-width: 1024px) {
  html {
    font-size: 18px;
  }
}

/* All rem values scale automatically */
h1 {
  font-size: 2.5rem;  /* 35px on mobile, 40px tablet, 45px desktop */
}
```

## Responsive Layout Patterns

### Stack to Horizontal

```css
.container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

@media (min-width: 768px) {
  .container {
    flex-direction: row;
  }
}
```

### Collapsible Sidebar

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
}

.sidebar {
  display: none;
}

@media (min-width: 1024px) {
  .layout {
    grid-template-columns: 250px 1fr;
  }
  
  .sidebar {
    display: block;
  }
}
```

### Responsive Grid

```css
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (min-width: 1200px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

### Hamburger Menu

```css
.nav-toggle {
  display: block;
}

.nav-menu {
  display: none;
}

.nav-menu.active {
  display: flex;
  flex-direction: column;
}

@media (min-width: 768px) {
  .nav-toggle {
    display: none;
  }
  
  .nav-menu {
    display: flex;
    flex-direction: row;
  }
}
```

## Container Queries (Modern)

Style elements based on container size, not viewport!

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

.card {
  padding: 20px;
}

@container card (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}
```

## Responsive Best Practices

### 1. Test on Real Devices

Browser DevTools are good, but test on actual phones/tablets.

### 2. Touch-Friendly Targets

```css
.button {
  min-height: 44px;  /* Apple recommendation */
  min-width: 44px;
  padding: 12px 24px;
}
```

### 3. Readable Text

```css
body {
  font-size: 16px;  /* Minimum for mobile readability */
  line-height: 1.6;
}
```

### 4. Optimize Performance

```css
/* Load only what's needed */
@media (min-width: 1024px) {
  .hero {
    background-image: url('hero-large.jpg');
  }
}
```

### 5. Use Flexible Layouts

```css
/* Avoid fixed widths */
.container {
  max-width: 1200px;
  width: 100%;
  padding: 0 20px;
}
```

## Exercises

### Exercise 1: Responsive Typography

Create headings that scale smoothly from mobile to desktop using clamp() or media queries.

### Exercise 2: Responsive Navigation

Build a navigation that:

- Shows hamburger menu on mobile
- Displays horizontally on desktop
- Includes smooth transitions

### Exercise 3: Card Grid

Create a card grid that shows:

- 1 column on mobile
- 2 columns on tablet
- 3 columns on small desktop
- 4 columns on large desktop

### Exercise 4: Flexible Container

Create a container that:

- Has padding on mobile
- Centers on desktop with max-width
- Uses different font sizes at different breakpoints

### Exercise 5: Responsive Images

Implement responsive images using:

- max-width: 100%
- Picture element OR srcset
- object-fit for aspect ratio control

## Challenge Project: Fully Responsive Landing Page

Create a complete landing page that adapts perfectly to all screen sizes:

**Mobile (< 768px):**

- Single column layout
- Hamburger navigation
- Stacked sections
- Touch-friendly buttons

**Tablet (768px - 1024px):**

- 2-column grid where appropriate
- Horizontal navigation
- Larger images

**Desktop (> 1024px):**

- Multi-column layouts
- Sidebar navigation
- Large hero section
- Maximum content width with centering

**Requirements:**

- Mobile-first approach
- Smooth transitions between breakpoints
- Responsive images (srcset or picture)
- Fluid typography (scales with screen)
- Touch targets (44px minimum)
- No horizontal scrolling on any device
- Test at least 5 different screen sizes
- Use REM units for typography
- Flexible layouts (no fixed widths)

## Common Mistakes to Avoid

1. **Forgetting viewport meta tag:** Site won’t be responsive without it
1. **Using fixed widths:** Use max-width and percentages instead
1. **Too many breakpoints:** 3-4 is usually enough
1. **Not testing on real devices:** DevTools aren’t perfect
1. **Desktop-first mindset:** Mobile-first is usually better

## Key Takeaways

- Always include viewport meta tag
- Use relative units (rem, %, vw, vh)
- Media queries adapt styles to screen sizes
- Mobile-first approach is recommended
- Test on real devices
- Make touch targets large enough (44px minimum)
- Responsive images save bandwidth
- Container queries are the future
- Fluid typography scales smoothly

-----

**Previous Module:** [Module 7 - Grid Layout](module-07-grid-layout.md)  
**Next Module:** [Module 9 - Transitions and Animations](module-09-transitions-animations.md)

## Additional Resources

- [MDN Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [Responsive Images Guide](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
- [Can I Use](https://caniuse.com/) - Check browser support
