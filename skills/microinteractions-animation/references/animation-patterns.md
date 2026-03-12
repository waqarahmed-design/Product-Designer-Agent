# Animation Patterns

## Table of Contents
1. [Loading Animations](#1-loading-animations)
2. [Hover Effects](#2-hover-effects)
3. [Click/Tap Feedback](#3-clicktap-feedback)
4. [Page Transitions](#4-page-transitions)
5. [Scroll-Based Animation](#5-scroll-based-animation)
6. [Pull-to-Refresh](#6-pull-to-refresh)
7. [Swipe Gestures](#7-swipe-gestures)
8. [Toggle Animations](#8-toggle-animations)
9. [Modal Animations](#9-modal-animations)
10. [Toast Notifications](#10-toast-notifications)

---

## 1. Loading Animations

**Purpose:** Fill the time while content is fetching, reducing perceived wait time and preventing blank-screen anxiety.

**When to use:** Any operation taking > 400ms. Below 400ms: skip the loading state entirely.

### Spinner

```
Use for: Indeterminate waits, short fetches, button-level loading
Avoid for: Content loading (use skeleton instead)

Spec:
  Size: 20–24px (inline), 32–40px (full-screen)
  Speed: 700–900ms per revolution
  Easing: linear (constant rotation speed)
  Color: Brand primary or neutral gray

CSS:
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  .spinner {
    animation: spin 750ms linear infinite;
    border: 2px solid rgba(255,255,255,0.2);
    border-top-color: var(--color-accent);
    border-radius: 50%;
  }

React Native:
  <ActivityIndicator size="small" color={Colors.accent} />
  Or custom with Reanimated:
    const rotation = useSharedValue(0);
    useEffect(() => {
      rotation.value = withRepeat(withTiming(360, { duration: 750, easing: Easing.linear }), -1);
    }, []);
```

### Skeleton Screen

```
Use for: Content loading (lists, cards, profile pages, feeds)
Prefer over spinner when: The layout is known before data arrives

Rules:
  - Mirror the actual content layout with gray placeholder shapes
  - Text lines: 100% width (title), 60–80% width (body), varying lengths look more real
  - Image slots: exact dimensions of the final image
  - No text, no icons — just shapes

Shimmer effect:
  A left-to-right gradient sweep communicates "loading in progress"
  Gradient: transparent → 10% lighter → transparent, moving right
  Speed: 1400–1600ms per sweep, linear, infinite

CSS shimmer:
  @keyframes shimmer {
    0%   { background-position: -200% 0; }
    100% { background-position: 200% 0; }
  }
  .skeleton {
    background: linear-gradient(90deg,
      var(--skeleton-base) 25%,
      var(--skeleton-highlight) 50%,
      var(--skeleton-base) 75%
    );
    background-size: 200% 100%;
    animation: shimmer 1500ms linear infinite;
  }

React Native (manual):
  Use Animated.loop + Animated.timing on a translateX or interpolated opacity.
  Or: react-native-skeleton-placeholder library.
```

### Progress Indicators

```
Determinate (known progress):
  Use a progress bar with actual % fill
  Animate the fill with ease-out: feels faster than linear
  Show % label only if meaningful precision helps the user

Indeterminate (unknown progress):
  Traveling dot or shrinking/growing bar
  Never show a fake progress bar (one that lies about progress)

Step progress (multi-step forms):
  Dots or numbered steps — no animation needed beyond fill change
  Fill step indicator with ease-out 300ms on advance
```

### Outputs
- Spinner component with size variants
- Skeleton component with layout props
- Progress bar (determinate + indeterminate)

---

## 2. Hover Effects

**Purpose:** Confirm interactivity and create a tactile, responsive feel before commitment.

**When to use:** Desktop/web only — hover doesn't exist on touch. Never design a feature that's hover-only.

### Hover Pattern Catalog

**Surface lift (cards):**
```css
.card {
  transition: transform 150ms ease-out, box-shadow 150ms ease-out;
}
.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
}
```

**Background tint (list items, nav items):**
```css
.list-item {
  transition: background-color 100ms ease-out;
}
.list-item:hover {
  background-color: var(--color-hover-tint); /* 5–8% opacity white or black */
}
```

**Icon reveal (action buttons that appear on hover):**
```css
.row .actions {
  opacity: 0;
  transition: opacity 150ms ease-out;
}
.row:hover .actions {
  opacity: 1;
}
```

**Underline grow (links):**
```css
.link {
  text-decoration: none;
  background: linear-gradient(currentColor, currentColor) no-repeat 0 100%;
  background-size: 0% 1px;
  transition: background-size 200ms ease-out;
}
.link:hover {
  background-size: 100% 1px;
}
```

**Scale (buttons, icons):**
```css
.button {
  transition: transform 100ms ease-out;
}
.button:hover {
  transform: scale(1.03);
}
```

### Hover Rules

```
Duration: 100–150ms (fast — hover is immediate feedback, not a transition)
Easing: ease-out (arrives quickly, settles)
Scale: never exceed 1.05 — anything larger looks broken
Elevation: 2–4px translate-Y for cards is enough
Color: use opacity-based tints, not hardcoded colors (stays on-brand in both themes)
Never: disable hover on elements that look interactive
Never: hover that blocks or hides content
```

### Outputs
- Hover token system (CSS custom properties for hover states)
- Component hover specs

---

## 3. Click/Tap Feedback

**Purpose:** Provide immediate physical confirmation that a tap/click registered — before the result is visible.

**When to use:** Every interactive element. The fastest response possible.

### Press State

```
Desktop button press:
  onMouseDown: scale(0.97) + brightness(0.9), 50ms ease-out
  onMouseUp:   scale(1.0) + brightness(1.0), 100ms spring

Mobile tap (React Native):
  Pressable:
    onPressIn:  Animated.spring(scale, { toValue: 0.96, useNativeDriver: true })
    onPressOut: Animated.spring(scale, { toValue: 1.0, useNativeDriver: true })

Timing: 50ms into press, 100ms out — instant response is the goal
```

### Ripple Effect (Android / Material)

```
A circular ripple emanates from the tap point.
React Native: Built into <TouchableNativeFeedback> on Android.
Web: CSS clip-path expanding circle from pointer coordinates.

Spec:
  Origin: exact tap point (not center)
  Color: 12% opacity white (on dark) or black (on light)
  Duration: 400–600ms ease-out
  Radius: expands to cover the full element
```

### Icon Button Feedback

```
Icon buttons (no label) need extra feedback — they're small targets:
  Press: scale(0.85) + background circle appears
  Release: scale(1.0) + background fades out
  Duration: 100ms press / 200ms release

This creates a "dimple" effect that confirms the tap on small targets.
```

### Long Press

```
Visual cue that long press is activating:
  Progressive fill: border or background fills over hold duration
  Or: subtle scale increase over time
  Duration: 500ms to trigger (standard mobile long-press threshold)

Release before threshold:
  Immediately cancel the animation — don't commit
```

### Disabled State Feedback

```
Disabled elements should NOT respond to taps — not even with a shake.
A disabled state is a silent state.
Exception: If it helps the user understand WHY it's disabled
  (e.g., an error tooltip on hover), that's a UX pattern, not animation.
```

### Outputs
- Press animation implementation for target platform
- Ripple or dimple pattern for icon buttons
- Long press indicator component

---

## 4. Page Transitions

**Purpose:** Communicate navigation direction and spatial hierarchy while maintaining continuity between screens.

**When to use:** Every navigation event between major screens.

### Transition Types by Navigation Type

| Navigation type | Transition | Direction |
|----------------|-----------|-----------|
| Push (drill into) | Slide | New screen from right |
| Pop (go back) | Slide | New screen from left |
| Tab switch | Crossfade or slide | Right if tab index ↑, left if ↓ |
| Modal | Slide up + fade | From bottom |
| Modal dismiss | Slide down + fade | To bottom |
| Bottom sheet | Slide up | From bottom (shorter travel) |
| Alert/dialog | Scale up + fade | From center |
| Full-screen overlay | Fade | In/out |

### Slide Transition Spec

```
Enter (from right):
  Start: translateX(100%) + opacity(0)
  End: translateX(0) + opacity(1)
  Duration: 300ms spring (tension: 60, friction: 14)

Exit (to left, going behind):
  Start: translateX(0) + opacity(1)
  End: translateX(-30%) + opacity(0.8)
  Duration: 300ms ease-in

Note: The exiting screen moves only 30% — it doesn't completely leave the viewport.
This parallax-like effect maintains spatial context.

iOS-style:
  The outgoing screen moves left at 30% the speed of the incoming.
  This is the "iOS parallax" navigation feel.
```

### Modal/Sheet Transition Spec

```
Bottom sheet (partial):
  Enter: translateY(100%) → translateY(0), 350ms spring
  Backdrop: opacity 0 → 0.5, 300ms ease-out
  Dismiss: translateY(100%), 250ms ease-in (faster than enter)

Full modal:
  Enter: translateY(40px) + opacity(0) → position + opacity(1), 300ms ease-out
  Dismiss: translateY(20px) + opacity(0), 200ms ease-in

Dialog:
  Enter: scale(0.94) + opacity(0) → scale(1) + opacity(1), 200ms spring
  Dismiss: scale(0.97) + opacity(0), 150ms ease-in
```

### React Native Implementation Notes

```
Expo Router: Transitions are configured in the layout.
  Stack navigator handles slide automatically.
  Customize with gestureEnabled, animation, cardStyle.

React Navigation custom transition:
  cardStyleInterpolator: CardStyleInterpolators.forHorizontalIOS

Custom with Reanimated:
  Use Layout animation or entering/exiting props on Animated.View.
  entering={SlideInRight.duration(300)}
  exiting={SlideOutLeft.duration(250)}
```

### Outputs
- Transition map (navigation type → animation type)
- Implementation for target navigator
- Duration and easing specs

---

## 5. Scroll-Based Animation

**Purpose:** Reveal content progressively as users scroll, guide attention, and add depth through parallax layering.

**When to use:** Marketing/landing pages; onboarding flows; content-heavy screens where revealing on scroll improves comprehension.

### Reveal on Scroll

```
Pattern: Elements animate in as they enter the viewport.
Effect: Fade in + slight translateY (20–30px) as element crosses the fold.

Web (Intersection Observer):
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });

CSS:
  .element { opacity: 0; transform: translateY(24px); transition: opacity 400ms ease-out, transform 400ms ease-out; }
  .element.visible { opacity: 1; transform: translateY(0); }

Duration: 300–500ms ease-out
Threshold: 10–15% visible before triggering (not 0% — too early)
Don't re-animate: Once revealed, stay revealed (removing class on scroll-out is jarring)
```

### Parallax

```
Principle: Background elements move slower than foreground, creating depth.
Rate: Background moves at 30–50% of scroll speed.

Web:
  window.addEventListener('scroll', () => {
    const scrollY = window.scrollY;
    element.style.transform = `translateY(${scrollY * 0.4}px)`;
  });

Rules:
  - Never parallax text that users need to read while scrolling
  - Never parallax interactive elements
  - Test on low-end devices — can cause jank
  - Use will-change: transform to promote to GPU layer

React Native: Animated.event with Animated.ScrollView for scroll-driven values.
```

### Sticky Headers

```
Not animation per se, but a motion pattern:
  Header sticks to top on scroll, shrinks/changes style.

Transition into sticky: instant (no animation — it just snaps, which is correct)
Shrink: CSS transition on height/font-size, 200ms ease-out
Background: opacity transition from transparent to solid, 200ms
```

### Scroll Progress

```
A thin bar that fills as user scrolls through content.
Use for: Long articles, multi-section guides (shows how far through they are)
Height: 2–4px at top of viewport
Color: Brand accent or neutral
Animation: No easing needed — it's directly tied to scroll position
```

### Outputs
- Reveal on scroll implementation (IntersectionObserver or ScrollView listener)
- Parallax implementation (if applicable)
- Scroll progress indicator component

---

## 6. Pull-to-Refresh

**Purpose:** Provide a natural gesture to trigger content refresh on mobile, with clear visual feedback for gesture state.

**When to use:** Any scrollable feed or list where fresh data matters (social feed, financial data, news).

### Pull-to-Refresh States

```
State 1: Idle
  No indicator visible. ScrollView is at top.

State 2: Pulling (resistance)
  User pulls down. Indicator descends with resistance (pull more than actual scroll delta).
  Resistance ratio: ~0.4–0.5 (40px pull → 20px displacement)
  This "rubber band" feel signals the threshold hasn't been met yet.

State 3: Ready (threshold met)
  Indicator snaps to a visible "ready to release" state.
  Visual: Arrow flips from down to up (or spinner starts).
  Haptic: Light haptic feedback (iOS: UIImpactFeedbackGenerator .light)

State 4: Refreshing
  User releases. Indicator settles into fixed position.
  Spinner starts rotating.
  List locks scroll at top while refresh runs.

State 5: Complete
  Data arrives. Indicator hides with a quick fade.
  List content updates with stagger animation.
  Haptic: Success haptic on iOS.
```

### Spec

```
Trigger threshold:   60–80px of pull
Indicator size:      32–40px
Indicator position:  Fixed at 24px below the top of the list
Settle animation:    Spring — snaps from pull position to indicator position
Hide animation:      Fade out 200ms ease-in after refresh completes
Minimum display time: Show spinner for at least 600ms even if refresh is instant
  (Instant refresh with instant hide feels like a glitch)
```

### React Native

```jsx
<ScrollView
  refreshControl={
    <RefreshControl
      refreshing={isRefreshing}
      onRefresh={handleRefresh}
      tintColor={Colors.accent}
      colors={[Colors.accent]}  // Android
    />
  }
>
```

### Outputs
- Pull-to-refresh component with all 5 states
- Haptic feedback integration
- Minimum display time guard

---

## 7. Swipe Gestures

**Purpose:** Enable swipe-to-action patterns (delete, archive, snooze) and swipe-to-dismiss interactions, with real-time gesture feedback.

**When to use:** Mobile lists where swipe reveals secondary actions; dismissible cards or modals.

### Swipe-to-Reveal Actions

```
Pattern: Drag a list item left/right to reveal action buttons underneath.

Reveal threshold: 60–80px drag before actions are visible
Action button: appears behind the item as it slides

Gesture states:
  Dragging: Item follows finger in real time. Resistance after threshold.
  Threshold met: Haptic. Action button pulses.
  Release before threshold: Spring back to 0 (200ms spring).
  Release after threshold: Settle at action-visible position.
  Action confirmed: Item animates out (exit left/right 300ms) + list closes gap.

Spring spec:
  Mass: 1, stiffness: 200, damping: 20
  → Snappy return but not bouncy

React Native with Reanimated:
  PanGestureHandler + useSharedValue(0) for translateX.
  Use interpolate to map drag distance to action opacity.
  runOnJS(handleAction)() in gesture end handler.
```

### Swipe-to-Dismiss

```
Pattern: Swipe up (or left/right) to dismiss a card or overlay.

Dismiss threshold: 100px or 30% of element height (whichever is smaller)
Velocity threshold: If user flicks fast enough (velocity > 500), dismiss regardless of distance.

Dismiss animation: continue in swipe direction, 200ms ease-in
Return animation: spring back to origin, 300ms spring

Commonly used for:
  - Dismissible cards
  - Bottom sheet dismissal (swipe down)
  - Image viewer dismissal (swipe down to close)
```

### Implementation Rules

```
Always use useNativeDriver: true — gesture animations must be 60fps
Never block the JS thread in gesture handlers
Use react-native-gesture-handler over PanResponder for all swipe gestures
Wrap in GestureHandlerRootView at the app root
```

### Outputs
- Swipe-to-reveal implementation with reusable component
- Swipe-to-dismiss hook
- Gesture threshold and spring spec

---

## 8. Toggle Animations

**Purpose:** Make state changes in toggles, checkboxes, and radio buttons feel physical and satisfying — confirming the action with motion.

**When to use:** All binary toggle controls, checkboxes, switches, and radio button selections.

### Switch/Toggle

```
States: Off ←→ On
Visual: Thumb slides left/right; track changes color.

Spec:
  Thumb travel: track width - thumb width - 4px padding
  Duration: 200ms spring (tension: 60, friction: 10)
  Color transition: 200ms ease-out (track background)
  Haptic: Light impact on state change (iOS)

React Native:
  Animated.spring(thumbX, {
    toValue: isOn ? TRACK_WIDTH - THUMB_SIZE - 4 : 4,
    useNativeDriver: true,
    tension: 60, friction: 10,
  }).start();
  Simultaneously interpolate backgroundColor with Animated.timing
  (useNativeDriver: false for backgroundColor).

Important: useNativeDriver: true for translateX, false for color.
```

### Checkbox

```
States: Unchecked → Checked → Indeterminate

Checked animation:
  1. Background fills (scale from 0 or color fade), 150ms ease-out
  2. Checkmark draws (path stroke-dashoffset from 100% → 0%), 150ms ease-out
  Sequence: fill and checkmark start together; checkmark lags by 50ms

Uncheck animation:
  1. Checkmark fades/erases, 100ms ease-in
  2. Background clears, 100ms ease-in
  Faster than check — confirmation is slower; removal is quick.
```

### Radio Button

```
Selection animation:
  Inner circle scales from 0 to full size, 150ms spring
  Outer ring: border color changes, 100ms ease-out
  Deselect: inner circle scales to 0, 100ms ease-out

Group behavior:
  When selecting a new option:
    Old selection: deselects simultaneously (100ms)
    New selection: selects simultaneously (150ms)
  No choreography needed — they happen at the same time.
```

### Segmented Control / Tab Switch

```
Selected indicator moves between segments.

Spec:
  Sliding pill: translateX from current to next, 200ms spring
  Width: interpolates between old and new segment widths (if unequal)
  Label color: changes 100ms after indicator starts moving

React Native (custom tab bar):
  Measure segment widths on layout.
  Animate slideX and slideWidth Animated.Values.
  useNativeDriver: false (width animation cannot use native driver).
```

### Outputs
- Switch/toggle component with spring animation
- Checkbox with draw-on animation
- Segmented control with sliding indicator

---

## 9. Modal Animations

**Purpose:** Signal the appearance and dismissal of overlays with motion that reinforces their layer, importance, and relationship to the triggering element.

**When to use:** All dialogs, bottom sheets, modals, action sheets, and overlay panels.

### Modal Types and Animations

**Dialog (centered, small):**
```
Enter:
  Scale: 0.90 → 1.00
  Opacity: 0 → 1
  Duration: 250ms spring (slightly bouncy)
  Backdrop: opacity 0 → 0.6, 200ms ease-out

Dismiss:
  Scale: 1.00 → 0.95
  Opacity: 1 → 0
  Duration: 180ms ease-in (faster than enter)
  Backdrop: opacity 0.6 → 0, 200ms ease-out
```

**Bottom sheet (partial, slides up):**
```
Enter:
  translateY: 100% → 0%
  Duration: 350ms spring (tension: 55, friction: 14)
  Backdrop: opacity 0 → 0.6, 300ms ease-out

Dismiss (button tap):
  translateY: 0% → 100%
  Duration: 250ms ease-in
  Backdrop: fades simultaneously

Dismiss (swipe down):
  Follow gesture in real time, then animate to 100% on release
  (see Swipe Gestures)
```

**Full-screen modal:**
```
Enter: slide up from bottom (same as bottom sheet but full height)
Dismiss: slide down to bottom
Duration: 350ms spring enter / 280ms ease-in dismiss

iOS-style:
  The presenting screen scales down slightly (0.92) and moves up
  while the modal slides in — depth effect.
```

**Action sheet (iOS style):**
```
Items are grouped in a rounded card + separate cancel button.
Enter: Whole group slides up together, 300ms spring
Dismiss: Whole group slides down, 200ms ease-in
Cancel button: Same animation as group (moves together)
```

### Backdrop

```
Always animate the backdrop separately from the modal.
Backdrop should fade slightly faster than the modal slides.
Never let the backdrop linger after the modal is gone.

Tap backdrop to dismiss:
  Triggers same dismiss animation as button dismiss.
  Modal does NOT shake — tap-outside-to-dismiss is a valid interaction, not an error.
```

### Outputs
- Dialog component with enter/exit animation
- Bottom sheet component with gesture dismiss
- Backdrop component with fade animation

---

## 10. Toast Notifications

**Purpose:** Deliver ephemeral, non-blocking feedback that appears, holds for reading, and dismisses without requiring user action.

**When to use:** Success confirmations, error alerts, status updates, undo prompts.

### Toast Animation Lifecycle

```
1. Appear (enter animation)
   Slide in from top or bottom + fade in
   Duration: 300ms spring

2. Hold (display time)
   Duration based on message length:
     Short (1–3 words): 2000ms
     Standard (1 sentence): 3000ms
     Long (2+ sentences): 4000ms
   Never less than 2000ms — users need time to read

3. Dismiss (exit animation)
   Slide out + fade out in original direction
   Duration: 250ms ease-in

4. Interrupted dismiss (user swipes):
   Follow gesture, continue to dismiss on release
```

### Toast Position

```
Top toast (recommended for web):
  Slides down from top edge
  Position: fixed, top: safeAreaTop + 16px
  z-index: above most content, below critical system overlays

Bottom toast (recommended for mobile):
  Slides up from bottom edge
  Position above tab bar (bottom: tabBarHeight + 16px)
  Less likely to obscure primary content during action

Multiple toasts:
  Stack vertically with 8px gap
  New toast pushes existing up (or down if bottom)
  Limit to 3 visible at once — older ones dismiss early
```

### Toast Variants

```
Success: Green accent, checkmark icon
Error: Red accent, alert icon
Info: Neutral/blue, info icon
Warning: Yellow/amber, warning icon
Undo: Neutral, with "Undo" button — dismiss countdown visible as border progress
```

### Undo Toast (Special Case)

```
Appears immediately after a destructive action (delete, archive).
Contains: "[Action] [item name]" + "Undo" button.
Countdown: A progress bar shrinks across the bottom of the toast.
  Duration matches hold time (4000ms for destructive actions).
  User can tap Undo at any point before dismissal.

On Undo tap:
  Toast dismisses immediately with spring (100ms)
  Action reverses
  Optional: Success toast confirming reversal
```

### Outputs
- Toast component with all variants and lifecycle animation
- Toast queue manager (handles multiple toasts)
- Undo toast with countdown indicator
