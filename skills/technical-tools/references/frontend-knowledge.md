# Front-End Knowledge for Designers

## Table of Contents
1. [HTML/CSS Fundamentals](#1-htmlcss-fundamentals)
2. [Responsive CSS](#2-responsive-css)
3. [CSS Animations](#3-css-animations)
4. [JavaScript Basics](#4-javascript-basics)
5. [React/Vue/Angular Awareness](#5-reactvueangular-awareness)
6. [Design-to-Code Handoff](#6-design-to-code-handoff)
7. [Browser DevTools](#7-browser-devtools)

---

## 1. HTML/CSS Fundamentals

**Purpose:** Understand the medium designers design for — how HTML creates structure and CSS applies visual style — so design decisions are grounded in what's actually possible and efficient to build.

**When to use:** When making design decisions about layout, spacing, or visual properties; when reviewing developer implementations; when writing design specs.

### The Box Model

Every HTML element is a box:

```
┌────────────────────────────────┐
│           margin               │  ← Outside the element — space between elements
│  ┌─────────────────────────┐   │
│  │        border           │   │  ← The visible border (if any)
│  │  ┌───────────────────┐  │   │
│  │  │     padding       │  │   │  ← Inside the border — space within the element
│  │  │  ┌─────────────┐  │  │   │
│  │  │  │   content   │  │  │   │  ← Text, images, child elements
│  │  │  └─────────────┘  │  │   │
│  │  └───────────────────┘  │   │
│  └─────────────────────────┘   │
└────────────────────────────────┘

Design implication:
  Padding adds space INSIDE a card — between border and content.
  Margin adds space OUTSIDE a card — between this card and neighbors.
  Never confuse the two: "space inside card" = padding, "gap between cards" = margin or gap.
```

### CSS Box Sizing

```css
/* The default is confusing: width/height applies to content only */
.box { box-sizing: content-box; width: 200px; padding: 20px; }
/* Total rendered width = 240px (200 + 20 + 20) */

/* Modern standard: width/height includes padding and border */
*, *::before, *::after { box-sizing: border-box; }
.box { width: 200px; padding: 20px; }
/* Total rendered width = 200px (padding is inside) */

Design implication: With border-box, a 200px card with 20px padding
  has 160px of usable content space (200 - 20 - 20).
  Figma's width = the border-box width.
```

### CSS Display Types

```
block:   Takes full width, stacks vertically (div, p, h1, section)
inline:  Flows with text, no block formatting (span, a, strong)
inline-block: Flows with text but respects width/height/padding
flex:    One-dimensional layout — row OR column (most common for UI)
grid:    Two-dimensional layout — rows AND columns simultaneously
none:    Element removed from layout and not visible

Figma parallel:
  Flex row ≈ Figma Auto Layout (horizontal)
  Flex column ≈ Figma Auto Layout (vertical)
  Grid ≈ Figma Auto Layout (wrap) or Grid layout
```

### CSS Units for Designers

```
px:   Absolute pixels — use for borders, shadows, small fixed values
rem:  Relative to root font-size (usually 16px) — use for font sizes, spacing
em:   Relative to parent font-size — use sparingly (compounds in nesting)
%:    Percentage of parent — use for fluid widths, responsive layouts
vw:   Viewport width percentage (100vw = full viewport width)
vh:   Viewport height percentage (100vh = full viewport height)
dvh:  Dynamic viewport height (accounts for mobile browser chrome) — prefer over vh

Design implication: When specifying font sizes and spacing to engineers,
  use rem values, not px. This ensures user preferences for larger text are respected.
  16px = 1rem, 24px = 1.5rem, 32px = 2rem.
```

### CSS Specificity

```
When multiple CSS rules apply to the same element, specificity determines which wins:
  !important       Wins over everything (avoid — hard to override later)
  Inline style     Very high (don't use in components)
  ID selector      High (#header)
  Class selector   Medium (.button)
  Element selector Low (button, div)

Design implication:
  If an engineer says "I can't override that style," specificity is usually why.
  Prefer class-based styling (design system tokens as classes).
  Never design assuming !important will be available.
```

---

## 2. Responsive CSS

**Purpose:** Understand how layouts adapt to different screen sizes, so designs are rooted in how the web actually scales.

**When to use:** Designing responsive layouts; reviewing responsive implementations; writing breakpoint specifications.

### Media Queries

```css
/* Mobile-first: default styles apply to small screens */
.card { padding: 16px; }

/* Tablet (768px and up) */
@media (min-width: 768px) {
  .card { padding: 24px; }
}

/* Desktop (1024px and up) */
@media (min-width: 1024px) {
  .card { padding: 32px; }
}

/* Design implication:
   Designing mobile-first means: default = small screen.
   Add enhancements at larger sizes — don't subtract at smaller sizes.
   This matches how engineers write code. */
```

### Flexbox — The Alignment System

```css
/* One-dimensional layout — row or column */
.container {
  display: flex;
  flex-direction: row;          /* row (default) | column */
  justify-content: space-between; /* main axis alignment */
  align-items: center;          /* cross axis alignment */
  gap: 16px;                    /* space between children */
  flex-wrap: wrap;              /* items wrap to next line */
}

/* Figma Auto Layout = CSS Flexbox */
justify-content:
  flex-start  = Figma: "Pack items left / top"
  flex-end    = Figma: "Pack items right / bottom"
  center      = Figma: "Center"
  space-between = Figma: "Space between"

align-items:
  flex-start = Figma: "Start"
  center     = Figma: "Center"
  flex-end   = Figma: "End"
  stretch    = Figma: "Stretch"
```

### CSS Grid

```css
/* Two-dimensional layout — rows AND columns */
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);  /* 3 equal columns */
  gap: 16px;
}

/* Responsive grid without media queries */
.auto-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  /* Creates as many 250px+ columns as fit; stretches to fill */
}

/* Named grid areas */
.layout {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 250px 1fr;
}
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }

/* Design implication:
   CSS Grid is ideal for the outer page layout (header/sidebar/main).
   Flexbox is ideal for component-level layout (button contents, card items).
   Most real layouts use both. */
```

### Container Queries (Modern)

```css
/* Style based on parent container width, not viewport width */
/* Enables truly responsive components */
.card-container { container-type: inline-size; }

@container (min-width: 400px) {
  .card { flex-direction: row; } /* horizontal layout when card is wide */
}

@container (max-width: 399px) {
  .card { flex-direction: column; } /* vertical layout when card is narrow */
}

/* Design implication:
   Container queries solve the reusable component problem:
   the same card component can be wide in a wide container and narrow in a sidebar.
   This matches how designers think about responsive components. */
```

### Fluid Typography

```css
/* Font size scales smoothly between viewport sizes */
/* clamp(minimum, preferred, maximum) */
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
  /* Min: 32px, Max: 64px, scales with viewport between */
}

body {
  font-size: clamp(0.875rem, 1vw + 0.5rem, 1rem);
  /* Fluid body text between 14px and 16px */
}
```

---

## 3. CSS Animations

**Purpose:** Understand how CSS animations work technically — so you can specify animations accurately, understand what's feasible, and debug implementation issues.

**When to use:** Writing animation specs; reviewing implemented animations; understanding performance constraints.

### Transitions

```css
/* Simple property change over time — triggered by state change */
.button {
  background-color: #1a1a1a;
  transform: scale(1);
  transition: background-color 150ms ease-out,
              transform 100ms ease-out;
}
.button:hover {
  background-color: #2a2a2a;
  transform: scale(1.02);
}

/* Transition shorthand: property duration easing delay */
transition: all 200ms ease-out;  /* apply to all changed properties */
transition: transform 200ms ease-out, opacity 200ms ease-out; /* specific */

/* Design implication: transition is for state changes.
   The browser handles the interpolation — just define start and end states. */
```

### Keyframe Animations

```css
/* Explicit control over intermediate states */
@keyframes slide-in {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Multi-step keyframes */
@keyframes pulse {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.08); }
  100% { transform: scale(1); }
}

/* Applying the animation */
.element {
  animation: slide-in 300ms ease-out forwards;
  /* name  duration  easing  fill-mode */
}

.indicator {
  animation: pulse 2s ease-in-out infinite;
  /* infinite = loops; forwards = stays at end state after completing */
}

/* fill-mode:
   forwards: stay at final keyframe after animation ends
   backwards: apply initial keyframe before animation starts (during delay)
   both: both forwards and backwards */
```

### CSS Easing Functions

```css
/* Keyword curves */
ease-in:     cubic-bezier(0.4, 0, 1, 1)    /* slow start, fast end */
ease-out:    cubic-bezier(0, 0, 0.2, 1)    /* fast start, slow end */
ease-in-out: cubic-bezier(0.4, 0, 0.2, 1)  /* slow both ends */
linear:      cubic-bezier(0, 0, 1, 1)       /* constant speed */

/* Custom curves */
transition: transform 300ms cubic-bezier(0.34, 1.56, 0.64, 1); /* spring-like */

/* CSS spring (new, limited support): */
transition: transform 300ms linear(0, 0.009, 0.035 2.1%, 0.141...);
/* Use tools like linear() generator to create spring curves */
```

### Performance-Safe Properties

```css
/* GPU-accelerated — 60fps safe */
transform: translate(), rotate(), scale()
opacity

/* These cause layout recalculation — avoid animating */
width, height, top, left, margin, padding, font-size

/* Force GPU layer for an element (use sparingly) */
.animated { will-change: transform, opacity; }
/* Remove after animation to free GPU memory */
```

---

## 4. JavaScript Basics

**Purpose:** Understand enough JavaScript to communicate precisely with engineers, understand interaction possibilities, and read basic component code.

**When to use:** Reviewing implementations; speccing interactions; understanding what's feasible; reading Framer or React component code.

### Variables and Data Types

```javascript
const name = "Nexus";        // string — text
const count = 42;            // number
const isActive = true;       // boolean — true/false
const items = ["BTC", "ETH"]; // array — list of values
const user = {               // object — key/value pairs
  name: "Alex",
  balance: 1234.56,
};

// Accessing object properties:
user.name          // "Alex"
user.balance       // 1234.56
items[0]           // "BTC" (arrays are 0-indexed)
```

### Functions

```javascript
// Function that returns a formatted value
function formatPrice(value) {
  return "$" + value.toFixed(2);
}
formatPrice(1234.56); // "$1234.56"

// Arrow function (modern, compact syntax)
const formatPrice = (value) => "$" + value.toFixed(2);

// Why designers care:
// Functions like formatPrice() define how data is displayed.
// Knowing they exist helps you spec: "Show value as USD with 2 decimal places"
// rather than expecting the engineer to guess the format.
```

### Conditional Logic

```javascript
// if/else — show different UI based on condition
if (portfolio.change > 0) {
  showGreenArrow();
} else if (portfolio.change < 0) {
  showRedArrow();
} else {
  showNeutralIcon();
}

// Ternary (compact if/else)
const color = portfolio.change >= 0 ? "green" : "red";

// Why designers care:
// State design (empty/loading/error/success/etc.) maps directly to conditionals.
// When you design a component with 4 states, the engineer writes 4 conditions.
// Design all states explicitly — the engineer implements exactly what you specify.
```

### Events

```javascript
// Events are what trigger interactions
button.addEventListener("click", handleClick);
input.addEventListener("change", handleInputChange);
window.addEventListener("scroll", handleScroll);
document.addEventListener("keydown", handleKeyPress);

// Common events:
// click / tap: user taps/clicks
// hover: mouseenter / mouseleave
// scroll: user scrolls
// change: input value changes
// submit: form is submitted
// load: page or resource has loaded
// resize: viewport resizes

// Why designers care:
// Every interaction in a prototype connects to an event.
// "On tap" = click event. "On scroll past 50%" = scroll event.
// Understanding events helps you spec interactions unambiguously.
```

### Async Operations

```javascript
// Fetching data takes time — JavaScript is asynchronous
async function loadPortfolio() {
  try {
    const response = await fetch("/api/portfolio");
    const data = await response.json();
    displayPortfolio(data);
  } catch (error) {
    showErrorState(error);
  }
}

// Why designers care:
// Every network request creates a loading state.
// If the engineer makes an API call, there WILL be a delay.
// Always design: loading state + success state + error state.
// "Instant" data is mock data — real data has latency.
```

---

## 5. React/Vue/Angular Awareness

**Purpose:** Understand component-based architecture so design decisions map naturally to implementation — and designs are structured in ways engineers can actually build efficiently.

**When to use:** Designing for React/Vue/Angular codebases; creating component specs; working with Storybook; discussing implementation with engineers.

### Component Mental Model

```
In component-based frameworks:
  - UI is built from reusable components (like Figma components)
  - Each component has: props (inputs), state (internal memory), and rendered output
  - Components nest inside each other (like Figma frames and components)

Design → Code mapping:
  Figma main component → React component definition
  Figma instance → React component usage (<Button />)
  Figma component property → React prop (variant="primary")
  Figma variant → prop value ("primary", "ghost", "outline")
  Figma override → prop override (<Button label="Save" />)

When you design a component system that mirrors this structure,
engineers can map your designs to code almost 1:1.
```

### Props (Component Inputs)

```jsx
// A Button component accepts props that control its behavior
<Button
  variant="primary"
  label="Connect exchange"
  onPress={handleConnect}
  disabled={isLoading}
  loading={isLoading}
/>

// Props tell the component what to look like and what to do.
// Designers control these through component properties in Figma.

// Design implication:
// Every Figma component property should have a matching code prop.
// If you create a "size" property in Figma, the engineer creates a "size" prop.
// Name them identically — "variant", not "style" or "type" (inconsistent naming = confusion).
```

### State (Component Memory)

```jsx
// State is a value the component remembers across renders
const [isExpanded, setIsExpanded] = useState(false);
const [searchQuery, setSearchQuery] = useState("");
const [isLoading, setIsLoading] = useState(true);

// State changes trigger re-render (visual update).
// This is what makes interactions work.

// Design implication:
// Every interactive component has state.
// A toggle: isOn (true/false). A search: query (string). A list: items (array).
// When designing interactive components, list their states explicitly in specs.
```

### Component Lifecycle

```
Mount:   Component appears in UI (useEffect with [] = run once on appear)
Update:  Props or state changed (component re-renders)
Unmount: Component removed from UI (cleanup runs)

Design implication:
  "On load" animation = fires on mount.
  "When data changes" animation = fires on update.
  "When modal closes" = fires on unmount.
  Specify WHEN animations trigger using these lifecycle terms.
```

### Design System → Component Library

```
Figma design system → React component library → Storybook documentation

Ideal alignment:
  Figma: Button / Primary / Default
  React: <Button variant="primary" state="default" />
  Storybook: Button > Stories > Primary

When Figma component names match code component names,
  handoff is frictionless. Mismatched names = confusion and rework.

Practical rule: Use the same naming convention in Figma that engineers
  use for code. If the code uses "variant", don't call it "type" in Figma.
```

---

## 6. Design-to-Code Handoff

**Purpose:** Prepare and communicate designs so engineers have everything they need to implement correctly — without requiring constant back-and-forth.

**When to use:** Before any implementation begins; after completing a design ready for development.

### What a Complete Handoff Contains

```
1. Design files (Figma Dev Mode or Zeplin/Storybook link)
   - All screens with all states (default, hover, loading, error, empty)
   - All responsive breakpoints
   - All animations and transitions specified

2. Component specifications
   - Exact dimensions (or responsive rules if fluid)
   - Spacing (use token names, not raw pixel values)
   - Typography (use token names: TypeScale.body.lg, not "16px Inter")
   - Colors (use token names: Colors.accent, not "#C8E847")
   - Border radius, shadows (token names)

3. Interaction notes
   - Animation timing (duration, easing)
   - State transitions (what triggers what)
   - Scroll behavior
   - Gesture interactions

4. Asset exports
   - Icons as SVG
   - Images at 1x, 2x, 3x (or single SVG)
   - App icons at all required sizes
   - Lottie JSON if applicable

5. Edge cases
   - Long strings (text overflow behavior)
   - Empty states
   - Error states
   - Minimum/maximum content dimensions
```

### Annotation Best Practices

```
Annotate intention, not appearance.

❌ "This text is 16px, #666666, Inter Regular"
   (The engineer can see this in the inspect panel)

✅ "Use TypeScale.body.lg + Colors.gray — secondary supporting text"
   (Why this choice + the token to use)

❌ "This animation is 300ms"
   (Not enough detail)

✅ "Card enters with: opacity 0→1 + translateY 20px→0, 300ms ease-out"
   (Exactly implementable)

✅ "Only animate on first mount — not on re-renders or data refresh"
   (Prevents over-animation)

Annotate:
  - Responsive behavior (what changes at which breakpoints)
  - Touch target minimum (if unclear from design)
  - Z-index stacking order (for overlapping elements)
  - Scroll behavior (what scrolls, what's sticky)
  - Loading order (which elements appear first if staggered)
```

### Handoff Tools

| Tool | Best for |
|------|----------|
| Figma Dev Mode | Native Figma handoff — CSS, iOS, Android specs + asset export |
| Zeplin | Dedicated handoff with additional annotation features |
| Storybook | Component-level documentation with live code |
| Supernova | Design system tokens to code |
| Tokens Studio | Design token export (JSON/YAML) for engineers |

### Spec Format for Animations

```
For each animated element, provide:

  Element: [component name]
  Trigger: [user action or lifecycle event]
  Enter:
    Properties: opacity 0→1, transform translateY(20px)→translateY(0)
    Duration: 300ms
    Easing: ease-out (cubic-bezier(0, 0, 0.2, 1))
    Delay: 0ms (or Nth item × 50ms for staggered lists)
  Exit:
    Properties: opacity 1→0
    Duration: 200ms
    Easing: ease-in
  Notes: Only plays on mount — not on data refresh
```

### Outputs
- Figma file in Dev Mode with all states
- Annotation layer with interaction and responsive notes
- Asset export at all required sizes
- Animation spec document

---

## 7. Browser DevTools

**Purpose:** Inspect, debug, and test designs directly in the browser — identifying implementation deviations, testing responsive behavior, and verifying visual quality.

**When to use:** Design QA sessions; reviewing implementations; debugging visual discrepancies; testing responsive behavior.

### Opening DevTools

```
Chrome / Edge:
  Right-click any element → Inspect
  Mac: Cmd+Option+I  |  Windows: F12 or Ctrl+Shift+I

Firefox:
  Right-click → Inspect Element
  Mac: Cmd+Option+I  |  Windows: F12

Safari (Mac):
  Enable in Preferences → Advanced → Show Develop menu
  Right-click → Inspect Element
```

### Elements Panel — Inspect the Design

```
Hover over HTML elements → highlights in viewport.
Click element → shows its CSS on the right (Styles panel).

What to check:
  Width/height: matches the design?
  Padding/margin: correct spacing tokens?
  Font: correct family, size, weight?
  Color: correct hex or CSS variable?
  Border radius: correct value?
  Box shadow: correct values?

Edit live:
  Click any CSS value and type to change it — previews instantly.
  No save — refreshing resets. Great for trying fixes before telling engineers.

Find the token:
  If a CSS custom property (--color-accent) is used: good, tokens are working.
  If a raw hex is used: no token — flag to engineer.
```

### Toggle Device Mode (Responsive Testing)

```
Chrome: Click phone/tablet icon (top-left of DevTools) or Cmd+Shift+M
  → Select from device presets (iPhone 14, iPad, etc.)
  → Or set custom viewport dimensions
  → Throttle network speed to simulate slow connections

Test at key breakpoints:
  375px: iPhone SE / most narrow mobile
  390px: iPhone 14 Pro
  768px: iPad portrait / tablet
  1024px: iPad landscape / small laptop
  1440px: Standard desktop

Check for:
  Layout breaking or overflowing
  Text too large or too small
  Touch targets too small (< 44px)
  Images not scaling correctly
  Fixed elements covering content
```

### Network Panel — Test Loading States

```
Simulate slow connections:
  Network tab → Throttling dropdown → Slow 3G or Custom (e.g., 500ms latency)

Verify:
  Loading skeleton appears before content
  Loading spinner displays within 50–100ms of action
  Content transitions in smoothly on arrival
  Error state appears when request fails

Force request failure:
  Network tab → Right-click a request → Block request URL
  Reload → Loading state should transition to error state
```

### Performance Panel — Check Animation

```
Click record → interact with animation → stop recording.

Look for:
  Green bar = 60fps rendering ✅
  Red/orange = dropped frames, long tasks ❌
  Purple "Layout" = layout thrash (avoid animating layout properties)

Analyze:
  Long JS tasks blocking animation: move work off main thread
  Layout thrashing: only animate transform/opacity
  Paint storms: reduce repaints with will-change or containment
```

### Console — Spot Errors

```
Open console: Cmd+Option+J (Chrome)

Red errors: JavaScript exceptions — notify engineer, likely affects functionality
Yellow warnings: Deprecations, non-critical issues
Console.log output: Engineers often log data to debug — can see mock data structure

Design-relevant errors:
  "Cannot find font 'X'": Font not loading — typographic rendering is wrong
  Image 404 errors: Missing assets — visual appears broken
  CORS errors: API calls failing — may affect loading/error states
```

### Useful DevTools Shortcuts

| Action | Mac | Windows |
|--------|-----|---------|
| Inspect element | Cmd+Shift+C | Ctrl+Shift+C |
| Toggle DevTools | Cmd+Option+I | F12 |
| Toggle device mode | Cmd+Shift+M | Ctrl+Shift+M |
| Open console | Cmd+Option+J | Ctrl+Shift+J |
| Full page screenshot | Cmd+Shift+P → "screenshot" | Ctrl+Shift+P → "screenshot" |
| Force element state | Right-click element → Force state | Same |

### Outputs
- List of implementation deviations (with DevTools evidence)
- Responsive test results at all breakpoints
- Animation performance check (recorded performance trace)
- Annotated screenshots comparing design vs. implementation
