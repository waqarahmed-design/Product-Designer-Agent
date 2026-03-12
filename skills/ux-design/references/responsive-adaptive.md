# Responsive & Adaptive Design Methods

## Table of Contents
1. [Mobile-First Design](#1-mobile-first-design)
2. [Breakpoint Strategy](#2-breakpoint-strategy)
3. [Touch Target Sizing](#3-touch-target-sizing)
4. [Responsive Layout Patterns](#4-responsive-layout-patterns)
5. [Platform-Specific Patterns](#5-platform-specific-patterns)
6. [Cross-Device Continuity](#6-cross-device-continuity)

---

## 1. Mobile-First Design

**Purpose:** Start design from the constraints of the smallest screen, then progressively enhance for larger screens — producing leaner, more focused products that work everywhere.

**When to use:** Any product with mobile users (which is virtually every product). Especially critical when >50% of traffic is mobile.

### Why Mobile-First

- **Forces prioritization** — small screens can't fit everything; you must decide what matters
- **Better performance** — mobile-first CSS is lighter; desktop enhancement adds less than mobile subtraction
- **Real constraint design** — designing for desktop first and "squishing" for mobile produces bad mobile UX

### Mobile-First Design Process

```
1. Design mobile (375px / 390px) first
   - What is the ONE primary action on this screen?
   - What information is essential vs. supplementary?
   - What can move below the fold?

2. Identify enhancement opportunities for tablet (768px)
   - What secondary content can appear alongside primary?
   - What navigation can expand from hamburger to visible?

3. Fully enhance for desktop (1280px+)
   - What can move into persistent sidebars?
   - What tables and data grids now have room to breathe?
   - What hover states become available?
```

### Content Priority on Mobile

Every screen has one primary purpose. On mobile, structure content accordingly:

```
Screen: Portfolio Dashboard (mobile)

Above fold (visible without scroll):
  - Total portfolio value (hero — biggest element)
  - 24h change indicator

First scroll:
  - 7-day sparkline

Second scroll:
  - Asset list (top 4–5 visible)

Below the fold / expandable:
  - Exchange breakdown
  - Detailed metrics
```

### Mobile-First CSS Pattern

```css
/* Mobile base styles — no media query needed */
.container {
  padding: 0 20px;
  max-width: 100%;
}

.grid {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

/* Tablet enhancement */
@media (min-width: 768px) {
  .grid {
    flex-direction: row;
    flex-wrap: wrap;
  }
  .grid > * { flex: 1 1 calc(50% - 8px); }
}

/* Desktop enhancement */
@media (min-width: 1280px) {
  .container {
    padding: 0 80px;
    max-width: 1440px;
    margin: 0 auto;
  }
  .grid > * { flex: 1 1 calc(33.33% - 11px); }
}
```

### Outputs
- Mobile-first wireframes (mobile designed before desktop)
- Content priority map per screen
- Mobile-to-desktop enhancement notes

---

## 2. Breakpoint Strategy

**Purpose:** Define the screen widths at which layout changes occur, and specify what changes at each breakpoint.

**When to use:** Before building any responsive UI; during design system definition.

### Standard Breakpoint System

```
xs:  < 480px   — Small phones (older, narrow)
sm:  480–767px — Phones (most common mobile)
md:  768–1023px — Tablets, large phones landscape
lg:  1024–1279px — Small laptops, tablets landscape
xl:  1280–1535px — Desktop
2xl: 1536px+   — Wide desktop, external monitors
```

Design breakpoints, not device breakpoints — let the content tell you where to break.

### What Changes at Each Breakpoint

Document explicitly what changes at each breakpoint per layout:

```
Component: Navigation
  < 768px (mobile)
    - Hamburger menu icon visible
    - Nav links hidden in off-canvas drawer
    - Logo centered or left

  768–1023px (tablet)
    - Hamburger hidden
    - Top 3–4 nav items visible
    - "More" dropdown for overflow items

  1024px+ (desktop)
    - All nav items visible
    - Horizontal layout
    - Optional: sticky on scroll

Component: Data Table
  < 768px
    - Card layout (each row becomes a card)
    - or: Horizontal scroll within a fixed container
    - Priority columns only (hide less important columns)

  768px+
    - Full table layout
    - All columns visible
    - Sortable columns
```

### Content-First Breakpoints

Instead of designing to standard breakpoints, find where your specific content breaks:

1. Design the mobile layout
2. Resize the browser slowly wider
3. Mark the width where the layout starts to look awkward or waste space
4. That's your breakpoint

This produces fewer, more meaningful breakpoints specific to your content.

### Fluid vs. Stepped Layout

| Approach | How it works | Best for |
|----------|-------------|---------|
| **Stepped** | Layout snaps at defined breakpoints | Complex, intentional layout changes |
| **Fluid** | Elements scale proportionally between breakpoints | Simpler content, text-heavy pages |
| **Hybrid** | Fluid within ranges, stepped at breakpoints | Most modern products |

### Outputs
- Breakpoint scale definition
- Per-component breakpoint behavior documentation
- Layout diagrams at each major breakpoint

---

## 3. Touch Target Sizing

**Purpose:** Ensure interactive elements are large enough for accurate finger taps across all users — including older users, people with motor impairments, and users in motion.

**When to use:** Designing any mobile or touch interface.

### Minimum Target Size Standards

| Platform | Standard | Guideline source |
|----------|----------|-----------------|
| iOS | 44×44pt | Apple HIG |
| Android | 48×48dp | Material Design |
| Web (WCAG 2.5.5) | 44×44px | WCAG AA |
| Web (WCAG 2.5.8, enhanced) | 24×24px min, 24px spacing | WCAG AAA |

**Recommended minimum:** 44×44px / 44×44pt on all platforms.

### Target Size vs. Visual Size

The tap target can be larger than the visible element:

```
Icon button (visual: 20×20px)
  ❌ Tap target = icon size (too small)
  ✅ Tap target = 44×44px via padding around icon

Row tap target
  ✅ Entire row height = 44px minimum
  ✅ Full row width tappable (not just text label)

Checkbox / radio
  ✅ Include label in tap target (tapping label toggles checkbox)
```

### CSS Implementation

```css
/* Icon button — visible icon is small, tap target is 44px */
.icon-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  /* Icon inside will be 20–24px; padding provides tap area */
}

/* Minimum row height */
.list-row {
  min-height: 44px;
  display: flex;
  align-items: center;
}

/* Checkbox with label as tap target */
.checkbox-label {
  display: flex;
  align-items: center;
  gap: 8px;
  min-height: 44px;
  cursor: pointer;
}
```

### Target Spacing

Adjacent targets need separation to prevent mis-taps:

```
Minimum spacing between adjacent targets:
  iOS: 8pt between tap zones
  Material: 8dp
  Web: targets or padding must not overlap

Bad (too close):
  [Button A][Button B]  ← mis-tap risk

Good:
  [Button A]  [Button B]  ← 8px+ gap
```

### Common Touch Target Failures

- Icon-only navigation without a containing tap area
- Small "×" close buttons (icon-only, no padding)
- Checkbox and radio inputs without extending target to label
- Closely spaced list items (row height < 44px)
- Stepper buttons (+ / −) smaller than 44px

### Outputs
- Touch target size spec for all interactive elements
- List of elements needing target size remediation
- Implementation notes for developers

---

## 4. Responsive Layout Patterns

**Purpose:** Use proven layout patterns that adapt gracefully across screen sizes using fluid grids, flexible images, and strategic reflow.

**When to use:** Designing any multi-column, card-based, or data-heavy layout.

### Core CSS Layout Tools

**CSS Grid — for two-dimensional layouts:**
```css
/* Auto-fitting card grid */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 16px;
}
/* Result: fills available space with as many 280px+ cards as fit */
```

**CSS Flexbox — for one-dimensional layouts:**
```css
/* Flexible row that wraps on small screens */
.flex-row {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
.flex-row > * { flex: 1 1 240px; } /* each item min 240px, grows to fill */
```

**CSS Container Queries — component-level responsiveness:**
```css
/* Component adapts to its container, not the viewport */
.card-container { container-type: inline-size; }

@container (min-width: 400px) {
  .card { flex-direction: row; } /* horizontal layout in wider containers */
}
```

### Responsive Layout Patterns

**Reflowing columns:**
```
Mobile:  [Card 1]
         [Card 2]
         [Card 3]

Desktop: [Card 1] [Card 2] [Card 3]
```

**Holy grail:**
```
Mobile:  [Header]
         [Content]
         [Sidebar]
         [Footer]

Desktop: [Header              ]
         [Sidebar] [Content   ]
         [Footer              ]
```

**Off-canvas navigation:**
```
Mobile:  [Content] (nav hidden, triggered by hamburger)
Tablet+: [Nav | Content] (nav always visible)
```

**Priority+ navigation:**
```
Narrow:  [Logo] [Item1] [Item2] [More▾]  ← overflow in "More"
Wide:    [Logo] [Item1] [Item2] [Item3] [Item4] [Item5]
```

**Card to table:**
```
Mobile:  Card per row (vertical scan)
Desktop: Table (horizontal comparison)
```

### Flexible Images

```css
/* Images never overflow their container */
img {
  max-width: 100%;
  height: auto;
}

/* Responsive image with aspect ratio lock */
.image-container {
  aspect-ratio: 16/9;
  overflow: hidden;
}
.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

### Outputs
- Layout pattern selection per screen
- Grid and column specification per breakpoint
- Responsive image treatment spec

---

## 5. Platform-Specific Patterns

**Purpose:** Follow the established conventions of each platform so the product feels native and familiar to users.

**When to use:** Building iOS apps, Android apps, web apps, or any cross-platform product.

### iOS Design Conventions (Apple HIG)

| Pattern | iOS Convention |
|---------|----------------|
| **Navigation** | Tab bar at bottom (5 items max); push navigation for drill-down |
| **Back navigation** | Back button top-left with parent screen title; swipe-from-left-edge |
| **Primary CTA** | Top-right of navigation bar (text button) for contextual actions |
| **Modals** | Card sheet from bottom (pageSheet); full-screen for immersive content |
| **Destructive actions** | Red color; confirm via action sheet (not modal dialog) |
| **Text inputs** | Labels above fields; keyboard avoidance built in |
| **Lists** | GroupedInsetListStyle with rounded-corner sections |
| **Icons** | SF Symbols preferred; 1.5–2px stroke weight |
| **Typography** | SF Pro; Dynamic Type for system font scaling |
| **Haptics** | Impact feedback on significant interactions; notification feedback on success/error |

### Android Design Conventions (Material Design 3)

| Pattern | Android Convention |
|---------|-------------------|
| **Navigation** | Navigation bar at bottom (3–5 items); Navigation drawer for many sections |
| **Back navigation** | System back button / gesture; predictive back (Android 13+) |
| **Primary CTA** | FAB (Floating Action Button) for primary screen action |
| **Modals** | Bottom sheet for contextual menus; Dialog for critical decisions |
| **Destructive actions** | Error color; confirmation dialog |
| **Text inputs** | Filled or outlined text fields; floating labels |
| **Components** | Material components (Cards, Chips, Snackbar, etc.) |
| **Icons** | Material Symbols (outlined/filled/rounded variants) |
| **Typography** | Roboto; Material Type Scale |
| **Motion** | Material motion (container transform, shared axis, fade through) |

### Web Conventions

| Pattern | Web Convention |
|---------|---------------|
| **Navigation** | Top nav bar (desktop); hamburger or bottom bar (mobile) |
| **Links** | Underlined or distinct color; visited state change |
| **Forms** | Labels above inputs; submit button at bottom; Enter submits |
| **Back** | Browser back button; breadcrumbs for deep hierarchy |
| **Hover states** | Required on desktop; not available on touch |
| **Right-click** | Context menus may be expected for power users |
| **Keyboard** | Full keyboard navigation required; shortcuts expected for power users |
| **Scroll** | Vertical scroll primary; horizontal scroll signals (gradient fade) |

### Cross-Platform Decisions

When building for multiple platforms:

| Decision | Recommendation |
|----------|---------------|
| Same interaction model? | Follow each platform's native patterns — users expect platform behavior |
| Same visual design? | Brand consistency OK; adapt spacing, typography, component shapes to each platform |
| Same navigation structure? | Yes — but rendered using platform-native navigation patterns |
| Same feature set? | Yes — but some features may be platform-exclusive (widgets, live activities) |

### Outputs
- Platform-specific interaction spec (navigation, modals, back behavior)
- Component mapping: design system component → platform native component
- List of platform-specific behaviors to implement

---

## 6. Cross-Device Continuity

**Purpose:** Design experiences that feel cohesive and connected when users switch between or use multiple devices.

**When to use:** Products where users access the same account on phone, tablet, and desktop.

### Continuity Dimensions

**State continuity** — user progress persists across devices:
- Scroll position, reading progress
- Form partial completion
- Onboarding step completed on one device
- Shopping cart, watchlist, saved items

**Context continuity** — user picks up where they left off:
- "Continue reading" on a different device
- Notification on phone opens relevant content on desktop
- Search history and recent items shared

**Preference continuity** — settings and customizations sync:
- Theme (dark/light mode)
- Notification preferences
- Display density, font size
- Language and locale

### Handoff Patterns

**Explicit handoff:**
```
"Continue on desktop →"  ← user deliberately switches
QR code to open same page on phone
"Send to device" feature
```

**Seamless handoff:**
```
Autosave + cloud sync → user opens app on any device and continues naturally
Push notification → tapping opens to exact context
```

**Recovery handoff:**
```
User was filling a form on mobile, loses connection
Opens desktop → "You have an incomplete [form name] from [time]. Continue?"
```

### Responsive vs. Adaptive: Which to Use

| Approach | How it works | When to use |
|----------|-------------|------------|
| **Responsive** | Same HTML/content, CSS changes layout | Most web products |
| **Adaptive** | Different layouts served per device class | When mobile and desktop experiences differ significantly |
| **Native per platform** | Separate codebases | When platform conventions matter most |
| **Hybrid** | Web core + native shell (RN, Flutter) | Cross-platform with native feel |

### Continuity Failure Points to Avoid

- Auth session doesn't persist (users must log in on every device)
- Settings changed on mobile don't sync to desktop
- In-progress actions not recoverable on different device
- Push notification links to wrong content on different device
- Different feature sets between platforms (creates confusion about product capabilities)

### Implementation Requirements

For state continuity, the backend must:
- Persist user state server-side (not just localStorage)
- Associate state with user account, not device
- Provide last-activity timestamp for "continue where you left off" UI
- Conflict resolution strategy for simultaneous edits on multiple devices

### Outputs
- Continuity requirements per user flow
- Sync spec (what state is synced, how often, conflict resolution)
- Cross-device handoff UI designs
- List of device-specific features that break continuity
