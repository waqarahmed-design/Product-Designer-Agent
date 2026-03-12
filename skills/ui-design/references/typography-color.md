# Typography & Color

## Table of Contents
1. [Font Selection](#1-font-selection)
2. [Type Scale](#2-type-scale)
3. [Line Height & Spacing](#3-line-height--spacing)
4. [Typographic Pairing](#4-typographic-pairing)
5. [Web Font Optimization](#5-web-font-optimization)
6. [Internationalization](#6-internationalization)
7. [Readability](#7-readability)
8. [Color Psychology](#8-color-psychology)
9. [Color Harmony](#9-color-harmony)
10. [Brand Color Systems](#10-brand-color-systems)
11. [Semantic Color](#11-semantic-color)
12. [Tint & Shade Systems](#12-tint--shade-systems)
13. [Color Accessibility](#13-color-accessibility)
14. [Dark Mode Design](#14-dark-mode-design)

---

## 1. Font Selection

**Purpose:** Choose typefaces that fit the product's personality, are readable at all sizes, and perform well across devices.

**When to use:** Establishing a new product or design system; rebranding; any time the current type feels wrong.

### Font Personality Map

| Personality | Font Style | Examples |
|-------------|------------|---------|
| Trustworthy, institutional | Traditional serif | Georgia, Merriweather, Playfair Display |
| Modern, clean, neutral | Geometric sans | Inter, DM Sans, Outfit |
| Premium, editorial | High-contrast serif | Freight Display, Canela, GT Super |
| Technical, precise | Monospace | JetBrains Mono, IBM Plex Mono, Fira Code |
| Friendly, approachable | Rounded sans | Nunito, Poppins, Quicksand |
| Bold, confident | Extended display | Syne, Space Grotesk, Clash Display |
| Luxury, fashion | High-contrast display | Bodoni, Cormorant Garamond, Italiana |
| Retro, distinctive | Slab serif | Roboto Slab, Zilla Slab, Bitter |

### Font Selection Criteria

1. **Personality match** — does it feel right for the brand and audience?
2. **Readability at small sizes** — open apertures, generous x-height, clear letterforms at 12–14px
3. **Weight range** — at minimum: regular (400) + bold (700); ideally 6+ weights for design flexibility
4. **Character set** — does it support all characters needed (currency symbols, numbers, accents)?
5. **Performance** — available on Google Fonts or system fonts? Self-hosted? File size?
6. **License** — free for commercial use? Desktop + web licensing?

### Avoiding Generic Choices

Avoid overused fonts that produce commodity-feeling designs:
- Inter (overused in SaaS)
- Roboto (overused in consumer apps)
- Arial / Helvetica (zero personality)
- Space Grotesk (trending → becoming cliché)

Distinctive alternatives that still read cleanly:
- DM Sans, Outfit, Plus Jakarta Sans (clean sans alternatives to Inter)
- Neue Haas Grotesk, Aktiv Grotesk (premium alternatives to Helvetica)
- Fraunces, Lora, Source Serif (interesting serifs)

---

## 2. Type Scale

**Purpose:** Define a system of harmonious font sizes that establishes clear hierarchy and scales proportionally.

**When to use:** Establishing a design system; when typography feels inconsistent across screens.

### Modular Scale

A modular scale uses a ratio to generate each size from the previous:

```
Base: 16px
Ratio: 1.25 (Major Third)

Scale:
  xxs:  10px  (16 / 1.25 / 1.25 / 1.25)
  xs:   12px  (16 / 1.25 / 1.25)
  sm:   13px  (16 / 1.25)
  base: 16px
  md:   20px  (16 × 1.25)
  lg:   25px  (16 × 1.25²)
  xl:   32px  (16 × 1.25³) — snap to 32 for 4px grid
  2xl:  40px  (16 × 1.25⁴) — snap to 40
  3xl:  48px  — snap to 48
  4xl:  56px  — snap to nearest multiple of 4
```

Common ratios: 1.125 (tight), 1.25 (moderate), 1.333 (open), 1.5 (expressive)

### 4px Grid Snapping

After calculating modular values, snap to the nearest multiple of 4:
- 13px → 12px
- 25px → 24px
- 50px → 48px or 52px

### Type Scale for Product UI (Recommended)

```
display:   52 / 48 / 40 / 32    — hero, marketing
title:     28 / 24 / 20 / 16    — page titles, section headers
body:      16 (large) / 14 / 12 — content, supporting
label:     12 / 8               — always uppercase in UI
numeric:   40 / 24 / 20 / 16 / 12 / 8   — financial values (monospace)
```

### Type Scale Rules

- Minimum 3:1 size ratio between display and body (ensures clear hierarchy)
- Never use more than 8 distinct sizes in a product
- All sizes must be multiples of 4
- Document line heights alongside font sizes — they define the layout grid contribution

---

## 3. Line Height & Spacing

**Purpose:** Optimize the vertical spacing within and between text blocks for maximum readability.

**When to use:** Setting up a type system; reviewing any screen where text feels crowded or disconnected.

### Line Height by Text Type

| Text type | Recommended line height | Ratio |
|-----------|------------------------|-------|
| Display / hero (40px+) | 1.1–1.2× | Tight — large text needs less leading |
| Headings (20–40px) | 1.2–1.3× | Moderate |
| Body copy (14–18px) | 1.5–1.75× | Generous — long reading requires breathing room |
| UI labels (12px and below) | 1.2–1.4× | Tight — single line labels |
| Monospace / code | 1.6–1.8× | Extra generous — characters are narrower |

**4px grid snapping example:**
```
16px font × 1.5 = 24px line height ✅ (multiple of 4)
16px font × 1.625 = 26px → snap to 24px or 28px
```

### Letter Spacing

| Text type | Letter spacing |
|-----------|---------------|
| Display headlines | −0.5px to −2px (negative — large text tracks too wide) |
| Body copy | 0 to 0.2px (neutral) |
| UI LABELS (ALL CAPS) | +1px to +2px (positive — caps need breathing room) |
| Monospace | 0 (already spaced by design) |

### Paragraph Spacing

```
Between paragraphs: 0.75–1.0× the font size (or use margin-bottom)
Between sections:   1.5–2.0× the font size

Example (16px body):
  Paragraph gap: 12–16px
  Section gap: 24–32px
```

---

## 4. Typographic Pairing

**Purpose:** Combine two (occasionally three) typefaces to create a cohesive type system with both personality and function.

**When to use:** Establishing a new product typeface; when current type feels flat.

### Pairing Strategies

**Contrast pairing (most common):**
Display/heading = serif or display sans → Body = neutral sans
```
Heading: Playfair Display (editorial serif)
Body: DM Sans (clean, neutral)
— contrast creates visual interest without clashing
```

**Complementary family pairing:**
Two cuts from the same typeface family
```
Heading: Freight Display (expressive)
Body: Freight Text (optimized for reading)
— guaranteed harmony; feels intentional
```

**Mono accent pairing:**
Primary sans or serif → Mono for data/code/numbers
```
UI: Inter
Numbers/data: JetBrains Mono
— very common in fintech/data products; clearly differentiates data from labels
```

### Pairing Rules

- **Maximum 2 typefaces** (3 if one is monospace for data) — more creates chaos
- **Don't pair two serifs** — they compete without enough contrast
- **Don't pair two display fonts** — neither will read well as body
- **Moods should align** — don't pair a whimsical handwritten font with a rigid technical font unless the contrast is intentional
- **Weight differentiation matters more than face difference** — sometimes one typeface at two weights outperforms two typefaces

### Pairing Test: Read These Together

```
Heading: [Heading typeface at 28px bold]
Body:    [Body typeface at 16px regular] A paragraph of sample text long enough to
         read. Does it feel like the heading and body belong to the same product?
```

If they feel like they're fighting → too similar or too different → try a different pairing.

---

## 5. Web Font Optimization

**Purpose:** Load fonts fast enough that they don't delay rendering, cause layout shift, or degrade performance.

**When to use:** Any web product using non-system fonts.

### Font Loading Strategy

```html
<!-- 1. Preconnect to font CDN (reduces DNS lookup time) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- 2. Preload critical font files directly -->
<link rel="preload" href="/fonts/font-400.woff2" as="font" type="font/woff2" crossorigin>

<!-- 3. font-display: swap prevents FOIT (flash of invisible text) -->
@font-face {
  font-family: 'BrandFont';
  src: url('/fonts/font-400.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;   /* show fallback immediately; swap when loaded */
}
```

### Font Subsetting

Load only the characters you need:
```
Full Latin set: ~60KB per weight
Latin subset:   ~20KB per weight
Custom subset:  ~5–10KB (only characters in your UI)
```

Tools: `glyphhanger`, `pyftsubset`, or Google Fonts `&subset=` parameter

### Weight Selection

Only load the weights you actually use:
```
Minimal set (2 weights): 400 (regular) + 700 (bold) — ~40KB total
Standard set (3 weights): 400 + 600 + 700 — ~60KB total
Full set (5+ weights): loads slowly — only for editorial/marketing sites
```

### Variable Fonts

Variable fonts bundle all weights in one file with smaller total size:
```css
@font-face {
  font-family: 'BrandFont';
  src: url('/fonts/font-variable.woff2') format('woff2-variations');
  font-weight: 100 900;    /* entire range available */
  font-display: swap;
}

/* Use any weight on the continuous scale */
h1 { font-weight: 850; }
p  { font-weight: 430; }
```

### System Font Stack (Zero Load Time)

For performance-critical products, consider system fonts:
```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto,
             'Helvetica Neue', Arial, sans-serif;
```
Trade-off: zero personality, renders differently per OS.

---

## 6. Internationalization

**Purpose:** Design type systems that work across multiple languages and scripts without breaking layouts.

**When to use:** Any product serving users in more than one language.

### Text Expansion

Translated text is rarely the same length as English:

| Language | Expansion vs. English |
|----------|----------------------|
| German | +20–35% |
| French | +15–20% |
| Russian | +15–20% |
| Spanish | +15–25% |
| Japanese | −10 to 0% (characters are compact but wide) |
| Arabic | 0 to +20% (RTL) |
| Chinese | −20 to −30% (dense characters) |

**Design for 30–40% text expansion** — buttons, labels, and nav items must accommodate longer strings.

### Flexible Layout Rules

- Never fixed-width buttons with text — use `min-width` + padding:
  ```css
  button { min-width: 120px; padding: 10px 20px; }
  ```
- Truncate with ellipsis only as a last resort — prefer wrapping
- Test layouts with German or Finnish text (longest expansion)
- Reserve extra vertical space for wrapped navigation labels on mobile

### RTL (Right-to-Left) Support

Languages affected: Arabic, Hebrew, Persian, Urdu

```css
/* CSS logical properties work for both LTR and RTL */
margin-inline-start: 16px;  /* margin-left in LTR, margin-right in RTL */
padding-inline-end: 16px;   /* padding-right in LTR, padding-left in RTL */

/* Direction */
[dir="rtl"] { direction: rtl; }
```

RTL design considerations:
- Navigation bar: logo moves to right, hamburger moves to left
- Icons that indicate direction (arrows, chevrons) must flip
- Bi-directional text (RTL Arabic with LTR numbers) needs `unicode-bidi: embed`

### CJK (Chinese, Japanese, Korean) Typography

- Line break rules differ — no spaces between words; break anywhere
- No italic support in many CJK fonts — use weight for emphasis instead
- Larger minimum font size needed — 14px is often too small for CJK characters
- Line height: 1.8–2.0× for CJK body text (more generous than Latin)

### Outputs
- Text expansion budget per component
- RTL layout spec (mirroring rules)
- CJK fallback font stack

---

## 7. Readability

**Purpose:** Ensure body copy and headings can be read with minimal effort across ages, abilities, and contexts.

**When to use:** Any product with substantial text content; accessibility review.

### Readability Factors

| Factor | Optimal Range |
|--------|--------------|
| Font size (body) | 16px min (mobile), 16–18px (desktop) |
| Line length | 45–75 characters (about 7–12 words per line) |
| Line height | 1.5–1.75× for body copy |
| Contrast | 4.5:1 minimum for normal text (WCAG AA) |
| Letter spacing | 0 to slight positive for body; never tightly negative |
| Font weight | 400 for body (300 too light for small screens) |
| Column width | Max 680px for single-column reading content |

### Line Length Control

```css
/* Optimal reading width */
.article-body {
  max-width: 65ch;  /* ch = width of "0" character; ~65 characters per line */
}

/* Or in px for fixed layouts */
.content { max-width: 680px; }
```

### Readability Anti-patterns

- **Justified text** — creates uneven word spacing; avoid for digital
- **All caps body text** — dramatically reduces reading speed
- **Light weight on small text** — 300 weight at 12px is unreadable on most screens
- **Low contrast gray-on-gray** — common in "modern" designs; fails accessibility
- **Very long lines** — eye loses track of where the next line starts
- **Very short lines** — breaks reading flow; each line wrap interrupts

### Font Rendering Considerations

```css
/* Improve rendering on macOS/iOS */
body { -webkit-font-smoothing: antialiased; }

/* Improve rendering on Windows */
body { text-rendering: optimizeLegibility; }

/* Don't optimize legibility on small text — can degrade rendering */
small { text-rendering: auto; }
```

---

## 8. Color Psychology

**Purpose:** Understand the emotional associations of colors so choices reinforce (not undermine) the intended product experience.

**When to use:** Establishing a brand palette; reviewing whether color choices feel right for the context.

### Color Emotional Associations

| Color | Common associations | Product contexts |
|-------|--------------------|-----------------|
| **Blue** | Trust, calm, authority, professionalism | Finance, healthcare, enterprise, tech |
| **Green** | Growth, health, success, money, nature | Fintech (gains), health, sustainability |
| **Red** | Urgency, danger, passion, energy | Alerts, CTAs (high urgency), sale prices |
| **Orange** | Warmth, enthusiasm, creativity, affordability | Consumer apps, food, sports |
| **Yellow** | Optimism, attention, caution, warmth | Warnings, highlights, energy brands |
| **Purple** | Luxury, creativity, mystery, royalty | Premium, beauty, spirituality |
| **Pink** | Playful, romantic, modern, bold | Beauty, fashion, youth, Gen Z products |
| **Black** | Sophistication, premium, authority | Luxury, fashion, high-end tech |
| **White** | Cleanliness, simplicity, space | Minimal design, medical, Apple-style |
| **Gray** | Neutral, professional, balanced | UI backgrounds, secondary content |

### Cultural Variation

Color meaning varies by culture — critical for global products:

| Color | Western | East Asian | Middle Eastern |
|-------|---------|-----------|---------------|
| White | Purity, wedding | Mourning, death | Purity |
| Red | Danger, passion | Luck, prosperity | Danger, caution |
| Green | Nature, money | Growth | Islam, sacred |
| Yellow | Caution | Royalty (China) | Happiness |

### Practical Application

- Color psychology guides first impressions — wrong color creates dissonance before a user reads a word
- Trust signals (security badges, privacy copy) in blue reinforce the message
- Destructive actions in red make consequence feel real
- Gain indicators in green feel viscerally positive; loss in red feels viscerally negative (universal in financial UIs)

---

## 9. Color Harmony

**Purpose:** Combine colors that work together visually, creating a palette that feels unified and intentional.

**When to use:** Building a color palette; when current palette feels chaotic or flat.

### Harmony Types

**Monochromatic** — variations of one hue (different saturation and lightness)
```
Palette: navy → blue → light blue → very light blue
Effect: cohesive, calm, safe
Risk: can feel monotonous
```

**Analogous** — neighboring hues on the color wheel (within 60°)
```
Palette: blue → blue-green → green
Effect: harmonious, natural, pleasing
Risk: low contrast between colors
```

**Complementary** — opposite hues on the color wheel (180° apart)
```
Palette: blue + orange; red + green; purple + yellow
Effect: high contrast, vibrant, dynamic
Risk: can feel garish if both fully saturated; one should dominate
Rule: 80% dominant + 20% complement (not 50/50)
```

**Split-complementary** — one hue + two colors adjacent to its complement
```
Palette: blue + yellow-orange + red-orange
Effect: high contrast but more nuanced than complementary
Risk: complex to execute well
```

**Triadic** — three hues equidistant on the wheel (120° apart)
```
Palette: red + yellow + blue; orange + green + purple
Effect: vibrant, playful, balanced
Risk: hard to make premium; requires strong desaturation to avoid clashing
```

### Practical Harmony for UI

Most UI palettes are not pure harmony schemes — they're:
- 1 neutral range (grays or dark/light scale)
- 1 brand/primary hue
- 1 accent (often complementary to primary)
- 2–3 semantic colors (green, red, yellow — fixed regardless of brand)

The harmony principle applies most to the brand primary and accent choice.

---

## 10. Brand Color Systems

**Purpose:** Define a structured, reusable color system that expresses brand identity and scales consistently across all surfaces.

**When to use:** Designing a new product or design system; when color usage is inconsistent across the product.

### Color System Architecture

```
Brand colors (identity)
  Primary:    The dominant brand color; used for primary CTAs and key UI elements
  Secondary:  Supports primary; used for secondary actions and elements
  Accent:     High-contrast highlight; used sparingly for maximum impact

Neutrals (structure)
  Background: Page/screen background
  Surface:    Card/panel surfaces
  Border:     Dividers and outlines
  Muted:      Near-invisible fills (not for text)

Text colors
  Primary:    Highest contrast — main headings and body copy
  Secondary:  Reduced contrast — supporting text, labels
  Disabled:   Low contrast — unavailable states

Semantic colors (meaning — always the same regardless of brand)
  Success:    Green family
  Warning:    Yellow/amber family
  Error:      Red family
  Info:       Blue family

Each semantic color needs:
  Base:       The solid color (icon, border)
  Dim:        10–15% opacity version (background tint)
  Text:       Color for text on the dim background
```

### Token Naming Convention

```
--color-brand-primary
--color-brand-accent
--color-neutral-bg
--color-neutral-surface
--color-neutral-border
--color-text-primary
--color-text-secondary
--color-semantic-success
--color-semantic-success-dim
--color-semantic-error
--color-semantic-error-dim
```

---

## 11. Semantic Color

**Purpose:** Use color consistently to communicate meaning — so users learn the color language of the product and interpret states instantly.

**When to use:** Any UI with status states, data values, or interactive feedback.

### Core Semantic Colors

| Color | Meaning | Use for |
|-------|---------|---------|
| **Green** | Success, positive, gain | Upload complete, payment successful, profit/gain |
| **Red** | Error, danger, loss, destructive | Form error, failed action, loss, delete |
| **Yellow/Amber** | Warning, caution, pending | Approaching limit, degraded state, unverified |
| **Blue** | Info, neutral, primary | Informational messages, links, primary actions |

### Semantic Consistency Rules

- **Same semantic always uses the same color** — "success" is always green; it's never teal on one screen and green on another
- **Never use semantic colors for decoration** — red is for errors and destructive actions only; don't use it for a "hot" product label
- **Color + icon + text** — never convey state through color alone (accessibility)
- **Financial gains/losses** — green/red is a global convention in financial UIs; don't deviate

### Semantic Color Patterns

```
Success state:
  Icon:       green (filled checkmark)
  Background: greenDim (green at 10% opacity)
  Text:       slightly brighter green
  Border:     medium green (optional)

Error state:
  Icon:       red (filled x or alert)
  Background: redDim
  Border:     red
  Text:       error message in default text color (not red — hard to read)

Warning state:
  Icon:       amber/yellow
  Background: amberDim
  Text:       default text color (amber text has contrast problems)
```

---

## 12. Tint & Shade Systems

**Purpose:** Create a full color scale from a single brand hue — from very light tints to very dark shades — for use across all UI contexts.

**When to use:** Building a design system; when you need a full range of a color for backgrounds, surfaces, borders, and fills.

### Scale Structure (10-step)

```
50:   Lightest tint    — page background tint
100:  Very light       — subtle background
200:  Light            — hover state background
300:  Medium-light     — disabled fills
400:  Medium           — placeholder text
500:  Base color       — the pure brand hue (reference point)
600:  Medium-dark      — default UI color
700:  Dark             — hover/active states
800:  Very dark        — text on light backgrounds
900:  Darkest shade    — headings on light backgrounds
```

### Generation Methods

**HSL adjustment (simple):**
```
Base: hsl(220, 80%, 50%)   ← 500

Tints (increase lightness): hsl(220, 80%, 95%) → 50
Shades (decrease lightness): hsl(220, 80%, 15%) → 900
Adjust saturation too: tints slightly less saturated, shades more saturated
```

**OKLCH (perceptually uniform — modern):**
```css
@theme {
  --color-blue-500: oklch(55% 0.2 265);
  --color-blue-50:  color-mix(in oklab, var(--color-blue-500) 8%, white);
  --color-blue-100: color-mix(in oklab, var(--color-blue-500) 15%, white);
  --color-blue-900: color-mix(in oklab, var(--color-blue-500) 90%, black);
}
```

OKLCH produces perceptually equal steps — each step looks equally different from the next. HSL does not.

### Dark Theme Tint Usage

In dark mode, the scale flips partially:
- 900 as background, 50 as text (inverted)
- But 500 (brand color) often stays the same
- Dim versions: use opacity rather than scale values (e.g., blue at 12% opacity for background tints)

---

## 13. Color Accessibility

**Purpose:** Ensure colors work for users with color vision deficiency and meet WCAG contrast requirements.

**When to use:** Finalizing any color palette; before launch; accessibility audit.

### Color Blindness Types

| Type | Prevalence | Colors affected |
|------|------------|----------------|
| Deuteranopia (red-green) | 5% of males | Red/green confusion |
| Protanopia (red-green) | 1% of males | Red/green; red appears dark |
| Tritanopia (blue-yellow) | Rare | Blue/green, yellow/violet confusion |
| Achromatopsia | Very rare | No color perception |

**Most critical:** deuteranopia — 5% of men can't distinguish red from green. This directly affects gain/loss indicators in financial UIs.

### Making Color-Blind Safe Palettes

**Don't rely on red/green distinction alone:**
```
Loss indicator:   red + downward arrow icon       ← icon differentiates
Gain indicator:   green + upward arrow icon        ← icon differentiates
Error field:      red border + error icon + text   ← icon + text differentiates
Success:          green + checkmark icon           ← icon differentiates
```

**Colorblind-safe palette alternatives:**
```
Red/green → Red (#D62728) + Blue (#1F77B4)
Red/green → Orange (#FF7F0E) + Blue (#1F77B4)
Chart colors (Tableau accessible palette):
  #4E79A7 (blue) #F28E2B (orange) #E15759 (red) #76B7B2 (teal) #59A14F (green)
```

**Simulation tools:**
- Figma plugin: Stark, Color Blind
- Browser: Chrome DevTools → Rendering → Emulate Vision Deficiencies
- Web: Coblis (Color Blindness Simulator)

### Contrast Requirements

(See also `references/usability-accessibility.md` Color Contrast section)

| Text type | AA minimum | AAA |
|-----------|------------|-----|
| Body text (< 18pt) | 4.5:1 | 7:1 |
| Large text (≥ 18pt) | 3:1 | 4.5:1 |
| UI components / icons | 3:1 | — |

**Quick reference for dark UIs (#080808 background):**
- White (#F2F2F2): 19.5:1 ✅
- Light gray (#999): 6.8:1 ✅
- Mid gray (#666): 3.1:1 ✅ (large text only)
- Dark gray (#444): 1.8:1 ❌

---

## 14. Dark Mode Design

**Purpose:** Adapt a UI for dark backgrounds while preserving hierarchy, readability, and brand identity.

**When to use:** Adding dark mode support; designing a dark-first product.

### Dark Mode Color Mapping

```
Light mode → Dark mode
White background → Near-black (not pure black)
White cards → Slightly lighter than background
Black text → Near-white (not pure white)
Gray text → Muted light gray
Borders → Subtle lighter than surface

Light (#FFFFFF bg):          Dark (#080808 bg):
  Text: #0F172A                Text: #F2F2F2
  Secondary: #64748B           Secondary: #666666
  Card bg: #FFFFFF             Card bg: #111111
  Border: #E2E8F0              Border: #222222
  Input bg: #F8FAFC            Input bg: #0D0D0D
```

### Why Not Pure Black (#000000)

Pure black (#000000) with pure white (#FFFFFF) text creates too much contrast — uncomfortable for sustained reading. OLED displays also have blooming artifacts at extreme contrast. Use:
- Background: #080808–#111111
- Text: #F2F2F2 (not pure white)

### Elevation in Dark Mode

In light mode, elevation = shadow (elements cast shadows downward).
In dark mode, elevation = lightness (elements higher in the stack are slightly lighter):

```
Screen background:  #080808
Card surface:       #111111   ← elevation 1
Elevated card:      #171717   ← elevation 2
Tooltip/popover:    #1C1C1C   ← elevation 3
```

### Dark Mode Typography Adjustments

- Reduce font weight for large text — bold text on black can appear too heavy/bloated
- Increase letter spacing slightly for body text — white on black letters appear to bleed into each other
- Avoid pure white text for body copy — use #F2F2F2 or #E5E5E5

### Semantic Colors in Dark Mode

Semantic colors (green, red, yellow) may need adjustment:
```
Light mode green: #16A34A (darker — reads on white)
Dark mode green:  #4ADE80 (lighter — reads on dark)

Light mode red: #DC2626
Dark mode red:  #F87171 (lighter — reads on dark)
```

The dim versions (background tints) remain similar — already low opacity.

### Dark Mode Implementation Pattern

```css
/* CSS custom properties for theming */
:root {
  --color-bg: #FFFFFF;
  --color-surface: #F8FAFC;
  --color-text: #0F172A;
  --color-text-secondary: #64748B;
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #080808;
    --color-surface: #111111;
    --color-text: #F2F2F2;
    --color-text-secondary: #666666;
  }
}

/* Or class-based (for user toggle) */
.dark {
  --color-bg: #080808;
  /* ... */
}
```
