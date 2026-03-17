---
name: ux-design
description: UX design skill covering interaction design, wireframing, prototyping, usability, accessibility, and responsive design. Use when designing user flows, task flows, state design, edge cases, progressive disclosure, affordances, feedback design, or microcopy. Also use when wireframing (low or high fidelity), building interactive or code-based prototypes, or doing rapid prototyping. Also use for accessibility work including WCAG compliance, keyboard navigation, screen reader optimization, color contrast, focus management, inclusive design, cognitive load, error prevention, or forgiveness design. Also use for responsive and adaptive design including mobile-first design, breakpoint strategy, touch targets, responsive layout patterns, platform-specific patterns (iOS/Android/Web), or cross-device continuity. Triggers on: user flow, task flow, state design, empty state, edge case, progressive disclosure, affordance, feedback, microcopy, wireframe, prototype, Figma, Framer, ProtoPie, WCAG, accessibility, keyboard navigation, screen reader, color contrast, focus, tab order, inclusive design, cognitive load, error handling, mobile-first, breakpoints, touch target, responsive layout, iOS, Android, cross-device.
---

# UX Design

Comprehensive UX design guidance: interaction design, state design, feedback, forms, accessibility, cognitive load, mobile UX, and responsive design. 29 named methods, 100+ named rules, anti-pattern tables, and pre-delivery checklists.

---

## Mandatory Pre-UX Checklist

Complete this before wireframing or writing any interaction code. Output it at the top of your response.

```
UX BRIEF
───────────────────────────────────────────────────────
User goal:        [What does the user want to accomplish?]
Entry point:      [Where does this flow start? Direct / notification / link / nav]
Success state:    [How does the user know they succeeded?]
Failure states:   [What can go wrong? List 3–5 scenarios]
Edge cases:       [Empty / error / max / min / permission denied]
Platform:         [iOS / Android / Web / cross-platform]
Primary action:   [ONE verb: the single most important thing this screen does]
───────────────────────────────────────────────────────
```

Never skip this. Flows designed without a defined success state and failure states ship with holes.

---

## Rule Categories by Priority

| Priority | Category | Impact | Key Checks (Must Have) | Anti-Patterns (Avoid) |
|----------|----------|--------|------------------------|------------------------|
| 1 | Accessibility | CRITICAL | Contrast 4.5:1, keyboard nav, ARIA labels, touch targets 44px | Removing focus rings, color-only information, icon-only buttons without labels |
| 2 | Interaction & States | CRITICAL | All 8 states designed, feedback within 100ms, affordance clarity | Silent buttons, no loading state, identical hover/active states |
| 3 | Flow & Navigation | HIGH | No dead ends, predictable back, deep links, state preserved | Broken back, asymmetric entry/exit, missing empty states |
| 4 | Feedback & Microcopy | HIGH | Specific error messages, 100ms visual response, recovery path | "An error occurred", silent success, blame-y tone |
| 5 | Forms & Inputs | HIGH | Visible labels, on-blur validation, error below field, one primary CTA | Placeholder-only label, validation on keystroke, ambiguous submit |
| 6 | Cognitive Load | MEDIUM | Progressive disclosure, chunking, max 5–7 nav items, defaults | Overwhelming upfront, no defaults, requiring recall not recognition |
| 7 | Mobile & Touch | MEDIUM | Touch targets 44pt, safe areas, native gesture patterns, no hover-only | Targets <44pt, content under notch, blocking system gestures |
| 8 | Edge Cases | MEDIUM | Empty states with CTA, error states with retry, boundary conditions | Blank screens on no data, silent failures, no offline state |

---

## Quick Reference

### §1. Flow & Information Architecture (HIGH)

