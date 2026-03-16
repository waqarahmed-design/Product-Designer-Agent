# Mobile Design

## Table of Contents
1. [Native Patterns — iOS HIG & Material Design](#1-native-patterns--ios-hig--material-design)
2. [Touch Gestures](#2-touch-gestures)
3. [Mobile Navigation](#3-mobile-navigation)
4. [Notification Design](#4-notification-design)
5. [Onboarding](#5-onboarding)
6. [App Icon Design](#6-app-icon-design)

---

## 1. Native Patterns — iOS HIG & Material Design

**Purpose:** Design with platform conventions so apps feel native — reducing the cognitive load for users who already know how the platform works.

**When to use:** Any mobile UI that targets iOS or Android. Platform conventions should be the default; deviate only with clear reason.

### iOS Human Interface Guidelines — Core Principles

```
Clarity: Text is legible, icons precise, adornments minimal.
Deference: UI helps users understand and interact with content — doesn't compete with it.
Depth: Visual layers communicate hierarchy and position.
```

### iOS Platform Conventions

| Element | iOS Convention |
|---------|---------------|
| Navigation | Large title → collapses on scroll; back arrow ← with label |
| Tab bar | Bottom, 5 items max, system icons or custom 25×25pt |
| Action sheets | Slide up from bottom; system style; cancel always last |
| Context menus | Long press → menu of actions (replaces 3D Touch) |
| Alerts | Centered dialog; 2 buttons (Cancel left, destructive/confirm right) |
| Switches | Toggle with iOS system style; right-aligned in table rows |
| Lists | Inset grouped (rounded cards) or plain (full-width rows) |
| Pull-to-refresh | Standard UIRefreshControl — don't fight it |
| Safe areas | Top (status bar + notch/island), bottom (home indicator) |
| Haptics | Selection, success, warning, error — use UIImpactFeedbackGenerator |
| SF Symbols | Use for system iconography — already optimized for iOS rendering |

### iOS Typography Scale (Dynamic Type)

```
Text styles (system-defined, respect user's font size preference):
  largeTitle:  34pt regular (screen headings)
  title1:      28pt regular
  title2:      22pt regular
  title3:      20pt regular
  headline:    17pt semibold
  body:        17pt regular (primary body text)
  callout:     16pt regular
  subheadline: 15pt regular
  footnote:    13pt regular
  caption1:    12pt regular
  caption2:    11pt regular

Rule: Always use Dynamic Type — let users control text size.
  Hard-coded font sizes ignore accessibility user preferences.
  Use .body, .headline, etc. — not 17px.
```

### Material Design 3 (Android) — Core Principles

```
Material You: Adaptive design that responds to the user's personal color choices.
Expressive: Bolder, more personality-forward than M2.
Accessible by default: Contrast requirements met by the system.
```

### Material Design 3 Conventions

| Element | Material Design 3 |
|---------|-----------------|
| Navigation | Navigation bar (bottom, 3–5 items) or Navigation drawer (left) |
| FAB | Floating Action Button — primary action, bottom right |
| Top app bar | Compact → medium → large; collapses on scroll |
| Cards | Elevated, filled, or outlined variants |
| Dialogs | Centered, rounded (28dp); buttons right-aligned (Cancel + Confirm) |
| Bottom sheets | Modal (over backdrop) or standard (persistent) |
| Snackbars | Brief messages at bottom; single optional action |
| Chips | Filter, assist, suggestion, input — inline compact actions |
| Dynamic color | Apps can pick up user's Material You wallpaper colors |
| Ripple | Touch feedback via ripple from tap point |

### Cross-Platform Design Decisions

```
When building for both iOS and Android:

Option A: One design, one set of components
  Works if: Design is generic enough to feel acceptable on both
  Risk: May feel slightly "foreign" on each platform

Option B: Platform-adaptive (recommended for mature products)
  Share: Colors, typography, spacing, icons, content
  Differentiate: Navigation pattern, specific controls, interaction style

The 80/20 rule:
  80% of the design is shared (content, hierarchy, brand)
  20% adapts to each platform (specific controls, navigation)

Always adapt:
  Navigation bar position (iOS: bottom tab / Android: bottom nav or drawer)
  Back navigation (iOS: swipe right from edge / Android: system back gesture)
  Typography sizing (pt for iOS, sp for Android)
  Action sheet vs. bottom sheet style
```

### Outputs
- Platform-specific component variants (iOS + Android)
- Navigation pattern selected per platform
- Typography specified in platform units (pt / sp)
- Haptic feedback plan (iOS) + ripple plan (Android)

---

## 2. Touch Gestures

**Purpose:** Design intuitive, discoverable touch interactions that respect platform conventions and feel natural to mobile users.

**When to use:** Any mobile interaction beyond simple taps; when designing swipe actions, pull behaviors, or multi-touch interactions.

### Gesture Taxonomy

| Gesture | Description | Common use |
|---------|-------------|-----------|
| Tap | Single finger touch + release | Select, activate, navigate |
| Double tap | Two taps in quick succession | Zoom in, like/heart action |
| Long press | Hold without movement (500ms) | Reveal contextual actions, drag-to-reorder |
| Swipe | Single-direction slide | Navigate back (iOS), scroll, dismiss, reveal actions |
| Pan/drag | Free movement | Reorder lists, resize, drag objects |
| Pinch | Two fingers moving apart or together | Zoom in/out |
| Spread | Two fingers expanding | Zoom in (same as pinch out) |
| Rotate | Two fingers rotating | Rotate content (maps, images) |
| Pull | Scroll past the top of a list | Pull-to-refresh |
| Force touch | Pressure-sensitive press (iOS, select devices) | Peek and pop (deprecated in favor of long press) |
| Flick | Quick swipe with high velocity | Fast scroll, dismiss |

### Gesture Design Rules

**Discoverability:**
```
Problem: Gestures are invisible — users can't see what's possible.
Solutions:
  1. Use standard platform gestures (known from other apps)
  2. Visual affordance cues: drag handles, swipe arrows, "pull to refresh" label
  3. Onboarding: demonstrate gestures on first use
  4. Never rely solely on a gesture for a critical action — always provide a button fallback
```

**Conflict resolution:**
```
Gestures can conflict with each other and with the system.

iOS system gestures that designers cannot override:
  Swipe from left edge: Back navigation (cannot block)
  Swipe from bottom: Home indicator/Control Center (cannot block)
  Swipe from top-right corner: Control Center
  Long press on text: Text selection (cannot block in text areas)

If your gesture conflicts with a system gesture:
  Option 1: Change your gesture
  Option 2: Change the direction (use diagonal or two-finger if system uses one-finger)
  Option 3: Only enable gesture in specific contexts (not globally)
```

**Touch target sizing:**
```
Minimum: 44×44pt (iOS HIG) / 48×48dp (Material Design)
Preferred: 48×48pt for primary actions

For small visual elements (icons, badges):
  The tap target can be larger than the visual element.
  Add invisible padding around small elements.

Adjacent touch targets:
  Minimum 8pt gap between adjacent interactive areas
  Reduces mis-taps on neighboring elements
```

### Swipe Action Design

```
Swipe-to-reveal actions (list items):
  Left swipe: Reveal destructive action (delete, archive) — red background, right side
  Right swipe: Reveal affirmative action (mark read, flag) — green background, left side

Reveal threshold: 60–80pt before action icon becomes visible
Action trigger threshold: Full swipe (item disappears) OR tap revealed action button

Full-swipe-to-delete:
  Only use when action is easily understood from context
  Always show undo toast immediately after
  iOS: UIContextualAction pattern (native swipe appearance)
  Material: Swipe-to-dismiss snackbar with undo

Visual during swipe:
  Icon + label (first 80pt of reveal)
  Label disappears, icon only + background fills (past 80pt)
  Item springs back if released before threshold
```

### Multi-Touch Interactions

```
Pinch-to-zoom:
  Minimum: 2 fingers apart/together on zoomable content
  Visual feedback: Content scales from the midpoint of the two fingers
  Limits: Define min zoom (1× default) and max zoom (4× typical)

Two-finger scroll (iPad):
  Used for scrolling within a table/spreadsheet when one finger selects
  Indicates precision mode

Rotation:
  Use sparingly — requires significant finger coordination
  Best for: Maps, image editors, spatial content
  Always show current rotation angle numerically
```

### Outputs
- Gesture map for the screen/feature (which gesture does what)
- Touch target size audit
- Gesture tutorial component for novel interactions
- System gesture conflict analysis

---

## 3. Mobile Navigation

**Purpose:** Design navigation systems that clearly communicate where the user is, how to get anywhere else, and how to go back — without consuming excessive screen space.

**When to use:** Structuring the overall navigation architecture of a mobile app.

### Navigation Patterns

**Tab Bar (iOS) / Bottom Navigation (Android)**
```
Use for: Apps with 3–5 top-level destinations of roughly equal importance.
Position: Fixed at bottom of screen (above safe area on iOS).

iOS tab bar:
  Max: 5 tabs (more → "More" tab with a list)
  Icon: 25×25pt, system weight (not outline vs. filled — use SF Symbols)
  Label: 10pt, directly below icon
  Active: Bold icon + label; system tint color
  Badge: Red circle with count (notifications)

Material Navigation bar:
  3–5 items; icons (24dp) + labels; active shows filled icon
  Indicator pill behind active icon (M3)
  Avoid for linear or transactional flows (use drawers/other)

When NOT to use tab bar:
  Linear flows (onboarding, checkout) — use step navigation
  Single-purpose apps — use direct access
  Too many destinations (6+) — use navigation drawer
```

**Navigation Drawer (Android / iPad)**
```
Slide from left (standard) or persistent panel (iPad landscape).
Use for: Many destinations (6+); complex hierarchy; infrequent section switching.
Contains: List of destinations with icons + labels; user profile at top.
Trigger: Hamburger menu ≡ in top app bar; swipe from left edge.
Don't use for: Primary frequent navigation (creates extra tap for common actions).
```

**Bottom Sheet**
```
Partial: Slides up to show additional content; user can still see screen behind.
  Use for: Filters, options, secondary content, contextual menus.
  Dismiss: Tap outside or swipe down.
  Sizes: Peek (just a handle), Half screen, 90% screen.

Modal (full): Slides up from bottom, covers most of screen.
  Use for: Focused tasks (add item, compose message, quick form).
  Different from full modal: has a handle, feels lightweight.
  Dismiss: Swipe down or a close button.

Handle design:
  2–3pt height, 24–32pt width, center-aligned, Colors.muted or similar.
  Signals: "this can be dismissed by swiping down."
```

**Stack Navigation (Push/Pop)**
```
Every tap into deeper content = push. Every back = pop.
Always available: Back gesture (iOS: swipe right from edge) / System back (Android).
Large title: Collapses as user scrolls deeper (iOS convention).

Don't use for:
  Lateral navigation (same level) — use tabs or segmented control
  Actions (confirm, submit) — these don't change location
```

**Modal Presentation**
```
When to use a modal (instead of push):
  Self-contained task (compose, new item, settings)
  Task that could be canceled without losing context
  Creation flows (add exchange, create report)

When NOT to use a modal:
  Navigational content (drill-in detail views)
  Complex multi-step flows (use full navigation stack instead)
  Anything the user will spend more than ~5 min in

Modal dismiss:
  X (close) button: Top-left (iOS) or top-right
  Swipe down: Standard dismiss gesture for modals on iOS
  Confirm/Cancel in header: For forms with unsaved changes
```

### Deep Linking and State Preservation

```
Deep link: URL or notification tap that takes user directly to a specific screen.
Design for: Every screen should be reachable via deep link.
Preserve context: When a deep link opens, the user should be able to navigate back normally.

State preservation:
  If the user was mid-flow and switches apps, they should return to where they were.
  Don't reset to the home screen on every launch (unless security requires it).
  Financial apps: re-authentication required, but navigate back to last location after.
```

### Outputs
- Navigation architecture diagram (all screens + how they connect)
- Tab bar / nav bar design with all states
- Bottom sheet component (partial + modal variants)
- Deep link map

---

## 4. Notification Design

**Purpose:** Design push notifications, in-app banners, and badge indicators that deliver value without annoying users — respecting attention and earning permission.

**When to use:** Adding any notification system to an app; writing notification copy; designing notification settings.

### Push Notification Anatomy

```
iOS notification:
  App icon (auto)
  App name (auto)
  Time (auto)
  Title: Bold text — 50 chars max
  Body: Secondary text — 100 chars max (2 lines before truncation)
  Subtitle: Optional, between title and body
  Attachment: Image/video thumbnail (opt-in by user)
  Actions: 1–4 buttons (visible on long press or in notification center)

Android notification:
  Large icon: App icon or person photo (chat notifications)
  Title: Primary bold text
  Text: Secondary line
  Expandable: Long notification expands on tap (inbox style, big text, big image)
  Actions: 1–3 inline action buttons
  Reply: Inline reply field (messaging apps)
```

### Notification Types by Value

```
Transactional (highest value — always send):
  Examples: "Payment sent", "Order shipped", "Verification code: 847291"
  These are expected and requested. Always deliver immediately.

Alert (high value — user-relevant):
  Examples: "BTC dropped 15% in the last hour", "Your portfolio crossed $100k"
  User set a threshold or alert. Deliver promptly.

Engagement (medium value — earn this):
  Examples: "You haven't checked your portfolio in 5 days"
  Only send if user opted in. Never default on.
  Be honest about what value this provides the user (vs. what it does for the business).

Promotional (low value — use sparingly):
  Examples: "Try our new premium features"
  Require explicit opt-in. One per week maximum.
  Provide clear unsubscribe path.
```

### Notification Copy Rules

```
Title: What happened (specific, concrete)
  ✅ "Bitcoin down 12.3% today"
  ❌ "Market update" (vague, no information)

Body: Why it matters to this user
  ✅ "Your BTC holdings lost $1,847 in value"
  ❌ "Check your portfolio for details" (doesn't add value)

Action labels: What the tap does (not just "Open")
  ✅ "View portfolio" / "Dismiss"
  ❌ "OK" / "Cancel"

Personalization increases tap rate:
  Include the user's actual data (asset name, amount, threshold they set)
  Generic notifications feel like spam
```

### Notification Permission Design

```
The permission ask is the most important moment in notification design.
iOS: Requires explicit permission prompt. One chance — denied = must go to Settings.

Best practices:
  1. Don't ask on first launch. User has no context for why they'd want notifications.
  2. Provide value first. Let user experience the app's core value.
  3. Show pre-permission screen (soft ask) before triggering OS dialog.
     "To alert you when Bitcoin crosses your target price, Nexus needs permission."
     [Allow] [Not now]
     → If "Allow" → trigger OS dialog
     → If "Not now" → skip, can ask again later

Pre-permission screen elements:
  Icon: Bell or relevant icon
  Headline: The specific benefit ("Know the moment your targets hit")
  Body: What you'll send (specific, not vague)
  CTA: "Turn on alerts" (not just "Allow")
  Secondary: "Skip for now" (never "Deny" — negative framing hurts opt-in)
```

### Badge Counts

```
iOS badge: Red circle with number on app icon.
  Use for: Unread count, actionable items pending
  Don't use for: Marketing, general "something changed" without clear value
  Clear the badge: As soon as user opens the relevant screen
  Zero badge: Remove the badge entirely (don't show a 0)

Tab bar badges (in-app):
  Same rules — only for actionable unread counts
  Dot badge (no number): Something new exists, count is irrelevant
  Number badge: Specific count matters (unread messages, pending approvals)
```

### Outputs
- Notification templates (title + body) for all notification types
- Pre-permission screen design
- Notification settings screen (granular controls per type)
- Badge logic specification

---

## 5. Onboarding

**Purpose:** Guide new users to the moment of value as quickly as possible — building understanding, trust, and habit without overwhelming or delaying.

**When to use:** Any first-time user experience; when users aren't activating after signup; when core features aren't being discovered.

### Onboarding Goals

```
Not: "Show the user every feature"
Yes: "Get the user to their first moment of value"

The moment of value (Nexus example):
  The instant the user sees their real portfolio value for the first time.
  Everything in onboarding exists to reach this moment, nothing else.
```

### Onboarding Types

**Welcome screens (splash/intro):**
```
3–5 screens that introduce the product before signup.
Use when: Value isn't self-evident from the product name/icon.
Don't use when: Users already understand what the app does (skip to signup).

Each screen:
  One idea (not a feature list)
  Supporting illustration or screenshot
  Progress indicator (dots)
  "Get started" CTA on last screen; "Skip" on all others

Content pattern:
  Screen 1: Problem ("Your crypto is scattered across 5 exchanges")
  Screen 2: Solution ("Nexus brings it all together in one view")
  Screen 3: Key differentiator ("Read-only access — we never touch your funds")
  Screen 4: CTA ("See your portfolio right now")
```

**Progressive onboarding (recommended):**
```
Pattern: Onboard within the actual app experience. No carousel before signup.
  - Empty states teach (not just show "No data yet")
  - Tooltips/callouts appear as features become relevant
  - Coach marks overlay on specific elements

Nexus example:
  1. User creates account → lands on empty portfolio screen
  2. Empty state: "Your portfolio starts here. Connect your first exchange."
     [Connect exchange] button is the only CTA
  3. User connects exchange → portfolio populates
  4. MOMENT OF VALUE: user sees their total value for the first time
  5. Spotlight / coach mark: "Tap any asset to see its breakdown"

Only show each callout once. Mark as seen. Never repeat.
```

**Checklist onboarding:**
```
A visible progress checklist that guides setup completion.
  Example:
    [✓] Create account
    [✓] Connect first exchange
    [ ] Connect second exchange (optional)
    [ ] Set a price alert

Show in: Empty state, onboarding card, or persistent banner until complete.
Dismiss: When user completes all required steps.
Progress: Percentage or completed/total count visible.
```

### Onboarding Design Principles

```
1. Never block value with a tutorial
   User came for the app, not the instructions.
   Let them in immediately, teach as they go.

2. Design for the amnesia case
   First-time users will forget your tutorial the moment they close it.
   Teach at the point of need (contextual), not in advance.

3. One thing at a time
   Each screen/callout/step covers ONE concept.
   The user who sees 8 things at once learns 0 of them.

4. Celebrate completion
   The moment of value is a milestone — mark it.
   Simple animation, congratulations message, genuine moment of delight.
   This creates the first emotional memory with the product.

5. Permission asks in context
   Push notification permission: after user sets their first price alert
     "Get notified when Bitcoin hits $120,000 — allow notifications?"
   Biometric permission: on first login after creating account
   Never: all permissions on first launch
```

### Onboarding Anti-patterns

```
❌ Feature tour with 8+ screens before the user sees anything real
❌ Mandatory account creation before the user sees any value (paywall at the door)
❌ Permission asks on launch (notifications, contacts, location — all at once)
❌ Tutorials that require the user to remember and perform steps correctly
❌ Progress blocked until a non-essential step is completed
❌ Onboarding that never ends (every session has a new tutorial)
```

### Outputs
- Onboarding flow (first session user flow diagram)
- Empty state designs for all onboarded screens
- Coach mark / callout component + trigger conditions
- Activation metric defined (the moment of value + how it's measured)

---

## 6. App Icon Design

**Purpose:** Create an icon that is instantly recognizable at all sizes, communicates the app's identity, and stands out on a device home screen.

**When to use:** Designing or redesigning an app icon; evaluating icon quality; preparing icon assets for App Store submission.

### App Icon Principles

```
1. Recognizable at 60×60pt (the actual home screen size)
   Most icons are designed at 1024px but displayed at 120–180px.
   If the concept isn't clear at 60×60, it doesn't work.

2. Single focal point
   One strong shape, not a collage of elements.
   The simpler, the more memorable.

3. No text
   At 60×60, text is illegible. The app name appears below the icon.
   Exception: Single-letter monogram if it's the brand's identity (Google apps).

4. No photo-realistic complexity
   Gradients and simple 3D = ok. Drop shadows and photographic realism = dated.

5. Distinctive silhouette
   Recognizable as a shape even at small sizes or in grayscale.
   Test: Does it look like itself at 20px?
```

### Icon Grid and Construction

```
Apple icon grid (1024×1024, squircle shape applied by iOS):
  Margins:  Roughly 100px on each side for safe zone
  Centered: Primary symbol should sit centered, vertically slightly above center
  Optical:  Visual center is slightly above mathematical center

The squircle:
  iOS clips all icons to a continuous curve (squircle) — not a rounded rectangle.
  Design on a square; Apple applies the mask.
  Don't add your own corner radius to the icon content (iOS does it).
  Exception: Android allows custom shapes (circle, rounded rect, teardrop, etc.)
```

### Icon Sizes Required

```
iOS:
  App Store:          1024×1024pt (required, no transparency)
  iPhone home (3×):    180×180px
  iPhone home (2×):    120×120px
  iPad home (2×):      152×152px
  Spotlight (3×):       87×87px
  Spotlight (2×):       58×58px
  Notification (3×):    60×60px
  Settings (2×/3×):   58/87×58/87px

Android:
  Play Store:         512×512px
  App icon:           192×192px (xxxhdpi)
  Adaptive icon:      108×108dp with 72×72dp safe zone

Generate all sizes from: 1024px master, using Xcode asset catalog or makeappicon.com.
```

### Color and Style Guidelines

```
Background color:
  Bright and saturated: stands out in dark mode and on varied wallpapers
  Very dark backgrounds: hard to see on dark home screens
  White backgrounds: blend with the dock/folder backgrounds
  Recommend: Use a solid brand color as background — reliable and distinctive

Icon style (current trends):
  Flat with subtle gradient: most apps (Gmail, Instagram, YouTube style)
  Glyph on color: clean, legible (Maps, Messages, native iOS apps)
  3D/skeuomorphic: can stand out but risks feeling dated
  Photography: rarely works at small sizes

Test on:
  Light wallpaper
  Dark wallpaper
  iOS dark mode (system icons change to lighter tones)
  In a folder (smaller, surrounded by other icons)
  As a notification icon (very small, grayscale)
```

### Icon Variants

```
Primary icon: Full color, production version.
Dark mode variant: iOS 18+ allows an alternate icon for dark mode.
  Background should be dark; glyph/symbol in lighter color.
  iOS automatically requests this variant.

Light/tinted variants (iOS 18+):
  Tinted: Monochrome version with system accent color applied.
  Light: Light background variant.
  Supply these for a polished, native-feeling experience.
```

### App Store Requirements

```
1024×1024px, PNG, sRGB color profile
No transparency (no alpha channel)
No rounding — Apple applies the squircle mask
No device frame, no screenshots, no text overlay
Must represent the app honestly (shows what the app does)
```

### Outputs
- Icon at 1024px (master)
- Xcode asset catalog with all sizes (or AppIcon.appiconset folder)
- Dark mode + tinted variants (iOS 18+)
- Icon test at 60px and in a simulated home screen grid

---

*See also: `references/emerging-specializations.md` for onboarding's relationship to inclusive design and ethical dark pattern avoidance.*
