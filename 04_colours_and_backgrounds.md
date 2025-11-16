# Module 4: Colors and Backgrounds

## CSS Color Values

CSS offers multiple ways to specify colors, each with different use cases.

### Named Colors

CSS provides 140+ predefined color names.

```css
color: red;
color: blue;
color: limegreen;
color: hotpink;
color: cornflowerblue;
```

**Pros:** Easy to remember  
**Cons:** Limited options, not precise

### Hexadecimal (Hex) Colors

Six-digit codes representing Red, Green, Blue values.

```css
color: #ff0000;  /* Red */
color: #00ff00;  /* Green */
color: #0000ff;  /* Blue */
color: #ffffff;  /* White */
color: #000000;  /* Black */
color: #cccccc;  /* Gray */

/* Shorthand (when pairs are identical) */
color: #f00;     /* Same as #ff0000 */
color: #0f0;     /* Same as #00ff00 */
```

**Format:** `#RRGGBB` (each pair is 00-FF in hexadecimal)

### RGB Colors

Red, Green, Blue values from 0-255.

```css
color: rgb(255, 0, 0);      /* Red */
color: rgb(0, 255, 0);      /* Green */
color: rgb(0, 0, 255);      /* Blue */
color: rgb(128, 128, 128);  /* Gray */
```

### RGBA Colors

RGB with Alpha (transparency) channel (0-1).

```css
color: rgba(255, 0, 0, 1);      /* Fully opaque red */
color: rgba(255, 0, 0, 0.5);    /* 50% transparent red */
color: rgba(0, 0, 0, 0.8);      /* 80% opaque black */
background: rgba(255, 255, 255, 0.1);  /* Subtle white overlay */
```

**Alpha values:**

- `0` = fully transparent
- `0.5` = 50% transparent
- `1` = fully opaque

### HSL Colors

Hue, Saturation, Lightness - more intuitive for designers.

```css
color: hsl(0, 100%, 50%);    /* Red */
color: hsl(120, 100%, 50%);  /* Green */
color: hsl(240, 100%, 50%);  /* Blue */
color: hsl(0, 0%, 50%);      /* Gray */
```

**Components:**

- **Hue:** 0-360 (color wheel degrees)
  - 0/360 = Red
  - 120 = Green
  - 240 = Blue
- **Saturation:** 0-100% (color intensity)
  - 0% = Grayscale
  - 100% = Full color
- **Lightness:** 0-100% (brightness)
  - 0% = Black
  - 50% = Normal
  - 100% = White

### HSLA Colors

HSL with Alpha transparency.

```css
color: hsla(0, 100%, 50%, 0.5);    /* 50% transparent red */
background: hsla(240, 100%, 50%, 0.3);  /* Subtle blue */
```

## Color Properties

### Text Color

```css
color: #333333;
```

### Background Color

```css
background-color: #f5f5f5;
background-color: transparent;  /* No background */
```

### Border Color

```css
border-color: #cccccc;
border: 1px solid #dddddd;
```

### Outline Color

```css
outline: 2px solid blue;
outline-color: red;
```

## Opacity

Control transparency of entire element (including text and children).

```css
.box {
  background-color: red;
  opacity: 0.5;  /* 50% transparent */
}
```

**Note:** Unlike `rgba()`, opacity affects the entire element and all its children.

## Background Properties

### Background Color

```css
background-color: lightblue;
background-color: #f0f0f0;
```

### Background Image

```css
background-image: url('image.jpg');
background-image: url('https://example.com/image.png');

/* Multiple backgrounds (first on top) */
background-image: 
  url('overlay.png'),
  url('background.jpg');
```

### Background Repeat

```css
background-repeat: repeat;      /* Default - tile in both directions */
background-repeat: repeat-x;    /* Repeat horizontally only */
background-repeat: repeat-y;    /* Repeat vertically only */
background-repeat: no-repeat;   /* Don't repeat */
```

### Background Size

```css
background-size: auto;          /* Default - original size */
background-size: cover;         /* Cover entire area, may crop */
background-size: contain;       /* Fit entire image, may show gaps */
background-size: 100px 200px;   /* Specific width and height */
background-size: 50%;           /* Percentage of container */
```

**Most common:**

```css
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
```

### Background Position

```css
background-position: center;
background-position: top left;
background-position: bottom right;
background-position: 50% 50%;    /* Center (default) */
background-position: 0 0;        /* Top left */
background-position: 100px 50px; /* Specific position */
```

**Common positions:**

- `center` - Center both directions
- `top`, `bottom`, `left`, `right`
- `top left`, `top right`, `bottom left`, `bottom right`

### Background Attachment

```css
background-attachment: scroll;   /* Default - scrolls with page */
background-attachment: fixed;    /* Fixed position (parallax effect) */
background-attachment: local;    /* Scrolls with element content */
```

### Background Shorthand

Combine all background properties in one line.

```css
/* background: color image repeat position / size */
background: #f0f0f0 url('bg.jpg') no-repeat center / cover;

/* Common pattern */
background: url('hero.jpg') no-repeat center center / cover;
```

**Order matters in shorthand!**

## Gradients

CSS can create gradient backgrounds without images.

### Linear Gradients

