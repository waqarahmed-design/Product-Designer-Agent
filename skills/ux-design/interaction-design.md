# Interaction Design Methods

## Table of Contents
1. [User Flow Creation](#1-user-flow-creation)
2. [Task Flow Design](#2-task-flow-design)
3. [State Design](#3-state-design)
4. [Edge Case Handling](#4-edge-case-handling)
5. [Progressive Disclosure](#5-progressive-disclosure)
6. [Affordance Design](#6-affordance-design)
7. [Feedback Design](#7-feedback-design)
8. [Microcopy](#8-microcopy)

---

## 1. User Flow Creation

**Purpose:** Map all paths a user can take through a product to understand the full experience, identify gaps, and align teams on the intended journey.

**When to use:** Before wireframing, when adding new features that span multiple screens, when analyzing where users drop off.

### User Flow Notation

```
Oval       = Start / End
Rectangle  = Screen or page
Diamond    = Decision point (yes/no branch)
Arrow      = Navigation direction
Dashed     = Conditional path (requires auth, feature flag, etc.)
[N]        = Screen ID for cross-referencing with specs
```

### Flow Levels

| Level | Scope | Use For |
|-------|-------|---------|
| **High-level flow** | 5–10 nodes | Executive alignment, early discovery |
| **Mid-level flow** | 15–30 nodes | Design handoff, feature scoping |
| **Detailed flow** | 30+ nodes | Complex logic, edge case mapping |

### Flow Construction Process

1. **Define entry points** — where can users arrive at this flow? (direct, email link, push notification, back navigation)
2. **Map the happy path** first — the ideal sequence with no errors
3. **Branch on decisions** — every yes/no, logged-in/out, has-data/empty splits into branches
4. **Map error paths** — what happens when each step fails?
5. **Define exit points** — where can users leave? (complete, abandon, error, external link)

### Common Flow Anti-patterns
- **Dead ends** — screens with no forward path and no back button
- **Missing empty states** — flows that assume data always exists
- **Asymmetric navigation** — users can get in but can't get back out
- **Uncaptured re-entry** — flow doesn't account for users who return mid-task

### Outputs
- Flow diagram at the appropriate level of detail
- List of decision points and branching conditions
- Identified gaps (screens that need to be designed)

---

## 2. Task Flow Design

**Purpose:** Design the most efficient sequence of steps for a user to complete a specific task — optimizing for clarity, speed, and error avoidance.

**When to use:** Designing any multi-step interaction (checkout, onboarding, form submission, settings change).

### Task Analysis

Before designing the flow, analyze the task:

```
Task: [What the user wants to accomplish]
Trigger: [What prompts them to start]
Preconditions: [What must be true before they can start]
Steps (current): [How they do it today]
Steps (ideal): [How it could work with better design]
Success state: [How users know the task is complete]
Failure states: [What can go wrong at each step]
Frequency: [How often users do this]
```

### Step Minimization Principles

- **Eliminate mandatory steps** — every required step should justify its existence
- **Smart defaults** — pre-fill what you know; don't ask what you can infer
- **Progressive commitment** — ask for less upfront; gather more details after initial value is delivered
- **Parallel steps** — can two steps happen simultaneously rather than sequentially?
- **Conditional branching** — don't show steps that don't apply to this user's situation

### Multi-Step Flow Patterns

| Pattern | When to Use |
|---------|-------------|
| **Linear wizard** | Sequential steps with clear dependencies (onboarding, checkout) |
| **Hub and spoke** | Central screen with optional sub-tasks (settings, profile) |
| **Branching** | Different paths based on user choice or context (support triage) |
| **Resumable flow** | Long tasks users may need to pause (applications, complex forms) |

### Resumable Flow Design Rules
- Show progress state on re-entry ("You're 60% done — continue where you left off")
- Never lose user input on accidental navigation away
- Allow editing completed steps without restarting
- Show a clear summary before final submission

### Outputs
- Step-by-step task flow with decision points
- Annotated notes on smart defaults and conditional steps
- Identified steps that could be eliminated or merged

---

## 3. State Design

**Purpose:** Define every possible visual and functional state of an interactive element so the interface is never silent, ambiguous, or broken-looking.

**When to use:** Designing any interactive component — buttons, inputs, cards, toggles, list items.

### The Eight States

Every interactive element should be designed for:

| State | Trigger | Design Obligation |
|-------|---------|------------------|
| **Default** | Initial render | Clear affordance that interaction is possible |
| **Hover** | Cursor enters (desktop) | Visual change indicating interactivity |
| **Focus** | Keyboard navigation / tab | Visible focus ring (never remove outline without replacement) |
| **Active / Pressed** | Mouse down / tap | Visual compression or color shift confirming touch registered |
| **Loading** | Async action in progress | Spinner, skeleton, or progress indicator; disable further interaction |
| **Success** | Action completed | Confirmation (color, icon, message) — brief, not permanent |
| **Error** | Action failed / invalid | Specific message, field highlighted, recovery path visible |
| **Disabled** | Action unavailable | Reduced opacity, no pointer, tooltip explaining why if non-obvious |

### State Design Rules

**Hover vs. Active distinction:**
- Hover = "I can interact here" (subtle change)
- Active = "I am interacting now" (stronger, immediate change)
- Never make them identical

**Loading state requirements:**
- Show within 100ms of triggering — silence feels like a crash
- Disable the button/trigger during loading — prevent duplicate submissions
- If > 1 second, show determinate progress if possible
- Skeleton screens > spinners for content-loading states

**Error state requirements:**
- Error message must be specific — "Invalid input" is useless; "Email must include @" is helpful
- Position error message adjacent to the field that caused it
- Don't clear the user's input — show what they typed with the error
- Red alone isn't sufficient — add an icon for colorblind users

**Disabled state requirements:**
- Never disable a CTA without explaining why
- Use `cursor: not-allowed` + reduced opacity
- Consider whether the element should be hidden instead of disabled

### State Inventory Template

For each component, document:
```
Component: [Name]
Default:   [Description + visual spec]
Hover:     [Description + visual spec]
Focus:     [Description + visual spec]
Active:    [Description + visual spec]
Loading:   [Description + visual spec]
Success:   [Description + visual spec]
Error:     [Description + visual spec]
Disabled:  [Description + visual spec]
```

### Outputs
- State inventory for all interactive components
- Component spec with all 8 states illustrated
- Notes on state transitions (duration, easing)

---

## 4. Edge Case Handling

**Purpose:** Design for the full range of scenarios users encounter — not just the happy path — so the product feels robust and trustworthy.

**When to use:** After designing the happy path, before finalizing any screen.

### Edge Case Categories

**Empty states** — what the screen looks like when there's no data yet:
```
Types:
  First-time empty   — user has never added data (onboarding opportunity)
  User-cleared empty — user deleted everything (confirm + recovery)
  Search empty       — no results match query (search guidance)
  Error empty        — data failed to load (retry + explanation)

Good empty state = illustration/icon + headline + body copy + CTA
Bad empty state = blank screen or generic "No items found"
```

**Error states** — what happens when things fail:
```
Network error       — no connection, request timed out
Server error        — 500, service unavailable
Not found           — 404, deleted resource
Permission error    — 403, unauthorized
Validation error    — user input doesn't meet requirements
Partial failure     — some items loaded, some didn't
```

**Boundary conditions:**
- Minimum values (0 items, $0 balance, 0 characters)
- Maximum values (character limits, max file size, max list length)
- Exactly 1 item (list vs. singular treatment)
- Very long content (long names, long text, wrapping behavior)
- Very short content (single character names, empty strings)

**Unusual user contexts:**
- Slow/offline connection
- Small screen or zoomed-in viewport
- Large text size / system font scaling
- High contrast mode
- RTL (right-to-left) language

### Edge Case Checklist (per screen)

- [ ] Empty state designed (first-time and user-cleared)
- [ ] Error state designed (network and server)
- [ ] Loading state designed
- [ ] Long text content tested (names, descriptions, labels)
- [ ] Zero-item list state
- [ ] Single-item list state (does it look like a list or a singleton?)
- [ ] Character limit behavior (truncate vs. wrap vs. expand)
- [ ] Offline / degraded behavior considered
- [ ] Permission-denied state

### Empty State Design Template

```
[Illustration or icon — humanizes the void]
[Headline — direct, active: "No transactions yet"]
[Body — explain context and next step: "Your spending history will appear here after your first purchase."]
[CTA button — primary action that fills the empty state: "Add your first transaction"]
```

### Outputs
- Edge case inventory per screen
- Designed states for empty, error, and boundary conditions
- Annotation notes on fallback behavior

---

## 5. Progressive Disclosure

**Purpose:** Reveal complexity gradually, showing only what users need at each step — reducing cognitive load and making interfaces feel simpler than they are.

**When to use:** Complex forms, feature-rich settings, advanced configuration, data-dense dashboards.

### Disclosure Levels

```
Level 0 — Always visible
  The primary content; what most users need most of the time

Level 1 — Revealed on interaction
  Secondary content; shown on expand, tap, or hover
  Trigger: "Show more", chevron, "Advanced settings"

Level 2 — Revealed on explicit request
  Expert content; deep configuration, edge case options
  Trigger: "Advanced", "Developer settings", secondary navigation

Level 3 — Separate surface
  Specialized content; separate modal, drawer, or screen
  Trigger: deliberate navigation, "Manage", "Configure"
```

### Progressive Disclosure Patterns

**Show/Hide (accordion):**
```
▸ Advanced options          ← collapsed
▾ Advanced options          ← expanded
  [revealed content]
```
Best for: settings panels, FAQ sections, secondary form fields

**Drill-down navigation:**
```
Summary card → Detail screen → Edit screen
```
Best for: list→detail patterns, settings sections

**Staged forms (wizard):**
```
Step 1: [essential info only]
Step 2: [additional detail, shown because step 1 is complete]
Step 3: [confirmation, shown because step 2 is complete]
```
Best for: onboarding, checkout, complex setup

**Contextual reveal:**
```
[Checkbox: "Ship to different address"]
↓ checked
[Address fields appear]
```
Best for: conditional fields, optional configurations

### Disclosure Decision Rules

- If fewer than 20% of users need an option, progressively disclose it
- Always show the most common/important options by default
- Disclosed content must feel connected to its trigger (visual proximity, animation)
- Never hide content that users need to complete a required task

### Outputs
- Disclosure hierarchy marked on wireframes (L0/L1/L2)
- Trigger designs for each disclosure level
- Animation spec for reveal/hide transitions

---

## 6. Affordance Design

**Purpose:** Make interactive elements obviously actionable — so users never have to wonder "can I click this?" or "is this a button?"

**When to use:** Any interactive element design; critical review of any UI where user testing showed hesitation or confusion about interactivity.

### Visual Affordance Signals

| Signal | Examples | Effect |
|--------|----------|--------|
| **Elevation / shadow** | Raised button, card shadow | "This stands above the surface — it can be pressed" |
| **Border** | Outlined button, input border | "This is a distinct, interactive region" |
| **Fill / background** | Colored button, highlighted row | "This has a distinct state and responds to interaction" |
| **Underline** | Text link | "This is a hyperlink" |
| **Chevron / arrow** | Row with right arrow | "Tapping this navigates deeper" |
| **Cursor change** | pointer on hover | "This is clickable" |
| **Familiar shape** | Rectangle = button, magnifier = search | "I recognize this pattern" |

### False Affordance Anti-patterns (things that look interactive but aren't)

- Underlined text that isn't a link
- Colored boxes that look like buttons but are just labels
- Card-shaped containers that aren't clickable despite resembling clickable cards
- Rows with chevrons on non-navigable items
- Text styled like a link but is just decorative

### Clickability Clarity Test

For any UI element, ask:
1. Does it look different from surrounding non-interactive content?
2. Does it look like something a user has seen before that was interactive?
3. Does hovering (desktop) or pressing (mobile) produce immediate visual feedback?
4. If removed, would a user assume the page is broken?

If no to any: strengthen the affordance.

### Interactive Region Sizing

The affordance must match the actual touch/click target:
- Button label and its visible container should match — padding shouldn't extend the target invisibly
- For icon-only controls, make the entire icon + padding area the tap target, not just the icon
- Row-level tap targets: the entire row is tappable, not just the text

### Outputs
- Annotated affordance notes on wireframes
- List of false affordances removed from design
- Touch target sizing spec per interactive element

---

## 7. Feedback Design

**Purpose:** Ensure the system communicates the result of every user action — confirming what happened, what's happening, and what will happen next.

**When to use:** Any interactive element that triggers a state change, asynchronous operation, or navigational transition.

### Feedback Timing Framework

| Action type | Max feedback delay | Feedback type |
|-------------|-------------------|---------------|
| Button tap / click | < 100ms | Visual state change (pressed state) |
| Navigation | < 300ms | Screen transition begins |
| Short async operation (< 2s) | < 100ms | Loading indicator starts |
| Long async operation (> 2s) | < 100ms | Progress bar or step indicator |
| Success completion | Immediate | Success message / state |
| Error | Immediate | Error message adjacent to cause |

**The 100ms rule:** Any delay longer than 100ms between action and visible response feels broken. Always provide immediate visual feedback even before the async result returns.

### Feedback Types

**Inline feedback:** feedback within the element that was acted on
- Button: pressed state → loading state → success state → default
- Input: typing → validation → error or success indicator

**Toast / snackbar:** brief system-level message that auto-dismisses
- Use for: background completions, undo opportunities, non-critical errors
- Duration: 3–5 seconds; provide dismiss control
- Positioning: bottom of screen (mobile), top-right (desktop) — away from primary content

**Banner / alert:** persistent message requiring user acknowledgment
- Use for: critical errors, important status changes, action required
- Must have: explicit dismiss or action button; auto-dismiss is inappropriate

**Modal feedback:** blocks all interaction until acknowledged
- Use sparingly — only for irreversible actions or critical information
- Destructive action confirmation: "Delete project?" → "Cancel" / "Delete permanently"

### Feedback Content Rules

**Success messages:**
- Say what was done: "Password updated" not "Success"
- Optionally confirm next state: "Your order was placed. You'll receive a confirmation email."
- Brief — users don't read long success messages

**Error messages:**
- Be specific: "Incorrect password" not "Authentication failed"
- Be actionable: tell users what to do next
- Be non-blaming: "That email isn't registered" not "You entered an invalid email"
- Never expose system internals: no stack traces, no error codes alone

**Loading messages:**
- Show progress if known: "Uploading 3 of 5 files..."
- Set expectations if long: "This usually takes about 30 seconds"
- Use skeleton screens for content areas, spinners for actions

### Outputs
- Feedback spec per interactive element (timing + type + content)
- Toast/banner design specs
- Error message library

---

## 8. Microcopy

**Purpose:** Write the small interface text that guides users through the product — labels, placeholders, error messages, tooltips, confirmation dialogs, empty states, CTAs — with clarity and appropriate tone.

**When to use:** Any time UI text is being written or reviewed.

### Microcopy Locations

| Location | Purpose | Length |
|----------|---------|--------|
| **Button labels** | Describe the action | 1–3 words |
| **Input labels** | Identify the field | 1–3 words |
| **Placeholder text** | Example or hint (not a substitute for labels) | Brief |
| **Helper text** | Explain format or requirements | 1 sentence |
| **Error messages** | Describe problem + recovery | 1–2 sentences |
| **Empty states** | Context + next step | 1 headline + 1–2 sentences + CTA |
| **Tooltips** | Explain unfamiliar terms or actions | 1–2 sentences |
| **Confirmation dialogs** | Confirm irreversible actions | Headline + body + 2 button labels |
| **Onboarding hints** | Orient new users | Brief, dismissible |
| **Loading messages** | Set expectations | 1 phrase |
| **Success messages** | Confirm completion | 1 sentence |

### Microcopy Principles

**Be specific:**
- Bad: "An error occurred"
- Good: "We couldn't save your changes — check your connection and try again"

**Use active voice:**
- Bad: "Your account has been deleted"
- Good: "We deleted your account"

**Verb-first CTAs:**
- Bad: "Confirmation", "Submission", "Account Deletion"
- Good: "Confirm", "Submit", "Delete Account"

**Match the action to the button:**
- Dialog: "Are you sure you want to delete this file?"
- Bad buttons: "Yes" / "No"
- Good buttons: "Delete file" / "Keep file"

**Avoid jargon:**
- Bad: "Authentication failed — invalid credentials"
- Good: "Wrong email or password. Try again."

**Tone calibration:**
| Context | Tone |
|---------|------|
| Onboarding | Warm, encouraging |
| Errors | Calm, specific, non-blaming |
| Destructive actions | Direct, neutral (don't minimize the consequence) |
| Empty states | Light, inviting |
| Loading | Neutral, informative |
| Success | Brief, positive |

### Confirmation Dialog Template

```
[Headline — describe consequence, not question]
"Delete 'Project Alpha'?"  not  "Are you sure?"

[Body — explain what happens, especially if irreversible]
"This will permanently delete the project and all its files.
This cannot be undone."

[Buttons]
Primary (destructive): "Delete project"     ← matches headline noun
Secondary (cancel):    "Keep project"       ← affirmative, not just "Cancel"
```

### Outputs
- Microcopy for all labels, errors, empty states, and confirmations
- Tone guidelines per context type
- Error message library with specific messages per error type
