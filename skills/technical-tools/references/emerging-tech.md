# Emerging Technologies

## Table of Contents
1. [AR/VR Design](#1-arvr-design)
2. [Voice Interface Design](#2-voice-interface-design)
3. [AI/ML Integration](#3-aiml-integration)
4. [Gesture Control](#4-gesture-control)

---

## 1. AR/VR Design

**Purpose:** Design spatial experiences for augmented reality (AR) — digital content overlaid on the physical world — and virtual reality (VR) — fully immersive digital environments.

**When to use:** Designing for Apple Vision Pro, Meta Quest, ARKit (iOS), ARCore (Android), WebXR, or any experience where digital and physical space merge.

### AR vs. VR vs. MR

```
Augmented Reality (AR):
  Digital content overlaid on the real world.
  User sees both physical and digital elements.
  Devices: iPhone/iPad (ARKit), Android (ARCore), AR glasses (HoloLens, Magic Leap)
  Examples: IKEA Place (furniture in room), Snapchat filters, navigation overlays

Virtual Reality (VR):
  Fully immersive digital environment — physical world not visible.
  Devices: Meta Quest, PlayStation VR, Valve Index
  Examples: Games, training simulations, virtual tours

Mixed Reality (MR):
  Digital content that understands and interacts with physical geometry.
  Holograms land on real surfaces, react to real objects.
  Devices: Apple Vision Pro, HoloLens
  Examples: visionOS apps, spatial computing experiences

Spatial Computing (Apple term):
  Apple's framing for Vision Pro — apps float in space, interact with surroundings.
```

### Spatial Design Principles

**1. Depth and distance replace flat screens**
```
Everything exists at a distance from the viewer.
Near zone:   0–0.5m — hands, close manipulation
Middle zone: 0.5–3m — primary content, main UI
Far zone:    3m+     — environmental elements, backgrounds

Rule: Primary content should exist in the middle zone (0.5–3m).
Don't place critical content too close (uncomfortable to focus) or too far (hard to read).
```

**2. Scale in context**
```
UI elements must be sized for their intended viewing distance.
A "small" element at 1m vs. 3m requires different absolute sizes.

Guidance: Design in meters, not pixels.
A comfortable button at arm's length: ~4–6cm apparent height.
Text minimum at 2m: ~3cm apparent height.
```

**3. Comfort zones (ergonomics)**
```
Field of view: Humans comfortably see ~60° cone without head movement.
  Primary content: within ±30° of forward gaze (60° total cone)
  Peripheral information: up to ±50° (used for secondary content)
  Never require head movement > 90° — uncomfortable for extended use

Head height: Center primary UI at eye level or slightly below.
  Looking up for extended periods = neck fatigue.
  Menus and controls placed below eye level feel more natural.

Motion sickness prevention:
  Never move the world — move objects within it.
  If the environment moves, it must match real locomotion (or use teleportation).
  UI elements should feel "pinned to space" — they don't float erratically.
```

### visionOS Design (Apple Vision Pro)

```
Windows: Spatial panels that float in the user's space.
  Standard window: Similar to iPad UI, adapted for spatial input.
  Ornaments: UI attached to windows (like toolbars or related controls).

Input modalities:
  Eye tracking + pinch: Primary input. User looks at something → pinches to select.
  Hand gestures: Direct manipulation of nearby virtual objects.
  Voice: For text input and some commands.
  Indirect scroll: Look at scrollable area → flick gesture from any position.

Design rules for visionOS:
  Glass materials: Use translucent glass backgrounds — they blend with any room.
  No opaque dark backgrounds: They look like a black hole floating in the room.
  Hover state: Elements glow when looked at — must be tested.
  Depth layers: Background (room), base, content, overlay.
  Typography: Minimum 22pt for secondary text; 17pt absolute minimum.

Spatial audio:
  Sound emanates from its source location in 3D space.
  Design audio feedback to match visual position of its source.
```

### AR Mobile Design (ARKit / ARCore)

```
AR overlays on camera feed:
  Content placed on detected surfaces (planes, faces, images)
  User interacts via touch on the camera viewport

Design considerations:
  Contrast: Your UI must be legible over any background (light room, dark room)
    Use shadow/glow behind text for readability over any environment.
  Stability: AR elements that jitter/drift = nausea. Indicate when tracking is lost.
  Ground truth: Show clear indicators of WHERE things are placed.
  Distance: UI elements far away appear smaller — scale with distance or use fixed UI.

AR UI patterns:
  World-locked: Fixed in physical space (a label on a real object)
  Camera-locked: Moves with camera (HUD, controls overlaid on camera feed)
  Hybrid: Controls camera-locked; content world-locked

Onboarding in AR:
  Show the real world first → then introduce UI overlays
  Teach the placement gesture with clear visual cues
  Don't start with content already placed — let user discover
```

### Outputs
- Spatial UI layout with depth zones defined
- Comfort zone analysis (field of view, head movement required)
- Platform-specific specs (visionOS window sizes, AR surface detection states)
- Fallback design for non-spatial platforms

---

## 2. Voice Interface Design

**Purpose:** Design conversational interactions where voice is the primary or supplementary input — ensuring the interface is responsive, forgiving, and clearly communicates its capabilities.

**When to use:** Designing voice assistants, smart speaker apps, in-car interfaces, accessibility-first flows, or any interface supplemented with voice commands.

### Voice vs. Screen Interfaces

| Dimension | Screen UI | Voice UI |
|-----------|-----------|----------|
| Navigation | Visual hierarchy | Conversational flow |
| Discovery | Visible options | Must know what to say |
| Error recovery | Back button, visual feedback | Prompt rephrasing |
| Speed | Depends on reading/tapping | Faster for simple commands, slower for complex |
| Context | Persistent (visible) | Transient (remembered only if designed) |
| Attention | Can multi-task | Requires audio focus |

### Voice Interface Design Principles

**1. Make capabilities discoverable**
```
Users don't know what they can say. The system must teach them.
Patterns:
  Onboarding: "You can say things like 'Show my Bitcoin balance' or 'Connect exchange'"
  Help command: "What can I say?" → list of key commands
  Contextual hints: After each response, suggest the next possible command
  No surprises: Never let users hit "I don't understand" for a reasonable request
```

**2. Confirm, don't just execute**
```
For irreversible or significant actions, confirm before executing:
  User: "Delete my Binance exchange"
  System: "Are you sure you want to remove Binance? Say 'Yes, delete it' to confirm."

For reversible actions, execute immediately and offer undo:
  User: "Refresh my portfolio"
  System: [executes] "Portfolio updated. Say 'undo' to revert."
```

**3. Handle errors gracefully**
```
Error types:
  Not understood: "Sorry, I didn't catch that. Try saying 'show balance' or 'refresh'."
  Out of scope: "I can't do that yet. I can show your portfolio, check prices, or connect exchanges."
  Partial understanding: "Did you mean 'show Bitcoin balance'? Say yes or try again."

Error recovery rules:
  Never just say "Error" — always explain what happened and what to try
  Offer alternatives, not dead ends
  After 2 failed attempts: offer the most relevant commands explicitly
  Limit reprompt attempts to 2 before gracefully exiting the flow
```

**4. Design for conversation, not commands**
```
Bad: System only understands exact commands
  ✅: "check bitcoin price"
  ❌: "what's bitcoin at?" (fails — not the exact phrase)

Good: System understands natural language intent
  ✅: "check bitcoin price"
  ✅: "what's bitcoin at?"
  ✅: "how much is BTC worth right now?"
  All map to the same intent: GET_ASSET_PRICE(asset=BTC)
```

### Voice UI Components

**Utterance:** What the user says.
**Intent:** What the user means (mapped from utterance to action).
**Slot:** A variable extracted from an utterance.
  "Show me [BTC] balance" — BTC is a slot for asset.

**Conversation flow notation:**
```
User: "How much is Ethereum worth?"
  → Intent: GET_ASSET_PRICE
  → Slot: asset = "Ethereum"

System: "Ethereum is currently $3,421.18, up 2.4% today."
  → Offer follow-up: "Want to see your ETH holdings?"

User: "Yes"
  → Context: previous intent was about ETH
  → System: "You hold 0.54 ETH worth $1,847.44 across 2 exchanges."
```

### Visual Feedback for Voice

```
Visual indicators that voice is active/listening:
  Listening: Animated waveform or pulsing orb
  Processing: Loading indicator
  Speaking: Different animation (e.g., waveform when system speaks)
  Error: Brief red flash + error message on screen

Always show:
  Current transcript (what the system heard) — confirms understanding
  Response text (what the system said) — for users in noisy environments
  Key information (numbers, names) displayed on screen alongside audio
```

### Outputs
- Conversation flow diagrams (happy path + error paths)
- Intent map (utterances → intents → slots)
- Sample dialogue scripts for key interactions
- Visual feedback states for voice input lifecycle

---

## 3. AI/ML Integration

**Purpose:** Design interfaces that incorporate AI/ML features — managing user expectations, communicating uncertainty, and building trust when system behavior is probabilistic rather than deterministic.

**When to use:** Adding AI-powered features (recommendations, predictions, auto-fill, generation); designing for AI outputs (summaries, classifications, generated content).

### Core Challenges of AI UX

```
1. Unpredictability: AI outputs vary — no two interactions are identical.
   Design: Communicate that results may vary; provide ways to retry or adjust.

2. Uncertainty: AI is sometimes wrong.
   Design: Show confidence levels; never imply certainty the model doesn't have.

3. Opacity: Users don't know why the AI made a decision.
   Design: Provide explanations, evidence, and "why this?" pathways.

4. Trust calibration: Users who trust AI too much get burned by errors;
   users who trust too little don't benefit.
   Design: Right-size trust signals to actual accuracy.

5. Control: Users need to feel in control of AI-augmented actions.
   Design: Humans approve; AI suggests. Never automate irreversible actions.
```

### AI Feature Design Patterns

**Suggestion over automation:**
```
AI suggests → human decides → human executes.
Only automate when:
  - The action is easily reversible (auto-categorize → can re-categorize)
  - The accuracy is very high (> 95% confident)
  - The consequence of error is low (sorting a list vs. sending a payment)

Examples:
  AI suggests: "This looks like an ETH transaction. Tag it as Transfer?"
  Human confirms: [Confirm] [Change tag]

  Never: "AI automatically tagged all transactions" (no review possible)
```

**Confidence visualization:**
```
Show when the AI is uncertain:
  High confidence: Show result directly
  Medium confidence: Show result + "AI is less certain about this"
  Low confidence: Show options + "AI found multiple possibilities"

Visual patterns:
  Dotted border: "AI-generated content"
  Confidence badge: "85% match"
  Star rating: ★★★★☆ confidence
  Color coding: Green (high) → Yellow (medium) → Red (low)
```

**Explainability:**
```
"Why did the AI say this?" must be answerable.
Minimum: "Based on [evidence]" next to AI outputs.

Examples:
  "SOL dominates your gains this week" → "Based on: SOL +18.2% vs. portfolio +8.5%"
  "High concentration risk detected" → "Based on: BTC = 57% of portfolio"
  "Recommended: Diversify" → "Based on: Sharpe ratio below benchmark average"

Progressive disclosure:
  Surface: Summary statement
  Expand: Evidence list
  Deep: Methodology explanation (for power users)
```

**Feedback loops:**
```
Let users correct the AI — this improves the model AND builds trust.

Patterns:
  Thumbs up/down: Quick signal on AI output quality
  "Not this" button: Reject specific suggestion, get alternative
  "Why?" button: Reveal reasoning
  Edit mode: User refines AI output directly (acceptance = positive signal)

The correction IS the UI — it's not an afterthought.
```

### AI Loading States

```
AI operations are slower than regular data fetches.
Typical AI response: 1–5 seconds.

Design for AI latency:
  < 500ms: Standard spinner
  500ms–2s: Spinner + "Analyzing your portfolio…" (contextual message)
  2s+: Progressive reveal — show partial results as they arrive

For generative AI (text streaming):
  Show text as it appears character by character (streaming)
  This is faster than waiting for full response — even if total time is the same
  The perceived wait is much shorter with streaming

Streaming pattern:
  Cursor blinking → text appears word by word → cursor disappears = complete
```

### Designing AI Feature Boundaries

```
Clearly define and communicate what AI can and cannot do:

Can do:
  Summarize data from connected exchanges
  Identify patterns in portfolio history
  Suggest diversification based on holdings
  Explain market moves in plain language

Cannot do:
  Predict prices (no model can)
  Guarantee recommendations
  Access data beyond what's connected
  Know about events after [training cutoff]

Surface this in UI:
  Onboarding: "AI Insights uses your portfolio data to surface observations."
  Disclaimer near AI outputs: "Insights are based on your data, not financial advice."
  Error state when data is insufficient: "Connect more exchanges for better insights."
```

### Outputs
- AI feature interaction flow (suggestion → review → accept/reject)
- Confidence visualization system
- AI loading and streaming states
- Explainability component design
- AI capabilities/limitations documentation

---

## 4. Gesture Control

**Purpose:** Design touch-less or reduced-touch interactions driven by hand gestures, body motion, or device movement — for interfaces beyond the screen tap.

**When to use:** Designing for Apple Vision Pro, AR interfaces, in-car systems, accessibility-first flows, game controllers, smart TVs, or any input beyond touch and keyboard.

### Gesture Input Types

```
Hand gestures (vision-based):
  Pinch: Primary select/confirm (Vision Pro)
  Point: Hover/aim (Vision Pro — gaze + point)
  Palm facing camera: Stop/cancel
  Swipe: Navigate
  Pinch and drag: Move/resize spatial objects

Device motion (accelerometer/gyroscope):
  Tilt: Scroll, pan, steering (games, AR, in-car)
  Shake: Undo, refresh (iOS convention)
  Rotation: Change orientation, control values

Remote control (TV, Apple TV):
  D-pad: Navigate grid
  Click: Select
  Swipe on touchpad: Scroll
  Swipe off-screen: Back
  Long press: Options

Controller (game, accessibility):
  Buttons: Actions
  Thumbstick: Navigate, pan, rotate
  Triggers: Variable input (pressure-sensitive)
  Haptic feedback: Confirmation
```

### Gestural Interface Principles

**1. Affordance without touch**
```
Without physical buttons, affordances are visual:
  Hover state: Glow, highlight, or scale change when element is "aimed at"
  Depth cue: Elements that can be grabbed appear raised
  Animation invitation: Subtle motion suggests "this can be interacted with"

Rules:
  If it's interactive, it must communicate interactivity visually
  Hover state = "you're aiming here" → user knows what will happen on trigger
  Consistent vocabulary: Same gesture always does the same thing
```

**2. Error forgiveness**
```
Gestures are imprecise compared to mouse clicks.
  Touch target size in Vision Pro: min 60×60pt at arm's length
  Hover activation time: ~100ms dwell time before triggering (prevents accidents)
  Confirmation before irreversible actions: no accidental destructive gestures

Dead zones:
  Add inactive zones between interactive elements
  Prevents mis-triggering adjacent controls

Undo:
  All gesture-triggered actions should be undoable
  Gesture-driven deletion: always show undo toast
```

**3. Fatigue and ergonomics**
```
Gorilla arm syndrome: Extended arm use causes fatigue.
  Don't require held positions for more than 2–3 seconds
  Resting position should be neutral (arms at sides, lap)
  For extended input: allow voice or other alternatives

Vision Pro ergonomics:
  Primary interaction zone: lap or tabletop (where hands rest naturally)
  Don't require reaching above shoulder height
  Enable "indirect" gestures: air tap from resting position (gaze + thumb flick)
```

**4. Discoverability**
```
Gestures are invisible — users can't see what's possible.
Teach gestures before requiring them:

Onboarding: Animated demonstration of each gesture
  "Pinch to select" → shows animated hands pinching
  "Flick to dismiss" → animated card swiping away

Progressive teaching:
  Teach the one gesture needed now — not all gestures at once
  First screen: teach primary select
  Later: teach secondary gestures as they become relevant

Contextual hints:
  "Pinch to confirm" label appears near action that requires it
  Disappears after user has done it successfully 3× (learned)
```

### Gesture Design for Vision Pro (visionOS)

```
Primary gestures:
  Look + pinch: "Tap" (most common — no arm movement needed)
  Look + tap surface: Alternative tap
  Pinch + drag: Move window or object in space
  Two-finger pinch + expand: Scale spatial content
  Look + tap crown: Return to home

Design implications:
  Don't design interactions requiring held gestures (> 1-2 seconds)
  Don't require simultaneous two-hand gestures in complex positions
  All primary actions must be reachable with look + single hand pinch

Hover design in visionOS:
  Elements must have a visible hover state (the "eye hover" highlights them)
  Test: do all your interactive elements visibly react to gaze?
  Default: visionOS applies a subtle glow to standard controls automatically
  Custom elements: you must implement hover state manually
```

### TV / Remote Control Navigation

```
D-pad (directional navigation) design rules:
  Focus model: One element is focused at all times; visible focus ring required
  Focus moves predictably: Up, down, left, right must match spatial layout
  No traps: Focus must never get stuck with no valid adjacent target
  Long press: Reveals secondary options (like right-click)
  Back: Standard "back" button goes to previous state — always

Focus ring design:
  Must be clearly visible on any background
  Minimum: 3px white border + shadow for dark backgrounds
  Animated: scales slightly when element receives focus (100ms spring)

Grid navigation:
  When focus reaches edge of one section → jumps to next section's nearest item
  Not the first item of next row — the nearest spatial equivalent
```

### Outputs
- Gesture vocabulary document (what each gesture does throughout the app)
- Affordance specification (hover states, focus states, interactive visual cues)
- Onboarding gesture tutorial design
- Platform-specific gesture specs (Vision Pro, TV, AR)
