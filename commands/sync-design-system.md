---
description: Scan this repo's existing tokens, components, and patterns; write the design system to docs/design.md; add the design-first fenced block to CLAUDE.md.
---

You are running `/product-designer:sync-design-system`. Hand this task to the **`product-designer`** agent.

The agent should:

1. **Detect the stack** — read `package.json` / `Cargo.toml` / `pubspec.yaml` / `Package.swift` etc. Identify framework, language, styling approach, icon library.

2. **Find tokens** — search the repo for color, typography, spacing, radii files. Common patterns to grep for:
   - `constants/Colors.*` / `constants/Typography.*` / `constants/Spacing.*`
   - `tailwind.config.*` (extract theme tokens)
   - `src/theme/*` / `app/theme/*`
   - CSS custom properties in `*.css` files
   - SwiftUI token files
   Read every match and extract the actual values.

3. **Find components** — locate the component library. Look in `components/`, `src/components/`, `lib/components/`, `app/components/`. List every component, its variants, and its current props.

4. **Find icons** — locate the icon registry or detect the icon library being used. Note where icons are imported from and whether there's a central registry.

5. **Find patterns** — read 3-5 representative screens/pages to identify established layout, navigation, form, and state patterns.

6. **Write `docs/design.md`** — use the template embedded in the agent definition. Fill every section from what was discovered. For empty sections, mark as `TODO — undetected`. Add an opening row to the Decision Log:
   - Date: today
   - Decision: "Initial sync"
   - Rationale: "Scanned existing repo. Captured tokens, components, and patterns into docs/design.md."

7. **Write the `CLAUDE.md` fenced block** — additive and idempotent. If `CLAUDE.md` doesn't exist, create it. If the fenced block already exists, refresh its contents in place. Use the template embedded in the agent definition.

8. **Report** to the user:
   - Project state: NEW / PARTIAL / MATURE
   - Skills loaded: [list]
   - Tokens found / inferred / TODO
   - Components found / inferred / TODO
   - Patterns found / inferred / TODO
   - Files written: `docs/design.md`, `CLAUDE.md` (fenced block)
   - Anything ambiguous that needs a follow-up decision from the user

This is an additive command. It never overwrites code, never modifies tokens or components, never deletes anything from `CLAUDE.md` outside the fenced block. It only documents what already exists and surfaces gaps.