- `no-dead-ends` — Every screen has a forward path or an explicit back — never a screen with nowhere to go
- `symmetric-navigation` — If users can navigate into a state, they must be able to navigate out of it
- `deep-link-all-screens` — Every key screen must be reachable via deep link / URL for notifications and sharing
- `back-preserves-state` — Back navigation restores previous scroll position, filter state, and form input
- `entry-points-designed` — Map all entry points: direct navigation, notification tap, email link, back from sub-screen
- `capture-re-entry` — Flows that users pause mid-task must handle re-entry gracefully ("continue where you left off")
- `happy-path-first` — Design the ideal path first, then branch for errors, decisions, and empty states
- `decision-points-minimized` — Every fork in a flow is a potential drop-off — minimize or merge decision points
- `nav-max-five` — Primary navigation items: 5 maximum on mobile; more = cognitive overload and mis-tap risk
- `nav-hierarchy-clear` — Primary nav (bottom bar/tabs) vs. secondary nav (settings, sub-pages) must be visually distinct
- `nav-active-state` — Current location is always highlighted in the navigation; never ambiguous where the user is
- `flow-exit-designed` — Define where users exit: task complete, abandon, error, external link — each with appropriate UI

**Anti-patterns:**
| What you did | What to do instead |
|---|---|
| Screen has no back button and no forward path | Add explicit navigation or make it unreachable |
| Back button takes user to wrong screen | Use proper navigation stack; router.back() vs. router.replace() |
| Nav item missing from deep screen | Keep core navigation reachable from all levels |
| Flow assumes user always has data | Design empty and first-time states for every data-dependent screen |

---

### §2. Interaction & State Design (CRITICAL)

Every interactive element must be designed for all 8 states. Not 4. Not 6. All 8.

| State | Trigger | Required design |
|-------|---------|----------------|
| **Default** | Initial render | Clear affordance that interaction is possible |
| **Hover** | Cursor over (desktop) | Subtle signal: "I can interact here" |
| **Focus** | Keyboard tab | Visible ring — never `outline: none` without replacement |
| **Active / Pressed** | Mouse down / tap | Stronger immediate change — distinct from hover |
| **Loading** | Async in progress | Indicator starts within 100ms; button disabled |
| **Success** | Action completed | Specific confirmation; brief (3–5s), not permanent |
| **Error** | Action failed | Specific message + icon + recovery path |
| **Disabled** | Action unavailable | Reduced opacity + tooltip explaining why |

Named rules:

- `feedback-100ms` — Any action with no visual response within 100ms feels broken; always provide immediate press state
- `loading-disable` — Disable the trigger during async operations to prevent duplicate submissions
- `loading-threshold` — < 300ms: no indicator; 300ms–1s: spinner; > 1s: skeleton screen; > 3s: progress with estimate
- `skeleton-over-spinner` — Use skeleton screens for content-loading areas; spinners for action-triggered operations
- `error-specific` — Error messages must name the cause: "Email already registered" not "Something went wrong"
- `error-adjacent` — Place error message directly below the field or element that caused it
- `error-preserves-input` — Never clear user input when showing a validation error; show what they typed
- `disabled-explains-why` — If a CTA is disabled, a tooltip or adjacent message must explain the condition blocking it
- `hover-active-distinct` — Hover = "I can click this" (subtle); Active = "I am clicking this" (stronger); never the same
- `affordance-visual` — Interactive elements must look different from non-interactive ones: border, fill, elevation, or underline
- `false-affordance-none` — Never style a non-interactive element to look interactive (colored box, underlined text, chevron on non-nav row)
- `press-feedback-mobile` — On mobile, scale (0.95–0.97) or opacity change within 80ms confirms tap registered
- `success-brief` — Success feedback lasts 3–5 seconds; permanent success states cause confusion about current status
- `eight-states-rule` — Before shipping any interactive component, verify all 8 states are designed and implemented

**Anti-patterns:**
| What you did | What to do instead |
|---|---|
| Button shows no loading state | Show spinner + disable button within 100ms of tap |
| Error message says "Invalid input" | Say exactly what's wrong and how to fix it |
| Disabled button with no explanation | Add tooltip or helper text stating the condition |
| Hover and focus look identical | Hover: color shift; Focus: visible ring (2px+ outline) |
| Success state persists indefinitely | Auto-dismiss after 3–5s or on next interaction |

---

### §3. Feedback & Microcopy (HIGH)

