# Animation Performance & Accessibility

## Table of Contents
1. [Animation Performance](#1-animation-performance)
2. [Reduced Motion](#2-reduced-motion)
3. [Progressive Enhancement](#3-progressive-enhancement)

---

## 1. Animation Performance

**Purpose:** Ensure animations run at 60fps (or 120fps on ProMotion) without jank, dropped frames, or layout thrashing — so motion enhances rather than degrades the experience.

**When to use:** Before shipping any animated UI element; as an audit checklist; when investigating animation jank reports.

### The Browser Rendering Pipeline

Understanding which CSS properties trigger which pipeline stages:

```
Layout → Paint → Composite

Layout (expensive): Changing width, height, top, left, margin, padding, font-size
  → Forces full recalculation of element positions

Paint (moderate): Changing background-color, color, border-color, box-shadow
  → Repaint affected pixels

Composite (cheap, GPU-accelerated): transform, opacity
  → Element already on its own layer; GPU handles it

Rule: Only animate transform and opacity for 60fps animation.
      Animating width, height, or position = layout thrash = jank.
```

### The Two-Property Rule

```
Safe to animate at 60fps:
  transform: translate(), rotate(), scale()  ← positions, rotation, size
  opacity                                    ← visibility

Everything else causes layout or paint — use with extreme caution:
  width, height          → Layout
  top, left, right, bottom → Layout
  margin, padding        → Layout
  background-color       → Paint
  box-shadow             → Paint
  border-radius          → Paint (sometimes, depending on browser)
  filter                 → Paint (expensive)
  color                  → Paint

Example:
  ❌ Bad:  transition: width 300ms ease-out;     // layout — will jank
  ✅ Good: transition: transform 300ms ease-out; // composite — 60fps

  To "grow" a button: use transform: scaleX() instead of width change.
```

### will-change

```
Promote an element to its own compositor layer before animation starts:

CSS:
  .animated-element {
    will-change: transform, opacity;
  }

This tells the browser to prepare a separate GPU layer for this element.

Rules:
  Add will-change to elements that are about to animate (before animation starts)
  Remove will-change after animation completes (don't leave it on permanently)
  Don't overuse — every layer costs GPU memory
  Use sparingly: 3–5 elements max; don't add to entire lists

React Native:
  useNativeDriver: true handles GPU promotion automatically.
  All Animated values with useNativeDriver: true run on the UI thread / GPU.
```

### React Native Performance Rules

```
useNativeDriver: true
  ALL transform and opacity animations must use useNativeDriver: true.
  Runs on the native UI thread — JS thread is not involved.
  Survives JS thread slowdowns without dropping frames.

useNativeDriver: false (required for):
  backgroundColor, width, height — layout/color properties
  These run on JS thread and CAN drop frames.
  Minimize and test on low-end devices.

Reanimated vs. Animated:
  Reanimated 2/3: All worklets run on UI thread by default.
  Much more powerful and performant for gesture-driven animations.
  Use for: Gesture-driven animations, complex sequences, shared values.
  Use Animated for: Simple, non-gesture animations in legacy components.

InteractionManager:
  Defer non-critical work until after animations complete:
    InteractionManager.runAfterInteractions(() => {
      // expensive operation — runs after current animation finishes
    });
```

### Measuring Performance

**Web — Chrome DevTools:**
```
1. Open DevTools → Performance tab
2. Record animation
3. Look for:
   - Green bar: frames rendering at 60fps
   - Red/orange: dropped frames, long tasks
   - Purple (Layout/Recalculate Style): layout thrash
   - Green (Composite): good, GPU-accelerated

Aim: No red frames; purple sections should be rare and short.
```

**React Native — Flipper:**
```
Install Flipper + React Native Performance plugin.
Monitor:
  JS FPS: should stay near 60fps
  UI FPS: should stay at 60fps (or 120fps on ProMotion devices)
  If UI FPS drops while JS FPS stays at 60: animation is off the native thread
  → Add useNativeDriver: true or move to Reanimated

React Native DevTools:
  Enable "Perf Monitor" in developer menu
  Watch JS Thread and UI Thread FPS during animations
```

### Performance Anti-patterns

```
❌ Animating layout properties (width/height/margin/padding) in a loop
❌ Forgetting useNativeDriver: true on React Native opacity/transform animations
❌ will-change on every element ("just in case")
❌ Running heavy JS computation on the JS thread during animations
❌ Animating elements inside a large FlatList (use React.memo + stable keys)
❌ Creating new Animated.Value on every render (should be in useRef or useMemo)
❌ Calling setValue directly during animation (breaks native animations)
```

### FlatList / Virtualized List Animations

```
Entering animations on FlatList items:
  Each item renders as it scrolls into view.
  Use entering={FadeInDown} (Reanimated) on each item's Animated.View.
  Keep animations short (200ms) — longer animations overlap and look messy.

Don't:
  Stagger 50 list items — the stagger will be wrong for virtualized rendering
  Use complex animations that block the scroll gesture
  Animate items that are mid-scroll

Do:
  Simple fade-in on first render (not on scroll)
  Use React.memo on list items to prevent unnecessary re-renders
  Keep item components lean — fewer views = faster render = better scroll performance
```

### Outputs
- Performance audit checklist (transform/opacity audit, will-change audit)
- useNativeDriver migration guide (find all Animated values missing it)
- FPS baseline measurements before/after optimization

---

## 2. Reduced Motion

**Purpose:** Respect the user's operating system preference for reduced motion — providing a safe, accessible experience for users with vestibular disorders, motion sensitivity, or epilepsy risk.

**When to use:** On every animation in every product. This is not optional.

### Why Reduced Motion Matters

```
Users who need reduced motion:
  - Vestibular disorder (vertigo, nausea triggered by screen motion)
  - Migraine sensitivity (parallax, fast motion can trigger migraines)
  - Epilepsy risk (flashing > 3Hz can trigger seizures)
  - Cognitive or attention disabilities (motion is distracting)
  - Personal preference (they just don't like bouncy UIs)

Platform setting:
  macOS/iOS: Settings → Accessibility → Motion → Reduce Motion
  Android: Settings → Accessibility → Remove animations
  Windows: Settings → Ease of Access → Show animations in Windows (toggle)

Prevalence: ~35% of users have the setting enabled (Apple internal data estimate).
```

### Web Implementation

```css
/* Option 1: Disable all animations globally */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Option 2: Targeted (preferred — more control) */
@media (prefers-reduced-motion: no-preference) {
  .animated-enter {
    animation: slide-in 300ms ease-out;
  }
}

/* Inside the no-preference block = only runs when user has NOT requested reduction */
```

```javascript
// JavaScript: check the preference
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

if (!prefersReducedMotion) {
  // run animation
}

// React hook
function usePrefersReducedMotion() {
  const [prefersReduced, setPrefersReduced] = useState(
    window.matchMedia('(prefers-reduced-motion: reduce)').matches
  );
  useEffect(() => {
    const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    const handler = (e) => setPrefersReduced(e.matches);
    mediaQuery.addEventListener('change', handler);
    return () => mediaQuery.removeEventListener('change', handler);
  }, []);
  return prefersReduced;
}
```

### React Native Implementation

```javascript
import { AccessibilityInfo } from 'react-native';

// Check once
const isReduced = await AccessibilityInfo.isReduceMotionEnabled();

// Subscribe to changes
const subscription = AccessibilityInfo.addEventListener(
  'reduceMotionChanged',
  (isEnabled) => setReducedMotion(isEnabled)
);

// Hook
function useReducedMotion() {
  const [isReduced, setIsReduced] = useState(false);
  useEffect(() => {
    AccessibilityInfo.isReduceMotionEnabled().then(setIsReduced);
    const sub = AccessibilityInfo.addEventListener('reduceMotionChanged', setIsReduced);
    return () => sub.remove();
  }, []);
  return isReduced;
}
```

### What to Change Under Reduced Motion

```
Don't just disable animations. Replace them with instant or crossfade alternatives.

Animation type → Reduced motion alternative:

Slide/translate   → Instant (no transition) or crossfade
Scale             → Instant or crossfade
Bounce/spring     → Instant or short linear fade (100ms)
Parallax          → Disable entirely (position: static)
Continuous pulse  → Static indicator (just the color, no animation)
Loading shimmer   → Static skeleton (gray shapes, no movement)
Stagger entry     → All items visible immediately (no stagger)
Page transition   → Crossfade 150ms (minimal motion)
Scroll animation  → Visible from load (no trigger animation)

The goal: the UI still communicates state changes, just without motion.
```

### The WCAG Standard

```
WCAG 2.1 — Success Criterion 2.3.3 (AAA):
  "A mechanism is available to suppress motion animation triggered by interaction."

WCAG 2.1 — Success Criterion 2.3.1 (A, required):
  "Web pages do not contain anything that flashes more than three times per second"

What this means:
  - Never flash more than 3 times/second (no exception)
  - Respect prefers-reduced-motion at AA level (not strictly required at AA,
    but widely considered best practice and de facto requirement)
```

### Photosensitivity (Flashing)

```
Strictly prohibited:
  Anything flashing faster than 3Hz (3 times/second = 333ms on/off cycle)
  High-contrast flashes (especially red)

Examples to never do:
  Rapid notification flash (strobing)
  High-energy confetti flashing on/off
  Error indicator flashing at high frequency

Safe alternatives:
  Slow fade in/out (once, not repeating)
  A single static color change
  A border or icon that appears (doesn't flash)
```

### Outputs
- `useReducedMotion` hook for target platform
- Global reduced motion CSS reset (for web)
- Animation component with built-in reduced motion handling

---

## 3. Progressive Enhancement

**Purpose:** Treat animation as an enhancement layered on top of a fully functional base experience — so the UI works perfectly without animation, and motion only improves it.

**When to use:** Always. Animation must never be the only way to communicate information or state.

### The Core Principle

```
Layer 1: Functional (no animation)
  The UI works. State changes happen. Navigation works.
  Content is accessible. Information is clear.

Layer 2: Enhanced (with animation)
  Transitions communicate navigation direction.
  Loading states have skeletons.
  Interactions have tactile feedback.

Any user who can't see Layer 2 (reduced motion, animation off, old browser)
must still be able to use the product fully at Layer 1.

Test this: turn off all animations. Can you still use the app?
If the answer is "no" for any interaction, the animation is doing structural work
that belongs in Layer 1.
```

### Animation as Communication, Not Structure

```
BAD: A button only shows its disabled state through a fade animation.
  If animation is disabled, the button looks enabled but doesn't work.

GOOD: Disabled button has disabled visual styling AND no animation.
  Reduced motion users see the styling; animation users see both.

BAD: The only indication a form was submitted is a success animation.
  No animation = user doesn't know if it worked.

GOOD: Success state is a visual state (green, checkmark icon, success message).
  Animation ADDS the motion to the already-working visual state.

Rule: Every state change must be communicated through at least one static visual
      change (color, icon, text). Animation can reinforce it but never replace it.
```

### Feature Detection

```javascript
// Web: Detect animation support
const animationsSupported = CSS.supports('animation-name', 'none');

// Web: Check if user prefers reduced motion
const reducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

// Progressive enhancement pattern:
function animateIfSafe(animateFn, fallbackFn) {
  if (!reducedMotion && animationsSupported) {
    animateFn();
  } else {
    fallbackFn(); // or do nothing if fallback is the normal state
  }
}
```

### Animation Failure Modes and Fallbacks

| Scenario | Behavior |
|----------|----------|
| prefers-reduced-motion: reduce | Replace motion with instant/crossfade |
| JavaScript disabled | CSS fallbacks active; layout is visible without animation |
| Animation API unsupported | Static state visible; no broken UI |
| Lottie fails to load | Show static icon or image in its place |
| Framer Motion not loaded | Components render without motion (structure intact) |
| Low-end device (dropped frames) | Reduce complexity; test on real device |

### React Native Graceful Degradation

```javascript
// Always provide a non-animated base state
// so if animation is skipped, the final state is correct

const opacity = useRef(new Animated.Value(0)).current;  // Start hidden

// Animate to visible
Animated.timing(opacity, { toValue: 1, duration: 300, useNativeDriver: true }).start();

// If animation is disabled or very slow, the element is still visible after:
// - useNativeDriver crashes (falls back to JS)
// - Animation API unavailable
// Because we call setValue(1) as fallback in .start() callback if needed

// Safety pattern:
Animated.timing(opacity, config).start(({ finished }) => {
  if (!finished) {
    opacity.setValue(1); // force final state if animation didn't complete
  }
});
```

### Pre-flight Checklist (Before Shipping Animations)

```
Functionality (no animation required):
  ✅ Every state change has a visible non-animated indicator
  ✅ Navigation works without transition animations
  ✅ Loading states have static fallbacks (visible content / skeleton shapes)
  ✅ Error states are visually clear without the shake animation
  ✅ Interactive elements have hover/focus styles that don't depend on animation

Accessibility:
  ✅ prefers-reduced-motion handled (web or React Native)
  ✅ No flashing content > 3Hz
  ✅ Animated content doesn't trap keyboard focus
  ✅ Screen readers: animation doesn't interfere with announcements
  ✅ Animated information is also conveyed statically (not animation-only)

Performance:
  ✅ Only transform and opacity animated at 60fps critical paths
  ✅ useNativeDriver: true on all applicable React Native animations
  ✅ will-change used sparingly, removed after animation
  ✅ Tested on target low-end device (not just simulator)
  ✅ FPS maintained during animation (60fps web, 60fps RN)

Polish:
  ✅ Enter animations use ease-out; exits use ease-in
  ✅ Exit duration is shorter than enter (80% rule)
  ✅ Spring animations are appropriately damped (no excess bounce on professional UI)
  ✅ Stagger delays don't exceed 100ms per item
  ✅ Loading states display for minimum 400ms (no flash)
```

### Outputs
- Pre-flight animation checklist
- `useReducedMotion` hook wired up globally
- Documentation of all Layer 1 static states (what's communicated without animation)
