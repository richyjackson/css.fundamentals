# Module 9: Transitions and Animations

## Introduction

CSS transitions and animations add motion and interactivity to your websites. Transitions create smooth changes between states, while animations provide more complex, keyframe-based motion.

## CSS Transitions

Transitions smooth out changes from one state to another (like hover effects).

### Basic Transition Syntax

```css
.element {
  transition: property duration timing-function delay;
}
```

### transition-property

Which property to animate.

```css
/* Single property */
.box {
  transition-property: background-color;
}

/* Multiple properties */
.box {
  transition-property: background-color, transform;
}

/* All properties */
.box {
  transition-property: all;
}
```

### transition-duration

How long the transition takes.

```css
transition-duration: 0.3s;      /* 300 milliseconds */
transition-duration: 1s;        /* 1 second */
transition-duration: 500ms;     /* 500 milliseconds */
```

### transition-timing-function

The speed curve of the transition.

```css
transition-timing-function: ease;         /* Default - slow start, fast middle, slow end */
transition-timing-function: linear;       /* Constant speed */
transition-timing-function: ease-in;      /* Slow start */
transition-timing-function: ease-out;     /* Slow end */
transition-timing-function: ease-in-out;  /* Slow start and end */

/* Cubic bezier - custom curves */
transition-timing-function: cubic-bezier(0.42, 0, 0.58, 1);
```

**Visual comparison:**

- **ease:** Natural feeling, most common
- **linear:** Mechanical, good for colors
- **ease-in:** Good for elements leaving screen
- **ease-out:** Good for elements entering screen
- **ease-in-out:** Good for elements moving within screen

### transition-delay

Wait before starting transition.

```css
transition-delay: 0s;      /* No delay (default) */
transition-delay: 0.2s;    /* Wait 200ms */
transition-delay: 500ms;   /* Wait 500ms */
```

### Transition Shorthand

```css
/* transition: property duration timing-function delay */
.button {
  transition: background-color 0.3s ease 0s;
}

/* Multiple transitions */
.button {
  transition: 
    background-color 0.3s ease,
    transform 0.2s ease-out,
    box-shadow 0.3s ease;
}

/* Common shorthand */
.button {
  transition: all 0.3s ease;
}
```

### Practical Transition Examples

#### Button Hover Effect

```css
.button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.button:hover {
  background-color: #0056b3;
  transform: translateY(-2px);
}
```

#### Card Lift Effect

```css
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}
```

#### Menu Slide In

```css
.menu {
  transform: translateX(-100%);
  transition: transform 0.3s ease-in-out;
}

.menu.active {
  transform: translateX(0);
}
```

#### Image Zoom

```css
.image-container {
  overflow: hidden;
}

.image-container img {
  transition: transform 0.5s ease;
}

.image-container:hover img {
  transform: scale(1.1);
}
```

## Transform Property

Transforms modify element position, scale, rotation, or skew. Great with transitions!

### translate (Move)

```css
transform: translateX(50px);       /* Move right 50px */
transform: translateY(-30px);      /* Move up 30px */
transform: translate(50px, -30px); /* Move right 50px, up 30px */
```

### scale (Resize)

```css
transform: scale(1.5);           /* 150% size (both dimensions) */
transform: scale(2, 1);          /* Double width, same height */
transform: scaleX(1.5);          /* 150% width only */
transform: scaleY(0.5);          /* 50% height only */
```

### rotate

```css
transform: rotate(45deg);        /* Rotate 45 degrees clockwise */
transform: rotate(-90deg);       /* Rotate 90 degrees counter-clockwise */
```

### skew (Slant)

```css
transform: skewX(20deg);         /* Slant horizontally */
transform: skewY(10deg);         /* Slant vertically */
transform: skew(20deg, 10deg);   /* Both */
```

### Multiple Transforms

```css
/* Combine transforms (space-separated) */
transform: translateX(50px) rotate(45deg) scale(1.2);

/* Order matters! These are different: */
transform: rotate(45deg) translateX(50px);
transform: translateX(50px) rotate(45deg);
```

### transform-origin

Change the pivot point for transformations.

```css
transform-origin: center;        /* Default */
transform-origin: top left;
transform-origin: bottom right;
transform-origin: 50% 50%;       /* Same as center */
transform-origin: 0 0;           /* Top left corner */
```

