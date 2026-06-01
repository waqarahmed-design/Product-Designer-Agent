# Product Designer Agent

A senior product designer agent for [Claude Code](https://claude.ai/claude-code) that **persists itself into your repo**. Stack-agnostic. One command to install, one command to configure.

It thinks like a designer but communicates in code. It handles UI/UX design, design system governance, interaction design, and frontend implementation — for any project, brand new or already established — and it writes its decisions back into your repo so the next session inherits them.

---

## Installation

Inside Claude Code, run:

```
/plugin marketplace add waqarahmed-design/Product-Designer-Agent
/plugin install product-designer@waqarahmed-design
```

Restart Claude Code to load the agent, the `/product-designer:sync-design-system` slash command, and all 13 skills.

> The first command registers this repo as a plugin marketplace; the second installs the plugin from it. (Claude Code's installer requires a marketplace manifest — `claude /install <url>` against a bare plugin repo does not work.)

---

## What's new in v1.3.0

The agent now **manages two files in every repo it runs in**:

- **`docs/design.md`** — the canonical design system spec. Created on first run, auto-updated whenever a design decision is made.
- **`CLAUDE.md`** — a strictly-additive fenced block enforcing the **design-first protocol**: any visual / interactive / structural change must go through the designer agent before implementation begins.

Both files are idempotent and additive. The agent never overwrites your existing CLAUDE.md content or destroys design decisions. It only writes inside its fenced block and updates `docs/design.md` over time.

A new slash command — **`/product-designer:sync-design-system`** — lets you trigger a full repo scan and refresh whenever you want (or run it once in a mature repo to populate `docs/design.md` from existing code).

---

## What's included

### Agent

**`product-designer`** — Activates for any change that touches the visual or interactive layer. Designs, implements, reviews, and persists. Stack-agnostic: reads conventions from `CLAUDE.md` + `docs/design.md` + your tokens at runtime.

### Slash command

**`/product-designer:sync-design-system`** — Scans the current repo, captures tokens / components / patterns into `docs/design.md`, and adds the design-first fenced block to `CLAUDE.md`. Idempotent — safe to run repeatedly.

### 13 specialised skills

| Skill | What it covers |
|---|---|
| **ui-ux-pro-max** | 50+ styles, 161 palettes, 57 font pairings, 161 product types, 99 UX guidelines, 25 chart types across 10 stacks. Mandatory pre-design specification, aesthetic catalog, searchable design-system CLI. |
| **ux-design** | 115 named rules across 8 priority categories — flows, interaction states, feedback, forms, accessibility (WCAG), cognitive load, mobile/touch UX, edge cases. Pre-delivery checklist + symptom→solution troubleshooting. |
| **visual-design** | Design systems, component libraries, token governance, brand expression, pixel-perfect polish. |
| **frontend-design** | Bold creative direction, distinctive aesthetics, depth, motion, anti-generic design. |
| **microinteractions-animation** | Saffer's framework, motion principles, easing, spring physics, signature moments, performance. |
| **design-specializations** | iOS/Android native patterns, HIG, Material Design, mobile gestures, onboarding, dashboard design. |
| **planning-strategy** | Product strategy, feature scoping, RICE / MoSCoW / Kano, information architecture, success metrics. |
| **research-discovery** | User research, heuristic evaluation, competitive analysis, persona / journey mapping, JTBD. |
| **technical-tools** | Figma, design-dev collaboration, Git, Storybook, emerging tech. |
| **tailwind-design-system** | Tailwind CSS v4, design tokens, component libraries, responsive patterns, dark mode. |
| **business-knowledge** | Business models, unit economics, KPIs, funnels, growth loops, pricing, churn, OKRs. |
| **aidlc** | AI Design Lifecycle — AI product strategy, AI UX patterns, AI states, AI safety, AI personalization. |
| **skill-creator** | Guide for creating new skills to extend the agent. |

---

## How it works — in any repo

### First time you use it

Open Claude Code in your repo and either:

1. **Run the explicit setup command:**

   ```
   /product-designer:sync-design-system
   ```

   The agent scans your repo, populates `docs/design.md` with the design system it finds (tokens, components, patterns, anti-patterns), and adds the design-first fenced block to `CLAUDE.md`.

2. **Or just start designing.** Invoke the agent ("Design a login screen") and it will:
   - Classify the project state (NEW / PARTIAL / MATURE)
   - Run the right protocol (bootstrap for NEW projects, sync for PARTIAL, follow conventions for MATURE)
   - Persist the design system as it works

Either path, **after one session** your repo has:

- `docs/design.md` — full design system spec
- `CLAUDE.md` — design-first protocol fenced block

### Every subsequent session

The agent reads `docs/design.md` and `CLAUDE.md` first. It follows the conventions exactly. Any design decision made in the session — a new token, a new component, a new pattern, a change to a rule — is appended to `docs/design.md` and logged in the Decision Log.

The design system is now self-documenting and version-controlled.

---

## The three project states

After context discovery, the agent classifies your project and reports it at the top of every response.

| State | Signals | Action |
|---|---|---|
| **MATURE** | `docs/design.md` exists + CLAUDE.md has the fenced block + tokens + components | Follow existing conventions exactly. Update `docs/design.md` for any new decision. |
| **PARTIAL** | Some tokens or components exist, but no `docs/design.md` or no fenced block | Run Sync Flow silently — scan, write `docs/design.md`, add fenced block, then proceed with the task. |
| **NEW** | No tokens, no design system, no `docs/design.md` | Run the **New Project Bootstrap Protocol** — clarifying questions, propose tokens, scaffold components, then write both files. |

---

## The design-first protocol

The fenced block added to your `CLAUDE.md` makes this rule explicit for any agent or developer reading the repo:

> Any task that touches the visual, interactive, or structural layer of the product **MUST** go through the `product-designer` agent before implementation.
>
> 1. `product-designer` drafts a spec — layout, tokens, copy, every state.
> 2. User reviews and approves.
> 3. Implementation begins.
>
> If a UI task arrives without an approved spec, surface it and request the spec first.

Skip-allowed cases: pure bug fixes with zero visual change · type-only fixes · perf work with no visible change · test-only changes · navigation wiring where every affected screen already has a spec.

---

## New project bootstrap

If the project is new, the agent asks **before writing any code**:

> 1. Visual style? (Dark & premium / Clean & minimal / Bold & expressive / Warm & human / Technical / Custom)
> 2. Primary platform? (Mobile / Web desktop / Web mobile-first / Both)
> 3. Brand / accent color? (Hex or let agent decide)
> 4. Typography feel? (System / Modern sans / Serif accent / Mono)
> 5. One word for how this should feel?

Then it scaffolds:

- **Design tokens** — color, typography, spacing, radii — at the right location for your stack (`constants/Colors.ts` for RN, `tailwind.config.ts` for Tailwind, `src/theme/` for styled-components, etc.)
- **Icon registry** — semantic icon map using the right library for the stack
- **Core components** — Button, Card, Input, Badge, Icon (base five) with barrel export
- **`docs/design.md`** — the design system spec written from the bootstrap decisions
- **`CLAUDE.md` fenced block** — the design-first protocol

The agent always confirms key decisions (brand color, typography) before committing — to build ownership.

---

## What the agent enforces

### Token compliance

The agent flags and fixes:
- Hardcoded hex colors or `rgba()` literals
- Raw `fontFamily` strings
- Raw `fontSize`, `borderRadius`, or spacing numbers
- Direct icon library imports bypassing the registry
- Manual rebuilds of existing components
- Missing touch targets on interactive elements
- Brand / accent color used on more than one primary action per screen
- Destructive actions using brand color (should use error / red token)

### Design principles

1. **Restraint** — Add nothing unless it earns its place.
2. **Data first** — The most important number, action, or message is always the hero.
3. **Contrast matters** — Surfaces must be visibly distinct. Text hits WCAG AA at minimum.
4. **Accent = one thing** — Brand color reserved for the single primary CTA per screen.
5. **Consistency over creativity** — Use established patterns; don't invent new interactions for solved problems.
6. **Ergonomics** — 44×44pt touch targets on mobile, 36px on web. Destructive actions confirm.

### Microinteraction scoring

Every interactive element gets scored 0–10 using Saffer's Trigger–Rules–Feedback–Loops framework, with recommendations to reach a 10.

---

## Works with any stack

The agent is framework-agnostic. Tested mental model for:

- **React Native** (StyleSheet, Expo, HugeIcons)
- **Next.js / React + Tailwind** (loads `tailwind-design-system` skill)
- **Next.js / React + styled-components / CSS modules / vanilla CSS**
- **Vue / Nuxt** (Tailwind or otherwise)
- **SwiftUI**
- **Anything else** — adapts by reading your conventions

The agent uses your tokens, your components, your patterns. It doesn't impose a design system on you — it captures the one you have.

---

## Output format

**Implementing a design:**
1. `Project state: MATURE / PARTIAL / NEW`
2. `Skills loaded: [list]`
3. Design rationale (2–4 sentences)
4. Full code (complete file, not snippets)
5. Token / pattern decisions made
6. What to test
7. `docs/design.md` updated: yes / no — what sections

**Reviewing UX:**
1. `Project state: [state]`
2. `Skills loaded: [list]`
3. Issues found (file:line references)
4. Severity: critical / important / nice-to-have
5. Recommended fix for each

**Small targeted change:**
1. The change (file:line reference)
2. Token violations noticed
3. `docs/design.md` updated: yes / no

**New project bootstrap:**
1. Clarifying questions (waits for answers)
2. Proposed token system (confirms before creating)
3. Infrastructure created: tokens → icons → components
4. `docs/design.md` written, `CLAUDE.md` fenced block added

---

## Version history

- **1.3.0** — Self-config behaviour. Manages `docs/design.md` + `CLAUDE.md` fenced block in every host repo. Strictly additive, idempotent. New `/product-designer:sync-design-system` slash command. Agent definition refactored to be fully stack-agnostic (removed product-specific design system content from previous versions).
- **1.2.0** — Added `ui-ux-pro-max` skill, bootstrap protocol, project state detection (MATURE / PARTIAL / NEW), and rebuilt `ux-design` skill with 115 named rules.
- **1.1.0** — Skill loading fixes, flattened skill references, auto-discovery for undocumented projects.
- **1.0.0** — Initial release. Agent + 13 specialised skills.

---

## License

MIT