- `success-says-what` — "Password updated" not "Success"; name what was done
- `error-non-blaming` — "That email isn't registered" not "You entered an invalid email"
- `error-has-recovery` — Every error message includes what the user should do next
- `no-jargon` — "Wrong email or password" not "Authentication failed — invalid credentials"
- `cta-verb-first` — Button labels start with a verb: "Save changes" not "Confirmation"
- `cta-matches-dialog` — Dialog: "Delete this file?" → Button: "Delete file" / "Keep file" — never "Yes" / "No"
- `tone-calibrated` — Onboarding = warm; Errors = calm + specific; Destructive = direct and neutral; Empty states = inviting
- `toast-3-to-5s` — Auto-dismiss toasts in 3–5 seconds; always provide a manual dismiss
- `toast-bottom-mobile` — Toasts appear at the bottom on mobile; top-right on desktop — never over primary content
- `placeholder-not-label` — Placeholder text is supplementary (example format); it is never a substitute for a visible label
- `helper-text-persistent` — Helper text explaining format or constraints must remain visible while the field is focused
- `confirmation-names-item` — "Delete 'Project Alpha'?" not "Are you sure?" — state exactly what will be affected
- `confirmation-quantifies` — If multiple items affected: "This will delete 3 projects and 47 files" — quantify the impact
- `loading-sets-expectation` — If an operation takes > 3s: "This usually takes about 30 seconds" reduces perceived wait

**Tone calibration:**
| Context | Tone | Example |
|---------|------|---------|
| Onboarding | Warm, encouraging | "You're all set — your portfolio is ready" |
| Errors | Calm, specific, non-blaming | "We couldn't connect to Binance. Check your API key." |
| Destructive | Direct, neutral | "This will permanently delete your account." |
| Empty states | Light, inviting | "No assets yet. Connect an exchange to get started." |
| Loading | Neutral, informative | "Syncing your portfolio..." |
| Success | Brief, positive | "Connected successfully." |

---

### §4. Forms & Inputs (HIGH)

- `label-always-visible` — Every input has a visible label above it — not inside as placeholder-only
- `required-marked` — Required fields are marked (asterisk + legend or "Required" text) — never color alone
- `error-below-field` — Validation error appears directly below the field it refers to; never only at the top of the form
- `validate-on-blur` — Validate when the field loses focus, not while the user is actively typing
- `no-keystroke-errors` — Never show error states while the user is still typing; wait for blur
- `password-reveal` — All password fields have a show/hide toggle
- `autofill-supported` — Use `autocomplete` and `textContentType` attributes so system autofill works
- `input-type-keyboard` — Use semantic input types (`email`, `tel`, `number`, `url`) to trigger the correct mobile keyboard
- `multi-step-progress` — Multi-step forms show step count and current position; allow back navigation to edit previous steps
- `autosave-long-forms` — Forms taking > 2 minutes should autosave drafts to prevent data loss on accidental dismissal
- `confirm-before-dismiss` — Confirm before dismissing a form/modal with unsaved user input
- `destructive-visual-separation` — Destructive form actions (delete, deactivate) are visually separated from primary submit
- `focus-first-error` — On submit with errors: auto-focus the first invalid field; screen reader gets error summary
- `inline-success` — Show inline success checkmark on fields that pass validation (password strength, username availability)
- `field-grouping` — Related fields are visually grouped; use section headers or card containers for long forms

**Validation timing:**
| Type | When to validate | Why |
|------|-----------------|-----|
| Format (email, phone) | On blur | User needs to finish before format is valid |
| Real-time constraints | While typing | Character count, password strength — benefit from live feedback |
| Cross-field (password confirm) | On second field blur + on submit | Needs both values to compare |
| Server-side (username taken) | On blur + debounced | Needs network; don't fire on every keystroke |
| Never | On first keystroke | Showing errors before user finishes types is hostile UX |

---

### §5. Accessibility & Inclusivity (CRITICAL)

