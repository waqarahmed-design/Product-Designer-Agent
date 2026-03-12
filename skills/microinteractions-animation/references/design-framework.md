# Microinteraction Design Framework (Saffer)

The "why and what" behind microinteractions — before reaching for any animation tool, understand what the interaction is doing and why. Based on Dan Saffer's four-part structure.

## What Is a Microinteraction?

A microinteraction is a **contained product moment built around a single use case**: changing a setting, syncing data, liking a post, setting an alarm. Users rarely think about them consciously — but they feel them. The difference between a product you tolerate and one you love is almost always in the microinteractions.

Every microinteraction follows the same structure: **Trigger → Rules → Feedback → Loops & Modes**.

---

## Scoring

**Goal: 10/10.** When reviewing or creating microinteractions, rate them 0–10 based on the principles below. Always provide the current score and specific improvements needed to reach 10/10.

---

## 1. Triggers

The trigger is what initiates a microinteraction.

**Two types:**
- **Manual** — user-initiated (tap, click, swipe, voice, type)
- **System** — fires automatically when a condition is met (time, threshold, data arrival, error)

**Key principles:**
- A trigger must communicate: that it exists, what it does, and what state it's in
- Every trigger needs distinct visual states: default, hover, active, disabled, loading
- Invisible triggers (gestures) must always have a visible alternative
- Touch targets: minimum 44×44pt (Apple HIG) / 48×48dp (Material)
- Placement follows platform convention — primary actions bottom-right (mobile), top-right (desktop)

**Trigger state transitions:**

| Transition | Duration | Easing |
|-----------|----------|--------|
| Default → Hover | Instant or 50ms | ease-out |
| Default → Active | Instant | none |
| Active → Loading | Instant | none |
| Loading → Success/Error | 200–400ms | ease-in-out |
| Any → Disabled | 150ms | ease-out |

**Invisible trigger checklist:**
- [ ] Visible alternative exists for the same action?
- [ ] Is the gesture a platform convention, not a custom invention?
- [ ] First-time coaching provided?
- [ ] Can users undo if triggered accidentally?

---

## 2. Rules

Rules determine what happens once a trigger fires. Users never see rules — they feel when they're wrong.

**Rules define:**
- What happens first and in what sequence
- What the user can and cannot do during the interaction
- Value boundaries (min, max, format constraints)
- When the interaction ends
- What happens on failure

**Goal-first method:**
1. State the goal in one sentence: "The user wants to set their alarm."
2. Identify minimum inputs
3. Define the simplest path
4. Add constraints
5. Handle failures
6. Define the end state

**Rule complexity vs. frequency:**

| Usage Frequency | Rule Complexity |
|-----------------|-----------------|
| Many times/day | Minimal — must be instant and frictionless |
| Once/day | Simple with smart defaults |
| Once/week | Moderate — options available |
| Once ever | Full rule set, onboarding acceptable |

**Core states every microinteraction must cover:**

| State | Description |
|-------|-------------|
| Idle | Ready and waiting |
| Active / In Progress | Processing or awaiting input |
| Success | Completed successfully |
| Error | Failed |
| Partial | Partially complete or loading |
| Disabled | Cannot be initiated |

**Error handling principles:**
1. Preserve the user's work — never erase input on error
2. Explain in human language ("That email looks incomplete" not "Error 422")
3. Point to the problem — inline, near the field
4. Offer a path forward — every error suggests a fix
5. Validate on blur for format errors; on submit for cross-field errors

**Actions to always prevent:**
- Double submission → disable trigger on first click
- Deleting without confirmation → destructive actions need a dialog
- Exceeding rate limits → throttle + "Try again in X seconds"

**State design checklist:**
- [ ] Every state defined (idle, active, success, error, disabled, partial)?
- [ ] Users can always tell which state they're in?
- [ ] Every state transition mapped?
- [ ] Constraints prevent errors (not punish them)?
- [ ] Error messages human-readable, specific, actionable?
- [ ] Input preserved on error?
- [ ] Edge cases covered: empty, max, rapid trigger, offline, interrupted?

---

## 3. Feedback

Feedback answers: "What just happened?" It closes the Gulf of Evaluation.

**Core principle — the minimum feedback rule:** Use the least amount of feedback that still communicates the message.

**Feedback hierarchy:**

| Event | Feedback Level | Duration | Example |
|-------|---------------|----------|---------|
| Micro (hover, focus) | Subtle visual change | Instant | Background lightens |
| Minor (tap, toggle) | Clear visual change | 100–300ms | Toggle slides |
| Medium (save, send) | Visual + state label | 1–3s | "Saved" text |
| Major (purchase, delete) | Multi-signal | 3–5s, dismissable | Banner + undo |
| Critical (error) | Prominent, persistent | Until acknowledged | Red banner |

**Timing thresholds:**

