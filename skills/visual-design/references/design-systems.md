# Design Systems Methods

## Table of Contents
1. [Component Library Creation](#1-component-library-creation)
2. [Design Token Definition](#2-design-token-definition)
3. [Pattern Library](#3-pattern-library)
4. [Documentation](#4-documentation)
5. [Versioning](#5-versioning)
6. [Governance](#6-governance)

---

## 1. Component Library Creation

**Purpose:** Build a reusable, maintainable set of UI components that express the design system and can be consumed by both designers (in Figma) and developers (in code) — eliminating duplication and enforcing consistency.

**When to use:** Starting a new product; scaling a team beyond 3 designers; when the same component is being rebuilt differently across screens; before any design handoff that involves code.

### Component Anatomy

Every component should be defined along these dimensions:

```
Component definition
  └── Anatomy (what sub-parts it contains)
  └── Variants (visual alternatives: primary, secondary, ghost)
  └── States (default, hover, pressed, focused, disabled, loading, error)
  └── Sizes (if applicable: sm, md, lg)
  └── Behavior (what it does and doesn't do)
  └── Content model (what content it accepts and what it rejects)
  └── Accessibility (ARIA role, keyboard behavior, screen reader text)
```

### Component Tiers

Not all components are equal. Tier determines investment level:

| Tier | Description | Examples | Investment |
|------|-------------|----------|------------|
| 1 — Core | Used everywhere; zero tolerance for inconsistency | Button, Input, Badge, Card | Very high: full variants, all states, documented |
| 2 — Feature | Used in multiple features but more specialized | Date picker, File upload, Table | High: key variants, key states |
| 3 — Domain | Used in one product area | Chart tooltip, Exchange card | Medium: functional coverage |
| 4 — One-off | Single use; not worth abstracting | A specific marketing hero | Low: built in place |

Only Tier 1 and 2 belong in the shared library.

### Component API Design

**Props/properties to define:**

```
Required props: the minimum to render correctly
Optional props: modifiers, callbacks, slots
Forbidden patterns: what consumers should NOT do with this component

Example — Button:
  Required: label (string), onPress (function)
  Optional: variant ('primary' | 'ghost' | 'outline'), size, disabled, loading, icon
  Forbidden: DO NOT pass children — use label prop. DO NOT override background color inline.
```

**Variant design rules:**
- Name variants by role, not appearance: `primary` not `green`, `destructive` not `red`
- States are not variants: `disabled` is a state, not `button-disabled` as a separate component
- Default to the most common usage: if 80% of uses are `primary`, make it the default

### Figma Component Structure

```
Component page structure:
  ├── 🧩 Components (published)
  │   ├── Button / Base (main component)
  │   ├── Button / Primary
  │   ├── Button / Ghost
  │   └── Button / Destructive
  └── 🔬 Playground (not published)
      └── Testing instances + edge cases
```

**Figma best practices:**
- Use component properties (not hidden layers) for variants and states
- Name layers semantically: `icon`, `label`, `container` — not `Frame 42`
- Set constraints correctly so components resize without breaking
- Expose only the properties consumers need — hide internal mechanics

### Code Component Correspondence

Every Figma component should have an exact code counterpart:

| Figma | Code | Bridge |
|-------|------|--------|
| Component variants | `variant` prop | Prop names must match |
| Component states | CSS/style states | Interaction states should match |
| Component sizes | `size` prop | Size names should match |
| Design tokens | Design token imports | Same token names |

### Outputs
- Figma component library (published to team)
- Code component library (npm package or shared directory)
- Component inventory (what exists, what's deprecated, what's pending)
- Per-component spec: anatomy, variants, states, API, accessibility

---

## 2. Design Token Definition

**Purpose:** Define the atomic values — colors, spacing, typography, radii, shadows, motion — that give the design system its visual character, and make them available as named constants to both design tools and code.

**When to use:** Before building any component; when hardcoded values are spreading through the codebase; when adding dark mode or theming; when introducing multiple brand or product variants.

### Token Tiers (3-layer model)

```
Layer 1: Primitive tokens (raw values)
  └── color.blue.500 = #3B82F6
  └── size.4 = 16px
  └── radius.2 = 8px

Layer 2: Semantic tokens (meaning-based references to Layer 1)
  └── color.action.primary = {color.blue.500}
  └── color.text.secondary = {color.gray.500}
  └── space.component.gap = {size.4}

Layer 3: Component tokens (component-specific references to Layer 2)
  └── button.background.primary = {color.action.primary}
  └── button.padding.horizontal = {space.component.gap}
```

**Why 3 layers matter:**
- Change `color.blue.500` → updates everywhere automatically
- Swap theme by remapping Layer 2 to different Layer 1 values
- Debug a specific component by inspecting Layer 3 tokens

### Token Naming Convention

```
Format: [category].[concept].[variant].[state]

Examples:
  color.background.primary
  color.background.primary.hover
  color.text.secondary
  color.border.error
  space.component.padding.md
  radius.card
  shadow.elevated
  motion.duration.enter
  motion.easing.standard
```

**Naming rules:**
- Use semantic names, not descriptive: `color.text.danger` not `color.text.red`
- Be consistent with word order: always category first
- Avoid abbreviations: `background` not `bg`, `secondary` not `sec`
- Prefix internal/experimental tokens: `_color.internal.foo`

### Token Categories

| Category | Examples | Notes |
|----------|----------|-------|
| Color | `color.background.*`, `color.text.*`, `color.border.*`, `color.action.*` | Light and dark mode variants |
| Typography | `font.family.*`, `font.size.*`, `font.weight.*`, `line.height.*` | Reference font system |
| Spacing | `space.1` through `space.16`, semantic aliases like `space.component.padding.md` | Base 4px grid recommended |
| Border radius | `radius.none`, `radius.sm`, `radius.md`, `radius.lg`, `radius.pill` | Match product visual language |
| Shadow / Elevation | `shadow.none`, `shadow.sm`, `shadow.md`, `shadow.lg` | 3–5 levels max |
| Motion | `motion.duration.fast` (100ms), `motion.duration.standard` (250ms), `motion.easing.*` | Drives animation system |
| Z-index | `layer.tooltip` (1000), `layer.modal` (1100), `layer.overlay` (1200) | Prevents z-fighting |

### Token Formats

Define every token in all required formats:

```json
{
  "color.accent": {
    "value": "#C8E847",
    "description": "Primary accent — CTAs and hero elements only",
    "type": "color",
    "css": "--color-accent",
    "ios": "colorAccent",
    "android": "color_accent"
  }
}
```

### Dark Mode Token Strategy

```
Approach: remap semantic tokens, not primitive tokens

Light mode:
  color.background.primary = {color.white}     → #FFFFFF
  color.text.primary = {color.gray.900}         → #111111

Dark mode:
  color.background.primary = {color.gray.950}  → #0A0A0A
  color.text.primary = {color.gray.50}          → #F9FAFB

The component uses `color.background.primary` — it never needs to know the mode.
```

### Outputs
- Token file in W3C Design Token format (`.json` or `.yaml`)
- Generated platform outputs: CSS custom properties, iOS Swift constants, Android XML, JS/TS constants
- Token documentation page (visual reference with all values and their names)
- Dark mode token mapping document

---

## 3. Pattern Library

**Purpose:** Document recurring UI patterns — combinations of components that solve specific interaction problems — so teams don't solve the same problems differently each time.

**When to use:** When the same type of interaction (form submission, empty states, loading states, filtering) is handled inconsistently across the product; when onboarding new team members; when extending the design system beyond atomic components.

### Pattern vs. Component

| | Component | Pattern |
|--|-----------|---------|
| What | A single UI element | A recurring combination of elements |
| Example | `Button`, `Input` | Form with validation, Infinite scroll, Paginated table |
| Scope | Atomic | Composite |
| Reuse | Exact reuse | Adapted to context |
| Documentation | Variants + states | When to use, how to adapt |

### Pattern Categories

```
Navigation patterns
  └── Tab bar, Breadcrumbs, Pagination, Infinite scroll, Back navigation

Form patterns
  └── Form validation (inline vs. summary), Multi-step forms, Autosave, Confirmation flows

Data display patterns
  └── Data tables (sortable, filterable), Card grids, List + detail, Master-detail

Feedback patterns
  └── Empty states, Error states, Loading states (skeleton, spinner, progress)
  └── Success confirmation, Destructive action confirmation

Search and filter patterns
  └── Search with autocomplete, Filter panels, Sort controls, Active filter chips

Onboarding patterns
  └── Progressive onboarding, Feature discovery (tooltip, spotlight), First-time empty states

Settings patterns
  └── Grouped settings, Dangerous action zones, Confirmation dialogs
```

### Pattern Documentation Structure

Each pattern entry should include:

```
Pattern: [Name]
──────────────────────────────────────────
Problem: What interaction problem does this solve?

When to use: Specific conditions where this pattern applies
When NOT to use: Conditions where a different pattern is better

Anatomy:
  - Required elements
  - Optional elements
  - Prohibited elements

Behavior:
  - Default state
  - Interaction flow
  - Edge cases (empty, error, loading, overflow)

Accessibility:
  - Keyboard navigation
  - Screen reader behavior

Variants:
  - Named variant A: [description + when]
  - Named variant B: [description + when]

Examples:
  - Screenshot/mockup of correct usage
  - Screenshot/mockup of incorrect usage with annotation

Related patterns: [links]
Related components: [links]
```

### Empty State Pattern (Example)

```
Problem: Screen has no content to display

When to use:
  - First-time user (no data yet)
  - Search with no results
  - Filtered view with no matches
  - Error prevented data from loading

Anatomy:
  Required: Illustration or icon, primary message
  Optional: Supporting text, primary CTA
  Prohibited: Multiple CTAs, technical error messages shown to user

Content rules by type:
  First-time empty: Forward-looking, inviting ("Connect your first exchange to start tracking.")
  Search/filter empty: Acknowledge the query ("No results for 'XRP futures'"), offer escape
  Error empty: Acknowledge the problem, offer resolution ("Something went wrong. Try refreshing.")

Illustration guidance:
  - Simple, on-brand illustration or icon
  - Not too large — empty state shouldn't feel like a destination
  - Avoid stock art or clip art
```

### Outputs
- Pattern library page (in documentation tool of choice)
- Pattern inventory (all patterns cataloged with status: approved / draft / deprecated)
- Pattern request process (how teams propose new patterns)

---

## 4. Documentation

**Purpose:** Make the design system discoverable, learnable, and usable by everyone who needs to implement it — designers, engineers, content designers, and new team members.

**When to use:** Once the system has more than ~10 components or tokens; before onboarding additional contributors; before sharing the system with external teams.

### Documentation Principles

**1. Show, don't tell.** Live examples beat descriptions. A visual of the component in all its states teaches faster than paragraphs.

**2. Answer the question people actually have.** Most readers arrive with a specific question: "Which card variant do I use here?" Write docs that answer real questions, not theoretical overviews.

**3. Document the why, not just the what.** "Use `color.text.danger` not `color.red`" is more memorable when followed by the reason: "because it survives a theme change."

**4. Maintain ruthlessly.** Outdated docs are worse than no docs — they teach the wrong thing confidently. Assign ownership.

### Documentation Structure

```
Getting started
  ├── What is this design system?
  ├── How to install (for engineers)
  ├── How to access in Figma (for designers)
  ├── Quick start guide (build something in 15 minutes)
  └── Who to contact

Foundations
  ├── Color (with live swatches and token names)
  ├── Typography (with live type scale)
  ├── Spacing (with visual spacing scale)
  ├── Motion (with live animation demos)
  └── Icons (searchable icon browser)

Components (one page per component)
  ├── Overview (what it is, when to use it)
  ├── Live examples with code snippets
  ├── Variants
  ├── States
  ├── Props/API reference
  ├── Accessibility
  └── Do / Don't examples

Patterns (one page per pattern)
  ├── Problem this pattern solves
  ├── When to use / when not to
  ├── Examples
  └── Related components

Content guidelines
  ├── Voice and tone
  ├── Capitalization
  ├── Punctuation
  └── Component-specific writing guidance (button labels, empty states, error messages)

Contributing
  ├── How to propose a new component
  ├── How to submit a bug or improvement
  ├── Design system roadmap
  └── Changelog
```

### Component Page Template

```markdown
# [Component Name]

[One sentence: what it is and what it's for.]

## When to use
- [Specific use case 1]
- [Specific use case 2]

## When not to use
- Use [Other Component] instead when [condition].
- Don't use [this component] for [misuse case].

## Examples
[Live embedded example]

```jsx
<Button variant="primary" onPress={handleSubmit}>
  Connect exchange
</Button>
```

## Variants
[Visual table of all variants with names]

## States
[Visual table: default, hover, pressed, focused, disabled, loading, error]

## Props
| Prop | Type | Default | Description |
|------|------|---------|-------------|

## Accessibility
- Role: `button`
- Keyboard: `Enter` and `Space` to activate
- Screen reader: reads `label` or `aria-label`

## Do / Don't
[Side-by-side examples]
```

### Tooling Options

| Tool | Best for | Trade-offs |
|------|----------|-----------|
| Storybook | Component-level docs co-located with code | Technical setup; best for engineers |
| Zeroheight | Polished design system sites synced from Figma | Paid; non-interactive by default |
| Notion | Quick internal wikis | No live examples |
| Custom site | Full control | High build cost |

### Outputs
- Documentation site (live or static)
- Getting started guide
- Component pages for all Tier 1 and 2 components
- Contribution guide
- Changelog

---

## 5. Versioning

**Purpose:** Manage changes to the design system over time so that consumers can adopt updates safely, breaking changes are communicated clearly, and the system can evolve without disrupting product teams.

**When to use:** Once the design system has multiple consumers (more than one team or product); before publishing the system as a package; when about to make a breaking change.

### Semantic Versioning for Design Systems

Adopt semver (MAJOR.MINOR.PATCH) with design system-specific interpretations:

```
MAJOR (breaking change)
  - Component API change that requires consumer code updates
  - Token renamed or removed
  - Behavior change that changes screen appearance
  - Component removed

MINOR (new feature, non-breaking)
  - New component added
  - New variant added to existing component
  - New token added
  - New optional prop added

PATCH (fix, non-breaking)
  - Visual bug fix that doesn't change the design intent
  - Documentation update
  - Internal refactor with no API change
  - Accessibility fix that doesn't change the visual appearance
```

### Breaking Change Protocol

Before releasing a breaking change:

```
1. Deprecation notice (MINOR release)
   - Add deprecation warning in code: console.warn('OldProp is deprecated. Use NewProp instead.')
   - Mark component/token as deprecated in documentation
   - Document migration path

2. Deprecation period
   - Keep deprecated API working for a defined period (typically 1–2 versions)
   - Communicate timeline to all consumer teams

3. Breaking release (MAJOR)
   - Remove deprecated items
   - Publish migration guide
   - Coordinate with consumer teams on upgrade timing
```

### Changelog Format

Every release needs a structured changelog:

```markdown
## [2.3.0] — 2025-03-11

### Added
- `Button` — new `icon-only` variant for icon buttons without labels
- `color.border.focus` — semantic token for keyboard focus indicators

### Changed
- `Card` — `elevated` variant now uses `shadow.md` token (previously hardcoded shadow)
- `Badge` — `status` variant label size increased from 11px to 12px for legibility

### Deprecated
- `Button` `size="large"` — use `size="lg"` instead. Will be removed in v3.0.0.

### Fixed
- `Input` — fixed incorrect focus ring color in dark mode
- `Badge` — fixed text overflow with long labels

### Migration
No breaking changes. Update deprecated `size="large"` to `size="lg"` before v3.0.
```

### Token Versioning

Tokens require special treatment because renaming a token is always a breaking change:

```
Renaming strategy:
  1. Add new token name (MINOR)
  2. Keep old token as alias pointing to new token
  3. Mark old token as deprecated
  4. Remove old token (MAJOR)

Never delete a token without a deprecation period.
```

### Outputs
- Versioned package (npm or equivalent)
- Changelog for every release
- Deprecation notices with migration paths
- Release communication to consumer teams

---

## 6. Governance

**Purpose:** Define how the design system evolves — who can contribute, how decisions are made, how quality is maintained — so the system grows coherently rather than by committee or by accident.

**When to use:** When more than one team contributes to or consumes the design system; when contribution requests are piling up without a clear process; when the system has inconsistent quality or conflicting patterns.

### Governance Models

| Model | Description | Best for |
|-------|-------------|----------|
| Solitary | One person or small team owns everything | Early stage; < 3 contributors |
| Federated | Central team sets standards; product teams contribute | Scaled teams; multiple products |
| Distributed | All teams contribute equally under shared standards | Large orgs; mature systems |

**Most common for product teams:** Federated — a core design system team owns the system, product teams can contribute via a defined process.

### Roles and Responsibilities

```
Design System Core Team
  ├── System Designer — owns visual direction and component design
  ├── System Engineer — owns code components and tooling
  └── System PM — owns roadmap, prioritization, and communication

Contributors (product teams)
  ├── Can submit: component proposals, bug reports, pattern suggestions
  └── Cannot unilaterally: add to the shared library, change token values, rename APIs

Design System Lead (or committee)
  └── Final approval on all additions and breaking changes
```

### Contribution Process

```
1. Proposal
   ├── Contributor submits a proposal (template below)
   ├── Defines: what, why, usage evidence, proposed API
   └── Links: existing usage screenshots, design mockup

2. Review (1–2 weeks)
   ├── Core team evaluates: Is it general enough? Does it duplicate existing?
   ├── Decision: Approve / Request changes / Decline (with reason)
   └── Feedback given within defined SLA

3. Build
   ├── Contributor builds to design system standards
   ├── Core team reviews design + code
   └── Accessibility review required for all Tier 1/2

4. Ship
   ├── Added to library + documented
   ├── Released in next MINOR version
   └── Announced to all consumers
```

### Component Proposal Template

```
Component: [Name]
Proposing team: [Team name]
Date: [Date]

Problem:
  What user or product problem does this solve?

Evidence of need:
  Where is this currently built ad hoc? (Links to Figma/code)

Proposed API:
  Variants: [list]
  Props: [key props with types]

Existing alternatives considered:
  Did you consider using/extending [existing component]? Why doesn't it work?

Design mockup: [Figma link]
```

### Quality Standards for Acceptance

A component or pattern must meet all of these before acceptance:

```
Design quality
  ✅ All states designed: default, hover, focus, active, disabled, error
  ✅ Responsive behavior defined
  ✅ Dark mode defined
  ✅ Uses design tokens only (no hardcoded values)

Code quality
  ✅ TypeScript props interface
  ✅ All variants implemented
  ✅ Unit tests for key behaviors
  ✅ No inline styles; uses token imports

Accessibility
  ✅ WCAG AA color contrast
  ✅ Keyboard accessible
  ✅ ARIA roles and labels correct
  ✅ Screen reader tested

Documentation
  ✅ Component page written
  ✅ Do / Don't examples
  ✅ Props table complete
  ✅ Usage examples with code
```

### Deprecation and Removal Policy

```
Decision to deprecate:
  - Component/pattern is superseded by a better option
  - Usage has dropped below threshold
  - Maintenance cost exceeds value

Deprecation process:
  1. Announce deprecation (release notes + Slack/email)
  2. Add deprecation notice in code and docs
  3. Provide migration path in the same announcement
  4. Wait minimum 60 days or 2 major releases
  5. Remove in next MAJOR version

Hard rule: Never remove without a migration path documented.
```

### System Health Metrics

Track these to know if governance is working:

| Metric | Good signal | Warning signal |
|--------|-------------|---------------|
| Component adoption | >80% screens use system components | Product teams rebuilding their own |
| Token compliance | <5% hardcoded values in codebase | Growing inline styles |
| Contribution rate | 1–3 proposals/month | 0 (siloed) or 20+ (out of control) |
| Time to ship new component | <2 weeks from proposal to release | >6 weeks regularly |
| Documentation freshness | Updated within 2 weeks of a release | Docs lag code by >1 version |

### Outputs
- Governance model document (roles, process, decision rights)
- Contribution process and proposal template
- Quality standards checklist
- Health metrics dashboard
- Meeting cadence: weekly sync for active work; monthly review for roadmap