- `contrast-4-5` — Normal text: 4.5:1 minimum contrast ratio against background
- `contrast-3-large` — Large text (≥18pt or ≥14pt bold): 3:1 minimum
- `contrast-ui-3` — UI components (borders, icons, interactive states): 3:1 minimum
- `focus-ring-visible` — Focus indicators: minimum 2px, 3:1 contrast against adjacent colors — never removed without replacement
- `keyboard-full-nav` — Every feature completable by keyboard alone: Tab, Shift+Tab, Enter, Space, Escape, Arrow keys
- `escape-closes-all` — Escape key closes any modal, drawer, popover, or overlay — always
- `focus-trap-modals` — Modals trap focus within themselves; Tab cycles only inside; focus returns to trigger on close
- `focus-order-logical` — Tab order matches visual reading order; never jumps unexpectedly
- `aria-icon-buttons` — Icon-only buttons must have `aria-label`; SVG inside must have `aria-hidden="true"`
- `alt-meaningful` — Meaningful images have descriptive alt text; decorative images have `alt=""`
- `color-not-only` — Color is never the sole differentiator: errors need icon + message, not just red border
- `aria-live-errors` — Form errors use `role="alert"` or `aria-live="polite"` to notify screen readers
- `semantic-html-first` — Use native HTML elements (`<button>`, `<a>`, `<nav>`) before ARIA — native semantics are free
- `touch-target-44` — Minimum 44×44pt (iOS) / 48×48dp (Android) for all interactive elements
- `target-spacing-8` — Minimum 8pt gap between adjacent touch targets to prevent mis-taps
- `dynamic-type` — Text must scale with system font size settings without truncation or layout breaking
- `reduced-motion` — All animations respect `prefers-reduced-motion`; UI must remain usable with motion disabled
- `plain-language` — Interface copy is understandable at a Grade 8 reading level; no internal jargon

**Anti-patterns:**
| What you did | What to do instead |
|---|---|
| `outline: none` with nothing replacing it | Design a custom 2px focus ring with 3:1 contrast |
| Red border only for form error | Red border + error icon + specific text message |
| Icon-only button with no label | Add `aria-label="Close"` to the button; `aria-hidden` on SVG |
| Hover-only interaction on touch screen | Provide tap/click alternatives for all hover interactions |
| Touch target smaller than 44px | Add padding to extend hit area without changing visual size |
| Animation with no reduced-motion alternative | Wrap in `@media (prefers-reduced-motion)` to disable/simplify |

---

### §6. Cognitive Load & Usability (MEDIUM)

- `one-primary-action` — Each screen has one primary CTA; secondary actions are visually subordinate
- `hicks-law` — Decision time grows with number of choices; limit primary nav to 5–7 items; limit actions per screen
- `recognition-over-recall` — Show options (dropdown, history, suggestions) rather than requiring users to remember
- `smart-defaults` — Pre-fill known values; select the most common option by default; don't ask what you can infer
- `progressive-disclosure` — Reveal complexity in layers: Level 0 = always visible; Level 1 = on interaction; Level 2 = on explicit request
- `chunking` — Group related information visually; the eye scans groups faster than undifferentiated lists
- `no-unnecessary-steps` — Every step in a flow must justify its existence; eliminate, merge, or defer anything optional
- `progressive-commitment` — Ask for minimal information upfront; gather more after initial value is delivered
- `whitespace-breathing-room` — Dense layouts increase cognitive load; whitespace is functional, not waste
- `avoid-orphaned-info` — Information that requires context from another screen to be meaningful should live near that context
- `familiar-patterns` — Use UI patterns users already know from other products; don't invent new interactions for solved problems
- `task-completion-estimate` — For multi-step flows: show step count ("Step 2 of 4") and estimated time for long processes

**Cognitive load audit questions — ask these for every screen:**
- How many decisions must the user make to accomplish their goal?
- Is any information displayed that the user doesn't need right now?
- Are any terms or labels unfamiliar to the target user?
- Must the user remember anything from a previous screen?
- Are there more than 2 competing primary actions?

---

### §7. Mobile & Touch UX (HIGH)

- `touch-44-minimum` — All interactive elements: minimum 44×44pt on iOS / 48×48dp on Android — no exceptions
- `extend-hit-area` — Visual icon can be smaller (20pt); padding extends the tap area to 44pt minimum
- `safe-area-all-screens` — Use `useSafeAreaInsets()` on every screen; never hardcode status bar or home indicator values
- `content-clear-tab-bar` — Floating tab bars need `paddingBottom: insets.bottom + tabBarHeight` on all scroll views
- `native-gestures-respected` — Never block or conflict with system gestures: iOS swipe-back, Android predictive back
- `no-hover-only` — Hover states are decorative on touch; critical functionality must have a tap/press alternative
- `swipe-has-affordance` — Swipe actions (delete, archive) must show a visual hint; users can't discover hidden swipes reliably
- `bottom-bar-top-level-only` — Bottom navigation is for top-level screens only; never nest sub-navigation inside it
- `modal-swipe-dismiss` — Bottom sheets and modals can be dismissed by swipe-down on mobile; always provide visible close button too
- `ios-tab-bar-5-max` — iOS tab bar maximum 5 items (Apple HIG); more requires a "More" pattern or restructuring
- `haptic-confirmations` — Use haptic feedback for significant confirmations (payment sent, file deleted); avoid overuse
- `scroll-beneath-fixed` — Floating/fixed elements don't push content; use explicit padding to make content reachable
- `pull-to-refresh` — Use `RefreshControl` with brand accent color for pull-to-refresh on list screens
- `input-keyboard-avoidance` — Text inputs must scroll into view when keyboard appears; use `KeyboardAvoidingView`
- `landscape-works` — Layout must remain operable in landscape orientation; test on real device

