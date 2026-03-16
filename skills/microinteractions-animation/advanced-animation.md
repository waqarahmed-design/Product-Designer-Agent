# Advanced Animation

## Table of Contents
1. [Morphing](#1-morphing)
2. [Physics-Based Animation](#2-physics-based-animation)
3. [Lottie Animations](#3-lottie-animations)
4. [SVG Animation](#4-svg-animation)
5. [Loading Optimism](#5-loading-optimism)
6. [Attention Direction](#6-attention-direction)
7. [Personality Expression](#7-personality-expression)

---

## 1. Morphing

**Purpose:** Animate an element as it transforms from one shape, size, or role into another — maintaining visual continuity between two distinct states.

**When to use:** FAB → dialog; search bar expansion; icon state changes (play → pause, menu → close); card → detail view expansion.

### Shape Morphing

```
Elements that change shape (not just size):
  - Must share an anchor point — both shapes stay in the same visual region
  - The interpolation path should feel physically natural
  - Brief hold at each extreme: don't rush through the morphed state

Play ↔ Pause icon morph:
  Two vertical bars ↔ right-pointing triangle
  Method: Two paths with same number of points, interpolate between them
  Duration: 250ms ease-in-out

Menu (hamburger) ↔ Close (×) icon:
  Top bar → top arm of ×, bottom bar → bottom arm, middle bar fades out
  Duration: 300ms ease-in-out
  Add rotation for extra polish (15–20deg rotation of the outer two bars)
```

### Container Morphing

```
A card expands to become a detail screen.

Process:
  1. Capture the card's position (getBoundingClientRect)
  2. Render detail screen in a portal/overlay at card's exact position and size
  3. Animate: position → center, size → full screen, border-radius → 0
  4. Simultaneously: fade in detail content (staggered, not instant)
  5. Old card: opacity 0 (hide, don't remove — keeps layout stable)

Dismiss (reverse):
  1. Animate: full screen → card position, border-radius → card's radius
  2. Simultaneously: fade out detail content
  3. Card: opacity 1 (restore)
  Duration: 350ms spring
```

### Numeric Morphing (Number Counters)

```
When a number value changes (balance updates, price ticks):
  Method 1: Count-up/down animation (number ticks to new value)
    Duration: 400–600ms ease-out
    Good for: Large changes, onboarding reveals

  Method 2: Slide transition (old number slides up/out, new slides in from below)
    Duration: 200ms ease-out
    Good for: Real-time tickers, live price feeds
    Direction: Up if value increases, down if decreases

  Method 3: Crossfade (old fades, new fades in)
    Duration: 150ms
    Good for: Precise financial values where animation shouldn't imply trend

Rule: Never animate individual digits independently (odometer style) for financial data
— it implies false precision and can misread as errors.
```

### SVG Path Morphing

```
Requirements:
  - Both paths must have the same number of points
  - Points must be in the same order
  - Complex shapes may need to be normalized (same point count) before animating

Web:
  CSS: Only works if both paths have the same number of commands
  d: path('M...') → path('M...') with transition: d 300ms ease-in-out;

GSAP MorphSVG (recommended for complex shapes):
  gsap.to('#shape', { morphSVG: '#targetShape', duration: 0.3 });

React Native: react-native-svg + Animated.Value interpolation on path 'd' attribute
```

### Outputs
- Icon morph implementation (play/pause, menu/close)
- Container morph component
- Number counter component

---

## 2. Physics-Based Animation

**Purpose:** Use spring physics, momentum, and inertia to create motion that feels natural and alive — as if elements have physical mass.

**When to use:** Any interaction that benefits from tactile, physical feeling — gesture responses, modals, bouncing elements, drag and drop.

### Spring Physics Concepts

```
Spring parameters:
  Mass:      Higher = heavier, slower to start and stop
  Stiffness: Higher = snappier, less overshoot
  Damping:   Higher = less bouncing, settles faster

  Low damping + high stiffness = very bouncy (playful)
  High damping + high stiffness = snappy but no bounce (professional)
  Low damping + low stiffness = floppy, slow (avoid)
  High damping + low stiffness = slow settle (cinematic)

Common presets:
  Snappy:     stiffness: 300, damping: 30  — fast response, tiny overshoot
  Springy:    stiffness: 100, damping: 10  — notable bounce
  Wobbly:     stiffness: 50,  damping: 5   — very bouncy
  Gentle:     stiffness: 120, damping: 14  — soft settle
  Stiff:      stiffness: 500, damping: 40  — near-instant, no bounce
```

### React Native — `Animated` API Spring

```javascript
Animated.spring(value, {
  toValue: 1,
  tension: 52,      // maps to stiffness
  friction: 16,     // maps to damping
  useNativeDriver: true,
}).start();
```

### React Native — Reanimated `withSpring`

```javascript
import { withSpring } from 'react-native-reanimated';

// withSpring(toValue, config)
value.value = withSpring(1, {
  mass: 1,
  stiffness: 100,
  damping: 15,
  overshootClamping: false,  // true = no bounce past target
  restDisplacementThreshold: 0.01,
  restSpeedThreshold: 0.01,
});
```

### Web — Framer Motion Spring

```javascript
import { motion, useSpring } from 'framer-motion';

<motion.div
  animate={{ scale: 1 }}
  transition={{ type: 'spring', stiffness: 200, damping: 20 }}
/>
```

### Momentum and Decay

```
After a flick/swipe gesture, elements should decelerate naturally.
This is "momentum" or "inertia" — the element coasts to a stop.

React Native: ScrollView has this built in (scroll momentum).
For custom: use withDecay() in Reanimated.

withDecay(config):
  velocity: initialVelocity (from gesture handler)
  deceleration: 0.997 (1.0 = no deceleration, 0.99 = fast stop)
  clamp: [min, max] (optional bounds)

value.value = withDecay({
  velocity: gestureVelocity,
  deceleration: 0.998,
  clamp: [0, MAX_VALUE],
});
```

### Drag and Drop with Physics

```
During drag: element follows finger directly (useNativeDriver: true, no easing)
On drop to valid target: spring to snapped position (stiffness: 300, damping: 25)
On drop to invalid target: spring back to origin (same spring)
On release mid-air: decay toward nearest valid snap point

Key: The return spring should feel like the object "wants" to be in place.
```

### Outputs
- Spring preset library (snappy, springy, gentle, stiff)
- Gesture-driven spring implementation
- Decay/momentum implementation for fling gestures

---

## 3. Lottie Animations

**Purpose:** Use high-fidelity vector animations exported from After Effects — enabling complex, branded animations that would be impractical to implement in CSS or native animation APIs.

**When to use:** Onboarding illustrations, success/error states, empty states, loading animations, brand moments where motion is part of the visual identity.

### When to Use Lottie vs. Code Animation

| Use Lottie | Use Code Animation |
|-----------|-------------------|
| Complex illustrated animations | Simple UI transitions |
| Designer-owned assets | Engineering-controlled motion |
| Brand-critical moments | Interactive, gesture-driven |
| Particle effects, path tracing | State machine transitions |
| Non-interactive playback | Needs to respond to data |

### Lottie Integration

**React Native:**
```javascript
import LottieView from 'lottie-react-native';

// Simple autoplay
<LottieView
  source={require('./animations/success.json')}
  autoPlay
  loop={false}
  style={{ width: 120, height: 120 }}
  onAnimationFinish={() => handleComplete()}
/>

// Controlled playback
const animRef = useRef<LottieView>(null);
animRef.current?.play();
animRef.current?.pause();
animRef.current?.reset();
```

**Web (lottie-web or @lottiefiles/dotlottie-react):**
```javascript
import { DotLottieReact } from '@lottiefiles/dotlottie-react';

<DotLottieReact
  src="/animations/loading.lottie"
  loop
  autoplay
  style={{ width: 80, height: 80 }}
/>
```

### Controlling Lottie Programmatically

```
Segment playback (play only part of the animation):
  animRef.current?.play(startFrame, endFrame);

Useful for:
  State 1 → idle loop: play frames 0–60 on loop
  Trigger: play frames 61–90 (transition)
  State 2 → success: play frames 91–120 once

This avoids needing separate animation files for each state.
```

### Performance Rules

```
File size:
  Target: < 100KB per animation JSON
  > 200KB: too heavy for inline use; lazy load
  > 500KB: red flag — simplify the After Effects file

Color:
  Use color tokens in Lottie JSON where possible (find/replace hex values)
  Or: Use Lottie's "color filter" layer to remap at runtime

Preload:
  For animations triggered on user action, preload on idle:
    import(`./animations/${name}.json`).then(data => setAnim(data));

Avoid:
  Rasterized images inside Lottie — defeats the purpose of vector
  Nested compositions > 3 levels deep (complex, hard to color-correct)
  Continuous loops on background — drain battery, distract users
```

### Outputs
- Lottie integration with segment control
- File size and quality guidelines for designers
- Runtime color remapping pattern

---

## 4. SVG Animation

**Purpose:** Animate scalable vector graphics for icons, illustrations, charts, and decorative elements using CSS or JS — without rasterization or file overhead.

**When to use:** Animated icons (checkmarks, loading spinners, progress), drawn charts, illustrated empty states, decorative line work.

### CSS SVG Animation

**Path drawing (stroke-dashoffset):**
```css
/* The classic "draw on" effect */
.path {
  stroke-dasharray: 200;     /* total path length */
  stroke-dashoffset: 200;    /* fully hidden at start */
  transition: stroke-dashoffset 600ms ease-out;
}
.path.visible {
  stroke-dashoffset: 0;      /* fully drawn */
}

/* Get path length in JS: */
const len = document.querySelector('.path').getTotalLength();
```

**Checkmark animation:**
```css
@keyframes draw-check {
  from { stroke-dashoffset: 60; }
  to   { stroke-dashoffset: 0;  }
}
.checkmark {
  stroke-dasharray: 60;
  animation: draw-check 400ms ease-out forwards;
}
```

**Rotating elements:**
```css
@keyframes spin {
  to { transform: rotate(360deg); }
}
.spinner-arc {
  transform-origin: center;
  animation: spin 1000ms linear infinite;
}
```

### GSAP for Complex SVG Animation

```javascript
import gsap from 'gsap';
import { DrawSVGPlugin } from 'gsap/DrawSVGPlugin';
gsap.registerPlugin(DrawSVGPlugin);

// Animate drawing a path
gsap.fromTo('.path', { drawSVG: '0%' }, { drawSVG: '100%', duration: 1, ease: 'power2.out' });

// Morph between two SVG paths
import { MorphSVGPlugin } from 'gsap/MorphSVGPlugin';
gsap.to('#shape', { morphSVG: '#target', duration: 0.4 });

// Stagger animate multiple paths (charts, illustrations)
gsap.from('.bar', { scaleY: 0, stagger: 0.05, duration: 0.4, ease: 'back.out(1.7)' });
```

### Animated Icons (React Native + react-native-svg)

```javascript
import { Path, Svg } from 'react-native-svg';
import Animated, { useSharedValue, withTiming } from 'react-native-reanimated';

const AnimatedPath = Animated.createAnimatedComponent(Path);

// Controlled stroke-dashoffset (requires Reanimated)
const progress = useSharedValue(0);
const animatedProps = useAnimatedProps(() => ({
  strokeDashoffset: interpolate(progress.value, [0, 1], [pathLength, 0]),
}));

<AnimatedPath
  animatedProps={animatedProps}
  strokeDasharray={pathLength}
  ...
/>
```

### Chart Animation

```
Bar charts: bars grow from 0 height upward
  scale(1, 0) → scale(1, 1), transform-origin: bottom center
  Stagger: 40ms between bars

Line charts: path draws left to right using stroke-dashoffset
  Duration: proportional to number of data points

Pie/donut charts: slices sweep in using stroke-dashoffset on arc paths
  Stagger: each slice after the previous

Area charts: path draws + fill fades in (opacity 0 → 0.3)

All chart animations:
  Only play on first render (not on every data refresh)
  On refresh: transition to new values without re-animating from zero
```

### Outputs
- Draw-on animation utility (stroke-dashoffset with auto path-length detection)
- Animated chart bar/line/pie components
- Icon morph SVG implementation

---

## 5. Loading Optimism

**Purpose:** Make the product feel faster by using animation to fill the perceived waiting time — reducing frustration while real operations complete.

**When to use:** Any operation with latency: API calls, navigation, image loading, form submission.

### Optimistic UI

```
Pattern: Assume success. Update the UI immediately. Revert only on error.

Without optimistic UI:
  User taps "Like" → waits 300ms for server → UI updates → awkward pause

With optimistic UI:
  User taps "Like" → UI updates instantly → server call happens in background
  If server fails: revert with a gentle shake + error message

Rules:
  Use for: Low-stakes, high-frequency actions (likes, follows, toggles, reactions)
  Don't use for: Irreversible or high-stakes (payment, delete, security actions)
  Always handle failure: revert gracefully, never silently
```

### Skeleton-First Rendering

```
Pattern: Render the skeleton layout before data arrives.
         Content animates in when data is ready (not a sudden swap).

Without:  Blank → content (jarring)
With:     Skeleton → content with stagger fade (smooth)

Content arrival animation:
  Elements fade in + translateY(8px) → position, 200ms ease-out
  Stagger: 30ms between items
  Start immediately — don't wait for all items before starting stagger
```

### Predictive Pre-loading

```
Pre-load the next screen before the user navigates to it:
  On hover (web): start prefetching the next route
  On scroll near bottom: start loading next page of content
  On tap: navigation starts and content loads simultaneously

Visual pattern:
  If content arrives before the transition completes: show content on arrival
  If transition completes before content: show skeleton briefly, then fill
  Never show a flash of empty screen
```

### Perceived Performance Tricks

```
1. Start animation before work begins
   Show the loading state within 50ms of the user action.
   Even if the request fires at 60ms, the user felt the response at 50ms.

2. Show incremental progress
   Streaming responses, progressive image loading (blur-up technique),
   partial content updates — partial information reduces anxiety.

3. Use ease-out for arrivals
   Content that arrives with ease-out feels faster than linear arrival
   (even at the same actual duration).

4. Blur-up image loading
   Load a tiny (10px) blurred placeholder → full image fades in on load.
   CSS: filter: blur(20px) → blur(0px), transition: 300ms ease-out

5. The 100ms rule
   Anything under 100ms is perceived as instant.
   Anything 100–300ms is fast but noticeable.
   Anything 300–1000ms needs a visual indicator.
   Anything over 1000ms needs a progress indicator.
```

### Outputs
- Optimistic update implementation pattern
- Skeleton → content transition component
- Blur-up image loading component

---

## 6. Attention Direction

**Purpose:** Use motion to guide the user's eye to what matters — directing focus to changes, new content, errors, or calls to action.

**When to use:** When something important has changed that the user must notice; when pointing to a new feature; when highlighting an error or required action.

### Attention Techniques

**Pulse (for persistent indicators):**
```css
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50%       { opacity: 0.6; transform: scale(1.08); }
}
.notification-dot {
  animation: pulse 2000ms ease-in-out infinite;
}
```
Use for: Live indicators, unread badges, active status

**Bounce (call attention once):**
```css
@keyframes bounce-attention {
  0%, 100% { transform: translateY(0); }
  30%       { transform: translateY(-6px); }
  60%       { transform: translateY(-3px); }
}
.attention {
  animation: bounce-attention 600ms ease-in-out 1;
}
```
Use for: First-time feature discovery, important CTA after a delay

**Shake (error/invalid action):**
Already covered in State Transitions — use for error states on form fields.

**Flash highlight (content change):**
```css
@keyframes flash-highlight {
  0%, 100% { background-color: transparent; }
  20%      { background-color: rgba(200, 232, 71, 0.15); }  /* accent at 15% */
}
.updated {
  animation: flash-highlight 1200ms ease-in-out 1;
}
```
Use for: A value that just changed (price update, balance change, new message)

**Entrance animation (new item in list):**
New item enters with fade + slide from right:
```
opacity: 0 → 1, translateX(20px) → 0, 300ms ease-out
This distinguishes newly-added from pre-existing items.
```

### Rules for Attention Direction

```
1. One primary focus per moment
   Never have two elements competing for attention simultaneously.
   If multiple things change, stagger the attention animation.

2. Be proportionate
   Small change: subtle flash highlight (low energy)
   Important change: entrance animation (medium energy)
   Critical error: shake + color + haptic (high energy)

3. Don't cry wolf
   If everything pulses, nothing stands out.
   Reserve attention animations for genuinely important moments.

4. End the animation
   Attention animations should fire once and stop.
   Continuous animations (infinite pulse) only for persistent states (live, unread).

5. Respect reduced motion
   If animation is purely for attention, ensure the color change (not just the motion)
   also communicates the state change — don't rely on motion alone.
```

### New Feature Discovery

```
Spotlight: Dim the rest of the screen (backdrop), highlight the new element.
  Backdrop: 60% opacity overlay with a transparent cutout
  Element: No dimming, slight scale (1.03) to feel elevated
  Tooltip: points to the element, fades in 300ms after spotlight appears

Badge/dot: A small colored dot appears on a tab or button.
  Entrance: scale(0) → scale(1), 200ms spring
  No continuous animation — static dot is enough

Tooltip pulse: Element pulses gently once when user hasn't interacted.
  Single pulse, not infinite. Fires after 3-second delay on first visit.
```

### Outputs
- Attention animation component (type: 'pulse' | 'bounce' | 'flash' | 'shake')
- Spotlight / new feature overlay component
- Flash-on-update directive/hook for live data

---

## 7. Personality Expression

**Purpose:** Use motion to communicate brand character — making the product feel like it has a distinct, intentional personality rather than defaulting to generic UI behavior.

**When to use:** When motion can reinforce brand positioning; onboarding; success/delight moments; distinctive navigation between screens.

### Defining Motion Personality

Every brand can map to a motion personality:

| Brand positioning | Motion character | Spring | Duration | Easing |
|-------------------|-----------------|--------|----------|--------|
| Premium / luxury | Slow, deliberate, no bounce | High damping | Long (400ms+) | Ease-in-out |
| Playful / consumer | Bouncy, energetic, springy | Low damping | Short–medium | Spring |
| Technical / precise | Fast, exact, minimal | Very high damping | Short (150–200ms) | Ease-out |
| Trustworthy / financial | Calm, smooth, no surprises | High damping | Medium | Ease-out |
| Friendly / approachable | Warm, gentle, slight bounce | Medium damping | Medium | Spring |

### Motion Vocabulary (3–5 rules per brand)

```
Example motion vocabulary for a fintech app (Nexus):
  1. Transitions are purposeful — no decorative motion; every animation has a reason
  2. Numbers count up — values reveal with a count-up, not a snap (precision + activity)
  3. Data arrives staggered — lists enter top-to-bottom, giving a sense of order
  4. Spring with restraint — spring physics on modals/sheets, but damped (no bounce)
  5. Enter fast, exit faster — UI gets out of the way; exits are 80% of enter duration
```

### Delight Moments

```
Delight moments are exceptional — not every interaction, only milestones:

  Onboarding complete: Confetti burst (particles fly from center, 1200ms)
  First portfolio connected: Counter animates to total value
  Performance milestone: Success animation plays (Lottie or SVG draw-on)
  Achievement unlocked: Trophy icon bounces in from bottom

Rules:
  - Delight once, not repeatedly (if user sees it every visit, it's noise)
  - Delight should match the user's emotional state (don't celebrate a small action hugely)
  - Always dismissible — delight that blocks the user is anti-delight
  - Keep it proportionate: 600–1200ms max, then it's done
```

### Transition Signatures

```
A "signature" transition is a distinctive animation that defines the product's
navigation feel — users recognize it across screens.

Example signatures:
  iOS: Slide with parallax (cards layer behind each other)
  Notion: Crossfade with slight scale
  Figma: Instant (no transition — speed IS the brand)

Defining Nexus's signature:
  Card → Detail: Card expands (shared element transition, spring)
  Tab navigation: Crossfade (0.2s) — clean, professional, no distraction
  Screen stack: Slide from right (standard, predictable, reliable)

Consistency is the brand: Use the same transition for the same navigation type, always.
```

### Motion as Feedback

```
The product's personality shows in how it responds to the user:

Generous response: Large touch targets, instant visual feedback — brand is welcoming
Precise response: Small, exact feedback — brand is technical
Warm response: Slight overshoot on spring, color warmth — brand is friendly

Design the feedback to match the brand position.
Nexus (financial, trustworthy): Precise, fast, confidence-inspiring.
  Press: scale(0.97) — controlled, not dramatic
  Success: Checkmark draws in, no confetti (money is serious)
  Error: Clear, calm red highlight — not alarming, just accurate
```

### Outputs
- Motion vocabulary document (3–5 rules with examples)
- Signature transition spec
- Delight moment implementations (for key milestones)
- Brand motion style guide entry