**Example - rotate from corner:**

```css
.card {
  transform-origin: top left;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: rotate(5deg);
}
```

## CSS Animations

Animations use keyframes to create more complex motion sequences.

### Keyframes Syntax

```css
@keyframes animation-name {
  from {
    /* Starting state */
  }
  to {
    /* Ending state */
  }
}

/* OR with percentages */
@keyframes animation-name {
  0% {
    /* Starting state */
  }
  50% {
    /* Middle state */
  }
  100% {
    /* Ending state */
  }
}
```

### animation-name

Which keyframe animation to use.

```css
.element {
  animation-name: slideIn;
}

@keyframes slideIn {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}
```

### animation-duration

How long the animation lasts.

```css
animation-duration: 2s;
animation-duration: 500ms;
```

### animation-timing-function

Speed curve (same as transitions).

```css
animation-timing-function: ease;
animation-timing-function: linear;
animation-timing-function: ease-in-out;
```

### animation-delay

Wait before starting animation.

```css
animation-delay: 1s;
animation-delay: 500ms;
```

### animation-iteration-count

How many times to repeat.

```css
animation-iteration-count: 1;          /* Once (default) */
animation-iteration-count: 3;          /* 3 times */
animation-iteration-count: infinite;   /* Forever */
```

### animation-direction

Which direction to play animation.

```css
animation-direction: normal;           /* Default - forward */
animation-direction: reverse;          /* Backward */
animation-direction: alternate;        /* Forward, then backward */
animation-direction: alternate-reverse; /* Backward, then forward */
```

### animation-fill-mode

What styles apply before/after animation.

```css
animation-fill-mode: none;        /* Default - no styles applied */
animation-fill-mode: forwards;    /* Keep ending state */
animation-fill-mode: backwards;   /* Apply starting state immediately */
animation-fill-mode: both;        /* Both forwards and backwards */
```

### animation-play-state

Pause or play animation.

```css
animation-play-state: running;    /* Default - playing */
animation-play-state: paused;     /* Paused */
```

**Example - pause on hover:**

```css
.spinner {
  animation: spin 2s linear infinite;
}

.spinner:hover {
  animation-play-state: paused;
}
```

### Animation Shorthand

```css
/* animation: name duration timing-function delay iteration-count direction fill-mode play-state */
.element {
  animation: slideIn 1s ease-in-out 0s 1 normal forwards running;
}

/* Common shorthand */
.element {
  animation: fadeIn 1s ease-in-out;
}
```

## Common Animation Patterns

### Fade In

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.fade-in {
  animation: fadeIn 1s ease-in;
}
```

### Slide In from Left

```css
@keyframes slideInLeft {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.slide-in-left {
  animation: slideInLeft 0.5s ease-out;
}
```

### Bounce

```css
@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-30px);
  }
}

.bounce {
  animation: bounce 1s ease-in-out infinite;
}
```

### Pulse

```css
@keyframes pulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

.pulse {
  animation: pulse 2s ease-in-out infinite;
}
```

### Spin/Rotate

```css
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.spinner {
  animation: spin 1s linear infinite;
}
```

### Shake

```css
@keyframes shake {
  0%, 100% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-10px);
  }
  75% {
    transform: translateX(10px);
  }
}

.shake {
  animation: shake 0.5s ease-in-out;
}
```

### Color Change

```css
@keyframes colorChange {
  0% {
    background-color: red;
  }
  33% {
    background-color: yellow;
  }
  66% {
    background-color: blue;
  }
  100% {
    background-color: red;
  }
}

.rainbow {
  animation: colorChange 3s linear infinite;
}
```

### Loading Dots

```css
@keyframes loadingDots {
  0%, 100% {
    opacity: 0.3;
  }
  50% {
    opacity: 1;
  }
}

.dot:nth-child(1) {
  animation: loadingDots 1.4s infinite;
  animation-delay: 0s;
}

.dot:nth-child(2) {
  animation: loadingDots 1.4s infinite;
  animation-delay: 0.2s;
}