**iOS vs. Android quick conventions:**
| Pattern | iOS | Android |
|---------|-----|---------|
| Primary navigation | Bottom Tab Bar | Bottom Navigation Bar or Navigation Drawer |
| Back navigation | Swipe-from-left + back button top-left | System back gesture / Predictive Back |
| Primary CTA | Top-right nav bar or large pill button | FAB (Floating Action Button) |
| Contextual actions | Action Sheet from bottom | Bottom Sheet or overflow menu |
| Destructive confirm | Action Sheet with red option | Dialog |
| Modals | Card sheet (pageSheet) from bottom | Bottom Sheet or full-screen dialog |

---

### §8. Edge Cases & Error States (HIGH)

Every screen has at least 4 states beyond the happy path. Design all of them.

- `empty-state-4-types` — First-time empty (onboarding), user-cleared (recovery), search empty (guidance), error empty (retry)
- `empty-state-anatomy` — Good empty state = illustration/icon + active headline + body explaining context + CTA action
- `no-blank-screen` — A blank screen is never acceptable; always provide a message, illustration, and action
- `error-retry-path` — Every error state has a retry button or recovery action visible
- `network-error-offline` — Design explicit offline / no-connection state with graceful degradation message
- `partial-failure-shown` — When some data loads and some fails, show what succeeded + inline error for what failed
- `boundary-min` — Design for 0 items, $0 value, 0 characters — not just the typical non-zero case
- `boundary-max` — Design for character limit reached, max file size exceeded, max list length — truncation or pagination
- `long-content-wraps` — Test with long names, long text, multi-line labels — never assume single line
- `permission-denied-explained` — 403 / permission denied shows why the user can't access this and what they can do
- `loading-placeholder` — Loading state shows skeleton matching the shape of the content to load; never a blank area
- `forgiveness-undo` — Every delete action offers undo (toast with "Undo" within 5–10 seconds)
- `soft-delete` — Permanent deletions should move to trash first; hard delete requires explicit "Empty trash"
- `autosave` — Long editing sessions autosave every 30–60 seconds; show last saved timestamp
- `resumable-flows` — Multi-step flows that users abandon must be resumable: "Continue where you left off"

**Empty state template:**
```
[Illustration or icon — humanizes the void]
[Headline — active verb: "No transactions yet"]
[Body — context + next step: "Your history will appear after your first trade."]
[CTA — action that fills the state: "Connect an exchange"]
```

**Error state template:**
```
[Error icon — not just color]
[Headline — what happened: "Couldn't load your portfolio"]
[Body — cause + what to do: "Check your connection and try again."]
[Primary action: "Retry"]
[Secondary action (optional): "Go back"]
```

---

## Do/Don't — Most Common UX Mistakes

| Category | Don't | Do |
|----------|-------|----|
| **Flows** | Design only the happy path | Map all entry points, error paths, and empty states |
| **Navigation** | Hide back button on sub-screens | Always provide a predictable way back |
| **States** | Ship a button with no loading state | Design all 8 states before considering a component done |
| **Feedback** | Show "Something went wrong" | Show exactly what went wrong and how to fix it |
| **Forms** | Use placeholder as the only label | Use visible labels; placeholders are supplementary |
| **Forms** | Validate on every keystroke | Validate on blur; real-time only for character count |
| **Accessibility** | Remove focus ring for "aesthetics" | Design a branded 2px focus ring in the accent color |
| **Mobile** | Make icon buttons their visual size | Extend hit area to 44pt minimum with padding |
| **Cognitive load** | Show everything at once | Progressive disclosure: level 0 only, reveal on demand |
| **Empty states** | Show a blank screen | Show illustration + headline + CTA |
| **Microcopy** | Write "Cancel" / "OK" buttons | Write "Delete project" / "Keep project" |
| **Error tone** | "You entered an invalid email" | "That email address isn't registered. Try signing up." |