| Delay | User Perception | Required Response |
|-------|----------------|-------------------|
| 0–100ms | Instantaneous | Visual state change |
| 100–300ms | Slight lag | Transition animation |
| 300ms–1s | Noticeable | Loading indicator |
| 1–5s | Waiting | Spinner or skeleton |
| 5–30s | Attention wanders | Progress bar |
| 30s+ | Will leave | Progress + backgrounding option |

**Optimistic UI:** Show the result immediately, correct if the server fails. Use when:
- Action is very likely to succeed (>99%)
- Reverting is possible and not confusing
- Action is low-stakes (not payment or deletion)

**Feedback overload warning signs:**
- Users ignore toast notifications → too many toasts for minor events
- Interface feels "jittery" → too many animations on trivial events
- Sound becomes annoying → audio on every click

**Feedback design checklist:**
- [ ] Every interactive element provides immediate visual feedback?
- [ ] Feedback proportional to event significance?
- [ ] Operations >300ms have a loading indicator?
- [ ] Operations >10s have a progress bar?
- [ ] Error messages explain what happened and how to fix it?
- [ ] Animations under 500ms and interruptible?
- [ ] All channels accessible (visual + ARIA + reduced-motion)?

---

## 4. Loops and Modes

**Loops** determine what happens over time — how the interaction evolves with use.

**Open loops** — repeat until stopped (repeating alarm, auto-save)
**Closed loops** — run a fixed number of times (countdown timer, 3-retry limit)

**Long loops — the most neglected dimension:**

Progressive reduction removes scaffolding as users demonstrate mastery:

| Use Count | Behavior |
|-----------|----------|
| 1–3 | Full labels, tooltips, coaching marks |
| 4–10 | Labels remain, tooltips disappear |
| 11–50 | Labels shrink to icons, hints removed |
| 50+ | Icons only, keyboard shortcuts promoted |

**Long loop principles:**
- Never degrade core functionality — remove scaffolding, not features
- Always provide a way to resurface removed help
- Track per-feature, not globally
- Test the 100th use, not just the first

**Modes** are temporary states where the same trigger produces a different result. They're dangerous.

**Why modes fail:**
- Mode errors: user performs right action in wrong mode
- Mode confusion: user doesn't know which mode they're in
- Mode amnesia: user forgets they entered a mode

**Mode design rules:**
1. Make current mode unmistakably visible (banner, color, label)
2. Mode entry must be deliberate — never accidental
3. Always-visible escape from every mode
4. Minimize modes: 1 = ideal, 2 = acceptable, 3+ = reconsider

**Spring-loaded modes** (quasi-modes) — exist only while trigger is held. Eliminates mode amnesia. Use whenever possible instead of toggle modes.

**Loops & modes checklist:**
- [ ] Open vs. closed loop — is that the right choice?
- [ ] Long loop designed (behavior at 1st, 10th, 100th use)?
- [ ] Progressive reduction for experienced users?
- [ ] Mode necessary, or can it be avoided entirely?
- [ ] Current mode visible at all times?
- [ ] Obvious, always-visible escape from every mode?
- [ ] Total modes 3 or fewer?

---

## 5. Reducing and Simplifying

The best microinteraction is one the user barely notices — so simple and fast it becomes invisible.

**Principles:**
- If a microinteraction needs instructions, it's too complex
- Remove options by choosing smart defaults
- Use progressive disclosure: simple first, complexity on demand
- The number of rules should be proportional to frequency of use

**Examples of simplification:**
- Camera defaults to photo mode (not settings)
- Credit card type detected from first digits
- Double-tap to like instead of: open menu → select reaction
- ZIP code auto-fills city and state

---

## Quick Diagnostic

Audit any microinteraction against these questions:

| Question | If No → Action |
|----------|----------------|
| Clear, discoverable trigger? | Add a visible control or affordance |
| Trigger shows current state? | Add distinct visual states |
| Rules simple and predictable? | Simplify; match platform conventions |
| Immediate feedback on action? | Add visual response within 100ms |
| Feedback matches event significance? | Scale feedback to event importance |
| Interaction evolves over time? | Add progressive reduction via long loops |
| Free of unnecessary modes? | Remove modes or make current mode visible |
| First-time user can figure it out? | Simplify or add a one-time hint |

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| No feedback on action | Add immediate visual state change to every interactive element |
| Overdesigning simple moments | Reserve rich animation for infrequent, high-impact moments |
| Ignoring edge cases | Map every state: empty, loading, partial, full, error, disabled |
| Invisible triggers | Pair gesture triggers with a visible alternative |
| Mode errors | Make current mode visible; minimize number of modes |
| Ignoring long loops | Use progressive reduction for returning users |
| Feedback overload | Use smallest feedback that communicates; reserve big for big events |
| Fake progress bars | Use honest, deterministic progress |
