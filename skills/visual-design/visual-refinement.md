# Visual Refinement Methods

## Table of Contents
1. [Pixel Perfection](#1-pixel-perfection)
2. [Optical Alignment](#2-optical-alignment)
3. [Consistency Auditing](#3-consistency-auditing)
4. [Polish & Craft](#4-polish--craft)

---

## 1. Pixel Perfection

**Purpose:** Ensure every element in the UI is rendered at exact intended dimensions, with no sub-pixel blurring, unintended overflow, misaligned edges, or spacing inconsistencies — making the design feel intentional and precise.

**When to use:** During final design QA; before handoff to engineers; when a design looks "slightly off" without an obvious cause; when comparing a live implementation to the design spec.

### Sub-pixel Rendering

Sub-pixel issues cause blurring and visual softness:

```
Problem sources:
  - Element positioned at x: 10.5px (non-integer coordinates)
  - Element dimension: 15px height on a 1x display (not divisible by 2 for retina)
  - SVG paths with fractional coordinates
  - CSS transforms: translate(-50%, -50%) on an element with odd dimensions

Detection:
  - Zoom to 200% — blurred edges indicate sub-pixel rendering
  - In Figma: check the X/Y/W/H panel — any decimal value is a red flag
  - In browser: element has fractional getBoundingClientRect() values

Fix:
  - Round all coordinates to integers
  - For centered elements: use integer dimensions so -50% lands on a whole pixel
  - Use pixel-snapping in Figma (View → Pixel Preview)
  - For transforms: use `transform: translateZ(0)` to force GPU rasterization
```

### The 4px Grid Rule

Everything should snap to a 4px grid:

```
Check: Is every value a multiple of 4?
  ✅ padding: 16px, margin: 24px, height: 48px, border-radius: 8px
  ❌ padding: 14px, margin: 10px, height: 44px, border-radius: 6px

Exceptions:
  - 1px borders (intentional hairlines)
  - 2px strokes (intentional)
  - Individual spacing tokens that define exact values (e.g., Spacing.touchTarget = 44)

Grid overlay method:
  - Enable 4px grid overlay in Figma
  - Every element edge should land exactly on a grid line
  - Any misalignment = spacing correction needed
```

### Icon Sizing and Placement

Icons are a common source of pixel imprecision:

```
Rules:
  - Icon containers must be even numbers (16, 20, 24, 32) — never 15 or 17
  - Icon SVG viewBox must match the container size
  - Icon must be centered with integer offsets
  - Don't scale icons to arbitrary sizes — use the defined icon size scale

Common failure: an icon in a 24×24 box visually renders at 22px because
  of internal SVG padding — verify the actual rendered size, not just the container.

Check in browser:
  document.querySelector('.icon').getBoundingClientRect()
  → width and height should be exactly the design-specified values
```

### Border and Stroke Precision

```
1px borders on retina displays:
  - On 2x displays, 1px CSS = 2 physical pixels — renders fine
  - On 1x displays, 1px renders as designed
  - Problem: 0.5px CSS = 1 physical pixel on retina, but 0px on standard — avoid

Stroke alignment:
  - In Figma, stroke defaults to "center" — check if this matches implementation
  - Border-box sizing in CSS means border eats into the element width
  - Always verify: does the Figma stroke go inward or outward? Match in CSS.

Border radius precision:
  - Figma 'independent corners' can produce inconsistent values — standardize
  - Use token values exclusively — never ad hoc values
```

### Overflow and Clipping Audit

```
Check list:
  - Text overflow: does long text truncate (ellipsis), wrap, or overflow?
  - Image overflow: does image respect border-radius clipping?
  - Shadow clipping: is parent container cutting off box shadows?
  - Scroll container: does content peek behind sticky headers/footers?

In browser:
  - Temporarily add outline: 1px solid red to all elements to see true boundaries
  - Check for overflow: hidden on parent cutting off intended visual effects
```

### Outputs
- Pixel audit document: list of issues with screenshots + coordinates
- Fixed design file (all values on grid, no sub-pixel values)
- Browser QA checklist (compare rendered vs. designed)

---

## 2. Optical Alignment

**Purpose:** Adjust elements so they look visually centered and balanced — correcting for the perceptual illusions that cause mathematically-correct layouts to appear misaligned to the human eye.

**When to use:** When a mathematically centered element looks off-center; when icons in buttons feel too high or too low; when a layout feels unbalanced despite equal measurements; as the final check before any design is considered complete.

### Mathematical vs. Optical Alignment

```
Mathematical alignment: every element shares the same X/Y coordinate
Optical alignment: elements are adjusted so they APPEAR to be in the correct position

The human eye is not a ruler. It perceives visual weight, not coordinates.
When they conflict, optical wins.
```

### Common Optical Illusions in UI

**1. Circle vs. square in a container**

A circle centered at the same coordinates as a square appears to float higher:

```
Fix: Move the circle 1–2px down from mathematical center.
Reason: Squares have mass in all four corners; circles don't. The circle's
  visual center of gravity is higher than its geometric center.
```

**2. Vertical centering with descenders**

Text like "Typography" appears to sit above center because descenders (p, g, y) extend below the baseline but aren't perceived as top-of-letter height:

```
Fix: Shift text 1px down from mathematical center.
Or: Use cap-height for centering calculations, not full line-height.
```

**3. Icon in a button**

An icon paired with a label in a button often looks vertically misaligned even when aligned to center:

```
Fix:
  - Align icon to text baseline or optical center, not container center
  - Add 1px nudge in the direction the icon appears to drift
  - Test at multiple font sizes — the optical correction changes with size
```

**4. Visual weight asymmetry**

A left-heavy icon (more mass on the left side of the glyph) will appear right-shifted even when centered:

```
Fix: Shift the icon slightly toward its heavier side
  (i.e., 1–2px left for a left-heavy icon to balance visually)
```

**5. Negative space asymmetry in type**

The letter 'A' has a triangular void at its top. 'R' has a right-heavy profile. Placing these near other elements requires optical, not mechanical, spacing:

```
Fix: In headlines and large type, use optical kerning (not metric kerning)
CSS: font-kerning: normal (browsers handle this automatically for text)
Figma: set kerning to "Auto" — but verify visually at final size
```

### Optical Spacing Rules

```
Equal padding ≠ equal perceived space:
  - Top and bottom padding that appears equal often needs top reduced by 1–2px
  - This is because descenders (letters below the baseline) create white space at
    the bottom that isn't perceived as part of the element

Practical test (the squint test):
  Squint until the screen is blurry. Can you tell which elements belong together?
  Do the margins between sections feel proportionally balanced?
  If a section "floats" separately — the spacing is probably right.
  If everything blurs into one block — increase the spacing contrast.
```

### Verifying Optical Alignment

```
Method 1: Screenshot overlay
  - Take a screenshot, open in a separate view
  - Draw center lines and margin guides
  - Then blur the screenshot 3–5px
  - Check if elements feel balanced with no ruler

Method 2: Flip test
  - Horizontally flip the design
  - Alignment errors become obvious when the brain stops pattern-matching
    familiar content

Method 3: The gray blob test
  - Replace all content with gray blobs of the same size
  - Inspect the spatial rhythm — do gaps feel consistent?
  - Does the layout feel balanced without the content to distract?

Method 4: New eyes
  - Look at the design after a break, or have someone else look
  - The first impression is closer to user perception than a close-up review
```

### Outputs
- Annotated design with optical corrections noted (with "mathematical" vs. "optical" values)
- Style guide note on known optical corrections (e.g., "icons are nudged 1px down in pill buttons")
- Before/after comparison for reference

---

## 3. Consistency Auditing

**Purpose:** Systematically identify all places where the design system is being applied inconsistently — wrong tokens, one-off styles, rebuilt components — and document a remediation path.

**When to use:** Before a major release; when a new designer joins and wants to understand the current state; quarterly as a health check; after a period of rapid feature development where standards may have slipped.

### Consistency Audit Types

| Audit type | What it checks | How |
|-----------|---------------|-----|
| Token audit | Are design tokens used everywhere, or are there hardcoded values? | Automated lint scan |
| Component audit | Are native system components used, or are there rebuilt copies? | Manual screen review |
| Spacing audit | Is the 4px grid respected throughout? | Figma grid overlay / browser tool |
| Typography audit | Are all text styles from the type scale, or are there one-offs? | Figma: Plugins → Find One-offs |
| Color audit | Are only brand/semantic colors used, or are there ad hoc hex values? | Lint script / Figma variable checker |
| Interaction audit | Are hover states, focus rings, animations consistent? | Interactive review |
| Icon audit | Are all icons from the approved library at the correct sizes? | Icon inventory check |
| Accessibility audit | Are color contrast, font sizes, and focus indicators consistent? | axe DevTools / manual check |

### Audit Process

```
1. Scope definition (30 min)
   - List all screens / pages in scope
   - Define audit depth: full audit vs. targeted (e.g., only token audit)
   - Assign owner per area if team is large

2. Baseline capture (1–2 hours)
   - Screenshot every screen in a grid
   - Create an "audit file" (Figma or Notion) with all screens side by side
   - Side-by-side comparison is faster than reviewing screens individually

3. Systematic scan (2–4 hours per audit type)
   - Go through each screen with one specific audit type in mind
   - Mark violations with annotations (don't try to fix during the audit)
   - Note: severity (cosmetic / minor / major / critical)

4. Remediation plan (1 hour)
   - Group violations by type
   - Identify patterns (if the same violation appears in 10 places, fix the source)
   - Prioritize: critical / major first; cosmetic in batch
   - Assign owners and timeline

5. Verification (after fixes)
   - Re-scan audited areas
   - Close audit items; keep open items in the backlog
```

### Severity Levels

| Level | Definition | Examples | Action |
|-------|-----------|---------|--------|
| Critical | Breaks functionality or accessibility | Missing focus indicator, contrast failure | Fix before release |
| Major | Clearly breaks design system rules; visible to users | Hardcoded color, rebuilt component with different behavior | Fix in current sprint |
| Minor | Subtle deviation; unlikely noticed by users | 1–2px spacing inconsistency, font weight one step off | Fix in polish pass |
| Cosmetic | Negligible; debatable whether it's a problem | Icon 1px larger than spec in one screen | Fix in batch cleanup |

### Automated Token Audit

For codebases, add linting to catch token violations automatically:

```javascript
// Example token lint rules (eslint or custom script):
// 1. Detect hardcoded hex values
const hexPattern = /#[0-9a-fA-F]{3,6}/;

// 2. Detect hardcoded font families
const fontFamilyPattern = /fontFamily:\s*['"][^'"]+['"]/;

// 3. Detect hardcoded font sizes
const fontSizePattern = /fontSize:\s*\d+/;

// Run on all component files, report file + line number
// Allowlist: design token definition files themselves
```

### Figma Consistency Check

```
Use Figma plugins to find inconsistencies:
  - "Variables" panel: find elements not using variables (= hardcoded)
  - "Find/Replace" plugin: search for specific pixel values to find one-offs
  - "Similayer" plugin: select all similar elements to compare styles
  - "Design Lint" plugin: automated check for detached styles, missing variables

Manual check:
  - Select all text → check for non-library text styles in the panel
  - Select all fills → check for non-library colors
  - Select all borders → check for non-standard border widths/colors
```

### Outputs
- Audit report: all violations categorized, scored, and assigned
- Remediation backlog with prioritized issues
- Patterns to fix at the source (avoids whack-a-mole individual fixes)
- Design system health score (% of elements using tokens correctly)

---

## 4. Polish & Craft

**Purpose:** Elevate a functional design to a great design through attention to the details that users feel but can't always name — the micro-moments of quality that build trust and delight.

**When to use:** After functionality is complete and UX flows are verified; during pre-launch polish pass; when a design is "correct" but doesn't feel excellent; when differentiating a product on design quality.

### The Polish Mindset

```
Good design: solves the problem correctly
Great design: solves it so well that users don't notice the solution

Polish is not decoration. It's precision in service of clarity.

Questions to ask:
  "Does this element earn its place?"
  "What would happen if I removed this?"
  "Does this feel as good as it looks?"
  "Does the interaction match the visual quality?"
```

### The Polish Checklist

**Typography polish:**

```
□ Headings use optical kerning, not metric
□ No orphans (single words on the last line of a paragraph)
□ No widows (single line from a paragraph at the top of a new column)
□ Numbers in data-dense views use tabular figures (equal-width digits)
□ Ligatures enabled for display type (only if the typeface supports them)
□ Ellipsis (…) used instead of three dots (...) for truncation
□ Quotes use typographic curly quotes ("...") not straight quotes ("...")
□ En dash (–) vs. em dash (—) vs. hyphen (-) used correctly
```

**Color and depth polish:**

```
□ Backgrounds have barely-perceptible texture or gradient — not flat #000000
□ Cards have very subtle elevation (0.5–1px inner highlight at top edge)
□ Interactive elements show depth change on press (subtle scale + shadow change)
□ Focus rings are styled, not default browser outline
□ Shadows have directional consistency (light source from top-left throughout)
□ Gradients use multi-stop to avoid the "gray muddy middle" (add a midpoint stop)
```

**Spacing polish:**

```
□ Section spacing increases as hierarchy level increases (more space = more importance)
□ Related items breathe together; sections breathe apart
□ The "paragraph" before a headline has more space than after it (headline owns what follows)
□ Icons sit on the optical center of their grid, not the mathematical center
□ Lists have consistent vertical rhythm — line-height + gap = same across all lists
```

**Motion polish:**

```
□ Enter animations: fade + translate (never scale from zero — feels cheap)
□ Exit animations: faster than enter (150ms max — don't make users wait)
□ Hover transitions: 100–150ms ease-out (instant feels janky; slow feels sluggish)
□ Skeleton loaders use shimmer in one direction (left to right) — never pulse/scale
□ Spring physics feel natural — test spring tension/friction, avoid linear easing
□ No animation fires twice (e.g., component unmounts and remounts on state change)
```

**Interaction detail polish:**

```
□ Buttons feel tactile: subtle scale (0.97) on press, restore on release
□ Scroll momentum feels natural — test on actual device, not simulator
□ Pull-to-refresh: indicator appears at the right threshold (not too early, not too late)
□ Haptic feedback on iOS at right moments (success, destructive confirmation, error)
□ Touch targets exceed 44×44px minimum but feel precise, not oversized
□ Long press reveals secondary actions exactly as long-press should feel
```

**Edge case polish:**

```
□ Long strings truncate gracefully (not broken layout)
□ Empty states have illustrations or icons — not just "No data found"
□ Error messages are human, not stack traces
□ Loading states feel estimated (skeleton with content shape) not generic (spinner alone)
□ Zero values display correctly: $0.00 not $0 or $NaN
□ Overflow lists have a clear "show more" — never unexplained cut-off
```

### The Squint Test

```
Blur your vision while looking at the screen (or squint until the screen blurs).

What you're checking:
  - Visual hierarchy: is the most important thing clearly dominant?
  - Balance: does the page feel stable, or does one side feel heavier?
  - Rhythm: does the vertical spacing feel consistent?
  - Contrast: do the interactive elements stand out?

If the answer to any of these is no — polish is needed before other judgments.
```

### The Fresh Eyes Test

```
Step away from the design for 30 minutes.
Return and notice:
  - What's the first thing your eye goes to?
  - What feels out of place?
  - What feels like it's trying too hard?

The first 3 seconds of returning are the most valuable for catching polish issues.
The longer you look at a design, the more you normalize its flaws.
```

### What Polish Is Not

```
Avoid these anti-patterns:

Decoration without purpose:
  Adding a gradient, texture, or animation because it "looks nice"
  Rule: Remove it. If nothing is lost, it wasn't needed.

Complexity as sophistication:
  Multiple shadows, multiple colors, multiple font weights in one component
  Rule: The more restraint, the more intentional it looks.

Animation theater:
  Long, elaborate transitions on every interaction
  Rule: Motion should serve communication, not performance.

Pursuing pixel perfection over user value:
  Spending 2 hours on a 1px alignment issue while a UX problem exists
  Rule: Polish the things users notice; fix the things users feel.
```

### Outputs
- Polish audit: list of improvements across all categories
- Before/after documentation (screenshot pairs for the most impactful fixes)
- Design system updates for any polish patterns worth codifying (e.g., a new shadow token, an updated animation spec)
- Handoff notes to engineers for interaction details (spring values, timing, haptics)