---

## Pre-Delivery UX Checklist

Run this before shipping any screen or feature.

### Flows & Navigation
- [ ] Every screen has a path forward or an explicit exit
- [ ] Back navigation takes users to the correct previous screen
- [ ] All key screens reachable via deep link
- [ ] Empty states designed for all data-dependent screens
- [ ] Error states designed with retry / recovery actions

### Interaction & States
- [ ] All 8 states designed for every interactive component
- [ ] Visual feedback starts within 100ms of any tap/click
- [ ] Loading states disable the trigger to prevent duplicate submissions
- [ ] Success states auto-dismiss in 3–5 seconds
- [ ] Disabled states explain why via tooltip or adjacent text

### Forms & Inputs
- [ ] Every input has a visible label (not placeholder-only)
- [ ] Validation fires on blur, not on keystroke
- [ ] Error messages appear directly below the offending field
- [ ] Error messages name the problem and how to fix it
- [ ] Destructive actions use semantic danger styling and confirmation dialogs

### Accessibility
- [ ] All text meets 4.5:1 contrast ratio (normal text) or 3:1 (large text)
- [ ] Custom focus rings designed (2px minimum, 3:1 contrast)
- [ ] All interactive elements reachable by keyboard (Tab, Enter, Escape)
- [ ] Icon-only buttons have `aria-label`
- [ ] Color is not the only indicator of any state (error, required, success)
- [ ] All touch targets ≥44×44pt (iOS) / 48×48dp (Android)
- [ ] `prefers-reduced-motion` supported — animations suppressible

### Mobile & Touch
- [ ] Safe areas respected on all screens
- [ ] Content clears floating tab bar (paddingBottom includes tab bar height)
- [ ] System gestures (back swipe, predictive back) not blocked
- [ ] Swipe-discoverable actions have visual affordance
- [ ] Keyboard avoidance implemented for all forms

### Cognitive Load
- [ ] Each screen has one clear primary action
- [ ] Secondary content progressively disclosed
- [ ] Smart defaults applied where possible
- [ ] Multi-step flows show progress and allow back navigation

---

## Common UX Problems → Solutions

| Problem | Likely cause | Fix |
|---------|-------------|-----|
| Users don't know what to do on a screen | No clear primary CTA or visual hierarchy | Apply `one-primary-action` + strengthen CTA visibility |
| Users abandon multi-step forms | Too much asked upfront / no progress indication | Apply `progressive-commitment` + add step counter |
| Error feels confusing or frustrating | Vague message or no recovery path | Apply `error-specific` + `error-has-recovery` |
| Users don't notice they need to scroll | Content above fold doesn't indicate more below | Show partial content at fold + scroll indicator |
| Taps on wrong element | Touch targets too small or too close | Apply `touch-44-minimum` + `target-spacing-8` |
| Users feel anxious about destructive actions | No confirmation or undo | Apply `confirm-before-destructive` + `forgiveness-undo` |
| UI feels overwhelming | Too much visible at once | Apply `progressive-disclosure` + `chunking` |
| Users with keyboards can't use the product | Missing keyboard navigation | Audit with Tab key; fix tab order; add `aria-label` to all controls |
| App feels unfamiliar on platform | Using web patterns on iOS/Android | Follow platform conventions from §7 table |
| Content hides behind tab bar | Missing bottom padding | Add `paddingBottom: insets.bottom + tabBarHeight` |
| Form re-entry loses all user input | No autosave or state persistence | Apply `autosave-long-forms` + confirm before dismiss |

---

## Method Selection Guide

