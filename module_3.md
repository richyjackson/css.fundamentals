# Module 3: Typography

## Introduction to Web Typography

Typography is the art of arranging text to make it readable, legible, and visually appealing. Good typography can make or break a design.

## Font Family

The `font-family` property specifies which font to use.

### Generic Font Families

```css
font-family: serif;       /* Times New Roman, Georgia */
font-family: sans-serif;  /* Arial, Helvetica */
font-family: monospace;   /* Courier, Monaco */
font-family: cursive;     /* Comic Sans, Brush Script */
font-family: fantasy;     /* Impact, Papyrus */
```

### Specific Fonts with Fallbacks

Always provide fallback fonts in case the first choice isn’t available.

```css
p {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

The browser tries each font in order, using the first available one.

### Web-Safe Fonts

Fonts commonly installed on most computers:

```css
/* Serif */
font-family: Georgia, serif;
font-family: "Times New Roman", Times, serif;

/* Sans-serif */
font-family: Arial, Helvetica, sans-serif;
font-family: Verdana, Geneva, sans-serif;
font-family: Tahoma, Geneva, sans-serif;

/* Monospace */
font-family: "Courier New", Courier, monospace;
font-family: Monaco, "Lucida Console", monospace;
```

## Font Size

Control the size of text with `font-size`.

### Units for Font Size

**Pixels (px) - Fixed size:**

```css
p {
  font-size: 16px;
}
```

**Em - Relative to parent:**

```css
body {
  font-size: 16px;
}

p {
  font-size: 1.5em;  /* 24px (16 * 1.5) */
}
```

**Rem - Relative to root element:**

```css
html {
  font-size: 16px;
}

h1 {
  font-size: 2rem;  /* 32px */
}

p {
  font-size: 1rem;  /* 16px */
}
```

**Percentage:**

```css
p {
  font-size: 120%;  /* 120% of parent font size */
}
```

**Keywords:**

```css
font-size: small;
font-size: medium;
font-size: large;
font-size: x-large;
```

**Best Practice:** Use `rem` for consistent, scalable typography.

## Font Weight

Control the thickness/boldness of text.

```css
font-weight: normal;    /* 400 */
font-weight: bold;      /* 700 */
font-weight: lighter;
font-weight: bolder;

/* Numeric values (100-900) */
font-weight: 100;  /* Thin */
font-weight: 300;  /* Light */
font-weight: 400;  /* Normal */
font-weight: 500;  /* Medium */
font-weight: 700;  /* Bold */
font-weight: 900;  /* Black */
```

## Font Style

```css
font-style: normal;
font-style: italic;
font-style: oblique;
```

## Text Color

```css
color: red;
color: #ff0000;
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5);  /* With transparency */
color: hsl(0, 100%, 50%);
```

## Text Alignment

```css
text-align: left;
text-align: center;
text-align: right;
text-align: justify;  /* Stretches lines to full width */
```

## Text Decoration

```css
text-decoration: none;           /* Remove underlines from links */
text-decoration: underline;
text-decoration: overline;
text-decoration: line-through;

/* Shorthand with color and style */
text-decoration: underline dotted red;
```

## Text Transform

```css
text-transform: uppercase;  /* MAKES TEXT UPPERCASE */
text-transform: lowercase;  /* makes text lowercase */
text-transform: capitalize; /* Makes First Letter Capital */
text-transform: none;       /* Normal text */
```

## Line Height

Space between lines of text. Crucial for readability.

```css
p {
  line-height: 1.5;    /* 1.5 times the font size (recommended) */
  line-height: 24px;   /* Fixed pixel value */
  line-height: 150%;   /* Percentage */
}
```

**Best Practice:** Use unitless values (1.5, 1.6) for line-height.

## Letter Spacing

Space between characters.

```css
letter-spacing: normal;
letter-spacing: 2px;    /* Increase spacing */
letter-spacing: -1px;   /* Decrease spacing */
letter-spacing: 0.1em;
```

## Word Spacing

Space between words.

```css
word-spacing: normal;
word-spacing: 5px;
word-spacing: 0.2em;
```

## Text Shadow

Add shadow effects to text.

```css
text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
/* horizontal vertical blur color */

/* Multiple shadows */
text-shadow: 
  2px 2px 4px rgba(0,0,0,0.3),
  -2px -2px 4px rgba(255,255,255,0.3);
```

## White Space and Text Wrapping

```css
/* How whitespace is handled */
white-space: normal;    /* Default - collapse whitespace */
white-space: nowrap;    /* Prevent line breaks */
white-space: pre;       /* Preserve whitespace */
white-space: pre-wrap;  /* Preserve whitespace but wrap */