.dot:nth-child(3) {
  animation: loadingDots 1.4s infinite;
  animation-delay: 0.4s;
}
```

## Performance Considerations

### Animate Performance-Friendly Properties

**Fast (GPU accelerated):**

- `transform` (translate, scale, rotate)
- `opacity`

**Slow (triggers layout/paint):**

- `width`, `height`
- `margin`, `padding`
- `top`, `left`, `right`, `bottom`

**Best practice:**

```css
/* Good - uses transform */
.box:hover {
  transform: translateX(100px);
}

/* Bad - uses left */
.box:hover {
  left: 100px;
}
```

### will-change

Hint to browser about upcoming changes.

```css
.animated-element {
  will-change: transform, opacity;
}

/* Remove after animation */
.animated-element.done {
  will-change: auto;
}
```

**Don’t overuse!** Only for elements that will actually animate.

## Practical Examples

### Button with Multiple Effects

```css
.fancy-button {
  background: linear-gradient(45deg, #667eea, #764ba2);
  color: white;
  border: none;
  padding: 15px 30px;
  position: relative;
  overflow: hidden;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.fancy-button::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background: rgba(255,255,255,0.3);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: width 0.6s ease, height 0.6s ease;
}

.fancy-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

.fancy-button:hover::before {
  width: 300px;
  height: 300px;
}
```

### Loading Spinner

```css
.spinner {
  width: 50px;
  height: 50px;
  border: 5px solid #f3f3f3;
  border-top: 5px solid #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}
```

### Progress Bar Fill

```css
.progress-bar {
  width: 100%;
  height: 20px;
  background: #f0f0f0;
  border-radius: 10px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #667eea, #764ba2);
  width: 0;
  animation: fillProgress 2s ease-out forwards;
}

@keyframes fillProgress {
  to {
    width: 100%;
  }
}
```

## Exercises

### Exercise 1: Button Transitions

Create a button with smooth hover effects:

- Background color change
- Slight lift (translateY)
- Box shadow increase
- All transitions should be smooth

### Exercise 2: Card Flip

Create a card that flips on hover to reveal back content.

### Exercise 3: Loading Animation

Create a loading animation with three dots that pulse in sequence.

### Exercise 4: Sliding Menu

Create a menu that slides in from the left when a button is clicked.

### Exercise 5: Image Gallery

Create a gallery where images zoom and brighten on hover.

## Challenge Project: Animated Landing Page

Create an animated landing page with:

**On Page Load:**

- Hero heading fades in and slides up
- Subheading appears after delay
- CTA button bounces in
- Background gradient animates

**Interactive Elements:**

- Buttons with hover effects (lift, glow, ripple)
- Cards that lift and cast shadow on hover
- Navigation links with underline animation
- Smooth scroll animations
- Form inputs with focus animations
- Loading spinner for fake “submit”

**Advanced Animations:**

- Parallax scrolling effect
- Staggered animations for list items
- Floating elements with infinite animation
- Smooth page transitions

**Requirements:**

- Use both transitions and keyframe animations
- At least 5 different animation effects
- Smooth timing functions
- Proper performance (use transform/opacity)
- Accessibility (respect prefers-reduced-motion)
- Professional polish

## Accessibility: Reduced Motion

Respect user preferences for reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Common Mistakes to Avoid

1. **Animating expensive properties:** Use transform and opacity
1. **Too much animation:** Subtle is better
1. **Too slow/fast:** 0.2s-0.5s is usually good
1. **Forgetting to test performance:** Check on slower devices
1. **Ignoring accessibility:** Respect prefers-reduced-motion

## Key Takeaways

- Transitions: smooth changes between states (hover, focus)
- Animations: complex sequences with keyframes
- Use transform and opacity for best performance
- Common timing: 0.2s-0.5s for interactions
- Timing functions: ease for natural motion
- Multiple animations: stagger with delays
- Accessibility: respect reduced-motion preferences
- Less is more: subtle animations feel professional

-----

**Previous Module:** [Module 8 - Responsive Design](module-08-responsive-design.md)  
**Next Module:** [Module 10 - Advanced Selectors](module-10-advanced-selectors.md)

## Additional Resources

- [Animista](https://animista.net/) - CSS Animation Generator
- [Cubic Bezier](https://cubic-bezier.com/) - Timing Function Generator
- [MDN Animations Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
