# Product Designer Agent

A senior product designer agent for [Claude Code](https://claude.ai/claude-code) that thinks like a designer but communicates in code. It handles UI/UX design, design system governance, interaction design, and frontend implementation — for any project, whether brand new or already established.

---

## What's included

### Agent
**`product-designer`** — Activates for any change that touches the visual or interactive layer. Designs, implements, and reviews UI/UX with strong opinions and token compliance enforcement.

### 14 Specialized Skills

| Skill | What it covers |
|-------|---------------|
| **ui-ux-pro-max** | Comprehensive UI/UX intelligence — 50+ design styles, 161 color palettes, 57 font pairings, 161 product types, 99 UX guidelines, 25 chart types across 10 stacks. Includes mandatory pre-design specification, aesthetic direction catalog, and searchable design system CLI |
| **ux-design** | 115 named rules across 8 priority categories — flows, interaction states, feedback, forms, accessibility (WCAG), cognitive load, mobile/touch UX, and edge cases. Includes pre-delivery checklist and symptom→solution troubleshooting |
| **visual-design** | Design systems, component libraries, token governance, brand expression, pixel-perfect polish |
| **frontend-design** | Bold creative direction, distinctive aesthetics, depth, motion, anti-generic design |
| **microinteractions-animation** | Saffer's framework, motion principles, easing, spring physics, signature moments, performance |
| **design-specializations** | iOS/Android native patterns, HIG, Material Design, mobile gestures, onboarding, dashboard design |
| **planning-strategy** | Product strategy, feature scoping, RICE/MoSCoW/Kano, information architecture, success metrics |
| **research-discovery** | User research, heuristic evaluation, competitive analysis, persona/journey mapping, JTBD |
| **technical-tools** | Design tools (Figma, Sketch), frontend knowledge (HTML/CSS/JS), design-dev collaboration, Git |
| **tailwind-design-system** | Tailwind CSS v4, design tokens, component libraries, responsive patterns, dark mode |
| **business-knowledge** | Business models, unit economics, KPIs, funnels, growth loops, pricing, churn, OKRs, competitive intelligence, regulatory compliance |
| **aidlc** | AI Design Lifecycle — AI product strategy, AI UX patterns (chatbots, copilots, prompts), AI states (streaming, hallucination), AI safety/ethics, AI personalization, emerging AI patterns |
| **skill-creator** | Guide for creating new skills to extend the agent's capabilities |

---

## Installation

```bash
claude /install https://github.com/waqarahmed-design/Product-Designer-Agent
```

That's it. The agent and all 14 skills are now available in your Claude Code.

---

## How it works

### Step 1 — Context discovery (before anything else)

When the product designer activates, its first action is reading your project:

1. **`CLAUDE.md`** — Primary source of truth for design system, tech stack, and conventions
2. **Documentation** — Spec, PRD, research docs, and technical specs
3. **Design tokens** — Scans for color, typography, spacing, and component constants
4. **Existing screens** — Reads established patterns before creating anything new

After reading, the agent classifies your project and reports it at the top of every response:

| State | Signals | What happens |
|-------|---------|--------------|
| **MATURE** | CLAUDE.md + tokens + icons + components | Follows existing conventions exactly |
| **PARTIAL** | Some infrastructure, some gaps | Fills gaps; asks only where genuinely ambiguous |
| **NEW** | Little or no design infrastructure | Runs the New Project Bootstrap Protocol |

### Step 2 — For new projects: Bootstrap Protocol

If your project is new, the agent asks clarifying questions **before writing a single line of code**:

> **"Before I start, I need to understand your visual direction:"**
>
> 1. Visual style? (Dark & premium / Clean & minimal / Bold & expressive / Warm & human / Technical / Custom)
> 2. Primary platform? (Mobile / Web desktop / Web mobile-first / Both)
> 3. Brand / accent color? (Hex or let agent decide)
> 4. Typography feel? (System / Modern sans-serif / Serif accent / Monospace)
> 5. One word for how this should feel?

Then it creates missing infrastructure in order:
- **Design tokens** — Proposes color system and confirms with you before creating
- **Icon registry** — Creates semantic icon map (HugeIcons → Heroicons → FontAwesome fallback)
- **Component library** — Scaffolds Button, Card, Input, Badge, Icon with barrel export

The agent always confirms key design decisions (brand color, typography direction) before committing — this builds ownership and prevents wrong assumptions.

### Step 3 — Skill routing

Before every task, the agent matches it against a **Skill Routing Matrix** and loads the relevant skills. It reports them at the top of each response: `Skills loaded: [list]`

Example mappings:
- New screen → `ui-ux-pro-max` + `frontend-design` + `ux-design` + `design-specializations`
- Animation work → `microinteractions-animation`
- Small color/spacing tweak → `ui-ux-pro-max`
- Dashboard or data-heavy screen → `ui-ux-pro-max` + `frontend-design`
- Feature scoping → `planning-strategy` + `business-knowledge`
- UX audit → `research-discovery` + `ui-ux-pro-max` + `ux-design`
- Form design → `ux-design` + `ui-ux-pro-max`
- Empty / error states → `ui-ux-pro-max` + `microinteractions-animation`
- Bootstrapping component library → `visual-design` + `ui-ux-pro-max` + `frontend-design`
- AI chatbot or copilot UI → `aidlc` + `ux-design`
- New project with no design system → `ui-ux-pro-max` + `visual-design` + `frontend-design`

### Works without a CLAUDE.md too

If your project doesn't have a `CLAUDE.md`, the agent runs **auto-discovery** before asking you anything:

- Reads `package.json` to detect framework, styling library, and dependencies
- Searches for token files by common names: `*color*`, `*palette*`, `*theme*`, `*typograph*`, `*spacing*`, `*token*`, `*design-system*`
- Finds component directories: `components/`, `ui/`, `shared/`, `common/`, `lib/`
- Locates screens/pages: `screens/`, `pages/`, `views/`, `app/`, `routes/`
- Checks config files: `tailwind.config.*`, `tsconfig.json`, `.eslintrc*`

The agent only asks you questions when auto-discovery genuinely can't find something — and even then it's specific: *"I found your colors in `src/theme/colors.ts` but couldn't locate a spacing scale — where is it?"*

### For best results: add a `CLAUDE.md` to your project

```markdown
## Design tokens
- Colors: `constants/Colors.ts` — describe semantic meanings
- Typography: `constants/Typography.ts` — describe type scale
- Spacing: `constants/Spacing.ts` — describe grid system
- Icons: describe icon system and how to use it

## Components
- List reusable UI components (Button, Card, Input, etc.)
- Describe variants and usage rules

## Tech stack
- Framework, styling approach, libraries

## Patterns
- Layout patterns, navigation structure, established conventions
```

---

## What the agent enforces

### Token Compliance
The agent flags and fixes:
- Hardcoded hex colors or rgba values
- Raw fontFamily strings
- Raw fontSize, borderRadius, or spacing numbers
- Direct icon library imports (bypassing the registry)
- Manual rebuilds of existing components
- Missing touch targets on interactive elements

### Design Principles
1. **Restraint** — Add nothing unless it earns its place
2. **Data first** — The most important number is always the hero
3. **Contrast matters** — Surfaces must be visibly distinct from backgrounds
4. **Accent = one thing** — Accent color reserved for the single primary CTA only
5. **Consistency over creativity** — Use established patterns; don't invent new interactions for solved problems
6. **Mobile ergonomics** — 44×44px minimum touch targets, always

### Microinteraction Scoring
Every interactive element gets scored 0–10 using Saffer's Trigger-Rules-Feedback-Loops framework, with recommendations to reach a 10.

---

## Output format

**Implementing a design:**
1. `Project state: MATURE / PARTIAL / NEW`
2. `Skills loaded: [list]`
3. Design rationale (2–4 sentences)
4. Full code (complete file, not snippets)
5. Navigation changes needed
6. Data changes needed
7. What to test

**Reviewing UX:**
1. `Project state: [state]`
2. `Skills loaded: [list]`
3. Issues found (file:line references)
4. Severity: critical / important / nice-to-have
5. Recommended fix for each

**Small change:**
1. The change (file:line reference)
2. Token violations noticed

**New project bootstrap:**
1. Clarifying questions (waits for answers)
2. Proposed token system (confirms before creating)
3. Infrastructure created in order: tokens → icons → components

---

## Works with any stack

The agent is framework-agnostic. It adapts to:
- **React Native** (StyleSheet.create, Expo, HugeIcons)
- **React + Tailwind** (loads tailwind-design-system skill)
- **Next.js, Vue, Angular, Svelte** (reads project conventions)
- **Any CSS-in-JS or vanilla CSS approach**

The key is your project's documentation — the agent reads it and follows your conventions.

---

## License

MIT
