# Iconography & Imagery

## Table of Contents
1. [Icon Design](#1-icon-design)
2. [Icon System Consistency](#2-icon-system-consistency)
3. [Icon Sizing](#3-icon-sizing)
4. [Icon + Text Pairing](#4-icon--text-pairing)
5. [Metaphor Selection](#5-metaphor-selection)
6. [Photo Selection & Curation](#6-photo-selection--curation)
7. [Image Optimization](#7-image-optimization)
8. [Illustration Style](#8-illustration-style)
9. [Data Visualization](#9-data-visualization)
10. [Empty State Design](#10-empty-state-design)
11. [Placeholder Design](#11-placeholder-design)

---

## 1. Icon Design

**Purpose:** Create custom icons that are visually consistent, clearly recognizable, and appropriate for the product's context.

**When to use:** When existing icon libraries don't contain needed icons or don't match the product's visual language.

### Icon Anatomy

```
Viewbox:    Standard 24×24 (or 20×20 for compact, 32×32 for feature icons)
Grid:       2px internal padding → 20×20 usable area within 24×24 viewbox
Stroke:     1.5px–2px (consistent across all icons in the set)
Line caps:  Round (friendly) or Square (technical) — pick one, never mix
Corners:    Round (0.5–1px radius on joins) or Sharp — pick one
```

### Icon Grid Construction

```
24×24 viewbox
┌────────────────────────┐
│  2px padding all sides │
│  ┌──────────────────┐  │
│  │  20×20 live area │  │
│  │                  │  │
│  └──────────────────┘  │
└────────────────────────┘
```

Design within the live area. Circular icons can touch the outer edge of the viewbox.

### Icon Optical Sizing

Geometric shapes of equal mathematical size appear different in size. Compensate optically:

```
Circle at 20px diameter   feels smaller than square at 20×20
Triangle at 20px height   feels smaller than both

Fix: Circle = 22px, Square = 18×18px, Triangle = 20×20 with extra height
→ All three appear the same visual weight
```

### Pixel Hinting

For icons displayed at exact icon sizes (16px, 20px, 24px), align paths to pixel boundaries:
- Horizontal and vertical lines on whole pixel values
- Avoid 0.5px offsets on stroked paths — creates blurry rendering
- Use even stroke widths (1, 1.5, 2px) — not 1.3px or 1.7px

---

## 2. Icon System Consistency

**Purpose:** Maintain a visual language where all icons look like they belong to the same family.

**When to use:** Starting an icon system; auditing existing icons for consistency.

### System-Level Rules

Define once, enforce everywhere:

| Property | Rule | Example |
|----------|------|---------|
| **Style** | Outline OR filled — never both at the same tier | All navigation icons = outline; all status dots = filled |
| **Stroke weight** | Single value for all icons | 1.5px |
| **Corner style** | Round OR square cap/join | Round cap, round join |
| **Corner radius** | Consistent for rectangular forms | 1px on icon corners |
| **Viewbox** | Single standard size | 24×24 everywhere |
| **Optical balance** | All icons fill the viewbox consistently | No icon dramatically smaller or larger than peers |

### Mixing Libraries Safely

When using a third-party icon library (HugeIcons, Lucide, Heroicons):
- Use **one library only** — mixing Lucide (14px, 1.5px stroke) with Heroicons (20px, 2px stroke) is visually inconsistent
- Access all icons through a centralized registry (`Icons.ts`) — never import icon components directly in screen files
- Test at multiple sizes — some libraries degrade at 16px or below

### Consistency Audit Checklist

- [ ] All navigation icons are from the same library and style
- [ ] All icons at the same size use the same stroke weight
- [ ] No icons use a different visual style (some filled, some outline) at the same hierarchy level
- [ ] All icon components are accessed through the central registry
- [ ] No direct third-party icon imports in feature screens

---

## 3. Icon Sizing

**Purpose:** Use appropriate icon sizes for each context — neither too small to recognize nor too large for the space.

**When to use:** Any screen where icons appear; design system definition.

### Named Size Scale

```
feature:  32px  — zero-state illustrations, onboarding graphics, large feature callouts
md:       24px  — standard UI icons (navigation bars, primary actions, list items)
sm:       20px  — secondary actions, nav bar labels, input leading icons
xs:       16px  — micro contexts (badges, inline labels, table rows)
```

### Context Mapping

| Context | Size |
|---------|------|
| Hero / feature illustration | 32–48px |
| Primary navigation (tab bar, sidebar) | 24px |
| Action button icon | 20–24px |
| Input leading/trailing icon | 20px |
| Inline text icon (next to label) | 16px |
| Badge or tag icon | 12–16px |
| Micro status dot | 8px (not an icon — use a filled circle) |

### Icon Container Sizing

Icons often sit inside a container (button, avatar, badge). Container size must accommodate the icon + padding:

```
Icon 24px in a 40px container → 8px padding each side (comfortable)
Icon 20px in a 44px container → 12px padding each side (touch target sized)
Icon 16px in a 32px container → 8px padding each side

Container sizes:
  lg: 48px  (prominent interactive icon buttons)
  md: 40px  (standard icon buttons)
  sm: 32px  (compact icon buttons, avatar with icon)
  xs: 24px  (inline icon containers, tight UI)
```

---

## 4. Icon + Text Pairing

**Purpose:** Combine icons with text labels so they reinforce each other without competing.

**When to use:** Navigation items, buttons, list rows, badges, any element with both an icon and a label.

### Alignment

```
Vertical alignment options:
  Middle:    Icon and text share a horizontal center axis
             Best for single-line text and most navigation items

  Baseline:  Icon sits on the text baseline
             Useful for inline icons within body copy

  Cap-height: Icon center aligns to cap height (top of capital letters)
              Optical improvement for geometric icons next to text
```

**Default rule:** Middle alignment for UI components; never top or bottom alignment unless the text is multi-line.

### Spacing Between Icon and Label

```
xs (tight, badge):         4px
sm (standard inline):      8px
md (button with icon):     8px
lg (navigation with icon): 8–12px
```

### Icon Before or After Text

| Position | Use for |
|----------|---------|
| **Before (left)** | Leading icons that categorize (mail icon before email address) |
| **After (right)** | Trailing icons that indicate action (chevron for navigation, external link icon) |
| **Only icon** | When label is available via tooltip or adjacent context (icon buttons in toolbars) |

### When Icon-Only Works

Icon-only buttons are acceptable when:
- The metaphor is universally understood (close ×, settings gear, search magnifier, back arrow)
- The button has an accessible `aria-label`
- It's used in a context where repeated labels would feel redundant (toolbar, header row)

Icon-only buttons are NOT acceptable for:
- Primary CTAs (always include a text label)
- Actions that could be confused with other actions
- Novel metaphors or product-specific icons

---

## 5. Metaphor Selection

**Purpose:** Choose icon metaphors that users will immediately recognize based on universal conventions or context-specific patterns.

**When to use:** Selecting or designing any icon; icon audit.

### Universal Metaphors (Use Without Hesitation)

| Action | Metaphor |
|--------|---------|
| Search | Magnifying glass |
| Close / dismiss | × (multiply/cross) |
| Menu | Hamburger (≡) or dots (⋯) |
| Settings / configuration | Gear or sliders |
| Back navigation | Left arrow (LTR) |
| Add / create | Plus (+) |
| Delete / remove | Trash can |
| Edit | Pencil |
| Save | Floppy disk (legacy but universally understood) |
| Share | Upward arrow from box |
| Home | House |
| User / account | Person silhouette |
| Email | Envelope |
| Notification | Bell |
| Download | Downward arrow |
| Upload | Upward arrow |
| Favorite / bookmark | Star or bookmark ribbon |
| Visibility toggle | Eye / eye-slash |

### Domain-Specific Metaphors

Financial / crypto:
- Portfolio: chart or wallet
- Exchange: building or network nodes
- Gain: upward trend arrow
- Loss: downward trend arrow
- Security: shield or lock
- API key: key

### Metaphor Pitfalls

- **Floppy disk for save** — understood by adults; may not be by Gen Z — but still universal enough to use
- **Hamburger menu** — widely understood but can be missed by older users; always label it "Menu" on mobile
- **House for home** — occasionally confused with "real estate" in property apps — provide a label
- **Bell for notifications** — universally understood; safe
- **Gear for settings** — sometimes confused with "processing/loading" — ensure it's never animated

### Metaphor Testing

When uncertain, use a **5-second test:**
- Show the icon alone (no label) for 5 seconds
- Ask: "What would you expect to happen if you tapped this?"
- If fewer than 80% of users answer correctly → add a label or choose a clearer metaphor

---

## 6. Photo Selection & Curation

**Purpose:** Choose photography that reinforces brand tone, represents users authentically, and feels appropriate for the context.

**When to use:** Onboarding screens, marketing pages, empty states, hero sections, or any screen with people or contextual photography.

### Photo Selection Criteria

**Brand alignment:**
- Does the mood match the product's personality? (premium vs. accessible, technical vs. human)
- Does the lighting/color palette complement the UI's color system?
- Does it feel like the same visual world as other photos in the product?

**Representation:**
- Do photos reflect the actual diversity of users?
- Avoid tokenism — include diverse representation throughout, not just in one hero image
- Age, ability, and context diversity matters as much as race and gender

**Authenticity:**
- Avoid stock photo clichés: forced smiles, handshakes, people pointing at laptops
- Prefer candid-feeling moments, real tools, realistic settings
- People should look like they're actually doing the task shown

### Photo Treatment Consistency

Define treatments that unify diverse photos:

```
Color treatment:
  Tint overlay: semi-transparent brand color over photos
  Desaturate: reduce saturation to 0–30% (unifies varied photos)
  Color grade: apply LUT or consistent color curve

Crop:
  Aspect ratio: always 16:9 or 4:3 (never vary per photo)
  Subject placement: consistent (centered, left-weighted, etc.)
  Safe zone: face or key subject always in top 60% of frame

Blend:
  Dark overlay: for text readability over photos
  Edge fade: photo fades into background color at edges
```

### Photo Accessibility

- All meaningful photos must have descriptive alt text
- Decorative photos use `alt=""`
- Text overlaid on photos must pass 4.5:1 contrast (use overlay to ensure this)

---

## 7. Image Optimization

**Purpose:** Deliver images at the quality users expect while minimizing file size for fast load times.

**When to use:** Before shipping any image asset; during performance review.

### Format Selection

| Format | Use for | Notes |
|--------|---------|-------|
| **WebP** | Photos, complex images | 25–35% smaller than JPEG; use with JPEG fallback |
| **AVIF** | Photos (cutting edge) | 50% smaller than JPEG; browser support growing |
| **JPEG** | Photos, complex images | Universal fallback; no transparency |
| **PNG** | Graphics with transparency | Lossless; large for photos |
| **SVG** | Icons, logos, illustrations | Infinitely scalable; tiny for vector art |
| **GIF** | Avoid | Replace with video or CSS animation |

### Responsive Images

```html
<!-- srcset delivers the right size per viewport -->
<img
  src="hero-800.jpg"
  srcset="hero-400.jpg 400w,
          hero-800.jpg 800w,
          hero-1200.jpg 1200w"
  sizes="(max-width: 600px) 100vw,
         (max-width: 1200px) 50vw,
         800px"
  alt="Portfolio dashboard overview"
  loading="lazy"
  decoding="async"
>

<!-- Modern format with fallback -->
<picture>
  <source srcset="hero.avif" type="image/avif">
  <source srcset="hero.webp" type="image/webp">
  <img src="hero.jpg" alt="Portfolio dashboard overview">
</picture>
```

### File Size Targets

| Image type | Target size |
|------------|------------|
| Hero/full-width photo | < 200KB |
| Card/thumbnail photo | < 50KB |
| Avatar / user photo | < 20KB |
| Icon (SVG) | < 2KB |
| Logo (SVG) | < 5KB |
| Illustration (SVG) | < 10KB |

### Lazy Loading

```html
<!-- Native lazy loading — supported in all modern browsers -->
<img src="card-image.jpg" loading="lazy" alt="...">

<!-- Above-fold images: never lazy load -->
<img src="hero.jpg" loading="eager" alt="...">
```

---

## 8. Illustration Style

**Purpose:** Define a consistent illustration language that reinforces brand personality and communicates concepts visually.

**When to use:** Adding illustrations to empty states, onboarding, marketing, or error screens.

### Illustration Style Categories

| Style | Characteristics | Brand fit |
|-------|----------------|-----------|
| **Flat** | Solid colors, minimal gradients, geometric | Clean, modern, professional |
| **Isometric** | 3D perspective, precise angles | Technical, product-oriented |
| **Line art** | Outlined, minimal fill | Elegant, minimal, editorial |
| **Outlined + color fill** | Bold outlines with flat color inside | Friendly, approachable |
| **3D / render** | Photorealistic 3D objects | Premium, tech-forward |
| **Abstract / geometric** | Shapes and patterns, no people | Data, fintech, B2B |
| **Character-based** | People/mascots as central element | Consumer, friendly, B2C |

### Style Consistency Rules

Once a style is chosen, lock these properties:

```
Line weight:     consistent stroke width (1.5px, 2px, 3px — choose one)
Color palette:   max 4–6 colors from the product palette
Corner style:    round OR sharp — never mixed
People style:    consistent body proportions, skin tone range, facial detail level
Shadow style:    flat OR drop shadow at one consistent angle — not both
```

### Illustration Scale

Illustrations should scale across uses without losing quality:

```
Spot illustrations:   64×64 to 128×128px   — inline with content
Section illustrations: 200×200px+          — above content blocks
Hero illustrations:   400px+               — full-section backgrounds
Empty state:          160×160 to 240×240px — center of empty area
```

SVG is preferred for all illustrations under 100KB — infinitely scalable, tiny files.

---

## 9. Data Visualization

**Purpose:** Translate numerical data into visual representations that communicate patterns, comparisons, and trends faster than raw numbers.

**When to use:** Any dashboard, analytics feature, or screen with time-series, comparative, or statistical data.

### Chart Type Selection

| Data type | Chart type |
|-----------|------------|
| Change over time (single value) | Line chart, area chart, sparkline |
| Change over time (multiple values) | Multi-line, grouped area |
| Comparison of parts to whole | Pie chart (max 5 segments), donut chart |
| Comparison between categories | Bar chart (vertical or horizontal) |
| Distribution | Histogram, violin plot |
| Correlation between two variables | Scatter plot |
| Flow between states | Sankey diagram |
| Portfolio allocation | Stacked bar, treemap |
| Ranked list with value | Horizontal bar chart |
| Single metric at a glance | Stat card, gauge, number with trend |

### Chart Design Rules

**Simplify ruthlessly:**
- Remove grid lines (or make them very faint, ~10% opacity)
- Remove chart borders
- Remove unnecessary axis labels
- Remove legends when data is labeled directly
- Keep only the ink that communicates information

**Color in charts:**
- Use a single brand color for single-series charts
- Use sequential palette (light → dark of one hue) for intensity/magnitude
- Use diverging palette (e.g., red → white → green) for gain/loss or above/below baseline
- Use categorical palette for multi-series comparison (max 6 colors)
- Always test chart colors for colorblind accessibility

**Sparklines (inline charts):**
```
Purpose: At-a-glance trend within a list row or stat card
Size: 52–80px wide × 24–32px tall
No axes, no labels, no grid
Line color: brand accent or semantic color (green for up, red for down)
Filled area: very low opacity fill (8–12%) under the line
```

**Tooltips:**
```
Show on hover/press
Content: exact value + date/label
Position: above the data point, within chart bounds
Style: dark background, readable font, no border-radius excess
```

### Accessibility for Charts

- Provide a data table alternative for every chart (toggleable)
- Use ARIA label describing what the chart shows
- Ensure color is not the only differentiator (use labels or patterns too)
- Minimum tooltip text: 14px

---

## 10. Empty State Design

**Purpose:** Design the state of a screen before data exists — turning a potentially dead end into an orientation or onboarding opportunity.

**When to use:** Any list, dashboard, or content area that can be empty.

### Empty State Types

| Type | Trigger | Design approach |
|------|---------|----------------|
| **First-time / onboarding** | User has never used this feature | Welcome + explain value + primary CTA to get started |
| **User-cleared** | User deleted all items | Acknowledge + gentle recovery option |
| **No results** | Search/filter returns nothing | Acknowledge query + suggest alternatives |
| **Error** | Data failed to load | Acknowledge failure + retry action |
| **No permission** | User doesn't have access | Explain why + path to getting access |

### Empty State Structure

```
[Illustration or icon]   — humanizes the void (optional but recommended)
[Headline]               — short, active, direct: "No assets yet" not "Assets not found"
[Body copy]              — 1–2 sentences explaining context and what happens next
[Primary CTA]            — the action that fills the empty state
[Secondary link]         — optional: "Learn more" or "View documentation"
```

### Empty State Copy Tone

```
First-time:  Welcoming, encouraging
  "You're all set to track your first exchange.
   Connect an account to see your portfolio."

User-cleared: Neutral, acknowledging
  "You've removed all connected exchanges.
   Add one back to start tracking your portfolio again."

No results:  Helpful, constructive
  "No assets matching 'eth2'"
   Try 'ETH' or browse all assets below."

Error:       Honest, actionable (non-blaming)
  "We couldn't load your portfolio right now.
   Check your connection and try again."
```

### Illustration Guidance for Empty States

- Size: 160×160 to 240×240px centered above the headline
- Style: consistent with product illustration system
- Tone: matches the empty state type (friendly for onboarding, neutral for no-results)
- Avoid: sad/broken imagery for first-time empty states — it's not a failure yet

---

## 11. Placeholder Design

**Purpose:** Show meaningful loading states while content is being fetched, preventing layout shift and reducing perceived wait time.

**When to use:** Any content that loads asynchronously — lists, cards, images, profile data, dashboard stats.

### Skeleton Screen

A skeleton screen shows the layout structure with placeholder shapes before content arrives.

**Design rules:**
- Match the exact dimensions of the real content (prevents layout shift on load)
- Use a background color slightly lighter than the card surface
- Add a shimmer animation — a shine that sweeps left to right
- Never show loading spinners for skeleton-replaced areas — spinners imply system activity; skeletons imply content is coming

**Skeleton anatomy:**
```
Text placeholder:  rounded rectangle, full width or partial width, 8–12px height
Image placeholder: same aspect ratio as the real image
Avatar placeholder: circle at exact avatar size
Number placeholder: narrow rectangle at approximately number width
```

**Shimmer animation:**
```css
@keyframes shimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

.skeleton {
  background: linear-gradient(
    90deg,
    #1C1C1C 25%,
    #242424 50%,     /* slightly lighter — the "shine" */
    #1C1C1C 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: 4px;
}
```

### Spinner

Use a spinner (not skeleton) when:
- The action produces new content in an unpredictable location
- The wait time is expected to be very short (< 500ms)
- The existing layout doesn't have a predictable structure to mirror

**Spinner sizing:**
```
Large:  40px — full-page or section loading
Medium: 24px — card or container loading
Small:  16px — inline loading (button, input)
```

**Spinner color:** brand accent or `currentColor` (inherits text color)

### Loading Text

For operations where duration is uncertain:
```
< 2 seconds:  No text — spinner alone
2–5 seconds:  "Loading your portfolio..."
5–10 seconds: "This is taking longer than usual..."
10+ seconds:  "Still working... you can keep using the app" + ability to cancel
```

### Image Placeholders

While images load:
- Use a `background-color` matching the dominant color of the expected image (if known)
- Or use a generic skeleton placeholder at the exact image dimensions
- Use `loading="lazy"` for below-fold images
- Set explicit `width` and `height` attributes to prevent layout shift
