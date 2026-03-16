# Microinteraction Case Studies

Detailed design breakdowns of five common UI patterns analyzed through the four-part structure: Trigger → Rules → Feedback → Loops & Modes. Each includes edge cases and platform notes.

---

## Case Study 1: Form Submission

High-stakes microinteraction — user has invested time and data. Getting this wrong destroys trust.

### The Four Parts

**Trigger:** Submit button (manual) | Enter key in last field | Auto-save after 30s inactivity (system)

**Rules:**
1. Validate all required fields client-side before sending
2. If validation fails → prevent submission, highlight first invalid field
3. If validation passes → disable submit button, show loading state
4. Send to server
5. Server success → show confirmation, redirect or reset
6. Server error → show error, preserve all input
7. Network timeout (>15s) → show retry option with preserved input

**Feedback by state:**

| State | Visual | Copy | Duration |
|-------|--------|------|----------|
| Idle | Blue button | "Submit" | Persistent |
| Validation error | Red border on invalid fields | Inline "Please enter a valid email" | Until corrected |
| Submitting | Spinner replaces button text | "Submitting..." | Server response time |
| Success | Green checkmark | "Done! Redirecting..." | 1–2s |
| Server error | Red banner, button re-enabled | "Something went wrong. Try again." | Until dismissed |
| Network error | Yellow banner, retry button | "Connection lost. Data saved locally." | Until retry |

**Loops & Modes:**
- Auto-save loop: draft to localStorage every 30s (open loop)
- Long loop: after 3+ submissions, hide optional tooltips and hints

### Edge Cases

| Edge Case | Handling |
|-----------|---------|
| Double-click submit | Disable on first click; debounce server request |
| Navigate away mid-submission | "Unsaved changes" dialog; save draft |
| Session expires during submission | Queue, re-authenticate, retry |
| Very long form (20+ fields) | Progress indicator; validate sections independently |

---

## Case Study 2: Toggle / Switch

Deceptively simple — binary state, but requires careful attention to state communication and accessibility.

### The Four Parts

**Trigger:** Tap anywhere on the toggle | Space bar when focused | Drag thumb | System state change

**Rules:**
1. Start transition animation immediately on trigger
2. If server confirmation needed → send in background
3. Rapid toggling → debounce 500ms, send only final state
4. Server rejects → revert to previous state with error message

**Feedback by state:**

| State | Thumb | Track Color | Haptic |
|-------|-------|-------------|--------|
| Off | Left | Gray | None |
| Transitioning on | Sliding right | Transitioning | None |
| On | Right | Green | Light tap |
| Loading | Current | Faded + inline spinner | None |
| Error | Reverted | Brief red flash | Error pattern |

**Animation spec:**

| Property | Duration | Easing |
|----------|----------|--------|
| Thumb position | 150–200ms | ease-in-out |
| Track color | 150–200ms | ease-in-out (synchronized) |
| Error revert | 200ms | ease-out with red flash |

**Accessibility:**
- `role="switch"` + `aria-checked="true/false"`
- Space bar toggles (not Enter, per switch role spec)
- Minimum 44×44pt touch target
- Reduced motion: instant state change, skip animation

### Edge Cases

| Edge Case | Handling |
|-----------|---------|
| Toggle with settings reveal | Panel slides open below, 200ms accordion |
| Toggle with destructive off | Confirmation: "Disabling will delete all data." |
| Server failure | Revert toggle; inline error for 3s |
| Dependent toggles | Child toggles disable when parent turns off |

---

## Case Study 3: Pull-to-Refresh

Invented by Loren Brichter for Tweetie. Transforms a natural gesture into data refresh. One of the most widely adopted mobile patterns.

### The Four Parts

**Trigger:** Pull down past threshold (~60pt) | Must be scrolled to top of list | System auto-refresh on app foreground (fallback)

**Rules:**
1. Pull below threshold → visual hint, no refresh
2. Pull past threshold → "locks" refresh
3. Release after threshold → triggers refresh request
4. Release before threshold → snaps back, no refresh
5. While refreshing → spinner visible, list still scrollable
6. Minimum spinner display: 500ms (prevents flash on fast connections)
7. Rate limit: ignore pull if last refresh < 5 seconds ago

**Feedback by pull distance:**

| Pull Distance | Visual | Haptic |
|--------------|--------|--------|
| 0–20pt | Slight rubber-band stretch | None |
| 20–60pt | Spinner appears, partially rotated proportional to pull | None |
| 60pt (threshold) | Spinner completes rotation; visual snap | Light tap |
| Release (past threshold) | Spinner animates spinning | None |
| Data received | Spinner stops; new items slide in from top | None |
| Error | Spinner stops; brief error text | Error pattern |

**Loops & Modes:**
- Auto-refresh: if user hasn't refreshed in 5+ min and returns to app (system trigger)
- Long loop: first 3 uses show "Pull down to refresh" hint text
- No modes

### Discoverability (zero visible affordance)

| Strategy | Remove When |
|----------|------------|
| "Pull down to refresh" hint text above list | After 3 successful uses |
| Auto-refresh animation on first visit | After first visit only |
| Visible refresh button in header | Never (always keep as fallback) |

### Platform Notes

| Platform | Implementation |
|----------|---------------|
| iOS | `UIRefreshControl` — native, threshold system-defined |
| Android | `SwipeRefreshLayout` — circular progress fills as user pulls |
| Web | Custom; `overscroll-behavior: contain` on scroll container |

---

