# Wireframing & Prototyping Methods

## Table of Contents
1. [Low-Fidelity Wireframing](#1-low-fidelity-wireframing)
2. [High-Fidelity Wireframing](#2-high-fidelity-wireframing)
3. [Interactive Prototyping](#3-interactive-prototyping)
4. [Rapid Prototyping](#4-rapid-prototyping)
5. [Paper Prototyping](#5-paper-prototyping)
6. [Code-Based Prototyping](#6-code-based-prototyping)

---

## 1. Low-Fidelity Wireframing

**Purpose:** Quickly explore and communicate layout structure, content hierarchy, and navigation without investing time in visual design details.

**When to use:** Early in design, when exploring multiple layout options, when alignment on structure is needed before visual design begins.

### Fidelity Rules

Low-fi wireframes use:
- **Boxes** for images and media (labeled with content type)
- **Lorem ipsum or real labels** for text (real labels preferred — layout breaks with real content earlier)
- **Grayscale only** — no colors, no typography decisions
- **No icons** — use labeled boxes or simple shapes
- **Approximate sizing** — layout proportions matter; pixel perfection doesn't

### Content Priority Mapping

Before wireframing a screen, rank every content element:

```
P1 — Primary content     Must be immediately visible above the fold
P2 — Secondary content   Important but can be below fold or secondary position
P3 — Tertiary content    Supplementary; can be collapsed or de-emphasized
P4 — Navigation/chrome   Persistent UI, shouldn't compete with content
```

Map layout to priority: P1 elements get the most visual weight and prominent position.

### Layout Exploration (6-Up Method)

Before committing to one layout:
1. Sketch 6 different layout variations in 10 minutes (1–2 min each)
2. Share all 6 with the team — discuss trade-offs
3. Combine the strongest elements from 2–3 into a refined direction
4. Only then invest in a detailed wireframe

### Wireframe Annotation

Add annotations to explain what the wireframe can't show:
```
[A] — This list auto-scrolls horizontally on mobile
[B] — "See more" expands inline, doesn't navigate
[C] — This section only appears if user has connected an account
[D] — Button is disabled until all required fields are complete
```

### Outputs
- 1–3 layout explorations per screen
- Priority-annotated wireframe of chosen direction
- Behavior annotations for non-obvious interactions

---

## 2. High-Fidelity Wireframing

**Purpose:** Create detailed, accurate layout documents that serve as the blueprint for final visual design and developer handoff.

**When to use:** After low-fi direction is approved, before visual design, or as the final deliverable when visual design follows a design system.

### Hi-Fi Wireframe Components

High-fidelity wireframes include:
- **Real content** — actual labels, real (or realistic) data, actual copy
- **Accurate spacing** — real padding, margins, and grid adherence
- **Component states** — all variants of interactive elements specified
- **Responsive behavior notes** — how layout changes at breakpoints
- **Real typography** — typeface and hierarchy specified (size/weight, not color)
- **Interaction annotations** — notes on every non-obvious behavior

### Spacing and Grid Documentation

```
Grid spec:
  Columns: 12 (desktop), 8 (tablet), 4 (mobile)
  Gutter: 24px (desktop), 16px (tablet/mobile)
  Margin: 80px (desktop), 40px (tablet), 20px (mobile)

Component spacing:
  Card internal padding: 16px
  Section gap: 32px
  Row gap: 4px
  Screen horizontal padding: 20px
```

### Component Inventory

List every unique component appearing in the wireframe:
```
New components needed:
  - Asset list row (icon + name + value + sparkline)
  - Exchange allocation bar
  - Period selector (tab pill)

Existing components being reused:
  - Card (default variant)
  - Badge (change variant)
  - Button (primary variant)
```

### Handoff Annotation Standard

Each annotated element should specify:
- **Dimensions** (width, height, min/max)
- **Spacing** (padding, margin, gap)
- **Behavior** (interaction, animation, states)
- **Content rules** (max characters, truncation behavior, empty state)
- **Conditions** (when this element appears/hides)

### Outputs
- Full-screen wireframes with real content
- Component inventory (new vs. reused)
- Spacing and grid specification
- Annotated behavior notes
- Responsive variation wireframes (if applicable)

---

## 3. Interactive Prototyping

**Purpose:** Build a clickable prototype that simulates real navigation and transitions so users can interact with a design without it being built.

**When to use:** Usability testing, stakeholder demos, validating navigation logic, testing transitions and animations.

### Prototype Fidelity Levels

| Fidelity | Use For | Tool |
|----------|---------|------|
| Click-through (no animation) | Navigation validation, stakeholder alignment | Figma |
| Animated transitions | Testing navigation feel, animation decisions | Figma, Framer |
| Micro-interaction detail | Testing interaction polish | ProtoPie, Framer |
| Data-driven prototype | Testing with real content variation | Framer, ProtoPie |

### Prototype Scope Decision

Don't prototype everything — scope to the user task being tested:

```
Test: "Can users find and set up a new exchange connection?"

Prototype scope:
  ✅ Exchanges tab (all states)
  ✅ Add Exchange flow (3 screens: choose → credentials → success)
  ✅ Navigation between tabs
  ❌ Dashboard content (not needed for this task)
  ❌ Settings (not tested)
  ❌ Asset detail (not tested)
```

### Interaction Design in Figma

**Connection types:**
- `On click` → navigate to frame
- `On hover` → show overlay (tooltip, dropdown)
- `While pressing` → show pressed state
- `After delay` → auto-advance (loading states, success screens)
- `On drag` → swipe interactions

**Overlay patterns:**
- Dropdown menus: overlay positioned relative to trigger, close on outside click
- Modals: full-screen overlay with dimmed background
- Tooltips: hover-triggered, auto-dismiss

**Transition types:**
- Push (left/right): peer-level navigation
- Slide in from bottom: sheet/drawer patterns
- Dissolve: tab switching, modal dismiss
- Smart animate: micro-interaction detail (Figma only)

### Prototype Testing Setup

Before a test session:
- [ ] Start frame set to correct entry point
- [ ] All clickable areas have connections
- [ ] Dead-end screens have a back button (or back gesture)
- [ ] Prototype runs on the actual target device (not a desktop preview)
- [ ] Back button behavior tested on device
- [ ] Prototype link shared in advance if remote testing

### Outputs
- Shareable prototype link
- Prototype scope document (what's included, what isn't)
- Notes on known limitations ("In the real product, this would also...")

---

## 4. Rapid Prototyping

**Purpose:** Build a low-investment version of an idea to test its core concept before committing time to polished design.

**When to use:** Exploring multiple concepts, early user feedback, when time is short and learning matters more than fidelity.

### Rapid Prototyping Mindset

The goal is the **minimum viable prototype** — just enough to test the idea:
- Build only what's needed to answer your specific question
- Use shortcuts relentlessly: duplicate and edit vs. build from scratch
- Accept imperfection — if it answers the question, it's done
- Time-box: set a timer (2h, 4h, or 1 day max)

### Rapid Prototyping Techniques

**Component stacking (Figma):**
1. Start from an existing screen in the project
2. Swap or edit only the components you're testing
3. Connect screens with simple click-to-navigate links
4. Done in < 2 hours

**Wizard of Oz:**
- Facilitator manually simulates what a system would do automatically
- User types a search → facilitator shows a pre-prepared result screen
- Tests user mental model without building the algorithm

**Storyboard prototype:**
1. Draw 6–8 key frames as thumbnail sketches
2. Photograph and stitch into a simple PDF or Keynote
3. Walkthrough with a user explaining transitions verbally
4. Tests narrative and flow without any screen design

**Keyframe prototype:**
- Design only the 3–5 most critical screens in the flow
- Leave "in-between" screens as white/grey placeholders
- Test with a task that traverses only the designed keyframes

### Questions Rapid Prototypes Can Answer

- "Does this navigation pattern make sense to users?"
- "Do users understand the value proposition of this feature?"
- "Which of these two layouts is clearer?"
- "Does the overall flow feel right?"

Questions they CANNOT answer reliably:
- Specific copy effectiveness (use real copy before testing)
- Visual design preferences (use hi-fi for this)
- Performance feel (use code prototype for this)

### Outputs
- Testable prototype (any fidelity) scoped to the core question
- 2–3 specific questions the prototype is designed to answer
- Learning summary after testing

---

## 5. Paper Prototyping

**Purpose:** Create physical, handmade representations of UI to test concepts at the lowest possible cost before any digital design work.

**When to use:** Very early discovery, when digital tools would slow the team down, when co-creating with non-designers, for exploring radical alternatives.

### Materials Needed

- Paper (letter/A4), index cards
- Scissors, tape, markers (Sharpie for UI elements)
- Sticky notes for overlay elements (modals, dropdowns)
- Paper clips to hold component states together

### Constructing a Paper Prototype

```
1. Draw each screen on a separate sheet
   - Rough proportions of the actual device
   - Clear labels on all elements
   - Arrows showing expected navigation

2. Create interactive overlays
   - Modals on separate smaller sheets
   - Dropdowns on sticky notes
   - Keyboard as a separate paper element

3. Simulate interaction
   - Facilitator swaps sheets on user action
   - "Computer" role: swap to next screen when user taps
   - Observer role: note what user does and says
```

### Paper Prototype Testing Protocol

```
Setup:
  Device frame drawn on paper (phone/tablet outline)
  Each screen as a separate card slid into the frame

Roles:
  Facilitator — gives tasks, asks questions
  "Human computer" — silently swaps paper components
  Observer — takes notes on user behavior

Task format:
  "Without me telling you how, try to [complete task]"
  "What would you tap next?"
  "What do you expect to happen?"
```

### What Paper Prototyping Is Good For

- Testing navigation logic and information architecture
- Revealing whether users understand what elements are interactive
- Exploring radically different layouts in 30 minutes
- Including non-designers (stakeholders, developers) in design exploration
- Testing with users before any screen has been designed

### Outputs
- Physical prototype (photograph for documentation)
- Observed user behaviors and quotes
- Navigation issues discovered
- Concepts eliminated cheaply before digital investment

---

## 6. Code-Based Prototyping

**Purpose:** Build a high-fidelity prototype using real code to test realistic interactions, performance, and behavior that visual tools can't simulate.

**When to use:** Testing complex animations, scroll behavior, real data rendering, form validation logic, or when designers need to hand off to engineering with confidence.

### When to Choose Code Over Visual Tools

| Situation | Best Tool |
|-----------|-----------|
| Navigation and flow testing | Figma |
| Animation and transition feel | Framer / ProtoPie |
| Scroll behavior, momentum | Code (HTML/CSS/JS) |
| Form validation, real logic | Code |
| Real data rendering, variable content | Framer (data) or Code |
| Performance testing | Code only |
| Complex gestures (swipe, drag) | ProtoPie or Code |

### Code Prototype Stacks by Fidelity

**HTML/CSS/JS (fastest):**
```html
<!-- Quick prototype shell -->
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    /* Mobile-first, no framework needed */
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: system-ui; max-width: 390px; margin: 0 auto; }
  </style>
</head>
<body>
  <!-- Screen content here -->
  <script>
    // Minimal interaction logic
    document.querySelectorAll('[data-nav]').forEach(el => {
      el.addEventListener('click', () => {
        document.querySelector('.screen.active').classList.remove('active');
        document.querySelector(el.dataset.nav).classList.add('active');
      });
    });
  </script>
</body>
</html>
```

**React (when component reuse matters):**
- Use Vite for fast setup: `npm create vite@latest prototype -- --template react`
- Mock data in a local JSON file — no API calls in prototypes
- Use CSS modules or plain CSS — no need for full design system
- Deploy to Vercel or Netlify for sharing with stakeholders

### Code Prototype Rules

- **No real APIs** — hardcode or mock all data
- **No error handling** — prototypes don't need defensive code
- **No tests** — prototype code is throwaway
- **Ship fast** — working prototype in hours, not days
- **Label clearly** — "PROTOTYPE — Not production code" in README

### Outputs
- Running prototype accessible via URL
- List of interactions that work vs. are hardcoded/simulated
- Notes on what the real implementation would need to handle that the prototype doesn't
