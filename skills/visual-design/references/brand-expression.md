# Brand Expression Methods

## Table of Contents
1. [Brand System Design](#1-brand-system-design)
2. [Style Guide Creation](#2-style-guide-creation)
3. [Design Language Development](#3-design-language-development)
4. [Tone & Voice](#4-tone--voice)
5. [Marketing Design](#5-marketing-design)

---

## 1. Brand System Design

**Purpose:** Create a cohesive visual identity that communicates a consistent brand across all surfaces — app, web, print, and motion.

**When to use:** New brand or product launch; rebranding; when visual inconsistency is eroding brand trust.

### Brand System Components

```
Foundation
  └── Logo system (primary, secondary, icon mark, wordmark)
  └── Color palette (primary, secondary, accent, neutrals, semantic)
  └── Typography (display, body, mono — with rules for each)
  └── Spacing and grid

Expression
  └── Iconography style
  └── Illustration style and rules
  └── Photography treatment
  └── Data visualization palette

Motion
  └── Animation principles (easing curves, duration ranges)
  └── Transition vocabulary (what kinds of movement represent the brand)

Voice
  └── Tone and personality traits
  └── Vocabulary and copy rules
```

### Brand Positioning → Visual Translation

Every brand has a position; the visual system must express it:

| Brand position | Visual expression |
|----------------|------------------|
| Premium / luxury | Dark palette, generous whitespace, refined serif, minimal UI chrome |
| Trustworthy / institutional | Conservative palette (blue), clean sans, structured grid |
| Friendly / approachable | Warm colors, rounded forms, illustrated elements, generous touch targets |
| Technical / precise | Monospace accents, strict grid, data-dense layouts, muted palette |
| Bold / disruptive | High-contrast palette, large type, asymmetric layouts, strong accent |
| Modern / minimal | Extreme whitespace, one typeface, limited palette, geometric forms |

### Logo System Rules

**Clear space:** Minimum clear space around the logo = height of the letter 'x' in the wordmark on all sides.

**Minimum size:** Define the smallest size at which the logo remains legible:
- Primary logo (with wordmark): min 120px wide
- Icon mark (standalone): min 24px wide

**Variations to define:**
```
1. Primary (color on white/light background)
2. Reversed (white on dark/color background)
3. Monochrome (black only)
4. Monochrome reversed (white only)
5. Icon mark only (for favicon, app icon, small contexts)
6. Horizontal vs. stacked arrangement (if applicable)
```

**Logo misuse to document:**
- Don't stretch or distort
- Don't apply drop shadows
- Don't use on busy backgrounds without sufficient contrast
- Don't use brand colors not approved for logo contexts
- Don't recreate the logo from scratch — always use approved assets

### Brand Consistency Across Surfaces

| Surface | Primary brand expression |
|---------|-------------------------|
| Mobile app | Color palette, typography, iconography, motion |
| Web | Full system including photography and illustration |
| Email | Logo, color, typography (web-safe fallbacks) |
| Social media | Color, logo, photography treatment, illustration |
| Print | Full system + print-specific color profiles (CMYK) |
| Motion/video | Color, typography, animation principles |

### Outputs
- Logo assets in all formats (SVG, PNG, AI) at all sizes
- Brand color system with hex, RGB, HSL, CMYK, and Pantone values
- Brand typography specification with weights and usage rules
- Brand asset library organized by surface and format
- Misuse examples to prevent common violations

---

## 2. Style Guide Creation

**Purpose:** Document design standards in a reference that enables designers, developers, and content creators to apply the brand consistently without needing to ask.

**When to use:** After the brand system is defined; when team members or agencies need to implement the brand; before scaling design work across multiple contributors.

### Style Guide Structure

```
1. Introduction
   - Brand overview (mission, values, personality)
   - How to use this guide
   - Who to contact for questions

2. Logo
   - Versions and file formats
   - Clear space rules
   - Minimum sizes
   - Correct and incorrect usage (with examples)

3. Color
   - Primary palette with all color values (hex, RGB, HSL, CMYK, Pantone)
   - Secondary and accent colors
   - Semantic colors (success, warning, error, info)
   - Color usage rules (what to use where)
   - Dark mode / light mode variants

4. Typography
   - Type families and where to download/license
   - Type scale (all sizes with sizes and line heights)
   - Usage rules per level (when to use display, title, body, etc.)
   - Font pairing rules
   - Examples of correct type hierarchy

5. Spacing & Grid
   - Spacing scale
   - Grid definition (columns, gutters, margins)
   - Usage examples

6. Iconography
   - Icon library or source
   - Style rules (stroke weight, size, color)
   - Correct usage examples

7. Imagery
   - Photography style and selection criteria
   - Illustration style and rules
   - Do's and don'ts with examples

8. Voice & Tone
   - Brand personality traits
   - Copy rules
   - Example before/after rewrites

9. Components (UI style guide only)
   - Core components with states
   - Usage guidelines

10. Motion (if applicable)
    - Animation principles
    - Duration and easing reference
```

### Style Guide Format Considerations

**Living document (recommended):** Hosted online (Notion, Zeroheight, Storybook) — always current, searchable, linkable.

**PDF/static:** Snapshot in time — useful for external agencies with no system access, but becomes outdated.

**Code-adjacent:** Style guide lives alongside the codebase (Storybook) — design and implementation are always in sync.

### What Makes a Good Style Guide

- **Examples, not just rules** — show correct usage, not just describe it
- **Do / Don't pairs** — side-by-side comparisons are faster to internalize than text descriptions
- **Rationale** — explain why rules exist; people follow rules they understand
- **Searchable** — a style guide no one can find is no style guide
- **Owned** — someone is responsible for keeping it current

### Outputs
- Complete style guide document (digital or PDF)
- Asset downloads embedded throughout (never link externally only)
- Changelog of updates
- Feedback/request channel for contributors

---

## 3. Design Language Development

**Purpose:** Define the principles, values, and rules that guide every design decision — creating a coherent aesthetic point of view that distinguishes the product.

**When to use:** Starting a new product; when designs feel inconsistent across screens or contributors; when the team lacks a shared design vocabulary.

### Design Language Components

**Principles** — 3–5 statements that define the philosophy behind all design decisions:

```
Good principle format:
  [Adjective that captures the principle]
  [1–2 sentences explaining what it means in practice]
  [How to apply it, with one example]

Example:
  "Numbers first"
  In a financial app, every screen must ask: what is the most important number?
  That number gets maximum visual weight; everything else supports it.
  Example: Portfolio value is always the largest element on the dashboard.
```

**Personality traits** — 4–6 adjectives describing the brand's design character:
```
Examples:
  Precise, Transparent, Confident, Human, Dark, Technical
  → Each trait becomes a filter: "Is this design decision Precise? Transparent?"
```

**Aesthetic direction** — the visual style and mood that runs through all surfaces:
```
Decision: Dark, data-dense, financial precision aesthetic
→ Drives: dark backgrounds, monospace numerics, tight spacing, minimal decoration
→ Opposes: colorful gradients, illustration-heavy, playful curves
```

**Motion language** — how the product moves:
```
Functional motion:  transitions that communicate state changes
  - Enter/exit: elements arrive purposefully (fade + translate, not pop)
  - Loading: skeleton shimmer, not blank flashes
  - Feedback: immediate and proportionate to action weight

Prohibited motion:
  - No arbitrary decorative animations
  - No motion that delays the user's primary goal
  - No infinite animation loops on content screens
```

### Design Principles Anti-patterns

**Bad principle:** "Be user-friendly" — too vague, can't make a decision from it

**Bad principle:** "Use consistent spacing" — that's a rule, not a principle

**Good principle:** "Show, don't summarize" — when data can be visualized, visualize it. Avoid descriptions of what the chart shows in text form.

**Good principle:** "Earn every pixel" — no decorative element survives without justifying its presence. If removing it doesn't break anything, remove it.

### Making Principles Actionable

For each principle, define:
1. A decision the principle helps make
2. A specific example of following it
3. A specific example of violating it

This transforms abstract values into a daily design tool.

### Outputs
- 3–5 design principles with rationale and examples
- Personality trait set with do/don't examples
- Aesthetic direction brief
- Motion language reference

---

## 4. Tone & Voice

**Purpose:** Define how the brand sounds in every piece of interface text — and how that voice adapts to different emotional contexts.

**When to use:** Establishing a new product; when copy feels inconsistent or off-brand; before writing microcopy, onboarding, or marketing copy.

### Voice vs. Tone

**Voice** — consistent brand personality; doesn't change
**Tone** — adapts to context; the mood adjusts while the personality stays the same

```
Example: A person with a consistent voice can be:
  Encouraging in onboarding ("You're almost there!")
  Direct in error states ("That card was declined.")
  Serious in security contexts ("This action can't be undone.")

The voice (confident, clear, human) stays constant.
The tone (encouraging / direct / serious) shifts by context.
```

### Voice Definition

Define 3–5 voice characteristics, each with two dimensions:

```
We are [X]         but not [Y]
──────────────────────────────────────────
Confident          but not arrogant
Clear              but not dumbed down
Human              but not casual
Direct             but not blunt
Knowledgeable      but not jargon-heavy
```

This "but not" structure prevents one-sided interpretations that take the voice too far.

### Tone by Context

| Context | Tone | Example |
|---------|------|---------|
| Onboarding | Warm, encouraging, brief | "You're all set. Your portfolio is live." |
| Success | Affirming, brief | "Payment sent." |
| Error | Calm, specific, actionable | "That address wasn't found. Check the format and try again." |
| Destructive action | Direct, factual, neutral | "This will permanently delete all data in this exchange." |
| Empty state | Inviting, forward-looking | "No transactions yet. Connect an exchange to start tracking." |
| Security / legal | Clear, transparent, no jargon | "Your API keys are encrypted and never shared." |
| Loading | Neutral, unobtrusive | "Loading your portfolio…" |

### Copy Rules

Linguistic rules that define the brand voice in text:

```
Active voice:
  ✅ "We saved your changes."
  ❌ "Your changes have been saved."

First person (where appropriate):
  ✅ "Can't find your account? Let us help."
  ❌ "Users experiencing issues should contact support."

Action-first CTA labels:
  ✅ "Connect exchange"
  ❌ "Exchange Connection"

Plain English, never jargon:
  ✅ "Your API key gives Nexus read-only access to your exchange."
  ❌ "OAuth2 bearer token authorization has been granted."

Short sentences:
  ✅ "Something went wrong. Try again."
  ❌ "We encountered an unexpected error while processing your request, and we apologize for the inconvenience."
```

### Vocabulary List

Maintain a canonical vocabulary — the words the brand uses and avoids:

```
Use:          Not:
Portfolio     Wallet (we're not a wallet)
Connect       Link / Authorize / Integrate
Exchange      Platform / Exchange platform
Holdings      Balance / Crypto / Assets (too generic)
Read-only     View-only / Non-custodial (jargon)
Refresh       Sync / Update (too technical)
```

### Outputs
- Voice definition with "X but not Y" statements
- Tone guide by context
- Copy rules with before/after examples
- Vocabulary list (use this / not that)

---

## 5. Marketing Design

**Purpose:** Design landing pages, promotional materials, and marketing surfaces that attract, convert, and build brand equity — extending the product's visual identity into acquisition contexts.

**When to use:** Building a marketing site, landing page, onboarding emails, promotional campaigns, or App Store assets.

### Marketing vs. Product Design

| Dimension | Marketing design | Product design |
|-----------|-----------------|----------------|
| Goal | Attract and convert | Retain and enable |
| Audience | Prospective users | Existing users |
| Density | More breathing room | More efficient |
| Tone | Bold, aspirational | Clear, functional |
| Fidelity | Often higher visual polish | Functional > decorative |
| Motion | Scroll-triggered reveals | Feedback animations |

Marketing design can stretch the brand further than product design — more expressive typography, more dramatic layouts, more elaborate effects — while staying within the same brand system.

### Landing Page Structure

```
Hero (above fold)
  └── Headline: What the product does + for whom (8 words max)
  └── Subheadline: One more sentence of context / key benefit
  └── Primary CTA: Single action (not two equal CTAs)
  └── Hero image/video: Shows the product or outcome, not stock photos

Social proof (just below fold)
  └── Logos of known customers / press mentions
  └── Star rating + review count

Feature/benefit sections
  └── 2–4 sections, each: one feature → one concrete user benefit
  └── Alternate layout direction to create visual rhythm
  └── Screenshot or illustration per section

How it works
  └── 3–4 numbered steps (keep it simple)
  └── Progressive detail: headline → one sentence → optional expansion

Testimonials
  └── Specific, outcome-focused ("I used to spend 2 hours checking 4 exchanges. Now it's instant.")
  └── Name, role, photo — no anonymous quotes

Pricing (if applicable)
  └── Simple comparison; highlight recommended tier
  └── Address the most common objection (usually cost or lock-in)

Final CTA
  └── Repeat primary action
  └── Address last objection: "Free to start. No credit card required."
```

### Marketing Typography Rules

Marketing headlines can use more expressive type than product UI:
- Larger sizes (48–96px for hero headlines)
- Greater weight contrast (900 for display, 400 for body)
- Negative letter-spacing on large display type (−1 to −3px)
- Brand typeface prominently — this is a showcase surface

### Conversion-Focused Design Principles

**One primary CTA per section:** Multiple CTAs compete with each other and reduce conversion. Define ONE action per section.

**Above-fold promise:** The hero must answer "what is this and why should I care?" within 5 seconds. Test this with a 5-second test.

**Objection-driven design:** Map the most common objections and address them near the CTA:
```
Objection: "I don't trust giving it my API keys"
Response near CTA: "Read-only access. Your keys are AES-256 encrypted. Nexus cannot trade or withdraw."
```

**Hierarchy of evidence:**
1. Your claims (weak — self-reported)
2. Social proof — logos, numbers ("10,000 portfolios tracked")
3. User testimonials (strong — third party)
4. Press coverage (strong — credible third party)
5. Awards / certifications (strong for specific audiences)

### App Store Design

**Screenshots (most important marketing asset):**
- Frame 1: Hero benefit statement + key feature shown
- Frames 2–5: One feature per frame with context caption
- Use device frames; show real UI, not mockup art
- Caption text: benefit statement, not feature name ("See your whole portfolio" not "Portfolio Tab")

**App icon:**
- Recognizable at 60×60px (the actual display size in lists)
- Test at all sizes: 1024px (App Store), 180px (iPhone home), 60px (notification), 40px (spotlight)
- No text — too small to read
- Simple shape, not busy illustration

### Outputs
- Landing page wireframe following the structure above
- Hero section design with CTA
- Social proof and feature section designs
- App Store screenshots (6 per platform)
- Email template design
