# Motion Principles

## Table of Contents
1. [Timing & Easing](#1-timing--easing)
2. [Duration](#2-duration)
3. [Orchestration](#3-orchestration)
4. [Continuity](#4-continuity)
5. [State Transitions](#5-state-transitions)

---

## 1. Timing & Easing

**Purpose:** Define the rhythm and character of motion. Easing curves control how an element accelerates and decelerates — turning robotic, mechanical motion into natural, physical-feeling movement.

**When to use:** Every animation needs an easing decision. The choice communicates physicality and intent.

### The Core Easing Curves

```
Linear
  Constant speed from start to finish.
  Feels mechanical, unnatural.
  Use: Progress bars, loading indicators where constant rate is the point.
  Never use: For elements that enter or exit.

Ease-in (acceleration curve)
  Starts slow, ends fast.
  Feels like an object launching.
  Use: Elements leaving the screen (exiting). The object "launches" away.
  Never use: For elements entering — they'd slam in at full speed.

Ease-out (deceleration curve)
  Starts fast, ends slow.
  Feels like an object arriving and settling.
  Use: Elements entering the screen. Elements responding to a tap.
  This is the most natural-feeling curve for most UI motion.

Ease-in-out (symmetrical)
  Starts slow, accelerates through the middle, decelerates to end.
  Feels like a complete, self-contained motion.
  Use: Elements moving from one position to another on screen.
  Don't use for elements that enter/exit — use ease-out / ease-in instead.

Spring (physics-based)
  Overshoots the target slightly, then settles back.
  Feels alive, bouncy, physical.
  Use: Floating UI elements, modals, cards, anything that benefits from a tactile feel.
  Don't over-use: Every element bouncing = carnival, not product.
```

### Easing Curve Reference

```css
/* Standard curves */
ease-out:     cubic-bezier(0.0, 0.0, 0.2, 1.0)   /* enter */
ease-in:      cubic-bezier(0.4, 0.0, 1.0, 1.0)   /* exit */
ease-in-out:  cubic-bezier(0.4, 0.0, 0.2, 1.0)   /* move on screen */

/* Expressive curves */
--ease-spring:    cubic-bezier(0.34, 1.56, 0.64, 1.0)   /* slight overshoot */
--ease-snap:      cubic-bezier(0.2, 0.0, 0.0, 1.0)      /* fast then settle */
--ease-anticipate: cubic-bezier(0.36, -0.4, 0.64, 1.4)  /* pull back then launch */

/* React Native (Animated API) */
Easing.out(Easing.cubic)     // ease-out
Easing.in(Easing.cubic)      // ease-in
Easing.inOut(Easing.cubic)   // ease-in-out
Easing.spring()              // physics spring (use withSpring() in Reanimated)
```

### Easing Selection Guide

| Motion type | Easing | Why |
|-------------|--------|-----|
| Element entering | ease-out | Arrives fast, settles gently |
| Element exiting | ease-in | Starts slow, accelerates away |
| Element moving on screen | ease-in-out | Full arc of motion |
| Response to tap/click | ease-out | Immediate, snappy response |
| Spring/modal/sheet | spring | Physical, alive feeling |
| Progress bar fill | linear | Constant rate is the point |
| Attention pulse | ease-in-out | Smooth pulse feels organic |

### Custom Curves for Personality

```
Conservative / professional (fintech, medical):
  Stick to standard ease-out/ease-in. Avoid spring.
  Message: Stable, predictable, trustworthy.

Playful / consumer:
  Use spring liberally. Add anticipation curves.
  Message: Energetic, fun, delightful.

Premium / luxury:
  Slow, deliberate ease-in-out. Long durations. No bouncing.
  Message: Unhurried, considered, expensive.

Technical / productivity:
  Fast ease-out. Near-instant. No decorative motion.
  Message: Efficient, out of the way.
```

### Outputs
- Easing token system (CSS custom properties or JS constants)
- Curve selection rationale per context
- Brand motion vocabulary (which curves represent the brand)

---

## 2. Duration

**Purpose:** Match animation length to the size, distance, and importance of the motion — so animations feel instant when they should, and deliberate when they should.

**When to use:** Every animation decision includes a duration. Wrong duration kills an otherwise correct easing.

### Duration Scale

```
Instant:   0ms       No animation — state switches immediately (theme toggle internals)
Micro:     50–100ms  Near-instant feedback (button state change, checkbox tick)
Fast:      100–150ms Hover transitions, tooltip appear, quick reveals
Standard:  200–300ms Most UI transitions — modal open, dropdown appear, card expand
Deliberate: 300–500ms Page transitions, sheet slide-up, significant layout changes
Slow:      500–800ms Intentional pauses — onboarding reveals, hero animations
Very slow: 800ms+    Marketing only — never in a product UI for functional interactions
```

### Rules for Choosing Duration

**Rule 1: Distance ∝ Duration**
An element moving 400px should take longer than one moving 40px. Constant speed feels wrong.

```
Small movement (< 50px):   100–150ms
Medium movement (50–200px): 200–250ms
Large movement (> 200px):   300–400ms
Full screen:                350–450ms
```

**Rule 2: Size ∝ Duration**
A large modal takes slightly longer than a small tooltip. Larger surfaces have more visual mass.

**Rule 3: Enter < Exit**
Exits should be slightly faster than entrances.

```
Enter: 250ms ease-out
Exit:  180ms ease-in

Why: Users triggered the exit — they're ready to move on. Don't make them wait.
```

**Rule 4: Hierarchy ∝ Duration**
Important transitions (navigating between pages) can be slower. Micro-interactions must be faster.

**Rule 5: Faster is almost always better**
When in doubt, cut 20% of the duration. Most UI animations are too slow, not too fast.

### Platform Duration Baselines

| Platform | Fast | Standard | Slow |
|----------|------|----------|------|
| Web (browser) | 150ms | 250ms | 400ms |
| iOS (UIKit) | 250ms | 350ms | 500ms |
| Android (Material) | 200ms | 300ms | 400ms |
| React Native | 200ms | 300ms | 400ms |

### Duration Anti-patterns

```
❌ All animations the same duration — feels uniform and robotic
❌ Durations over 400ms for functional UI — feels sluggish
❌ Exit duration longer than enter — feels like UI is fighting the user
❌ Long duration + linear easing — the worst combination: slow and mechanical
❌ Duration too short + spring — looks glitchy (spring needs time to settle)
```

### Outputs
- Duration token system: `--duration-micro`, `--duration-fast`, `--duration-standard`, `--duration-deliberate`
- Per-component duration guidelines
- Enter/exit duration pairing rules

---

## 3. Orchestration

**Purpose:** Coordinate multiple animations that happen together — deciding what plays first, what's staggered, and what happens simultaneously — to create rhythm, hierarchy, and clarity rather than chaos.

**When to use:** Any time more than one element animates. A list of 8 items all animating simultaneously looks broken; staggered, it looks designed.

### Orchestration Patterns

**1. Simultaneous**
All elements animate at the same time.

```
Use when: Elements are a single unit (card with icon + text — they enter together)
Use when: Speed matters more than hierarchy
Avoid when: There are more than 2–3 independent elements
```

**2. Stagger**
Elements animate in sequence with a fixed delay between each.

```
Use when: List items, grid cards, series of related elements
Stagger delay: 30–80ms between items (never more than 100ms — feels too slow)
Direction: Top-to-bottom is most natural (matches reading direction)

Code (CSS):
  .item:nth-child(1) { animation-delay: 0ms; }
  .item:nth-child(2) { animation-delay: 50ms; }
  .item:nth-child(3) { animation-delay: 100ms; }

Code (React Native Animated):
  Animated.stagger(50, items.map(anim => Animated.timing(anim, config)));

Code (Reanimated / entering animations):
  entering={FadeInDown.delay(index * 50)}
```

**3. Sequence**
One animation must complete before the next begins.

```
Use when: Animations have a causal relationship
  Example: Button press → success checkmark → text changes
  Example: Form submit → loading state → success message

Avoid: Chaining more than 3 animations — users can't track it
```

**4. Spring train**
A value change propagates through connected elements with decreasing amplitude.

```
Use for: Drag-and-drop reordering, list item deletion (other items close the gap)
Character: Feels physical, like knocking dominoes
```

### Stagger Guidelines

```
List items (enter on mount):
  Delay between items: 40–60ms
  Max staggered items: 6–8 (beyond that, truncate remaining at zero delay)
  Base delay (first item): 0ms (don't add a global delay — start immediately)

Grid cards (enter on mount):
  Stagger by row (not individual card): 60–80ms per row
  Cards in same row: animate simultaneously

Insight cards / sections:
  Stagger by section: 80–100ms between major sections
  Elements within a section: simultaneous
```

### Choreography — Entrance vs. Exit

```
List entrance:
  Items enter top-to-bottom with stagger (matches reading direction)

List exit (e.g., deleting all items):
  Items exit bottom-to-top or all at once (reverse read order for exit)

Modal entrance:
  1. Backdrop fades in (0ms, 200ms ease-out)
  2. Modal scales + fades in (50ms delay, 250ms spring)

Modal exit:
  1. Modal fades + scales out (0ms, 180ms ease-in)
  2. Backdrop fades out (0ms, 200ms ease-out)
  Both play simultaneously — no delay between them
```

### Outputs
- Stagger timing system (token: `--stagger-list: 50ms`, `--stagger-section: 80ms`)
- Choreography guide per key interaction
- Code snippets for stagger in target framework

---

## 4. Continuity

**Purpose:** Maintain spatial and visual relationships during transitions so users never lose their mental model of where things are — reducing cognitive load and making navigation feel natural.

**When to use:** Any navigation between two screens; any element that moves between two states; any interaction where an element changes role or position.

### Continuity Patterns

**1. Shared element transition (hero animation)**
An element from screen A becomes an element on screen B — traveling between its positions.

```
Classic example: Tapping a thumbnail → thumbnail expands to full-screen image
Product example: Tapping a card → card expands to detail screen

Rules:
  - Element must be visually identical in both states (or interpolate smoothly)
  - Transition makes the relationship explicit (this detail IS that card)
  - Duration: 300–400ms spring
  - Other elements: fade out during the transition, fade in on arrival

React Native (Reanimated shared elements):
  <Animated.View sharedTransitionTag="card-{item.id}" />
```

**2. Crossfade**
Old screen fades out as new screen fades in.

```
Use for: Screens with no shared elements; tab navigation; settings navigation
Duration: 200ms each, with slight overlap (start fade-in at 50ms)
Avoid: Pure crossfade for parent → child navigation (use slide instead)
```

**3. Slide**
Screens slide in from a direction matching the navigation direction.

```
Forward navigation:  new screen slides in from right, old from left
Back navigation:     new screen slides in from left, old to right
Bottom sheet:        slides up from bottom
Modal:               slides up + fades in

Direction consistency is critical — breaking it confuses users about
their position in the navigation hierarchy.
```

**4. Container transform**
An element expands into a full surface (not just scale — it morphs shape).

```
Example: A card corner radius animates from 16px to 0px as it expands to fill the screen
Example: A FAB morphs into a dialog

Character: Smooth, physically continuous, no jarring jump
Duration: 350ms spring
```

### Spatial Consistency Rules

```
Navigation hierarchy → slide direction:
  Deeper level:   slide from right (going deeper into hierarchy)
  Parent level:   slide from left (going back up)
  Sibling level:  crossfade or horizontal slide based on position

Maintain viewport position:
  If user has scrolled 300px down a list, and taps an item and returns,
  the list should return to the same scroll position — not jump to top.

Keep focus context:
  After a modal closes, focus returns to the element that triggered it.
  After a toast appears and disappears, focus stays where it was.
```

### Outputs
- Shared element transition specifications
- Navigation transition map (which direction for each navigation type)
- Continuity checklist per screen pair

---

## 5. State Transitions

**Purpose:** Communicate state changes clearly through motion — making it obvious that something changed, what changed, and what the new state means.

**When to use:** Every interactive element has multiple states. The transition between them is an opportunity to confirm action and reduce uncertainty.

### The 8 UI States

Every interactive element should have defined transitions for all relevant states:

| State | Description | Motion character |
|-------|-------------|-----------------|
| Default | Resting state | None |
| Hover | Mouse/cursor over | Fast, subtle (150ms) |
| Focus | Keyboard focus | Immediate, high contrast ring |
| Active/Pressed | Currently being pressed | Instant scale/color (50ms) |
| Loading | Awaiting result | Continuous, looping |
| Success | Action completed | Brief confirmation (200ms) |
| Error | Action failed | Shake/highlight (200ms) |
| Disabled | Not interactable | Fade to 40% opacity |

### State Transition Rules

**Default → Hover:**
```
Fast (100–150ms), ease-out.
Subtle — background tint, shadow lift, or slight scale (1.02 max).
The hover state should never surprise — it confirms interactivity.

CSS:
  transition: background-color 150ms ease-out, transform 150ms ease-out;
  &:hover { background-color: var(--hover); transform: scale(1.02); }
```

**Default → Pressed/Active:**
```
Near-instant (50–80ms), ease-out.
Slight scale down (0.97) + brightness shift — feels like physical press.
Release: spring back to default (100ms spring).

React Native:
  Pressable with:
    onPressIn:  Animated.spring(scale, { toValue: 0.97, ... })
    onPressOut: Animated.spring(scale, { toValue: 1.0, ... })
```

**Loading state:**
```
Two approaches:
  1. Spinner — circular rotation (for indeterminate, short waits)
  2. Skeleton — shimmer across content shape (for content loading)

Transition into loading: immediate (user just tapped — respond NOW)
Transition out of loading: ease-out 200ms (content arrives)

Minimum loading display time: 400ms
Why: If it resolves in < 400ms, skip the loading state entirely.
     Flickering loading states are worse than none.
```

**Success state:**
```
Sequence:
  1. Loading → checkmark (spring pop, 200ms)
  2. Checkmark holds for 600ms (let user see it)
  3. Returns to default (200ms ease-out)

Or for permanent success (form submitted):
  Entire component replaced by success message (crossfade 200ms)
```

**Error state:**
```
Visual: Red tint on the element + error message
Motion: Horizontal shake (3 rapid oscillations, 400ms total)

CSS shake keyframe:
  @keyframes shake {
    0%, 100% { transform: translateX(0); }
    20%       { transform: translateX(-4px); }
    40%       { transform: translateX(4px); }
    60%       { transform: translateX(-4px); }
    80%       { transform: translateX(4px); }
  }
  animation: shake 400ms ease-in-out;
```

**Disabled state:**
```
Transition: No animation into disabled — the state change is a result of logic,
            not user action. Instant is correct.
Visual: opacity: 0.4, cursor: not-allowed
Motion: None — disabled elements are inert.
```

### Continuous State Indicators

For states that persist (loading, syncing, recording):

```
Spinner: Continuous rotation, 600–800ms per revolution, linear easing
Pulse:   Scale 1.0 → 1.08 → 1.0, 1200ms ease-in-out, infinite
Shimmer: Left-to-right gradient sweep, 1500ms linear, infinite

Rules:
  - Keep it subtle — the motion should not compete with content
  - One motion indicator at a time per screen area
  - No infinite animations on content (only on loading/empty states)
```

### Outputs
- State transition map per component
- Animation specs for each state change (duration, easing, keyframes)
- Code snippets for common state transitions