```css
/* Top to bottom (default) */
background: linear-gradient(red, blue);

/* Specific direction */
background: linear-gradient(to right, red, blue);
background: linear-gradient(to bottom right, red, blue);
background: linear-gradient(45deg, red, blue);

/* Multiple color stops */
background: linear-gradient(red, yellow, green);

/* Color stops with positions */
background: linear-gradient(
  red 0%,
  yellow 50%,
  green 100%
);

/* Practical example */
background: linear-gradient(
  135deg,
  #667eea 0%,
  #764ba2 100%
);
```

### Radial Gradients

```css
/* Center outward (default) */
background: radial-gradient(red, blue);

/* Specific shape and size */
background: radial-gradient(circle, red, blue);
background: radial-gradient(ellipse, red, blue);

/* Position */
background: radial-gradient(circle at top left, red, blue);

/* Practical example */
background: radial-gradient(
  circle at center,
  rgba(255,255,255,0.3) 0%,
  rgba(0,0,0,0.8) 100%
);
```

### Multiple Backgrounds

```css
background: 
  linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
  url('image.jpg') center/cover;
```

## Color Schemes and Best Practices

### Contrast for Readability

Ensure sufficient contrast between text and background.

```css
/* Good contrast */
.readable {
  color: #333333;
  background-color: #ffffff;
}

/* Poor contrast - avoid */
.hard-to-read {
  color: #cccccc;
  background-color: #ffffff;
}
```

**WCAG Guidelines:**

- Normal text: 4.5:1 contrast ratio
- Large text: 3:1 contrast ratio

### Color Variables

Use CSS custom properties for consistent color schemes.

```css
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --accent-color: #e74c3c;
  --text-color: #333333;
  --bg-color: #ffffff;
  --gray-light: #f8f9fa;
  --gray-dark: #6c757d;
}

.button-primary {
  background-color: var(--primary-color);
  color: white;
}

.button-secondary {
  background-color: var(--secondary-color);
  color: white;
}
```

### 60-30-10 Rule

- 60% dominant color (usually neutral)
- 30% secondary color
- 10% accent color

```css
body {
  background-color: #f5f5f5;  /* 60% - neutral background */
}

.sidebar {
  background-color: #2c3e50;  /* 30% - secondary */
}

.button {
  background-color: #e74c3c;  /* 10% - accent */
}
```

## Practical Examples

### Card with Gradient Background

```css
.card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 30px;
  border-radius: 10px;
}
```

### Hero Section with Overlay

```css
.hero {
  background: 
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url('hero-image.jpg') center/cover no-repeat;
  height: 500px;
  color: white;
}
```

### Transparent Card

```css
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 10px;
  padding: 20px;
}
```

### Button States with HSL

```css
.button {
  background-color: hsl(210, 100%, 50%);
}

.button:hover {
  background-color: hsl(210, 100%, 40%);  /* Darker on hover */
}

.button:active {
  background-color: hsl(210, 100%, 30%);  /* Even darker when clicked */
}
```

## Exercises

### Exercise 1: Color Formats

Create five boxes, each with a different color format:

1. Named color
1. Hex color
1. RGB color
1. RGBA with transparency
1. HSL color

### Exercise 2: Gradient Backgrounds

Create three cards with different gradient backgrounds:

1. Linear gradient (top to bottom)
1. Linear gradient (diagonal)
1. Radial gradient

### Exercise 3: Background Images

Create a hero section with:

- Background image
- Dark overlay using gradient
- Centered white text
- Cover background size

### Exercise 4: Color Scheme

Create a color scheme using CSS variables:

- Define 5 colors as variables
- Use them throughout a sample page
- Include primary, secondary, accent, text, and background colors

### Exercise 5: Transparency

Create overlapping elements demonstrating:

- Opacity property
- RGBA colors
- Transparent backgrounds

## Challenge Project: Landing Page Hero

Create a landing page hero section with:

- Full-screen background image with `background-size: cover`
- Dark gradient overlay for text readability
- Centered headline and subheadline in white
- Call-to-action button with gradient background
- Button hover effect with color change
- Implement using CSS variables for colors
- Proper contrast ratios

**Requirements:**

- Use at least 3 color formats (hex, rgba, hsl)
- Implement linear gradient
- Use background shorthand properly
- Create a cohesive color scheme
- Ensure text is readable over images

## Common Mistakes to Avoid

1. **Poor contrast:** Always check text is readable on backgrounds
1. **Too many colors:** Stick to a limited color palette
1. **Ignoring transparency:** Use rgba/hsla for overlays instead of opacity when you want text to stay opaque
1. **Not using variables:** Hard-coding colors makes changes difficult

## Key Takeaways

- Multiple color formats available: named, hex, rgb, hsl
- Use rgba/hsla for transparent colors
- Gradients can replace background images
- Background shorthand simplifies code
- CSS variables make color schemes maintainable
- Always ensure proper contrast for accessibility
- HSL is often more intuitive for color manipulation

-----

**Previous Module:** [Module 3 - Typography](module-03-typography.md)  
**Next Module:** [Module 5 - Layout Basics](module-05-layout-basics.md)

## Additional Resources

- [Color Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Coolors Color Palette Generator](https://coolors.co/)
- [MDN Color Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)
