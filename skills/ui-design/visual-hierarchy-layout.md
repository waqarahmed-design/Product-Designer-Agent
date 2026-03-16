# Visual Hierarchy & Layout

## Table of Contents
1. [Typographic Hierarchy](#1-typographic-hierarchy)
2. [Spatial Hierarchy](#2-spatial-hierarchy)
3. [Visual Weight](#3-visual-weight)
4. [Emphasis Techniques](#4-emphasis-techniques)
5. [Scanning Patterns](#5-scanning-patterns)
6. [Grid Systems](#6-grid-systems)
7. [Alignment](#7-alignment)
8. [Spacing Systems](#8-spacing-systems)
9. [Balance](#9-balance)
10. [Negative Space](#10-negative-space)
11. [Containment](#11-containment)
12. [Gestalt Principles](#12-gestalt-principles)

---

## 1. Typographic Hierarchy

**Purpose:** Use type size, weight, color, and spacing to communicate the relative importance of information — so users know what to read first, second, and third.

**When to use:** Any screen with more than one level of text content.

### Hierarchy Levels

```
Level 1 — Display / Hero
  Largest size, highest weight (800–900)
  One per screen or section
  Example: Portfolio value, page title, onboarding headline

Level 2 — Section heading
  Large, bold (700–800)
  Groups a section of content
  Example: "ASSETS", "CONNECTED EXCHANGES"

Level 3 — Subsection / card title
  Medium size, semi-bold (600–700)
  Labels a specific block of content

Level 4 — Body copy
  Reading size (16px min on mobile), regular weight (400)
  Primary narrative or data content

Level 5 — Supporting text
  Smaller, muted color, regular/medium weight
  Labels, captions, timestamps, metadata

Level 6 — Micro / label
  Smallest (8–12px), often uppercase with letter-spacing
  Form field labels, badge text, stat labels
```

### Hierarchy Rules

- **Never more than 3 active hierarchy levels on one screen** — more creates visual noise
- **Size alone is not enough** — pair size with weight and color to reinforce hierarchy
- **Contrast over size** — a bold 16px text reads as more important than light 20px text
- **Consistent levels** — every instance of "section header" must look identical; inconsistency breaks hierarchy
- **Color carries hierarchy** — primary text `#F2F2F2`, secondary text `#666`, disabled text `#444`

### Common Hierarchy Failures

| Failure | Fix |
|---------|-----|
| Everything is the same size | Increase size spread; use at least 1.4× between levels |
| Headers and body are both bold | Reserve bold for headings; body at 400 weight |
| Important text is muted color | Primary content = highest-contrast color |
| Too many different sizes | Constrain to a defined type scale |

---

## 2. Spatial Hierarchy

**Purpose:** Use proximity, spacing, and grouping to communicate relationships between elements — things that belong together are placed closer together.

**When to use:** Any layout with multiple content groups.

### Law of Proximity (Gestalt)

Elements close together are perceived as related. Elements far apart are perceived as separate.

```
Bad (equal spacing — everything related to everything):
  Label
  Input

  Label
  Input

  Submit button

Good (grouped by relationship):
  Label        ← tight spacing: label belongs to its input
  Input

  ← gap: separation between field groups

  Label
  Input

  ← larger gap: section separation

  Submit button
```

### Spatial Hierarchy Scale

Use a consistent multiplier system:

```
Within a component:   4–8px   (tight — same element)
Between siblings:     12–16px (related — same group)
Between sections:     24–32px (separated — different groups)
Between major regions: 40–64px (distinct — independent sections)
```

### Visual Grouping Without Lines

Avoid overusing dividers and borders — spacing alone creates hierarchy:

```
Needs divider:      No divider needed (enough gap):
  Item A            Item A
  ──────────
  Item B            Item B  ← 24px gap speaks for itself
```

Add a divider only when a gap alone doesn't create enough visual separation.

---

## 3. Visual Weight

**Purpose:** Balance competing elements by managing how "heavy" each element feels — so nothing dominates that shouldn't, and key elements naturally draw the eye.

**When to use:** Designing any screen with multiple visual elements; layout review.

### Visual Weight Factors

| Factor | Heavier | Lighter |
|--------|---------|---------|
| Size | Larger | Smaller |
| Color | Saturated / dark | Muted / light |
| Weight | Bold / thick | Thin / light |
| Contrast | High contrast vs background | Low contrast |
| Texture | Complex / noisy | Simple / smooth |
| Position | Center / top | Edge / bottom |
| Isolation | Surrounded by space | Crowded |

### Weight Balancing

A heavy element on the left needs a counterbalance on the right (or center):

```
[Heavy: large hero image]     [Light: text block]
         ↕ tension — unbalanced

[Heavy: large hero image]     [Heavier: multiple cards stacked]
         ↕ balanced — equal visual mass on each side
```

This applies asymmetrically — a small, high-contrast element can balance a large, muted element.

### Reducing Unwanted Weight

Elements that unintentionally draw the eye:
- Remove or de-saturate competing colors
- Reduce border thickness and opacity
- Reduce icon size or color intensity
- Use muted (not white) for secondary surfaces

---

## 4. Emphasis Techniques

**Purpose:** Draw attention to the single most important element or action on a screen.

**When to use:** Every screen should have one primary focus; use emphasis to establish it.

### Emphasis Methods (weakest → strongest)

| Technique | Effect | Use for |
|-----------|--------|---------|
| **Size increase** | Moderate | Primary headings, hero numbers |
| **Weight (bold)** | Moderate | Key labels, selected state |
| **Color accent** | Strong | Primary CTA, active elements |
| **Isolation (whitespace)** | Strong | Hero elements, key CTAs |
| **Contrast reversal** | Very strong | Primary button (dark text on bright bg) |
| **Scale disproportion** | Very strong | Hero value vs. surrounding text |
| **Motion** | Strongest | Animated counters, loading progress |

### The One Primary Rule

**One element per screen should receive maximum emphasis.** If everything is emphasized, nothing is.

Design review question: "What is the ONE thing I want the user to look at first on this screen?" — that element should receive the strongest emphasis; everything else should step back.

### Emphasis Anti-patterns

- Multiple primary buttons competing on the same screen
- Every heading is bold and large (no hierarchy — all equal)
- Accent color used on 8+ elements (accent loses meaning)
- Animation on secondary elements drawing attention away from primary content

---

## 5. Scanning Patterns

**Purpose:** Design layouts that align with how users naturally scan screens — so key information is encountered in the order it matters.

**When to use:** Designing any content-heavy screen, landing page, or dashboard.

### F-Pattern (Most Common for Text-Heavy Content)

Users scan: horizontal across the top → shorter horizontal scan lower → vertical scan down the left edge

```
████████████████████████   ← Full horizontal scan (first line)
██████████████             ← Shorter horizontal scan (second line)
████                       ← Vertical scan down left edge
████
████
```

**Design for F-pattern:**
- Put the most important content in the first horizontal band
- Front-load value — key information in the first 3–5 words of each line
- Left edge is a hot zone — use it for labels, icons, and key data
- Right side (especially bottom-right) is rarely read

### Z-Pattern (For Low-Text / Advertising Layouts)

Users scan: top-left → top-right → diagonal to bottom-left → bottom-right

```
Start ────────────── End
       ↘
Start ────────────── CTA
```

**Design for Z-pattern:**
- Top-left: Logo / trust signal
- Top-right: Secondary navigation / CTA
- Bottom-left: Supporting information
- Bottom-right: Primary CTA (highest conversion position)

### Layer-Cake Pattern (For Data / Dashboard Screens)

Users scan horizontally across the page in bands, looking for relevant section headers:

```
████████████████████████   ← Section header (scanned)
                           ← Section content (skipped unless header relevant)
████████████████████████   ← Next section header (scanned)
```

**Design for layer-cake:**
- Section headers must be visually distinct — the scan target
- Headers should use user language (not internal product terms)
- Sections must be visually separated (enough gap, optional divider)

### Applying Scanning Patterns

1. Identify which pattern your content type follows
2. Map the 3 most important pieces of information to scan-zone hotspots
3. Ensure key content sits in the top horizontal band (all patterns) or left edge (F-pattern)
4. Review: does the visual hierarchy match the scanning priority?

---

## 6. Grid Systems

**Purpose:** Use a structured column system to create consistent, proportional, and organized layouts.

**When to use:** Designing any multi-column layout or screen that needs structural consistency.

### Standard Grid Configurations

| Context | Columns | Gutter | Margin |
|---------|---------|--------|--------|
| Mobile (375–430px) | 4 | 16px | 20px |
| Tablet (768–1024px) | 8 | 16px | 32–40px |
| Desktop (1280px+) | 12 | 24px | 80px |
| Wide (1440px+) | 12 | 24px | 120px+ or max-width cap |

### Column Span Patterns (12-column)

```
Full width:        12 cols  — hero, section headers, wide charts
3/4 width:         9 cols   — main content with narrow sidebar
2/3 width:         8 cols   — article, modal content
Half:              6 cols   — two-column split, card grid
1/3 width:         4 cols   — card in 3-column grid, sidebar
Quarter:           3 cols   — small card, stat box
```

### Grid Composition Patterns

**Card grid:**
```css
display: grid;
grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
gap: 16px;
```

**Main + sidebar:**
```css
display: grid;
grid-template-columns: 1fr 320px;
gap: 24px;
```

**Holy grail:**
```css
display: grid;
grid-template-columns: 240px 1fr 240px;
gap: 24px;
```

### Baseline Grid

Pair column grid with a baseline grid for vertical rhythm:

- Baseline unit: 4px (or 8px for coarser systems)
- All vertical spacing must be multiples of the baseline unit
- Line heights set to align to the baseline (e.g., 24px line height on a 4px grid = 6 units)

---

## 7. Alignment

**Purpose:** Create visual order and professionalism by ensuring elements share consistent edges and relationships.

**When to use:** Designing any layout; critical during review of any screen.

### Alignment Types

**Edge alignment** — elements share a left, right, top, or bottom edge
**Center alignment** — elements share a center axis (use sparingly — harder to scan)
**Baseline alignment** — text elements share a common baseline (essential for inline mixed elements)

### Alignment Rules

- **Left-align body text** — center alignment slows reading speed
- **Align to a grid, not to each other** — two elements aligned to the same grid column are more robust than two elements manually positioned to match each other
- **Icons and text: baseline or center** — align icons to the text cap height or optical center, not the bounding box
- **Numbers: right-align in columns** — right-aligning financial numbers in a column lets the eye compare magnitudes
- **Never mix alignment** — a column of left-aligned items next to center-aligned items creates visual noise

### Optical Alignment vs. Mathematical Alignment

Mathematical center is often visually off-center for geometric shapes:

```
Mathematical center:    Optical center:
  ▲                       ▲
  ──── center ────        ──── center ────

The triangle's visual mass is at the base,
so optical center is slightly higher than mathematical center.
```

Apply to: icon placement in containers, text in buttons, logos in headers.

---

## 8. Spacing Systems

**Purpose:** Use a consistent spacing scale so all gaps, padding, and margins feel related and intentional.

**When to use:** Any UI implementation; establishing a design system.

### 4px Base Grid

All spacing values are multiples of 4:

```
4px   (1×) — Micro: icon-to-label gap, inner component spacing
8px   (2×) — Small: tight component padding, badge padding
12px  (3×) — Medium-small: field label gap, icon container padding
16px  (4×) — Base: card padding, standard gap, form field padding
20px  (5×) — Screen edge padding (mobile)
24px  (6×) — Section gap, header spacing
32px  (8×) — Large section gap
40px  (10×) — Extra large section gap
48px  (12×) — Hero padding
64px  (16×) — Major section separation
80px  (20×) — Screen edge padding (desktop)
```

### Named Semantic Tokens

Give semantic names to spacing values used in specific contexts:

```
cardPad:        16px   — internal card padding
cardGap:        4px    — gap between stacked cards in a list
screenH:        20px   — screen horizontal edge padding
sectionGap:     24px   — gap between sections
fieldGap:       12px   — gap between sibling form fields
fieldLabelGap:  8px    — gap between label and input
touchTarget:    44px   — minimum touch target height
```

### Spacing Audit Questions

- Does every spacing value appear in the defined scale?
- Are related elements consistently spaced the same way across all screens?
- Is internal spacing (within a card) consistent with the `cardPad` token?
- Are section gaps consistent across all screens?

---

## 9. Balance

**Purpose:** Distribute visual weight evenly across the composition so the layout feels stable and resolved — not top-heavy, bottom-heavy, or lopsided.

**When to use:** Reviewing any layout; designing hero sections or landing pages.

### Types of Balance

**Symmetrical balance** — elements mirror across a central axis
- Feels: formal, stable, trustworthy
- Use for: corporate, institutional, high-trust contexts
- Risk: can feel static or boring

**Asymmetrical balance** — different elements of unequal weight achieve equilibrium
- Feels: dynamic, modern, interesting
- Use for: editorial, creative, consumer products
- Technique: balance a large light element with a small heavy element

**Radial balance** — elements arranged around a central point
- Feels: focused, energetic
- Use for: feature spotlights, circular data visualizations

### Achieving Asymmetric Balance

```
Large, muted image    ←→    Small, high-contrast text block
(heavy by size)              (heavy by contrast)

Wide, light panel     ←→    Narrow, dark panel
(heavy by width)             (heavy by color weight)
```

### Balance Red Flags

- All heavy elements on the left side (most common in LTR layouts)
- Large image with no counterweight — floats unanchored
- Empty right column or right half with no visual anchor
- Navigation items only on the left with nothing on the right

---

## 10. Negative Space

**Purpose:** Use empty space intentionally to create breathing room, improve readability, establish tone, and make individual elements more impactful.

**When to use:** Any layout review; especially important for premium, luxury, or minimal design aesthetics.

### Types of Negative Space

**Micro negative space** — space within and between type characters; padding within components
**Macro negative space** — large open areas between sections and around key elements

### What Negative Space Achieves

- **Readability** — text surrounded by space is faster to read than text in a crowded layout
- **Perceived quality** — generous spacing signals premium; cramped spacing signals commodity
- **Emphasis** — an element surrounded by space draws more attention than one in a crowded area
- **Rest** — the eye needs places to pause; constant density causes fatigue

### Negative Space Rules

- **Don't fill every available pixel** — restraint is a design decision
- **Increase inner padding before adding more content** — when a layout feels empty, the instinct is to add content; often the fix is more spacing
- **Consistent vertical rhythm** — section gaps should be consistent; random gaps feel unintentional
- **Above-fold density** — slightly denser above fold (important content) is acceptable; below fold can breathe more

### Premium vs. Utilitarian Space

```
Premium (luxury, SaaS, editorial):
  Large margins (80–120px desktop)
  Generous section gaps (64–96px)
  Cards with substantial internal padding (24–32px)

Utilitarian (tools, dashboards, admin):
  Tighter margins (24–40px)
  Compact section gaps (16–24px)
  Cards with efficient padding (12–16px)
```

Match spacing density to product personality.

---

## 11. Containment

**Purpose:** Use cards, panels, and visual containers to group related content, create hierarchy, and define interactive regions.

**When to use:** Any layout with multiple distinct content areas; any list of items.

### Container Types

| Container | Visual Treatment | Use For |
|-----------|-----------------|---------|
| **Card** | Background fill + border-radius + optional border | Grouping a discrete content item |
| **Panel / section** | Subtle background change; no border-radius | Large content regions (sidebars, header areas) |
| **Elevated card** | Shadow + slightly lighter background | Content that should feel "above" the page |
| **Info callout** | Subtle tinted background + left accent border | Important notices, tips, trust signals |
| **Inset** | Darker background within a card | Nested content; code blocks; input areas |
| **Divider** | 1px horizontal rule | Lightweight separation without container weight |

### Container Hierarchy

Containers carry visual weight — more elevated = more important:

```
Screen background  #080808   (base)
└── Card           #111111   (elevation 1)
    └── Elevated   #171717   (elevation 2)
        └── Inset  #0D0D0D   (depression — sits below card surface)
```

### Containment Decisions

**Use a container when:**
- The content is independently browsable (a contact card, a product card, an exchange row)
- The content needs clear separation from adjacent content
- The area is interactive (tappable card)

**Don't use a container when:**
- Content is part of a flowing narrative (use spacing instead)
- Every item already on the screen is contained (container soup — no hierarchy)
- A divider or spacing alone is sufficient

### Card Design Rules

- **Consistent border-radius** — all cards at the same level should have the same radius
- **Consistent padding** — all cards should use the same internal padding token
- **Hover state for tappable cards** — subtle background lightening or shadow increase
- **Never nest cards more than 2 levels** — deeper nesting creates confusing hierarchy

---

## 12. Gestalt Principles

**Purpose:** Apply the psychological principles of visual perception to design layouts that feel natural and coherent.

**When to use:** Any layout design; UI audits; understanding why something "feels wrong."

### The Core Principles

**Proximity** — Elements close together are perceived as a group.
```
Application: Form fields grouped by their labels (not floated separately)
Anti-pattern: Section header closer to the section above it than the section below it
```

**Similarity** — Elements that look alike are perceived as related.
```
Application: All primary buttons the same color and shape
Anti-pattern: Two different blue elements — one a button, one a data badge (confusing relationship)
```

**Closure** — The brain completes incomplete shapes.
```
Application: Truncated list items ("See 12 more") suggest more content exists
Application: Progress ring with a gap communicates percentage without a number
```

**Continuity** — The eye follows paths and flows.
```
Application: Step indicators (1 → 2 → 3) guide the eye through a flow
Application: Horizontal card scroll implies there are cards beyond the viewport edge
```

**Figure-Ground** — Elements are perceived as either foreground (figure) or background (ground).
```
Application: Cards (figure) against the screen background (ground)
Application: Modal (figure) against dimmed overlay (ground)
Anti-pattern: Card background too close to screen background — no clear figure/ground separation
```

**Common Fate** — Elements moving in the same direction are perceived as related.
```
Application: A list row highlights and its chevron changes color together on hover — both belong to the same interactive target
```

**Symmetry** — Symmetrical elements are perceived as stable and belonging together.
```
Application: Two equal columns of content feel related and balanced
Application: Centered modals feel stable; offset modals feel dynamic/temporary
```

### Applying Gestalt to UI Review

When something "feels off" in a layout, check against each principle:
- Are related things close together and similar? (Proximity + Similarity)
- Is there clear figure-ground contrast? (Figure-Ground)
- Are interactive regions consistent and recognizable? (Similarity + Common Fate)
- Does the eye know where to go next? (Continuity)
