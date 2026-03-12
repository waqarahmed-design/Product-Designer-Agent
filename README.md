# Product Designer Agent

A senior product designer agent for [Claude Code](https://claude.ai/claude-code) that thinks like a designer but communicates in code. It handles UI/UX design, design system governance, interaction design, and frontend implementation — for any project.

---

## What's included

### Agent
**`product-designer`** — Activates for any change that touches the visual or interactive layer. Designs, implements, and reviews UI/UX with strong opinions and token compliance enforcement.

### 15 Specialized Skills

| Skill | What it covers |
|-------|---------------|
| **ui-design** | Visual hierarchy, typography, color theory, spacing systems, Gestalt principles, iconography |
| **ux-design** | User flows, interaction design, accessibility (WCAG), touch targets, wireframing, responsive design |
| **visual-design** | Design systems, component libraries, token governance, brand expression, pixel-perfect polish |
| **frontend-design** | Bold creative direction, distinctive aesthetics, depth, motion, anti-generic design |
| **microinteractions-animation** | Saffer's framework, motion principles, easing, spring physics, signature moments, performance |
| **design-specializations** | iOS/Android native patterns, HIG, Material Design, mobile gestures, onboarding, dashboard design |
| **planning-strategy** | Product strategy, feature scoping, RICE/MoSCoW/Kano, information architecture, success metrics |
| **research-discovery** | User research, heuristic evaluation, competitive analysis, persona/journey mapping, JTBD |
| **technical-tools** | Design tools (Figma, Sketch), frontend knowledge (HTML/CSS/JS), design-dev collaboration, Git |
| **tailwind-design-system** | Tailwind CSS v4, design tokens, component libraries, responsive patterns, dark mode |
| **business-knowledge** | Business models, unit economics, KPIs, funnels, growth loops, pricing, churn, OKRs, competitive intelligence, regulatory compliance |
| **aidlc** | AI Design Lifecycle — AI product strategy, AI UX patterns (chatbots, copilots, prompts), AI states (streaming, hallucination), AI safety/ethics, AI personalization, emerging AI patterns, AI technical collaboration |
| **skill-creator** | Guide for creating new skills to extend the agent's capabilities |

---

## Installation

```bash
claude /install https://github.com/waqarahmed-design/Product-Designer-Agent
```

That's it. The agent and all skills are now available in your Claude Code.

---

## How it works

### The agent adapts to your project automatically

When you invoke the product designer, it reads your project's context before doing anything:

1. **`CLAUDE.md`** — Your project's instructions file. This is the primary source of truth for product description, design system, tech stack, and conventions.
2. **Documentation** — Looks for PRD, spec, research, or design docs to understand users, scope, and constraints.
3. **Design tokens** — Scans for color, typography, spacing, and component constants in your codebase.
4. **Existing screens** — Reads established patterns before creating anything new.

### If no context is found

The agent will ask you:
- What is this product and who are its users?
- Where are the design tokens / constants?
- What is the tech stack and component library?

### For best results: add a `CLAUDE.md` to your project

The more your project documents its design system, the better the agent performs. A good `CLAUDE.md` includes:

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

## What the agent does

### Skill Routing
Before every task, the agent scans a **Skill Routing Matrix** to determine which skills apply. It loads the relevant skills and reports them at the top of each response.

Example mappings:
- New screen → `frontend-design` + `ui-design` + `ux-design` + `design-specializations`
- Animation work → `microinteractions-animation`
- Small color/spacing tweak → `ui-design`
- Feature scoping → `planning-strategy` + `business-knowledge`
- UX audit → `research-discovery` + `ui-design` + `ux-design`
- Pricing page design → `business-knowledge` + `ui-design`
- AI chatbot or copilot UI → `aidlc` + `ux-design`
- AI streaming/loading states → `aidlc` + `microinteractions-animation`

### Token Compliance
The agent enforces strict token compliance. It flags and fixes:
- Hardcoded hex colors or rgba values
- Raw fontFamily strings
- Raw fontSize, borderRadius, or spacing numbers
- Direct icon library imports
- Manual rebuilds of existing components
- Missing touch targets on interactive elements

### Design Principles
1. **Restraint** — Add nothing unless it earns its place
2. **Data first** — The most important number is always the hero
3. **Contrast matters** — Surfaces must be visibly distinct
4. **Accent = one thing** — Accent color reserved for the primary CTA only
5. **Consistency over creativity** — Use established patterns
6. **Mobile ergonomics** — 44x44px minimum touch targets

### Microinteraction Scoring
Every interactive element gets scored 0–10 using Saffer's Trigger-Rules-Feedback-Loops framework, with recommendations to reach a 10.

---

## Output format

The agent structures its responses based on the task:

**Implementing a design:**
1. Skills loaded
2. Design rationale (2–4 sentences)
3. Full code (complete file)
4. Navigation changes needed
5. Data changes needed
6. What to test

**Reviewing UX:**
1. Skills loaded
2. Issues found (file:line references)
3. Severity (critical / important / nice-to-have)
4. Recommended fix for each

**Small change:**
1. The change (file:line reference)
2. Token violations noticed

---

## Works with any stack

The agent is framework-agnostic. It adapts to:
- **React Native** (StyleSheet.create)
- **React + Tailwind** (loads tailwind-design-system skill)
- **Vue, Angular, Svelte** (reads project conventions)
- **Any CSS-in-JS or vanilla CSS approach**

The key is your project's documentation — the agent reads it and follows your conventions.

---

## License

MIT
