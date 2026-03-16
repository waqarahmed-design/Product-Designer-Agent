# Design-Dev Collaboration

## Table of Contents
1. [Version Control](#1-version-control)
2. [Design APIs](#2-design-apis)
3. [Component Libraries](#3-component-libraries)
4. [Design QA](#4-design-qa)
5. [Technical Constraints](#5-technical-constraints)

---

## 1. Version Control

**Purpose:** Use Git-based workflows to track design file changes, collaborate without conflicts, and maintain a history of design decisions — bringing engineering's most powerful collaboration practice to design work.

**When to use:** When multiple designers work on the same files; before making significant changes; when design files need to be version-controlled alongside code.

### Git for Designers — Core Concepts

```
Repository (repo): A folder tracked by Git. Contains all files and their full history.
Commit: A snapshot of all changes at a point in time. Always add a message.
Branch: An independent line of work. Doesn't affect main until merged.
Main/Master: The primary branch — the "official" current state.
Pull Request (PR): A proposed merge from a branch to main.
Merge: Incorporate changes from one branch into another.
Clone: Copy a remote repo to your local machine.
Pull: Fetch and apply latest changes from remote to local.
Push: Upload local commits to remote.
```

### Git Basics for Designers

```bash
# Check what's changed
git status

# See what changed in a file
git diff filename.md

# Stage changes for commit
git add filename.md          # specific file
git add .                    # all changed files

# Commit with a message
git commit -m "Add dark mode variant to Button component"

# Push to remote (share with team)
git push origin main

# Pull latest from remote (before starting work)
git pull origin main

# Create a new branch (for a new feature/screen)
git checkout -b feature/analytics-screen

# Switch between branches
git checkout main
git checkout feature/analytics-screen

# Merge a branch into main
git checkout main
git merge feature/analytics-screen
```

### Design-Specific Version Control Workflows

**Figma + Git (for design tokens and specs):**
```
Design tokens (JSON files) live in the repo alongside code.
Designers update tokens in Figma → Tokens Studio exports JSON → commit to repo.

Workflow:
1. git pull (get latest)
2. Update design in Figma
3. Export tokens: Tokens Studio → Sync to repo (or manual export)
4. git add tokens/
5. git commit -m "Update spacing scale: add Spacing[7] = 28px"
6. git push
7. Engineer reviews token change via PR before it goes live
```

**Abstract (for Sketch):**
```
Abstract wraps Git for Sketch files — no manual Git needed.
Branch: Create a branch in Abstract for each design task.
Commit: "Save version" in Abstract.
Review: Submit for review → teammate reviews + comments.
Merge: Merge branch back to main.
```

**Branching strategy:**
```
main          → Shipped, production-ready designs
feature/X     → New screen or feature (one branch per feature)
fix/X         → Small corrections to existing designs
experiment/X  → Exploratory work, may not ship

Never design directly on main.
Always branch → design → review → merge.
```

### Commit Message Conventions

```
Format: [type]: [short description]

Types:
  feat:     New screen or component
  update:   Modification to existing design
  fix:      Correction of design error
  refactor: Restructuring without visual change
  tokens:   Design token changes

Examples:
  feat: Add Analytics screen with benchmark comparison
  update: Revise exchange card spacing to 4px grid
  fix: Correct button touch target to 44px minimum
  tokens: Add Colors.accentDim for background tinting
  refactor: Reorganize components into tier 1/2/3 folders
```

### Outputs
- Git-tracked design token files
- Branching conventions document for the design team
- PR template for design changes

---

## 2. Design APIs

**Purpose:** Automate the transfer of design decisions (tokens, assets, components) from design tools into code — eliminating manual transcription and keeping design and code in sync.

**When to use:** Setting up a design system; automating token export; integrating Figma with engineering workflows.

### Figma API

```
The Figma REST API enables programmatic access to design files.
Base URL: https://api.figma.com/v1/

Authentication: Personal Access Token or OAuth
  Header: X-Figma-Token: {your_token}

Key endpoints:
  GET /files/{file_key}              Full file structure as JSON
  GET /files/{file_key}/nodes        Specific nodes by ID
  GET /files/{file_key}/images       Export images/assets
  GET /files/{file_key}/variables    All variables (design tokens)
  GET /files/{file_key}/components   All components

Common use cases:
  1. Extract all colors → generate CSS custom properties
  2. Export all icon components → generate icon sprite or React components
  3. Monitor file changes → trigger CI/CD pipeline
  4. Pull token values → populate design token files
```

### Design Token Automation

```
The pipeline: Figma Variables → JSON → Platform code

Step 1: Define tokens in Figma Variables panel
  Collections: Colors, Spacing, Typography
  Modes: Light, Dark

Step 2: Export with Tokens Studio (plugin)
  Tokens Studio → Sync to GitHub
  Creates tokens.json (or separate files per collection)
  On Figma save or manual sync → pushes to repo

Step 3: Transform with Style Dictionary (or equivalent)
  Style Dictionary reads JSON → outputs CSS, iOS Swift, Android XML, JS/TS

  config.json:
    {
      "source": ["tokens/**/*.json"],
      "platforms": {
        "css":  { "transformGroup": "css",  "buildPath": "dist/", "files": [{ "destination": "variables.css", "format": "css/variables" }] },
        "ios":  { "transformGroup": "ios",  "buildPath": "ios/",  "files": [{ "destination": "Colors.swift" }] },
        "js":   { "transformGroup": "js",   "buildPath": "src/",  "files": [{ "destination": "tokens.js" }] }
      }
    }

  Run: style-dictionary build

Step 4: Outputs
  dist/variables.css:  --color-accent: #C8E847;
  ios/Colors.swift:    static let accent = UIColor(hex: "#C8E847")
  src/tokens.js:       export const colorAccent = "#C8E847";
```

### Figma-to-Code Pipelines

```
Component code generation:
  Figma → Code (built-in): Figma's "Dev Mode" provides CSS/Swift/Android specs.
  Anima: Generates React/HTML from Figma layouts (review output before using).
  Builder.io: Drag-to-code with AI assistance.

Asset export automation:
  Figma API: GET /files/{key}/images → export all marked assets
  figma-export npm package: CLI tool for batch asset export

Icon pipeline:
  Mark icons in Figma with "exportable" setting
  Script: Figma API → download SVGs → run SVGO → generate React icon components
  Example output:
    export const IconBTC = () => <svg>...</svg>;
    export const IconETH = () => <svg>...</svg>;
```

### Webhooks

```
Figma Webhooks: Get notified when a file changes.
  POST /v2/webhooks (register endpoint)
  Events: FILE_UPDATE, FILE_VERSION_UPDATE, COMMENT

Use for:
  Auto-trigger token export when design file saves
  Notify Slack when a design is updated
  Rebuild Storybook when component library changes
  Run design lint when file updates
```

### Outputs
- Automated token export pipeline (Tokens Studio → Style Dictionary)
- Asset export scripts
- Webhook for automated design-to-code sync

---

## 3. Component Libraries

**Purpose:** Bridge design components in Figma to their code counterparts in React/Vue/Angular — ensuring the design system's components are consistently implemented and documented.

**When to use:** Setting up a design system; onboarding engineers to design components; maintaining parity between Figma and code.

### Storybook — Component Documentation

```
Storybook: An isolated development environment and documentation site for UI components.

Benefits:
  - Each component rendered in isolation (no app context needed)
  - All variants visible in one place (default, hover, error, loading)
  - Interactive controls to test prop combinations
  - Documentation co-located with code

Designer's role in Storybook:
  Review implemented components against Figma spec
  Flag deviations (wrong spacing, missing state, incorrect color)
  Approve component before it enters the shared library
```

### Storybook Stories — What They Look Like

```jsx
// Button.stories.tsx
import { Button } from './Button';

export default {
  title: 'Components/Button',  // hierarchy in the sidebar
  component: Button,
  argTypes: {
    variant: { control: 'select', options: ['primary', 'ghost', 'outline'] },
    label: { control: 'text' },
    disabled: { control: 'boolean' },
    loading: { control: 'boolean' },
  },
};

// Individual stories = individual states
export const Primary = { args: { variant: 'primary', label: 'Connect exchange' } };
export const Ghost = { args: { variant: 'ghost', label: 'Cancel' } };
export const Loading = { args: { variant: 'primary', label: 'Saving...', loading: true } };
export const Disabled = { args: { variant: 'primary', label: 'Submit', disabled: true } };
```

### Figma Code Connect

```
Code Connect: Figma's native feature to link Figma components to code components.

When a developer inspects a Figma component, they see the exact code to use:
  <Button variant="primary" label="Connect exchange" />

Setup:
  Engineers run: npx figma connect create
  Links Figma component node ID to code component
  Publishes to Figma → appears in Dev Mode inspector

Designer's role:
  Ensure Figma component properties match code props exactly.
  If Figma has variant="primary" → code must also use variant, not type or style.
  Coordinate naming with engineers before publishing.
```

### Component Parity Audit

```
Regularly audit that Figma components match code components:

| Figma Component | Code Component | Status |
|-----------------|---------------|--------|
| Button/Primary  | <Button variant="primary"> | ✅ Matched |
| Button/Ghost    | <Button variant="ghost"> | ✅ Matched |
| Card/Default    | <Card variant="default"> | ✅ Matched |
| Badge/Change    | <Badge variant="change"> | ⚠️ Figma has more variants |
| Input/Search    | <Input variant="search"> | ✅ Matched |

Process:
  1. List all Figma components
  2. Find corresponding code component
  3. Compare: variant names, prop names, states, sizes
  4. Flag discrepancies — decide: update Figma to match code, or update code to match Figma

Priority: Name alignment > Visual alignment. Names drive DX.
```

### Component Request Process

```
When a designer needs a new shared component:

1. Check if it exists (in Storybook / Figma library)
2. Check if an existing component can be extended (add a variant)
3. If new component needed → submit proposal:
   - Component name
   - Which screens use it
   - Figma mockup of all variants and states
   - Why existing components don't cover this case

4. Engineer implements → creates Storybook story
5. Designer reviews in Storybook against spec
6. Approve → publish to shared library
```

### Outputs
- Storybook instance with all design system components
- Figma Code Connect mappings for all Tier 1 components
- Component parity audit document
- Component proposal template

---

## 4. Design QA

**Purpose:** Systematically verify that engineered implementations match the design spec — catching regressions, deviations, and missing states before they reach users.

**When to use:** After engineering implements a screen or component; before any release; as a regular cadence after sprint completion.

### Design QA Process

```
1. Prepare (before QA session)
   - Gather: Figma spec, device or browser with implementation, QA checklist
   - Define scope: which screens, which breakpoints, which states
   - Set up side-by-side view (Figma on one screen, implementation on the other)

2. Visual comparison
   - Compare each screen at all breakpoints
   - Use browser DevTools to measure exact pixel values when needed
   - Screenshot overlay: take screenshot of implementation → overlay on Figma at same scale

3. Interaction verification
   - Tap/click every interactive element
   - Verify hover states (desktop)
   - Verify focus states (keyboard navigation)
   - Verify all loading states (throttle network, network panel → block requests)
   - Verify all error states (force API failures)
   - Verify empty states (clear mock data)

4. Document deviations
   - Screenshot + annotation for each issue
   - Severity: Critical / Major / Minor / Cosmetic
   - Expected (from spec) vs. Actual (what's implemented)
   - Link to Figma frame for reference

5. Hand off issue list
   - Share with engineer
   - Agree on priority: what fixes before ship vs. what goes in backlog
   - Re-verify after fixes
```

### QA Checklist

```
Visual
  ✅ Colors match design tokens (no hardcoded hex)
  ✅ Typography matches type scale (correct size, weight, family)
  ✅ Spacing matches 4px grid (verify with DevTools)
  ✅ Border radii correct
  ✅ Shadows / elevation correct
  ✅ Icons correct size and color
  ✅ Images load and display correctly (aspect ratio preserved)
  ✅ Dark/light mode renders correctly

States
  ✅ Default state
  ✅ Hover state (desktop)
  ✅ Focus state (tab to element)
  ✅ Active/pressed state
  ✅ Loading state (with skeleton or spinner)
  ✅ Success state
  ✅ Error state
  ✅ Empty state
  ✅ Disabled state (cannot interact)

Layout
  ✅ Correct at mobile breakpoint (375px)
  ✅ Correct at tablet (768px)
  ✅ Correct at desktop (1440px)
  ✅ Horizontal scroll doesn't appear (overflow hidden)
  ✅ Content doesn't overflow containers
  ✅ Touch targets are at least 44×44px

Interaction
  ✅ All buttons / links are tappable
  ✅ Animations play correctly (duration, easing, trigger)
  ✅ Navigation works (correct screens, correct transitions)
  ✅ Forms validate and submit correctly
  ✅ Keyboard navigation works (Tab order correct)
  ✅ Screen reader: accessible labels present

Content
  ✅ All text matches spec copy
  ✅ Long strings truncate or wrap correctly
  ✅ Numbers formatted correctly (currency, percentages)
  ✅ Dates formatted correctly
```

### Issue Documentation Format

```
Issue: [Short description]
Screen: [Screen name + Figma link]
Severity: Critical / Major / Minor / Cosmetic
Expected: [What the spec shows — include Figma screenshot]
Actual: [What was implemented — include browser screenshot]
Reproduction: [Steps to reach this state]
Notes: [Additional context for the engineer]

Example:
Issue: Button uses wrong background color in loading state
Screen: Add Exchange / Step 2 [Figma: frame link]
Severity: Minor
Expected: Colors.muted (#1C1C1C) background when loading
Actual: Colors.card (#111111) — slightly too dark
Notes: Only visible when loading state is triggered; normal state is correct
```

### Overlay Comparison Technique

```
1. Open Figma frame at 1:1 scale, screenshot it
2. Open implementation in browser at same scale + same viewport size
3. Screenshot browser
4. Open both in image editor (Figma, Photoshop, or even Preview)
5. Layer browser screenshot on top of Figma screenshot at 50% opacity
6. Any misalignments immediately visible as double-images

Tools:
  Figma: Paste screenshot as image → set to 50% opacity → compare
  Chrome Extension: "PixelParallel" or "Perfect Pixel" — overlays design directly in browser
```

### Outputs
- QA issue list with severity ratings
- Annotated screenshots (expected vs. actual)
- Verified ✅ / Not verified ❌ status per screen
- Post-QA sign-off (what's approved to ship)

---

## 5. Technical Constraints

**Purpose:** Design within real-world platform, performance, and engineering constraints — avoiding specs that are impossible or extremely costly to build.

**When to use:** Before finalizing any design; when a developer pushes back on a design decision; when choosing between implementation approaches.

### Platform Constraints by Target

**Web:**
```
Performance budget: CSS bundle, JS bundle, image sizes all affect load time
  Images: < 200KB per above-fold image; WebP preferred; lazy-load below fold
  Fonts: Limit to 2 typefaces, 3–4 weights max; subset to used characters
  Animations: Only transform/opacity at 60fps; avoid layout/paint triggers

Browser rendering:
  Blending modes (mix-blend-mode): supported but may cause layer promotion issues
  filter: CSS filters (blur, brightness) are expensive — use sparingly on animated elements
  backdrop-filter: Limited support; always provide a fallback background color
  CSS variables: Fully supported modern browsers; IE11 not supported
```

**iOS (React Native / Swift):**
```
Safe areas: Always account for notch, Dynamic Island, home indicator
  Use useSafeAreaInsets() — never hardcode margins for safe areas

Performance:
  Main thread: Don't block it with heavy JS during animation
  useNativeDriver: true mandatory for all transform/opacity animations
  FlatList: Only renders visible items — designs for infinite scroll are fine

Platform expectations:
  Tab bar: 49pt height (standard) — custom heights feel wrong to iOS users
  Navigation: Swipe right to go back is a system gesture — don't intercept it
  Status bar: Light/dark style must be set explicitly for dark backgrounds
  Haptics: iOS users expect haptic feedback on significant interactions
```

**Android (React Native):**
```
Back gesture: Android has a system back gesture — always handle it correctly
  Modals must dismiss; navigation must go back

Material Design conventions:
  Users expect Material-like behaviors (FAB, bottom navigation, snackbars)
  Deviating too far creates confusion — match conventions when in doubt

Performance:
  Lower-end devices are common — test on midrange Android (not just Pixel flagship)
  Animations must degrade gracefully on low-end hardware
```

### Performance-Aware Design Decisions

```
High cost operations (avoid or use sparingly):
  - Blur effect (backdrop-filter, Gaussian blur): expensive, especially animated
  - Large list virtualization: FlatList handles this, but each item must be cheap
  - Custom fonts: each font file = network request; limit weights
  - Full-screen video backgrounds: battery drain, data cost, mobile performance
  - Heavy gradients on animated elements: GPU-intensive

Low cost (use freely):
  - Flat colors
  - Simple border-radius
  - Opacity transitions
  - Transform (translate, scale, rotate)
  - CSS Grid/Flexbox layouts

Design decision framework:
  Ask: "Does this effect require additional engineering effort beyond standard?"
  If yes: Is the visual benefit worth the engineering cost?
  If in doubt: Ask an engineer — "How hard is this to build?"
```

### Animation Technical Constraints

```
Avoid these animation patterns:
  Width/height animation: Causes layout recalculation on every frame
  → Use transform: scaleX/scaleY instead

  Color animation: Causes paint on every frame
  → Use opacity transitions or CSS filter instead

  Box shadow animation: Repaints every frame
  → Use opacity transition on a pseudo-element with the shadow

  Animating inside a scrolling container: Compound transforms create artifacts
  → Test thoroughly; sometimes needs position: fixed workaround

React Native-specific:
  Cannot animate backgroundColor with useNativeDriver: true
  → Use Animated.timing with useNativeDriver: false for color (accepts perf hit)
  → Or use opacity crossfade between two colored layers instead
```

### Engineering Cost Estimation for Designs

```
Quick cost assessment — helps designers prioritize polish:

Low effort (a few hours):
  - Adding a new color token
  - Minor spacing adjustments
  - Simple loading spinner
  - Text content changes

Medium effort (1–3 days):
  - New component variant
  - Simple entrance animation (fade + slide)
  - New screen with static content
  - Responsive layout adjustment

High effort (1–2 weeks):
  - Complex gesture interaction (swipe-to-delete, drag-to-reorder)
  - Real-time data integration
  - Complex multi-step animation sequence
  - Shared element transition between screens

Very high (2+ weeks):
  - Custom camera/AR feature
  - Complex data visualization (custom chart)
  - Real-time sync with WebSocket
  - Offline-first architecture

Rule: Match design ambition to available engineering time.
  A beautiful detail no one builds = no design value.
```

### Outputs
- Constraint checklist per platform (iOS, Android, Web)
- Design review with engineer to identify high-effort items
- Alternative design options for costly interactions
- Performance budget for animations and assets
