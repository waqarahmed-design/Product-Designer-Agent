# Usability & Accessibility Methods

## Table of Contents
1. [WCAG Compliance](#1-wcag-compliance)
2. [Keyboard Navigation](#2-keyboard-navigation)
3. [Screen Reader Optimization](#3-screen-reader-optimization)
4. [Color Contrast](#4-color-contrast)
5. [Focus Management](#5-focus-management)
6. [Inclusive Design](#6-inclusive-design)
7. [Cognitive Load Management](#7-cognitive-load-management)
8. [Error Prevention](#8-error-prevention)
9. [Forgiveness Design](#9-forgiveness-design)

---

## 1. WCAG Compliance

**Purpose:** Ensure the product meets Web Content Accessibility Guidelines so it's usable by people with disabilities — and legally compliant in most jurisdictions.

**When to use:** Any web or mobile product. WCAG 2.1 AA is the industry standard and legal minimum in many countries.

### WCAG Conformance Levels

| Level | Description | Target |
|-------|-------------|--------|
| A | Minimum — removing barriers that make content completely unusable | Legal floor |
| AA | Standard — removing barriers that significantly impede use | Industry standard |
| AAA | Enhanced — optimal accessibility | Specialist products (gov, health) |

### WCAG Four Principles (POUR)

**Perceivable** — users can perceive all information:
- Text alternatives for non-text content (alt text, captions)
- Captions for video, transcripts for audio
- Color is never the only way to convey information
- Text resizable to 200% without loss of content

**Operable** — users can operate all interface components:
- All functionality available via keyboard
- No content flashes more than 3 times per second
- Users can pause, stop, or hide moving content
- Skip navigation links for keyboard users

**Understandable** — users can understand content and interface:
- Language of page declared in HTML
- Pages behave predictably — navigation consistent across pages
- Error identification and suggestions provided
- Labels or instructions for user input

**Robust** — content interpreted by assistive technologies:
- Valid HTML (properly nested, closed tags)
- Name, role, and value for all UI components
- Status messages programmatically determinable

### Quick WCAG AA Checklist

**Images:**
- [ ] All `<img>` have `alt` attributes
- [ ] Decorative images have `alt=""`
- [ ] Complex images (charts, diagrams) have detailed descriptions

**Forms:**
- [ ] Every input has a visible `<label>` (not just placeholder)
- [ ] Required fields indicated (not just by color)
- [ ] Error messages identify the field and explain how to fix

**Interactive elements:**
- [ ] All interactive elements reachable by keyboard
- [ ] Focus indicator visible on all focusable elements
- [ ] Touch targets minimum 44×44px (iOS) / 48×48dp (Android)

**Content:**
- [ ] Color contrast: 4.5:1 for normal text, 3:1 for large text (18pt/14pt bold)
- [ ] Text doesn't disappear or become unreadable at 200% zoom
- [ ] No content conveys meaning through color alone

### Outputs
- WCAG compliance audit with issues rated by severity
- Remediation recommendations per issue
- Testing record (manual + automated tool results)

---

## 2. Keyboard Navigation

**Purpose:** Ensure every function in the product can be completed using a keyboard alone, for users who can't use a mouse or touchscreen.

**When to use:** Any web product; required for WCAG AA.

### Keyboard Navigation Standards

**Focus order:** Tab order must follow visual reading order (generally left-to-right, top-to-bottom). Users should never be surprised by where focus jumps.

**Essential keyboard interactions:**

| Key | Expected behavior |
|-----|------------------|
| `Tab` | Move focus to next interactive element |
| `Shift + Tab` | Move focus to previous interactive element |
| `Enter` / `Space` | Activate focused button or link |
| `Space` | Toggle checkbox; activate button |
| `Arrow keys` | Navigate within component (menu items, radio groups, tabs, listbox) |
| `Escape` | Close modal, dropdown, popover, or clear selection |
| `Home` / `End` | Jump to first/last item in a list or menu |

### Keyboard Trap Prevention

A keyboard trap occurs when focus enters a component and cannot escape via keyboard. This is a WCAG A failure.

Exception: Modals intentionally trap focus — but must be closable via `Escape`.

```
Modal keyboard behavior (correct):
  - On open: focus moves to first interactive element inside modal
  - Tab cycles only within modal (not to background content)
  - Escape closes modal and returns focus to the trigger that opened it
  - Close button also dismisses
```

### Skip Navigation Links

For pages with persistent navigation (header, sidebar), provide a skip link:

```html
<!-- First element in <body> -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Visible only on focus -->
<style>
  .skip-link {
    position: absolute;
    transform: translateY(-100%);
    transition: transform 0.2s;
  }
  .skip-link:focus {
    transform: translateY(0);
  }
</style>
```

### Custom Component Keyboard Patterns (ARIA Authoring Practices)

| Component | Pattern |
|-----------|---------|
| Dropdown/Select | Arrow keys to navigate options, Enter to select, Escape to close |
| Tab panel | Arrow keys switch tabs; Tab enters panel content |
| Accordion | Enter/Space toggles panel; Tab moves to next accordion header |
| Modal | Focus trapped; Escape closes; focus returns to trigger on close |
| Combobox | Type to filter; Arrow keys to navigate; Enter to select |
| Slider | Arrow keys adjust value; Home/End = min/max |
| Tree view | Arrow keys navigate hierarchy; Right expands; Left collapses |

### Outputs
- Keyboard navigation audit per interactive component
- Tab order documentation
- Custom component keyboard pattern specs

---

## 3. Screen Reader Optimization

**Purpose:** Ensure the product communicates meaningfully to users of assistive technologies (VoiceOver, TalkBack, NVDA, JAWS) who consume interfaces through audio rather than visual rendering.

**When to use:** Any web or mobile product. Required for WCAG AA.

### Semantic HTML First

Screen readers announce native HTML semantics automatically. Use native elements before ARIA:

```html
<!-- Correct: native button — keyboard accessible, announced as "button" -->
<button type="button">Submit</button>

<!-- Wrong: div styled as button — must add ARIA and JS manually -->
<div class="btn" onclick="submit()">Submit</div>
<!-- If you must: <div role="button" tabindex="0" onkeydown="..."> -->
```

**Semantic element mapping:**

| Element | Announced as |
|---------|-------------|
| `<button>` | "Button" |
| `<a href>` | "Link" |
| `<nav>` | "Navigation landmark" |
| `<main>` | "Main landmark" |
| `<h1>–<h6>` | "Heading level N" |
| `<ul>/<ol>` | "List, N items" |
| `<img alt="text">` | "Image: [alt text]" |
| `<input type="checkbox">` | "Checkbox, checked/unchecked" |

### ARIA Rules

**Rule 1: Don't use ARIA if a native HTML element does the job.**

**Rule 2: Don't change native semantics.** Don't add `role="heading"` to a `<button>`.

**Rule 3: Interactive ARIA elements must be keyboard-operable.**

**Rule 4: Don't hide focusable elements.** `display: none` and `visibility: hidden` remove from both visual and AT tree. `aria-hidden="true"` removes from AT tree while keeping visual.

### Common ARIA Patterns

```html
<!-- Icon button — announce the action, not the icon -->
<button aria-label="Close dialog">
  <svg aria-hidden="true">...</svg>
</button>

<!-- Loading state -->
<div aria-live="polite" aria-busy="true">
  Loading your portfolio...
</div>

<!-- Error message linked to input -->
<input id="email" aria-describedby="email-error" aria-invalid="true">
<p id="email-error" role="alert">Please enter a valid email address</p>

<!-- Dynamic content announcements -->
<div aria-live="polite">
  <!-- Changes here announced automatically -->
  3 results found
</div>
<div aria-live="assertive">
  <!-- High-priority interruptions only (errors, critical alerts) -->
</div>

<!-- Tabs -->
<div role="tablist" aria-label="Account sections">
  <button role="tab" aria-selected="true" aria-controls="panel-1" id="tab-1">Overview</button>
  <button role="tab" aria-selected="false" aria-controls="panel-2" id="tab-2">Activity</button>
</div>
<div role="tabpanel" id="panel-1" aria-labelledby="tab-1">...</div>
```

### Mobile Screen Reader (VoiceOver / TalkBack)

- Elements announced on tap (not on hover)
- Swipe right/left to move between elements
- Double-tap to activate
- Test with actual device — simulators don't replicate screen reader behavior
- Group related elements with `accessibilityElement` (iOS) / `importantForAccessibility` (Android)

### Outputs
- Screen reader audit (VoiceOver on Safari, NVDA on Chrome minimum)
- ARIA annotation spec for custom components
- List of missing `alt` text, labels, and live regions

---

## 4. Color Contrast

**Purpose:** Ensure text and interactive elements have sufficient contrast against their backgrounds for users with low vision or color vision deficiency.

**When to use:** Before finalizing any color palette; during design review of every screen.

### WCAG Contrast Requirements

| Content type | AA minimum | AAA enhanced |
|-------------|------------|--------------|
| Normal text (< 18pt / 14pt bold) | 4.5:1 | 7:1 |
| Large text (≥ 18pt / ≥ 14pt bold) | 3:1 | 4.5:1 |
| UI components (borders, icons) | 3:1 | — |
| Decorative content | None | — |
| Disabled UI elements | None | — |
| Logo / brand | None | — |

### Contrast Ratio Calculation

Contrast ratio = (L1 + 0.05) / (L2 + 0.05)
Where L1 = relative luminance of lighter color, L2 = relative luminance of darker color

**Don't calculate manually** — use tools:
- Figma plugin: Contrast (by Able)
- Browser: Chrome DevTools accessibility panel
- Web: WebAIM Contrast Checker
- Design system: define contrast-passing color pairings in advance

### Common Contrast Failures

```
Frequent failures:
  Gray text on white background
  ├── #999999 on #FFFFFF = 2.85:1 ❌
  ├── #767676 on #FFFFFF = 4.54:1 ✅ (just passes AA)
  └── #595959 on #FFFFFF = 7.0:1  ✅ (passes AAA)

  Placeholder text (intentionally light)
  ├── Typical placeholder (#999) fails for normal text
  └── Use #767676 minimum, or make placeholder match label style

  Accent color on dark background
  ├── Test your brand color against all surfaces it appears on
  └── Lime green (#C8E847) on dark (#080808) = ~9:1 ✅
```

### Color Not the Only Indicator

Beyond contrast ratios, ensure color is never the **sole** differentiator:

| Context | Color alone (wrong) | Color + shape/text (right) |
|---------|--------------------|-----------------------------|
| Error state | Red border only | Red border + error icon + message |
| Required field | Red asterisk only | Red asterisk + "Required" label |
| Success/failure | Green/red badge | Green/red badge + "Success"/"Error" text |
| Link vs. plain text | Blue color only | Blue color + underline |
| Chart data series | Color only | Color + pattern/label |

### Outputs
- Contrast audit for all text/background combinations
- Updated color palette with failing combinations flagged
- Alternative combinations for each failing pair

---

## 5. Focus Management

**Purpose:** Ensure keyboard focus is always visible, logically sequenced, and intelligently managed when UI changes dynamically.

**When to use:** Any interactive product, especially when designing modals, drawers, notifications, or dynamic content.

### Focus Indicator Design

The default browser focus ring is often invisible or ugly — always design a custom one:

```css
/* Remove default only if replacing it */
:focus { outline: none; }

/* Custom focus ring */
:focus-visible {
  outline: 2px solid #C8E847;      /* high-contrast color */
  outline-offset: 2px;              /* space between element and ring */
  border-radius: 4px;               /* match element border-radius */
}

/* :focus-visible only shows for keyboard nav, not mouse click */
```

**Focus ring requirements:**
- Minimum 2px thickness
- 3:1 contrast against adjacent colors
- Visible on both light and dark backgrounds (consider dual-tone ring)
- Never `outline: none` without a visual replacement

### Focus Order Rules

Focus must follow a logical sequence — typically matching visual left-to-right, top-to-bottom reading order:

```
❌ Bad focus order (z-index or DOM order mismatch):
  1. Header logo → 2. Footer link → 3. Nav item → 4. Main content

✅ Correct focus order:
  1. Skip link → 2. Nav items (left to right) → 3. Main content → 4. Footer
```

**Tab index rules:**
- `tabindex="0"` — make non-interactive element focusable (in natural DOM order)
- `tabindex="-1"` — programmatically focusable but removed from tab sequence (use for focus management)
- `tabindex="1+"` — avoid entirely; creates maintenance nightmares and overrides natural order

### Dynamic Focus Management

When UI changes dynamically, manually move focus to the appropriate element:

```javascript
// Opening a modal
function openModal() {
  modal.removeAttribute('hidden');
  // Move focus to first focusable element
  modal.querySelector('h2, button, input').focus();
}

// Closing a modal
function closeModal() {
  modal.setAttribute('hidden', '');
  // Return focus to the trigger that opened it
  triggerButton.focus();
}

// Form submission error
function showErrors() {
  errorSummary.focus(); // Move focus to error summary at top of form
}

// Loading complete
function onContentLoaded() {
  newContentHeading.focus(); // Announce new content to screen reader
}
```

### Focus Trap Implementation (Modals)

```javascript
function trapFocus(element) {
  const focusable = element.querySelectorAll(
    'a[href], button:not([disabled]), input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  const first = focusable[0];
  const last = focusable[focusable.length - 1];

  element.addEventListener('keydown', (e) => {
    if (e.key !== 'Tab') return;
    if (e.shiftKey) {
      if (document.activeElement === first) { e.preventDefault(); last.focus(); }
    } else {
      if (document.activeElement === last) { e.preventDefault(); first.focus(); }
    }
  });
}
```

### Outputs
- Custom focus indicator design spec
- Focus order documentation per screen
- Focus management spec for modals, drawers, and dynamic content

---

## 6. Inclusive Design

**Purpose:** Design products that work for the full diversity of human ability, context, and circumstance — going beyond compliance minimums to create genuinely accessible experiences.

**When to use:** From the start of any project. Accessibility retrofitted at the end costs 10× more than designed in from the beginning.

### Inclusive Design Principles (Microsoft)

1. **Recognize exclusion** — identify who is being excluded by the current design
2. **Solve for one, extend to many** — solutions for edge cases often improve the experience for everyone (curb cuts, captions, etc.)
3. **Learn from diversity** — people with disabilities are experts in adapting; research with them, not just about them

### Disability Categories to Design For

| Disability | Design Considerations |
|------------|----------------------|
| **Visual** (blindness, low vision, color blindness) | Screen reader support, contrast, scalable text, no color-only indicators |
| **Motor** (limited hand/arm mobility, tremors) | Keyboard nav, large touch targets, no time limits, reduce precision requirements |
| **Auditory** (deafness, hard of hearing) | Captions, transcripts, visual alerts, no audio-only information |
| **Cognitive** (dyslexia, ADHD, memory) | Clear language, consistent patterns, progress indicators, error forgiveness |
| **Situational** (bright sunlight, one hand occupied) | High contrast mode, large tap targets, voice input |
| **Temporary** (broken arm, eye surgery) | Same as permanent disability design; often the majority use case |

### Situational Exclusion Mapping

For any feature, identify situational exclusions:

```
Feature: Reading a notification
Permanent:    Blind user (can't see)
Temporary:    User with eye surgery (can't focus)
Situational:  User in bright sunlight (can't see screen)
Solution:     High contrast + screen reader announcement + haptic feedback
```

### Plain Language Guidelines

Cognitive accessibility starts with language:
- Use words your audience uses, not internal jargon
- One sentence per idea (max 20 words per sentence)
- Active voice: "Click Save" not "The form should be saved by clicking"
- Front-load the most important information
- Avoid idioms, metaphors, and culture-specific references in global products

### Outputs
- Inclusive design audit (who is excluded by current design?)
- List of design changes that improve experience for multiple groups
- Plain language review of all UI copy

---

## 7. Cognitive Load Management

**Purpose:** Minimize the mental effort required to use the product so users can accomplish goals with less frustration and fewer errors.

**When to use:** Any complex UI, onboarding flows, data-heavy dashboards, multi-step processes.

### Types of Cognitive Load

| Type | Definition | Reduce by |
|------|------------|-----------|
| **Intrinsic** | Complexity inherent to the task itself | Can't be eliminated; can be scaffolded |
| **Extraneous** | Complexity added by poor design | Eliminate this — it's wasted mental effort |
| **Germane** | Cognitive effort that builds useful mental models | Optimize this — it leads to mastery |

Design goal: eliminate extraneous load, reduce intrinsic load, optimize germane load.

### Cognitive Load Reduction Techniques

**Chunking:** Group related information together; the eye can scan groups faster than undifferentiated lists.
- Group form fields into logical sections
- Group navigation by category
- Break long text into scannable sections with headers

**Recognition over recall:**
- Show options rather than requiring users to remember them (dropdowns > free text where possible)
- Show recent history (searches, files, contacts)
- Use familiar icons and patterns from other products users know

**Progressive disclosure:** (see `references/interaction-design.md`)

**Defaults and automation:**
- Pre-fill what you know
- Select the most common option by default
- Calculate what can be calculated; don't ask users to do math

**Reducing simultaneous choices:**
- Hick's Law: decision time increases logarithmically with the number of choices
- Limit primary navigation to 5–7 items
- Limit action buttons per screen to 1 primary, max 2 secondary

**Visual hierarchy:**
- One primary action per screen draws the eye and reduces decision fatigue
- Size and weight hierarchy helps users scan before reading
- Whitespace creates breathing room and prevents overwhelm

### Cognitive Load Audit Questions

For any screen, ask:
- How many decisions must a user make before they can accomplish their goal?
- Is any information displayed that users don't need right now?
- Are any labels or terms unfamiliar to the target user?
- Must users remember anything from a previous screen to use this one?
- Are there more than 2 primary actions competing for attention?

### Outputs
- Cognitive load audit with specific extraneous load sources identified
- Simplified layouts removing unnecessary information
- Default and auto-fill recommendations

---

## 8. Error Prevention

**Purpose:** Design the interface to make mistakes unlikely or impossible — rather than relying on error messages to recover from them.

**When to use:** Any form, destructive action, complex input, or multi-step flow.

### Error Prevention Hierarchy

1. **Eliminate the error opportunity** — redesign so the mistake can't happen
2. **Constrain input** — only allow valid input
3. **Warn before acting** — show consequences before they're irreversible
4. **Confirm before irreversible actions** — make users consciously commit
5. **Recover gracefully** — if prevention fails, make recovery easy (see Forgiveness Design)

### Constraint Techniques

```
Date input:
  ❌ Free text field (users type "13/32/2024", "March 5", "05-03-24")
  ✅ Date picker (constrained to valid dates only)

Phone number:
  ❌ Validate on submit only
  ✅ Format as user types: "(___) ___-____" with input mask

File upload:
  ❌ Accept any file, error on wrong type after upload
  ✅ accept="image/*" attribute + drag-drop shows accepted types

Quantity input:
  ❌ Free text (users enter -1, 999999, "five")
  ✅ Stepper buttons with min/max constraints + numeric keyboard on mobile
```

### Confirmation Before Destructive Actions

Not every action needs confirmation — only irreversible or high-consequence ones:

```
Confirmation warranted:
  ✅ Delete account
  ✅ Delete project with collaborators
  ✅ Send bulk email to all users
  ✅ Publish article to 50k subscribers

No confirmation needed:
  ❌ Liking a post (reversible)
  ❌ Saving a draft (reversible)
  ❌ Archiving (reversible)
  ❌ Low-stakes navigation
```

**Confirmation dialog design:**
- State clearly what will be deleted/affected
- Quantify impact when possible: "This will delete 3 projects and 47 files"
- Make the destructive button require intentional action — consider typing the name to confirm for high-stakes deletions
- Label buttons with the action, not "Yes/No": "Delete account" / "Keep account"

### Smart Validation Timing

| Validation timing | Use when |
|-------------------|----------|
| **On blur** (field loses focus) | Format validation (email, phone) |
| **Real-time** (while typing) | Password strength, character count |
| **On submit** | Cross-field validation (password confirmation) |
| **Never on keystroke** | Avoid showing errors while user is still typing |

### Outputs
- Error prevention audit: list of inputs that could be constrained
- Confirmation dialog designs for all destructive actions
- Validation timing spec per input field

---

## 9. Forgiveness Design

**Purpose:** Make mistakes easy and safe to recover from — so users feel confident exploring without fear of breaking something.

**When to use:** Any destructive action, complex editing experience, multi-step process, or any screen where users can lose work.

### Forgiveness Mechanisms

**Undo:**
- Most powerful forgiveness mechanism — immediately reverses the last action
- Available for all reversible actions
- Accessible via keyboard shortcut (Cmd/Ctrl + Z) on desktop
- Toast notification with "Undo" button on mobile (5–10 second window)

```
Toast pattern:
  [Action name] · [Undo button]
  "Message sent · Undo"           ← tap Undo within 5 seconds
  "3 items deleted · Undo"
```

**Soft delete (trash/archive):**
- Items move to trash rather than permanent deletion
- Retention period: 7–30 days depending on product context
- "Deleted items" section in settings
- Empty trash requires explicit action

**Version history / autosave:**
- Autosave every 30–60 seconds for editable content
- Show last saved timestamp
- Named version history for significant states
- "Restore to previous version" without losing current version

**Drafts and auto-recovery:**
- Long forms: save progress on navigate away
- On return: "You have an unsaved draft. Continue?" / "Start fresh?"
- Browser crash recovery on next visit

**Graceful degradation:**
- Partial saves: if a complex action partially fails, save what succeeded
- Show exactly what was saved and what wasn't
- Don't make users redo the successful part

### Forgiveness vs. Confirmation

These serve different purposes and are often both needed:

| Mechanism | Purpose | When |
|-----------|---------|------|
| **Confirmation** | Prevent accidental trigger | Before irreversible action |
| **Undo** | Reverse after accidental trigger | After reversible action |
| **Soft delete** | Allow recovery window | After delete action |
| **Autosave** | Prevent work loss | During long editing sessions |

Forgiveness doesn't eliminate confirmation — it provides a safety net in case users clicked through confirmation too quickly.

### Outputs
- Undo/redo spec for reversible actions
- Soft delete implementation spec with retention period
- Autosave implementation spec (frequency, recovery UI)
- List of all irreversible actions with forgiveness mechanisms assigned