## Case Study 4: Loading States

Not one pattern — a family. The design challenge is keeping users informed during time they cannot control.

### Pattern Selection by Duration

| Scenario | Pattern | Why |
|----------|---------|-----|
| < 300ms | None | Any indicator would flash distractingly |
| 300ms–1s | Inline spinner | Acknowledges loading without drama |
| 1–5s | Skeleton screen | Shows layout immediately |
| 5–30s | Determinate progress bar | Users need actual progress |
| 30s+ | Progress bar + background option | Users should do other things |
| Unknown | Indeterminate spinner + status text | Transparency: "Processing..." → "Almost done..." |

### Skeleton Screen

**Rules:**
1. Show skeleton immediately (within 100ms of navigation)
2. Shapes must match final layout precisely
3. Subtle pulse animation: opacity 0.3→0.6, 1.5s loop
4. Load text first, then images
5. Crossfade skeleton → real content: 200ms
6. Never show skeleton for cached content

**Skeleton visual:**

| Content | Shape | Animation |
|---------|-------|-----------|
| Text line | Rounded rect, 60–80% width | Pulse 0.3–0.6 opacity |
| Heading | Rounded rect, 40–50% width, taller | Pulse |
| Avatar | Circle, matching size | Pulse |
| Image | Rounded rect, matching aspect ratio | Pulse |

### Progress Bar

**Rules:**
1. Appear within 200ms of operation start
2. Progress must be real — never fake
3. Never go backward (pause at current if real progress reverses)
4. Final 5% = server confirmation, not client processing
5. On completion: fills to 100% → brief pause → success state

| Progress | Visual | Text |
|----------|--------|------|
| 0% | Empty bar | "Starting upload..." |
| 1–99% | Fills proportionally | "Uploading... 47%" |
| 99% | Nearly full, slight pause | "Finalizing..." |
| 100% | Fills, transitions to green | "Complete!" |
| Error | Turns red, stops | "Upload failed at 47%. Retry?" |

**Accessibility:**
- `aria-live="polite"` announces "Loading content" and "Content loaded"
- `role="progressbar"` with `aria-valuenow`, `aria-valuemin`, `aria-valuemax`
- Reduced motion: replace pulse with static gray; spinner → "Loading..." text

---

## Case Study 5: Toast Notifications

Transient microinteractions for system events. Design determines whether they're helpful or infuriating.

### The Four Parts

**Trigger:** Action completes (save, send, delete) | External event (new message) | Error detected | User action with reversible outcome (delete → "Undo" toast)

**Rules:**
1. Consistent position: bottom-center (mobile), bottom-left or top-right (desktop)
2. Stack if multiple appear — max 3 visible, queue additional
3. Auto-dismiss: 5–8s for info; persist for errors until acknowledged
4. Enter: 300ms ease-out; exit: 200ms ease-in
5. Must not cover critical UI (primary actions, navigation)
6. "Undo" action available for full display duration
7. Dismissable via swipe (mobile) or close button (desktop)

**Types:**

| Type | Auto-Dismiss | Action |
|------|-------------|--------|
| Success | 5s | None or "View" |
| Info | 5s | Optional link |
| Warning | 8s | "Fix" or "Dismiss" |
| Error | No (persist) | "Retry" + "Dismiss" |
| Undo | 8s | "Undo" (primary) |

**Layout:**
```
┌────────────────────────────────────────────┐
│  [Icon]  Message text          [Action] [X] │
│          Secondary text (optional)          │
└────────────────────────────────────────────┘
```

- Width: min 288px, max 568px (desktop); full-width minus margins (mobile)
- Padding: 16px horizontal, 12px vertical | Border radius: 8px | Z-index: above content, below modals

**Animation spec:**

| Transition | Duration | Easing | Direction |
|-----------|----------|--------|-----------|
| Enter | 300ms | ease-out | Slide up from below (mobile) |
| Exit (auto) | 200ms | ease-in | Slide down or fade |
| Exit (swipe) | 150ms | ease-out | Follow swipe |
| Stack push | 200ms | ease-in-out | Existing toasts shift up |

**Loops & Modes:**
- Stacking loop: max 3 visible, dismiss oldest first
- Long loop: batch repeated events — "3 items saved" instead of three separate toasts
- No modes

**Accessibility:**
- `role="status"` + `aria-live="polite"` for info/success
- `role="alert"` + `aria-live="assertive"` for errors
- Pause auto-dismiss timer on hover/focus
- Esc key dismisses; Tab reaches action buttons
- Reduced motion: replace slide with fade (200ms)

### Edge Cases

| Edge Case | Handling |
|-----------|---------|
| 10 toasts at once | Queue: show 3, dismiss oldest, show queued |
| Toast covers primary action | Reposition above the action |
| Click Undo at last second | Accept if within timeout window, even if fade started |
| Long text | Truncate at 2 lines + "Show more" |
| Network loss during Undo | Queue locally; execute when connection returns |

---

## Cross-Cutting Patterns

| Pattern | Application |
|---------|-------------|
| **Debouncing** | Double-click submit, rapid toggle, pull-to-refresh spam |
| **Optimistic UI** | Toggle, like, delete with undo |
| **Progressive disclosure** | Error summary first, full details expandable |
| **Graceful degradation** | Form submits via native HTML; toggle works without animation |
| **State persistence** | Form drafts, scroll position, toggle state across sessions |
| **Accessibility baseline** | ARIA roles, keyboard operation, reduced motion for all patterns |