| Question | Method | Reference |
|----------|--------|-----------|
| How does a user move through the product? | User Flow Creation | `interaction-design.md §1` |
| How does a user complete a specific task? | Task Flow Design | `interaction-design.md §2` |
| What does every state of this element look like? | State Design | `interaction-design.md §3` |
| What happens when things go wrong or are empty? | Edge Case Handling | `interaction-design.md §4` |
| How do we avoid overwhelming users with complexity? | Progressive Disclosure | `interaction-design.md §5` |
| How do users know this is clickable/tappable? | Affordance Design | `interaction-design.md §6` |
| How does the system communicate what just happened? | Feedback Design | `interaction-design.md §7` |
| What does the UI text say? | Microcopy | `interaction-design.md §8` |
| How do we quickly explore layout options? | Low-Fidelity Wireframing | `wireframing-prototyping.md §1` |
| How do we document the final layout precisely? | High-Fidelity Wireframing | `wireframing-prototyping.md §2` |
| How do we test navigation and transitions? | Interactive Prototyping | `wireframing-prototyping.md §3` |
| How do we validate a concept in hours? | Rapid Prototyping | `wireframing-prototyping.md §4` |
| Does this meet accessibility standards? | WCAG Compliance | `usability-accessibility.md §1` |
| Can users navigate without a mouse? | Keyboard Navigation | `usability-accessibility.md §2` |
| Does this work with VoiceOver / TalkBack? | Screen Reader Optimization | `usability-accessibility.md §3` |
| Do colors pass contrast ratios? | Color Contrast | `usability-accessibility.md §4` |
| Is focus management logical and visible? | Focus Management | `usability-accessibility.md §5` |
| Does this work for diverse abilities and contexts? | Inclusive Design | `usability-accessibility.md §6` |
| Are we asking too much of users' mental bandwidth? | Cognitive Load Management | `usability-accessibility.md §7` |
| Does the design prevent mistakes? | Error Prevention | `usability-accessibility.md §8` |
| Can users easily recover from errors? | Forgiveness Design | `usability-accessibility.md §9` |
| Does this work on the smallest screen first? | Mobile-First Design | `responsive-adaptive.md §1` |
| How does layout adapt across screen sizes? | Breakpoint Strategy | `responsive-adaptive.md §2` |
| Are touch targets large enough to tap accurately? | Touch Target Sizing | `responsive-adaptive.md §3` |
| How do grids and images adapt fluidly? | Responsive Layout Patterns | `responsive-adaptive.md §4` |
| Are we following iOS / Android / Web conventions? | Platform-Specific Patterns | `responsive-adaptive.md §5` |
| Does experience feel continuous across devices? | Cross-Device Continuity | `responsive-adaptive.md §6` |

---

## Domain Sequencing

```
Interaction Design (define the experience logic)
  └── User Flow → Task Flow → State Design → Edge Cases
      → Progressive Disclosure → Affordance → Feedback → Microcopy

Wireframing & Prototyping (make it tangible)
  └── Low-Fi Wireframes → High-Fi Wireframes
      → Interactive Prototype → Rapid / Paper / Code Prototype

Usability & Accessibility (make it inclusive)
  └── WCAG → Color Contrast → Keyboard Nav → Screen Reader
      → Focus Management → Inclusive Design
      → Cognitive Load → Error Prevention → Forgiveness

Responsive & Adaptive (make it universal)
  └── Mobile-First → Breakpoint Strategy → Touch Targets
      → Responsive Patterns → Platform Conventions → Cross-Device
```

---

## Reference Files (Deep Dives)

- **Interaction design** — Read `.claude/skills/ux-design/interaction-design.md` for: user flows, task flows, state design, edge cases, progressive disclosure, affordance design, feedback design, microcopy — includes templates, notation, and output specs
- **Wireframing & prototyping** — Read `.claude/skills/ux-design/wireframing-prototyping.md` for: low-fi wireframing, high-fi wireframing, interactive prototyping, rapid prototyping, paper prototyping, code-based prototyping
- **Usability & accessibility** — Read `.claude/skills/ux-design/usability-accessibility.md` for: WCAG compliance, keyboard navigation, screen reader optimization, color contrast, focus management, inclusive design, cognitive load, error prevention, forgiveness design — includes code patterns
- **Responsive & adaptive design** — Read `.claude/skills/ux-design/responsive-adaptive.md` for: mobile-first design, breakpoint strategy, touch target sizing, responsive layout patterns, platform-specific patterns (iOS/Android/Web), cross-device continuity