/* Word breaking */
word-wrap: break-word;      /* Break long words */
overflow-wrap: break-word;  /* Modern syntax */
word-break: break-all;      /* Break anywhere */
```

## Web Fonts (Google Fonts)

Use custom fonts from Google Fonts or other providers.

### Method 1: Link in HTML

```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
</head>
```

### Method 2: Import in CSS

```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
```

### Using the Font

```css
body {
  font-family: 'Roboto', sans-serif;
}
```

### Popular Google Fonts

- **Sans-serif:** Roboto, Open Sans, Lato, Montserrat
- **Serif:** Playfair Display, Merriweather, Lora
- **Monospace:** Roboto Mono, Source Code Pro

## Font Shorthand

Combine multiple font properties in one line.

```css
/* font: [style] [variant] [weight] size/line-height family */
p {
  font: italic bold 16px/1.5 Arial, sans-serif;
}

/* Minimum requirement: size and family */
p {
  font: 16px Arial;
}
```

## Typography Best Practices

### 1. Font Pairing

Combine complementary fonts for headings and body text.

```css
h1, h2, h3 {
  font-family: 'Playfair Display', serif;
}

body {
  font-family: 'Open Sans', sans-serif;
}
```

### 2. Hierarchy with Size and Weight

```css
h1 {
  font-size: 2.5rem;
  font-weight: 700;
}

h2 {
  font-size: 2rem;
  font-weight: 600;
}

h3 {
  font-size: 1.5rem;
  font-weight: 600;
}

p {
  font-size: 1rem;
  font-weight: 400;
}
```

### 3. Readable Line Length

Keep line length between 50-75 characters for optimal readability.

```css
.content {
  max-width: 65ch;  /* ch unit = character width */
}
```

### 4. Adequate Line Height

```css
body {
  line-height: 1.6;  /* 1.5-1.6 is ideal for body text */
}

h1, h2, h3 {
  line-height: 1.2;  /* Headings can be tighter */
}
```

## Practical Examples

### Modern Article Typography

```css
.article {
  font-family: 'Georgia', serif;
  font-size: 1.125rem;
  line-height: 1.7;
  color: #333;
  max-width: 65ch;
  margin: 0 auto;
}

.article h1 {
  font-size: 2.5rem;
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 1rem;
  color: #111;
}

.article h2 {
  font-size: 1.875rem;
  font-weight: 600;
  margin-top: 2rem;
  margin-bottom: 1rem;
}

.article p {
  margin-bottom: 1.5rem;
}
```

### Button Text

```css
.button {
  font-family: 'Helvetica', sans-serif;
  font-size: 1rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
```

### Code Block

```css
code {
  font-family: 'Monaco', monospace;
  font-size: 0.875rem;
  background-color: #f5f5f5;
  padding: 2px 6px;
  border-radius: 3px;
}
```

## Exercises

### Exercise 1: Font Families

Create a page with three paragraphs, each using a different font family (serif, sans-serif, monospace).

### Exercise 2: Text Hierarchy

Create a blog post layout with:

- Main heading (h1)
- Subheading (h2)
- Body paragraphs
- Use different font sizes and weights to create visual hierarchy

### Exercise 3: Google Fonts

1. Choose two complementary fonts from Google Fonts
1. Import them into your project
1. Use one for headings, one for body text
1. Create a sample page demonstrating the pairing

### Exercise 4: Text Styling

Style a quote block with:

- Italic font style
- Larger font size
- Increased line height
- Custom color
- Text shadow

### Exercise 5: Responsive Typography

Create a heading that changes font size at different screen widths using media queries (preview for Module 8).

## Challenge Project: Typography Showcase

Create a single-page typography showcase featuring:

- Page title with custom Google Font
- Introduction paragraph with optimal line length and height
- Section with at least 3 levels of headings (h1, h2, h3)
- Pull quote styled distinctively
- Code snippet in monospace font
- List items with custom styling
- Footer with smaller, uppercase text

**Requirements:**

- Use at least 2 Google Fonts
- Implement proper typographic hierarchy
- Optimal line height and spacing
- Max-width for readable line length
- Consistent, professional appearance
- Proper use of font weights

## Key Takeaways

- Typography is crucial for readability and design
- Always provide fallback fonts
- Use relative units (rem, em) for scalability
- Line height of 1.5-1.6 is ideal for body text
- Limit line length to 50-75 characters
- Create clear hierarchy with size, weight, and spacing
- Web fonts expand design possibilities

-----

**Previous Module:** [Module 2 - The Box Model](module-02-box-model.md)  
**Next Module:** [Module 4 - Colors and Backgrounds](module-04-colors-backgrounds.md)

## Additional Resources

- [Google Fonts](https://fonts.google.com/)
- [MDN Web Fonts Guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)
- [Typography.js](http://kyleamathews.github.io/typography.js/)
