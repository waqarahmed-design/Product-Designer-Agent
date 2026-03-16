# Design Tools

## Table of Contents
1. [Figma](#1-figma)
2. [Sketch](#2-sketch)
3. [Adobe XD](#3-adobe-xd)
4. [Framer](#4-framer)
5. [ProtoPie](#5-protopie)
6. [Principle](#6-principle)
7. [After Effects](#7-after-effects)
8. [Illustrator](#8-illustrator)
9. [Photoshop](#9-photoshop)

---

## 1. Figma

**Purpose:** Browser-based collaborative design and prototyping — the industry-standard tool for product design teams.

**When to use:** Primary design tool for UI/UX, design systems, prototyping, and developer handoff.

### Core Figma Concepts

```
Frames vs. Groups:
  Frame: A design container with independent layout, constraints, and clipping.
         Use for screens, components, and any container with layout rules.
  Group: A temporary collection of elements with no independent properties.
         Use only for grouping elements you want to move together.
  Rule: Default to Frame. Use Group only when you specifically don't want layout/constraints.

Auto Layout:
  Figma's CSS Flexbox equivalent. Enables responsive, resizing components.
  Properties: direction (row/column), gap, padding, alignment, wrapping
  Key settings:
    Hug contents: frame shrinks to fit its children
    Fill container: frame expands to fill parent
    Fixed: explicit width/height (use sparingly)
  Always use Auto Layout for components — enables responsive resizing.

Constraints:
  Define how an element moves/resizes when its parent frame resizes.
  Horizontal: Left, Right, Left & Right (stretch), Center, Scale
  Vertical: Top, Bottom, Top & Bottom, Center, Scale
  Use "Left & Right" for full-width elements; "Center" for centered content.
```

### Component System

```
Main component: The single source of truth. Edit here → all instances update.
Instance: A copy of a main component. Overrides allowed (text, icons, colors).
Component set: Multiple variants of one component in a single frame.

Naming convention:
  Component/Variant/State
  e.g.: Button/Primary/Default, Button/Primary/Hover, Button/Ghost/Disabled

Component properties (Figma's native system):
  Boolean: show/hide layers (e.g., icon visibility)
  Text: override text content
  Instance swap: swap nested components
  Variant: switch between variants in the set

Expose only what needs to change. Hide internal construction.
```

### Variables and Design Tokens

```
Collections: Group of related variables (Colors, Spacing, Typography)
Modes: Variants of a collection (Light mode / Dark mode)

Primitive variables:
  color/blue/500 = #3B82F6

Semantic variables (reference primitives):
  color/background/primary = {color/blue/500}

Assign to:
  Fill, stroke, corner radius, padding, gap, width, height, opacity

Variable modes enable one-click theme switching.
Design system tokens → Figma variables → developer variables (same names).
```

### Prototyping in Figma

```
Connection types:
  Navigate to: Go to a frame (page navigation)
  Open overlay: Overlay a frame on top (modals, menus)
  Scroll to: Scroll to position within frame
  Back: Return to previous frame

Smart animate: Automatically interpolates between matching layers.
  Layers must have the same name to be matched.
  Works for: position, size, opacity, rotation, corner radius, fill.

Interaction types: On click, On hover, On drag, On key press, On component event
Animations: Instant, Dissolve, Smart animate, Slide in/out, Push, Move in/out
```

### Developer Handoff

```
Inspect panel:
  Exact CSS values for every property
  Copy CSS for selected element
  Export assets (SVG, PNG at 1x/2x/3x)

Code mode (Dev Mode):
  Toggle Dev Mode for developers — restricted to inspect only
  Links from design to code via Code Connect

Annotations:
  Add annotations explaining intent (not just what, but why)
  Document: interaction states, responsive behavior, edge cases
```

### Figma Plugins (Essential)

| Plugin | Use |
|--------|-----|
| Tokens Studio | Design token management + export to code |
| Iconify | Access any icon library |
| Unsplash | Stock photos in mockups |
| Stark | Accessibility contrast checker |
| Design Lint | Find inconsistent styles and detached components |
| Figma to React | Export components to React code |
| Super Tidy | Auto-organize layers and frames |

### Outputs
- Organized component library with Auto Layout
- Variable collections for all design tokens
- Prototype with Smart Animate for key flows
- Dev Mode annotations for handoff

---

## 2. Sketch

**Purpose:** Mac-native vector design tool — historically the industry standard before Figma, still widely used in some teams.

**When to use:** When the team uses Sketch; when working on Mac-only workflows with Sketch-native libraries.

### Sketch vs. Figma Key Differences

| Feature | Sketch | Figma |
|---------|--------|-------|
| Platform | Mac only | Browser + desktop |
| Collaboration | Via Abstract or Sketch for Teams | Real-time built-in |
| Prototyping | Basic | More advanced |
| Variables | Libraries + styles (no native variables) | Native variables + modes |
| Plugins | Large ecosystem | Growing ecosystem |
| File format | `.sketch` (binary) | Cloud-based |
| Price | One-time + updates | Subscription |

### Core Sketch Concepts

```
Artboards: Equivalent to Figma Frames. Define screen canvases.
Groups: Primary organization unit (unlike Figma, used more heavily).
Symbols: Equivalent to Figma Components.
  Master Symbol: Like a Figma main component.
  Symbol Instance: Like a Figma instance.
  Overrides: Text, image, nested symbol swaps.

Shared Styles:
  Text Styles: Reusable typography definitions
  Layer Styles: Reusable fill/border/shadow combinations
  These are like Figma Styles (not variables — no theming/modes).
```

### Libraries

```
Sketch Libraries: Shared Sketch files that serve as component sources.
  Link a library: Sketch → Preferences → Libraries → Add Library…
  Components in linked libraries appear in the Insert menu.
  Updates: Sketch notifies when the library has changed → accept update.

Team Libraries (Sketch for Teams):
  Hosted in Sketch Cloud, synced across the team.
  Equivalent to Figma's shared library / Team Library.
```

### Prototyping in Sketch

```
Basic prototyping: Click hotspot → connect to artboard → define transition.
Advanced prototyping: Use ProtoPie or Framer for complex interactions.

Transitions: Dissolve, Move In/Out, Slide In/Out, Push
Duration: 100–500ms
No Smart Animate equivalent — use Principle or Framer for animated transitions.
```

### Plugins for Sketch

| Plugin | Use |
|--------|-----|
| Abstract | Version control for Sketch files |
| Zeplin | Developer handoff (inspect + assets) |
| Avocode | Alternative handoff tool |
| Runner | Quick search and command palette |
| Sketch Measure | Add measurement annotations |
| SVGO Compressor | Optimize SVG exports |

### Outputs
- Symbol library with master components
- Shared Text Styles and Layer Styles
- Artboard-based prototype with transitions
- Zeplin or Abstract integration for handoff

---

## 3. Adobe XD

**Purpose:** Adobe's design and prototyping tool, integrated with the Creative Cloud ecosystem.

**When to use:** When team is invested in Adobe CC; when workflows involve heavy use of Photoshop/Illustrator assets; when client requires Adobe deliverables.

### XD vs. Figma

| Feature | Adobe XD | Figma |
|---------|----------|-------|
| CC integration | Deep (Assets, fonts, stock) | Plugin-based |
| Prototyping | Good | Better |
| Collaboration | Adobe Share | Real-time built-in |
| Price | CC subscription | Freemium |
| Performance | Desktop app | Browser + desktop |

### Core XD Concepts

```
Artboards: Equivalent to Figma Frames — design canvases.
Components: Reusable elements with states (equivalent to Figma components).
  States: Default, Hover, Active, Disabled (up to 5 custom states)
  State transitions play in prototype mode.

Assets Panel:
  Colors, Character Styles, Components — shared across the document.

Repeat Grid: Select an item → drag to repeat it in a grid.
  Auto-fills with placeholder content.
  Drag different images onto each slot — auto-distributes.
  Useful for rapidly creating list mockups.
```

### XD Prototyping

```
Auto-Animate: Like Figma's Smart Animate — interpolates matching layers between artboards.
Named matches: Layers with the same name animate between states.

Prototype triggers: Tap, Drag, Time, Voice, Keyboard, Gamepad
Actions: Transition, Auto-Animate, Overlay, Speech Playback, Previous artboard

Scroll groups: Define scrollable areas within an artboard (sticky headers, lists).

Sharing: Share link → stakeholders view in browser or XD iOS/Android app.
```

### Creative Cloud Integration

```
Libraries:
  Colors, type styles, and components sync to Adobe Libraries.
  Accessible across Photoshop, Illustrator, and InDesign.

Stock integration: Search Adobe Stock directly in the assets panel.
Fonts: Full Adobe Fonts (Typekit) library available instantly.
Assets: Paste vectors from Illustrator, raster from Photoshop — fidelity preserved.
```

### Outputs
- Artboard-based design file with components
- Auto-Animate prototype for key flows
- Shared library integrated with CC ecosystem
- Spec export via XD Share or Zeplin

---

## 4. Framer

**Purpose:** Code-based design and prototyping tool that bridges design and production React code — enabling high-fidelity, interactive prototypes and published websites.

**When to use:** When prototypes need real interactions impossible in Figma; when building interactive marketing sites; when exploring complex animation; when the team is React-capable.

### Framer Modes

```
Design mode: Visual canvas (like Figma) with drag-and-drop layout.
Code mode: Write React components and override visual layers with code.
Preview: Real-time preview as you design — runs actual React in the browser.
Publish: Deploy directly to Framer hosting as a live website.
```

### Framer Components

```
Two types:
  Design components: Created visually, like Figma components.
  Code components: React components (.tsx files) with full access to hooks, state, APIs.

Code component example:
  export default function Counter() {
    const [count, setCount] = useState(0);
    return (
      <button onClick={() => setCount(c => c + 1)}>
        Count: {count}
      </button>
    );
  }

Code components appear in the asset panel like design components.
Any visual property can be exposed as a Framer property (like Figma component properties).
```

### Framer Motion

```
Framer uses its own Framer Motion library for animations.

<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  exit={{ opacity: 0, y: -20 }}
  transition={{ duration: 0.3, ease: 'easeOut' }}
/>

Built-in animation tools:
  Transition effects on frame connections: Smart, Dissolve, Push, Slide
  Scroll-linked animations: element properties driven by scroll position
  Variants: named animation states that transition automatically
```

### When to Use Framer vs. Figma

```
Use Figma for:
  Design system work, component libraries, design handoff
  Anything that produces specs for engineers

Use Framer for:
  High-fidelity interactive prototypes (realistic scrolling, real data)
  Marketing/landing pages that need complex scroll animations
  Testing interaction patterns before engineering
  Demos and presentations that need to feel real
```

### Outputs
- Interactive prototype running real React
- Scroll-animated marketing page
- Code components with exposed properties
- Published URL for stakeholder review

---

## 5. ProtoPie

**Purpose:** Advanced interaction prototyping tool that handles complex logic, conditions, variables, and sensor inputs — without writing code.

**When to use:** When Figma prototyping hits its limits; complex conditional interactions; multi-step interactions with state; testing interactions that involve device sensors (gyroscope, touch pressure).

### ProtoPie vs. Figma Prototyping

| Feature | Figma | ProtoPie |
|---------|-------|----------|
| Triggers | Click, hover, drag | All of the above + scroll, sensor, voice, gamepad |
| Conditions | None | Full if/else logic |
| Variables | None | Yes — store and use values |
| Formulas | None | Math expressions, string ops |
| Components | Static | Stateful (remember their state) |
| Import from | — | Figma (paste layers) |

### ProtoPie Concepts

```
Scene: Equivalent to a screen/artboard — one prototype state.
Layer: Any imported design element or shape.
Trigger: What initiates an interaction.
  - Tap, Drag, Scroll, Swipe
  - Time (auto-play), Load (on scene appear)
  - Sensor: Gyroscope, Accelerometer, Touch pressure, Mic, Camera
  - Message: Cross-prototype or Studio ↔ App communication

Response: What happens when triggered.
  - Move, Scale, Rotate, Opacity, Color, Text change
  - Go to scene (navigation)
  - Play sound, Haptic feedback
  - Send message (to another component or prototype)

Variables: Store values during interaction.
  var counter = 0
  Increment on tap, display in text layer.

Conditions: Branch logic.
  IF counter > 5 THEN go to scene "Limit Reached"
  ELSE increment counter
```

### ProtoPie Use Cases

```
1. Complex form validation
   Show/hide error messages based on input content.
   Enable submit button only when all fields are valid.

2. Swipe-based interactions
   Tinder-style card swipe with direction detection.
   Swipe threshold → trigger action.

3. Scroll-based animation
   Sticky header, parallax, element reveals at scroll depth.

4. Sensor-driven (device demos):
   Tilt device → content shifts (gyroscope)
   Shake device → refresh (accelerometer)
   Press harder → more action (pressure, iPad only)

5. Multi-screen state persistence:
   Cart count increments across screens.
   Form data persists between steps.
```

### Figma → ProtoPie Workflow

```
1. Design in Figma (all visual work stays in Figma)
2. Export/paste to ProtoPie (Figma plugin: ProtoPie Connect)
3. Add interactions in ProtoPie (all logic lives in ProtoPie)
4. Test on device (ProtoPie app for iOS/Android)
5. Share link for review

Never recreate visuals in ProtoPie — always import from Figma.
```

### Outputs
- Interactive prototype with conditional logic
- Device-ready test build (ProtoPie app)
- Share link for usability testing
- Interaction spec exported as documentation

---

## 6. Principle

**Purpose:** Mac animation and interaction design tool optimized for creating high-quality, timeline-based animations and micro-interactions.

**When to use:** When animating specific UI transitions with precision timeline control; creating demos of animated interactions; when After Effects is too heavy for simple UI animations.

### Principle vs. After Effects vs. Figma

| Tool | Best for | Control level |
|------|----------|--------------|
| Figma Smart Animate | Quick interaction demos | Low (auto-interpolates) |
| Principle | UI animation demos, timing control | Medium |
| After Effects | Complex motion graphics, Lottie output | High |

### Principle Concepts

```
Artboards: Design canvases — imported from Sketch or created in Principle.
  Principle imports Sketch files natively (not Figma directly).
  Figma → Sketch export → Principle (workflow workaround).

Drivers: Animation triggered by gesture or scroll.
  Drag driver: element position drives animation values.
    Move finger → other elements animate proportionally.
    Useful for: swipe interactions, pull effects, scroll-linked animations.

Timeline: Keyframe-based animation for transitions between artboards.
  Drag: Set timing and easing for each animated property.
  Curve editor: Adjust bezier easing with visual control.

Layer animation:
  Position, scale, rotation, opacity, corner radius, blur, color
  Clip layers: Mask content during animation (animating reveal)
```

### Principle Workflow

```
1. Design in Figma or Sketch (visual design)
2. Export to Principle (via Sketch native import)
3. Set up artboard connections (navigation)
4. Add timeline animations for transitions
5. Add drivers for gesture-based animations
6. Export as video (for presentations) or run on device (Principle Mirror app)
```

### Use Cases

```
1. Animated tab bar switch: Precise timing of sliding indicator + label color change
2. Card flip animation: 3D perspective rotation, timeline-controlled
3. Scroll-linked header: Header shrinks/changes as user scrolls (drag driver)
4. Pull-to-refresh: Rubber band pull → spinner → content reveal
5. Onboarding swipe sequence: Slide + parallax with exact spring tuning

Principle excels at the last 10% of motion polish —
when Figma Smart Animate isn't precise enough.
```

### Outputs
- Animated prototype running on device (Principle Mirror)
- Video export for presentations and stakeholder review
- Documented timing specs (duration, easing) for engineering handoff

---

## 7. After Effects

**Purpose:** Industry-standard motion graphics and animation tool — the source for Lottie animations, complex illustrated motion, and video-based design work.

**When to use:** Creating Lottie animations for app use; animated brand assets; motion graphics for marketing; any animation too complex for CSS or Framer Motion.

### After Effects in a Design Workflow

```
Primary design role: Authoring animations that become Lottie files.
  Lottie: Vector animation format that runs natively in web/mobile apps.
  Bodymovin plugin: Exports After Effects compositions as Lottie JSON.

Secondary role: Creating video assets, animated mockups, presentation videos.
```

### After Effects Core Concepts

```
Composition: The animation canvas — has its own dimensions and duration.
Layers: Elements in the composition (shape, text, image, null, camera).
  Keyframe: A value at a specific time.
  Between keyframes: After Effects interpolates the value.

Properties:
  Transform: Position, Scale, Rotation, Opacity, Anchor Point
  Shape layers: Paths, fills, strokes, trim paths (for draw-on effects)
  Text: Source text, path following, per-character animation

Parenting: Child layer inherits parent's transform.
  Null object: Invisible layer used as a parent/controller.

Expressions: JavaScript-based automation for properties.
  Common expressions:
    wiggle(2, 10)          // random wiggle, 2 times/sec, 10px range
    loopOut('cycle')       // loop animation continuously
    time * 100             // property increases linearly with time
```

### Lottie-Friendly After Effects

```
For Lottie output, use only:
  ✅ Shape layers (rectangles, ellipses, paths, polygons)
  ✅ Text layers (with specific fonts installed)
  ✅ Masks and mattes
  ✅ Transform keyframes on any layer
  ✅ Trim paths (for draw-on line animations)
  ✅ Color fills and strokes on shape layers

Avoid (not supported in Lottie):
  ❌ Rasterized images (PSD, PNG inside the comp)
  ❌ Layer effects (drop shadow, glow) — use shape layers instead
  ❌ 3D layers (basic 3D is ok, complex camera not)
  ❌ Expressions that are too complex (some are supported, test first)
  ❌ Plugins that render effects (Element 3D, Video Copilot, etc.)

Export:
  Window → Extensions → Bodymovin → Export (.json)
  Test in LottieFiles.com previewer before shipping
  Check file size: aim for < 100KB
```

### Key Techniques for UI Animation

```
Draw-on line effect (Trim Paths):
  1. Create a shape layer with a path (or stroke)
  2. Add Contents → Trim Paths
  3. Animate Start or End from 0% to 100%
  → Creates a line that draws itself

Morph between shapes:
  1. Create two paths in the same shape layer (as separate Path keyframes)
  2. Animate Path property between keyframe 1 and keyframe 2
  → Shape morphs from one form to another

Stagger animation (using expressions):
  Apply to Position/Opacity start time of each layer:
    delay = index * 0.05;   // 50ms stagger between layers
    Creates cascading entrance animation

Bounce easing (without plugins):
  Use graph editor to pull out overshoot on last keyframe.
  Or use spring expression:
    amp = 0.08; freq = 3; decay = 4;
    n = 0; if (numKeys > 0){ n = nearestKey(time).index; if (key(n).time > time){ n--; }}
    if (n == 0){ t = 0; } else { t = time - key(n).time; }
    if (n > 0 && t < 1){ v = velocityAtTime(key(n).time - thisComp.frameDuration/10);
    value + v*amp*Math.sin(freq*t*2*Math.PI)/Math.exp(decay*t) } else { value }
```

### Outputs
- Lottie JSON file (via Bodymovin export)
- Video preview (MP4) for presentation
- Animation specs (timing, easing) extracted for engineering reference

---

## 8. Illustrator

**Purpose:** Vector illustration and icon creation — the professional standard for producing scalable assets, icon sets, and complex illustrations.

**When to use:** Creating custom icons, illustrations, logo work, or any vector asset that needs to be scalable and production-ready.

### Illustrator in a Design Workflow

```
Primary use in product design:
  1. Custom icon creation (not from a library)
  2. Logo and brand mark design
  3. Complex illustrations (onboarding, empty states, marketing)
  4. SVG asset preparation for export to Figma or code

Workflow:
  Illustrator (create) → Figma (layout and prototype) → Code (SVG export)
```

### Core Illustrator Concepts

```
Artboards: Multiple canvases in one document.
  Tip: Create one artboard per icon or illustration. Name them correctly — the filename on export.

Vector paths:
  Anchor points + handles define curves.
  Pen tool (P): Draw precise paths.
  Bezier handles: Drag to control curve shape.
  Direct Selection (A): Edit individual anchor points.

Boolean operations (Pathfinder):
  Unite: Merge overlapping shapes into one
  Minus Front: Subtract top shape from bottom
  Intersect: Keep only overlapping area
  Divide: Split into separate pieces where shapes overlap

Shape Builder (Shift+M): Interactive Boolean — drag across shapes to unite, click gaps to fill.
```

### Icon Design in Illustrator

```
Set up icon grid:
  Create artboard: 24×24px (standard icon size)
  Enable pixel grid: View → Pixel Preview
  Align to pixel grid: Transform panel → Align to pixel grid ON

Design rules for icons:
  Stroke weight: 1.5–2px on a 24px grid (consistent throughout the set)
  Corner radius: Consistent (0px for sharp geometric, 2px for rounded)
  Optical sizing: Use optical corrections, not just mathematical centering
  Export: SVG (not PNG) for maximum scalability

Export SVG for web:
  File → Export → Export As → SVG
  Settings: Presentation attributes, SVG 1.1, Embed fonts (or convert to outlines)
  Simplify paths before export (less code = faster rendering)

Optimize SVG output:
  Remove unnecessary groups: Object → Ungroup
  Expand all strokes to fills before export (optional, for consistent rendering)
  Run through SVGO (svgo.dev) to remove metadata and optimize
```

### Illustration for Product Design

```
Consistency rules for illustration sets:
  Same color palette (pull from brand tokens)
  Same stroke weight throughout
  Same level of detail (all simple, or all complex — never mixed)
  Same perspective style (flat, isometric, 2.5D)

Exporting illustrations to Figma:
  Copy → Paste into Figma (SVG preserved)
  Or: Export SVG → drag into Figma
  Check: does Figma show the illustration correctly in all views?
```

### Outputs
- Production-ready SVG icon files (optimized)
- Icon set on a consistent grid
- Illustration assets for Figma import
- Logo variations in all required formats (SVG, PNG, AI)

---

## 9. Photoshop

**Purpose:** Raster image editing — for photo manipulation, UI mockup compositing, texture creation, and preparing photographic assets for use in designs.

**When to use:** Processing photos for use in mockups; creating realistic UI mockups with device frames; retouching product imagery; creating texture assets; editing screenshots.

### Photoshop in a Design Workflow

```
Where Photoshop belongs in modern product design:
  - Photo editing and retouching (not icon creation — use Illustrator)
  - Creating mockup compositions (phone/device in context)
  - Generating texture/noise layers for UI backgrounds
  - Preparing app store screenshots with device frames + backgrounds

Where Photoshop does NOT belong:
  - UI design (use Figma — Photoshop's pixel-based workflow creates non-scalable assets)
  - Icon design (use Illustrator — vectors only)
  - Prototyping (use Figma/Framer)
```

### Key Photoshop Techniques for Designers

```
Smart Objects:
  Non-destructive layer that preserves original quality.
  Double-click to edit in a separate tab. Save → updates in parent.
  Use for: Placing phone screens in device mockups (double-click → edit your design → save)

Device mockups:
  Download PSD mockup → open → find Smart Object layer → double-click
  → paste your design → save → returns to mockup with your design inside
  Most mockup templates use this Smart Object workflow.

Layer masks:
  Non-destructive way to hide parts of a layer.
  Black on mask = hidden; White = visible.
  Paint with brush to reveal or conceal areas.
  Use for: Blending photos, creating composite effects.

Adjustment layers:
  Non-destructive color and tone corrections applied above layers.
  Hue/Saturation: Change photo colors to match brand palette.
  Levels/Curves: Adjust brightness and contrast.
  Gradient Map: Apply a gradient over a photo (brand color overlays).

Blend modes:
  Multiply: Darkens (good for overlaying text on photos)
  Screen: Lightens (good for adding light effects)
  Overlay: Contrast boost (good for texture overlays)
  Soft Light: Subtle contrast (good for color grading)
```

### Exporting from Photoshop

```
Export for web:
  File → Export → Export As (not "Save for Web" — that's legacy)
  PNG: For assets with transparency
  JPEG: For photos (80% quality is usually sufficient)
  WebP: For web use where browser support is confirmed

Exporting app store screenshots:
  File → Export → Artboards to Files
  Resolution: 72 DPI for screen; 300 DPI only for print
  Size: Match App Store requirements (see App Store guidelines)

Smart Object assets:
  Right-click Smart Object → Export Contents → gets the original file
```

### Outputs
- Processed photo assets ready for Figma import
- Device mockup compositions with design screens applied
- App Store screenshot compositions
- Brand-colored photo overlays and textures
