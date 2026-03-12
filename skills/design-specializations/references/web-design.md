# Web Design Specializations

## Table of Contents
1. [Above-the-Fold Strategy](#1-above-the-fold-strategy)
2. [Form Design](#2-form-design)
3. [Table Design](#3-table-design)
4. [Dashboard Design](#4-dashboard-design)
5. [E-commerce](#5-e-commerce)
6. [Content-Heavy Sites](#6-content-heavy-sites)

---

## 1. Above-the-Fold Strategy

**Purpose:** Maximize the value of the first viewport — the content visible before the user scrolls — by answering the user's key questions immediately and giving them a reason to stay.

**When to use:** Designing landing pages, homepages, campaign pages, or any page where the first impression determines whether users engage or leave.

### The 5-Second Rule

```
A user decides whether to stay or leave in ~5 seconds.
In that time, the above-fold area must answer:
  1. What is this?
  2. What can I do here?
  3. Is this for me?
  4. What do I do next?

If any of these questions go unanswered, bounce rate increases.
```

### Above-Fold Layout Priorities

```
Priority 1 — Value proposition (always visible)
  Headline: What the product does + for whom (8 words or fewer)
  Subheadline: Supporting context (one sentence)
  These two lines must be visible without scrolling on every device.

Priority 2 — Primary CTA (always visible)
  One primary action. Not two equal CTAs.
  Positioned immediately below or beside the headline.
  High contrast, large touch target (min 44px height).

Priority 3 — Trust signal or social proof (if space allows)
  "10,000 portfolios tracked" or logos of known customers/press.
  Below headline and CTA, still within first viewport on desktop.

Priority 4 — Hero visual (supports the headline)
  Shows the product, the outcome, or the user in context.
  Never: stock photo of people smiling.
  Always: real product screenshot, illustration of outcome, or video.

What does NOT belong above the fold:
  Navigation with 8 items
  Legal/compliance text
  Detailed feature explanations
  Multiple competing CTAs
  Auto-playing video with sound
```

### Viewport-Based Design

```
Design for the actual viewport, not an imagined canvas.

Desktop above fold:
  1440×900px (common laptop): ~860px visible height after browser chrome
  Design: Header (~60px) + hero (~780px)
  Everything above 900px = guaranteed above fold for this device

Mobile above fold:
  375×812px (iPhone standard): ~720px visible height
  The entire value proposition + CTA must fit in this 720px.
  Test: hide everything below 720px — does the page still make sense?

The "false bottom" problem:
  Design that looks complete at the fold (no visual cue to scroll).
  Users think they've seen everything and leave.
  Fix: Content that bleeds past the fold edge encourages scrolling.
  Fix: Arrow indicator or partial next section visible.
```

### Hero Section Patterns

**Hero + CTA (standard):**
```
Left: Headline + subhead + CTA
Right: Product screenshot or illustration
Works for: SaaS, apps, B2B
```

**Full-width video/image background:**
```
Overlay text on image/video
Works for: Consumer brands, luxury, hospitality
Danger: Text legibility over video — always add text shadow or overlay
```

**Split screen:**
```
Left half: For one type of user (or before state)
Right half: For another type (or after state)
Works for: Two-sided markets, before/after comparisons
```

**Centered hero:**
```
Everything centered: logo, headline, subhead, CTA
Clean, premium feeling. Works for: Luxury, minimalist products
```

### Outputs
- Hero wireframe with priority mapping (1–4 above)
- 5-second test specification (what must be readable without scrolling)
- Desktop + mobile viewport comparison

---

## 2. Form Design

**Purpose:** Design forms that users can complete accurately, quickly, and without frustration — minimizing abandonment through clear labeling, sensible structure, and helpful validation.

**When to use:** Any data collection interface — registration, checkout, settings, onboarding, API key entry.

### Form Design Principles

**1. Ask only what you need**
```
Every field is a cost. Remove fields that:
  - The system can infer (country from IP address)
  - Can be asked later (profile photo on signup)
  - Are "nice to have" but not required

If removing a field would break the process: keep it.
If removing it would just be slightly less ideal: cut it.
```

**2. One column layout**
```
Multi-column forms increase errors and cognitive load.
Exception: Truly related short fields (first name + last name, month + day + year).
Rule: If fields are separate concepts, separate rows.
```

**3. Label placement**
```
Above the input (recommended):
  Most accessible, most scannable
  Labels remain visible while user types

Inside the input (placeholder):
  Disappears when typing — user forgets what the field is for
  Never use placeholder as a label replacement
  Use placeholder for: format hints ("AAAA-BBBB"), not labels

Inline right (for short forms):
  Labels right-aligned on the left, inputs on the right
  Only works for short, simple forms (< 5 fields)
```

**4. Appropriate input types**
```
Use the right input for the data:
  text:     Name, street address, search
  email:    Email address (mobile shows @ keyboard)
  tel:      Phone number (mobile shows numeric keyboard)
  number:   Numeric values with +/- stepper
  password: Secure text input
  date:     Date picker (avoid — native pickers are inconsistent)
  select:   Choose from a predefined list (< 7 options: radio buttons instead)
  checkbox: Multiple selections from a list
  radio:    Single selection from a list (< 7 options: use radio, not select)
  textarea: Free-text multi-line content
```

### Multi-Step Forms

```
When to use:
  Many fields (> 7–8 fields)
  Logical grouping exists (personal info → address → payment)
  Progressive disclosure (later steps depend on earlier answers)

Step structure:
  Progress indicator: "Step 2 of 4" or visual step dots
  One logical group per step — not one field per step (too many taps)
  Back always available — never trap users in a step
  Validation: Validate on step transition, not on final submit

Best practices:
  Name each step ("Account", "Connect Exchange", "Review")
  Show estimated total (4 steps, ~2 min)
  Save progress: Returning user sees where they left off
  Never lose data on back navigation
```

### Form Validation

```
Validation timing:
  On submit: Show all errors together (simple, but worst UX for long forms)
  On blur (leaving field): Validate when user leaves a field
    → Catches errors early without interrupting typing
    → Best for most fields
  On change (while typing): Only for length limits, character counts
    → Don't show errors while user is mid-type

Error display:
  Position: Directly below the field (not above, not in a toast)
  Color: Red text + red border on the field
  Icon: Warning icon + text (not just color — accessible)
  Message: Specific and actionable
    ✅ "Enter a valid email address (example: you@example.com)"
    ❌ "Invalid input"
    ❌ "Error"

Success indicator:
  Green checkmark beside field when valid
  Only show after the field has been touched (not on load)

Password strength:
  Real-time strength meter while typing
  Specific requirements visible (not shown after error):
    "At least 8 characters ✓"
    "One uppercase letter ✓"
    "One number —"

Auto-format:
  Phone: Format as user types (555) 555-5555
  Credit card: Space-group digits: 4242 4242 4242 4242
  Date: Auto-advance between MM / DD / YYYY fields
```

### Autofill Design

```
Enable browser/system autofill:
  <input name="email" autocomplete="email">
  <input name="given-name" autocomplete="given-name">
  <input name="cc-number" autocomplete="cc-number">

Common autocomplete values:
  email, username, new-password, current-password
  name, given-name, family-name
  address-line1, city, postal-code, country
  tel, cc-number, cc-exp, cc-csc

iOS Autofill:
  Correct autocomplete attributes → iOS shows suggested keyboard accessory
  Username + password: iOS Keychain suggests saved credentials
  Credit card: iOS suggests saved card from Wallet

Never disable autocomplete — it's an accessibility and usability feature.
```

### Outputs
- Form wireframe with field-type specifications
- Validation state designs (error, success, in-progress)
- Multi-step flow with progress indicator
- Autocomplete attribute spec for each field

---

## 3. Table Design

**Purpose:** Display structured, data-dense information in a way that supports scanning, comparison, sorting, and filtering — without overwhelming the user.

**When to use:** Displaying lists of records with multiple attributes (transactions, users, orders, inventory, analytics).

### Table Anatomy

```
Table structure:
  Header row: Column labels, sticky on scroll (for long tables)
  Data rows: One record per row
  Footer: Totals, aggregates, pagination

Column types:
  Text:      Left-aligned, truncated at max width
  Number:    Right-aligned, monospace font (so decimal points align)
  Currency:  Right-aligned, monospace, formatted ($1,234.56)
  Date/time: Right-aligned (or center for short dates)
  Status:    Badge/chip, center-aligned
  Actions:   Right-aligned, icon buttons
  Boolean:   Checkbox or icon (✓/—), center-aligned
```

### Typography in Tables

```
Use tabular (monospace) figures for all numbers in tables.
Regular proportional digits:  1,234  (1 and 4 are different widths)
Tabular figures:               1,234  (all digits equal width → columns align)

CSS: font-variant-numeric: tabular-nums;
     font-feature-settings: "tnum";

This is critical for financial data — misaligned decimal points cause errors.
```

### Sorting and Filtering

```
Column sorting:
  Click column header → sort ascending/descending
  Visual: Arrow icon in header (up/down, sorted/unsorted)
  Default: Unsorted shows unfilled double-arrow icon
  Active sort: Filled arrow + header text slightly darker/bolder

Multi-column sort:
  Advanced use case — hold Shift + click second column
  Show sort priority: "1st" / "2nd" badges on column headers
  For most products: single-column sort is sufficient

Filtering:
  Column filter (inline): Filter icon in column header → popover
  Filter bar (global): Above the table, chips show active filters
  Search: Full-text search across all columns

Active filter indicators:
  Show filter chips above table: "Exchange: Binance × | Date: Last 30 days ×"
  Clear all button when any filters are active
  Show filtered count: "Showing 23 of 147 transactions"
```

### Row States and Interaction

```
Hover:  Subtle background highlight — shows which row cursor is on
        Color: 4–6% opacity overlay

Selected: More distinct background — user explicitly selected this row
          Checkbox appears, row highlighted more strongly

Expanded: Row expands to show detail (accordion pattern)
          Use when detail data would create too many columns

Clickable rows:
  If the entire row is clickable: show hover cursor
  If only some cells are clickable (links, actions): show cursor on those

Striped rows (zebra):
  Alternating row backgrounds for very long, data-dense tables
  Not needed for short tables (< 10 rows) or card-based layouts
  Subtle: one step lighter/darker, not distractingly different
```

### Empty, Loading, and Error States

```
Empty table:
  Show column headers (maintains visual structure, tells user what data would appear)
  Empty state in the body area (not replacing the whole table)
  "No transactions yet. Connect an exchange to start tracking."
  CTA if there's an action that would populate the table

Loading table:
  Skeleton rows matching the number expected (or 5 if unknown)
  Skeleton cells: proportional widths matching actual data
  Column headers: show real labels (not skeleton)

Error state:
  Show error message in the table body area
  Retry button
  Keep column headers visible
```

### Responsive Tables

```
Tables are the hardest UI element to make responsive.
Options:

1. Horizontal scroll (simplest):
   Table overflows horizontally; container scrolls.
   Works for: Data-heavy tables where comparison matters.
   Problem: Users may not discover horizontal scroll.

2. Priority columns (recommended):
   At narrow widths, hide lower-priority columns.
   Show "column picker" to restore hidden columns.
   Rule: Always keep identifier column (name, ID) + 1–2 most important.

3. Card view for mobile:
   On mobile, each row becomes a card with label + value pairs.
   Works for: Most tables. But loses direct row comparison.

4. Expand-for-details:
   Mobile shows 2 columns; tapping a row reveals full detail view.
```

### Outputs
- Table component with all column types
- Sort/filter state designs
- Empty, loading, error states
- Responsive strategy (which columns hide at which breakpoints)

---

## 4. Dashboard Design

**Purpose:** Give users a fast, comprehensive picture of their most important metrics — enabling quick understanding of the current state and identification of what needs attention.

**When to use:** Any interface where multiple metrics, KPIs, or data summaries need to be displayed simultaneously.

### Dashboard Design Principles

**1. Answer one question first**
```
Every dashboard should answer the user's primary question instantly.
Define it before designing:
  Nexus: "What is my total portfolio worth right now, and how is it doing?"
  Analytics tool: "What's happening with my users today?"
  Operations: "Is everything working? What's broken?"

The metric that answers this question gets the most visual weight.
```

**2. Information hierarchy: summary → detail**
```
Layer 1: Key metrics at a glance (top of page)
  Large numbers, single values, trend indicators
  Answerable in < 3 seconds

Layer 2: Context and breakdown (middle)
  Charts, tables, comparisons
  Answerable in < 30 seconds

Layer 3: Detail and drill-down (bottom or in modals)
  Full data, filtering, export
  Used by power users for deep analysis
```

**3. Show changes, not just values**
```
A number alone is often meaningless without context.
Always accompany KPIs with:
  Change vs. previous period: "+$1,234 (3.4%) today"
  Trend: Sparkline showing 7-day/30-day trajectory
  Benchmark: "vs. last week" or "vs. industry average"
  Status: Is this good, neutral, or bad? (color coding)
```

### KPI Card Design

```
Anatomy of a KPI card:
  ┌─────────────────────────────┐
  │ TOTAL PORTFOLIO VALUE       │  ← Section label (TypeScale.label)
  │                             │
  │ $84,473.34                  │  ← Primary metric (large, monospace)
  │                             │
  │ ▲ +$2,839 +3.48% today      │  ← Change indicator (colored)
  │                             │
  │  ▁▂▃▄▅▆▇█  (sparkline)      │  ← Trend visualization
  └─────────────────────────────┘

Sizing:
  Primary metric: largest text on the card (TypeScale.numeric.xl or lg)
  Label: small, muted, uppercase (TypeScale.label.md)
  Change: medium, colored (green/red)
  Sparkline: 40–52px height, full card width

Grid:
  2–4 KPI cards per row on desktop
  1 card per row on mobile (stacked)
  Equal width; consistent height
```

### Chart Selection for Dashboards

```
Time series (line chart): "How is X changing over time?"
  Use for: Portfolio value, daily active users, revenue trend

Composition (area chart, stacked bar): "What makes up X?"
  Use for: Asset allocation, traffic sources

Distribution (bar chart): "How do values compare across categories?"
  Use for: Holdings by exchange, performance by asset

Part-of-whole (donut/pie): "What percentage is X of the total?"
  Use for: Portfolio allocation, traffic channel split
  Limit: 5 slices max; label slices directly (not legend only)

Scatter: "Is there a relationship between X and Y?"
  Use for: Risk vs. return, correlation analysis

Don't use the wrong chart:
  Pie chart with 8 slices: Use bar chart instead
  Bar chart for time series: Use line chart instead (time is continuous)
  3D charts: Never — distort values, reduce readability
```

### Dashboard Layout Patterns

```
Pattern 1: Big number + chart (single-metric focus)
  Massive KPI card at top; chart below
  Use for: Single-purpose dashboards

Pattern 2: KPI row + charts below
  Row of 3–4 KPI cards at top
  Larger charts occupying most of the page
  Use for: Analytics, financial dashboards (Nexus pattern)

Pattern 3: Grid/bento
  Asymmetric grid of cards at different sizes
  Use for: Operations dashboards, monitoring
  Risk: Complex to design; can feel cluttered

Pattern 4: Left sidebar + main content
  Navigation on left; main charts fill center
  Use for: Complex dashboards with many sections
```

### Dashboard Performance Considerations

```
Data freshness indicators:
  Show when data was last updated: "Updated 2 min ago"
  Loading states for each chart independently (not full-page spinner)
  Stale data indicator if update fails

Density vs. clarity trade-off:
  More data = more cognitive load
  Rule: Users can process ~7 independent data points simultaneously
  Group related metrics into single cards or sections
  Progressive disclosure: show top-level → let users drill into detail

Print/export mode:
  Dashboards get screenshot/exported frequently
  Design export styles: white background, no gradients that don't print
  "Export PDF" button with clean print stylesheet
```

### Outputs
- Dashboard wireframe with hierarchy mapped (Layer 1/2/3)
- KPI card component with all variants
- Chart selection for each metric
- Loading state for each section (not full-page)

---

## 5. E-commerce

**Purpose:** Design product discovery, product detail, and checkout flows that reduce friction, build trust, and guide users from intent to purchase.

**When to use:** Any transaction flow — physical products, digital goods, subscriptions, or marketplace experiences.

### Product Page Design

```
Above-fold requirements (product page):
  Product name (clear, prominent)
  Price (immediately visible, formatted correctly)
  Primary image (large, zoomable)
  Primary CTA ("Add to cart" or "Buy now") visible without scrolling

Product image gallery:
  Primary image: 60–70% of above-fold width on desktop
  Thumbnails: Below or beside primary image
  Zoom: Click to zoom or magnifying glass icon
  Mobile: Swipeable carousel, dots indicator

Product information hierarchy:
  1. Name + price (always first)
  2. Key selling point (1–2 lines — not a paragraph)
  3. Variants (size, color, quantity) — before CTA
  4. CTA (Add to cart / Buy now)
  5. Social proof (reviews, ratings, "X people bought this today")
  6. Detailed description (long, below the fold)
  7. Specifications, FAQs, reviews (tabbed or sectioned below description)
```

### Checkout Flow Design

```
Checkout steps (ideal):
  1. Cart review → 2. Contact/Account → 3. Shipping → 4. Payment → 5. Confirmation

Guest checkout:
  Always offer. Forcing account creation kills conversions.
  Offer account creation AFTER successful purchase ("Save your info for next time?")

Progress indicator:
  Show current step + total steps
  Completed steps: clickable to go back (allow editing)
  Future steps: greyed out, not clickable yet

Each step:
  One task per page (not all in one long form)
  Autofill enabled (billing, shipping, payment details)
  Default values where possible (country from locale, billing = shipping)
  Inline validation — don't surface errors only on submit

Payment page:
  Security signals: SSL badge, accepted payment logos
  Summary sidebar: Order contents + total (sticky on scroll)
  Payment fields: Card number autofills from device wallet
  "Place order" CTA: Clear, final, summarizes the total amount charged
```

### Trust Signals for E-commerce

```
Product page:
  Star ratings + review count (visible near price)
  In-stock indicator ("Only 3 left" for urgency, but honest)
  Return policy (near the CTA — reduces perceived risk)
  "X people viewing this" (social proof — use sparingly, not fake)

Checkout:
  Security badge: "256-bit SSL encrypted"
  Payment logos: Visa, Mastercard, PayPal, Apple Pay
  Guarantee: "30-day money-back guarantee"
  Privacy note: "We never sell your information"

Post-purchase:
  Order confirmation email within minutes
  Tracking information as soon as available
  Easy returns link in confirmation
```

### Cart Design

```
Mini-cart (slide-in panel): Appears on "Add to cart" without leaving page.
  Contents: Product thumbnail, name, quantity stepper, remove, subtotal.
  CTA: "View cart" + "Checkout" (two options — respect user intent).
  Don't: Auto-navigate away from the page — user may want to keep browsing.

Full cart page:
  Edit quantity inline (stepper, not a form submit)
  Remove item (× button, immediate — no confirmation dialog for removing)
  Save for later (optional)
  Promotions/coupon code field (collapsed by default — expanding on click)
  Order summary: Subtotal, shipping, tax, total
  CTA: Large, full-width on mobile "Proceed to checkout"

Empty cart:
  Icon + "Your cart is empty"
  CTA: "Continue shopping" → back to catalog
  Optionally: "You might like these" product recommendations
```

### Outputs
- Product page layout with hierarchy
- Checkout flow diagram with step-by-step states
- Cart component (mini + full)
- Trust signal placement map

---

## 6. Content-Heavy Sites

**Purpose:** Design reading experiences for articles, documentation, blogs, and knowledge bases that optimize for comprehension, scanning, and extended reading without fatigue.

**When to use:** Editorial sites, documentation, blogs, long-form content products, knowledge bases, help centers.

### Reading Experience Fundamentals

```
Optimal reading line length: 60–75 characters per line
  Too short (< 45 chars): Eye moves too frequently — tiring
  Too long (> 85 chars): Eye has trouble tracking back to start of next line
  CSS: max-width: 70ch; (ch unit = width of "0" in current font)

Line height for body text:
  Default (1.0): Cramped, hard to read
  Optimal: 1.5–1.6 for body text (24–26px for 16px base)
  Headings: 1.1–1.2 (tighter — short lines don't need as much leading)

Font size for comfortable reading:
  Minimum: 16px for body text on screen
  Better: 18–20px for long-form reading (books, articles, documentation)
  Subtext/captions: 14px minimum
```

### Article Layout Structure

```
Article anatomy:
  1. Meta: Category/tag + date + author (small, above headline)
  2. Headline: Large, specific, compelling
  3. Byline: Author name + photo + reading time
  4. Hero image (optional): Caption below
  5. Introduction: 2–3 sentences (the hook)
  6. Body content
  7. Author bio + related articles (below content)

Content width:
  Narrow column (660–740px): Body text — optimal reading width
  Wide column (full page or 1200px): Images, code blocks, tables, wide media

Two-column layout:
  Main column (70%): Body content
  Sidebar (30%): Table of contents, related articles, ads, tags
  On mobile: Sidebar moves below content or into accordion

Table of contents (long articles):
  Sticky sidebar on desktop (scrolls with the page)
  Inline at top on mobile
  Active section highlighted as user scrolls (scroll-spy)
  Collapsible on desktop if article is short
```

### Typography for Long-Form Reading

```
Serif vs. Sans-serif:
  Serifs: Traditional for print; studies are mixed for screen
    Better for: Dense text, book-like reading, premium/editorial feel
  Sans-serif: Cleaner on screen; easier to read in smaller sizes
    Better for: Documentation, UI text, smaller sizes

Font pairings for content sites:
  Heading + body from same family: Consistent, clean (Google uses Roboto/Roboto)
  Contrasting pair: Serif heading + sans body (NY Times, Medium style)

Contrast for extended reading:
  Not pure black (#000) on pure white (#fff) — reduces eye strain
  Soft black (#111, #1a1a1a) on off-white (#fafafa, #f8f8f8)
  Dark mode: Off-white text (#e8e8e8) on dark gray (#0d0d0d), not pure white on black

Heading hierarchy in articles:
  H1: Article headline (once per page)
  H2: Major sections (what a reader would see in a TOC)
  H3: Sub-sections
  H4: Rarely needed — consider restructuring instead
  Bold within paragraphs: Key terms, not decorative emphasis
```

### Scan-Friendly Content Design

```
Users scan before they read. Design for scanning first:

Visual anchors that aid scanning:
  Pull quotes: Key sentences styled larger and set off from body
  Callout boxes: Highlighted notes, warnings, tips
  Numbered/bulleted lists: Make parallel ideas scannable
  Bold text: First sentence of a paragraph, key term (don't over-bold)
  Subheadings: Every 300–400 words max — break up long sections
  Images: Break up text walls, reinforce concepts

What breaks scanning:
  Long paragraphs (> 5 lines)
  No subheadings for 800+ word sections
  Dense text with no visual hierarchy
  Walls of identical-weight text

Code blocks (documentation):
  Monospace font (code blocks should never use body font)
  Syntax highlighting
  Line numbers for long snippets
  Copy button (absolute top-right of block)
  Horizontal scroll for long lines (not word-wrap that breaks code)
```

### Performance and Reading Environment

```
Font loading:
  Preload critical fonts: <link rel="preload" as="font">
  System font fallback: Prevents FOUT (Flash of Unstyled Text)
  Variable fonts: One file for all weights — better performance

Dark mode for reading:
  Provide a dark mode toggle — readers often read at night
  System preference: @media (prefers-color-scheme: dark)
  Persist preference: localStorage

Reading progress:
  Progress bar at top of page (thin, 2–4px)
  "X min read" in the meta — helps users decide to commit
  Don't show word count — less intimidating than numbers

Print styles:
  @media print { ... }
  Hide: navigation, sidebar, ads, comments, forms
  Show: article content, images, captions, author
  Black text on white (no dark backgrounds)
  Full-width content (no narrow column constraint)
```

### Outputs
- Article layout with optimal line length + typography
- Reading environment (dark mode, font size control)
- Scan-friendly content component library (pull quotes, callouts, code blocks)
- Print stylesheet
