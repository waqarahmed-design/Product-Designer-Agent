# Emerging Specializations

## Table of Contents
1. [Design Ops](#1-design-ops)
2. [Inclusive Design](#2-inclusive-design)
3. [Ethical Design](#3-ethical-design)
4. [Sustainable Design](#4-sustainable-design)
5. [Service Design](#5-service-design)
6. [Design Thinking Facilitation](#6-design-thinking-facilitation)

---

## 1. Design Ops

**Purpose:** Scale design processes, tooling, and team health so that design quality doesn't degrade as the team, product, and organization grow.

**When to use:** When the design team is growing beyond 3–4 people; when design work is slowing down due to process friction; when design quality is inconsistent across teams; when onboarding new designers takes too long.

### What Design Ops Covers

```
Tooling & infrastructure
  Design tool stack (Figma, Storybook, token automation)
  Asset management and organization
  Handoff process and QA workflow
  Design token pipeline (Figma → code)

Process & workflow
  Design rituals (critiques, reviews, planning sessions)
  Prioritization and intake (how design work gets assigned)
  Collaboration with engineering and product
  Sprint/agile integration

Team & knowledge
  Onboarding for new designers
  Design system contribution governance
  Documentation standards
  Knowledge sharing (critiques, design reviews)

Measurement
  Design velocity (how fast designs move from wireframe to shipped)
  Design quality metrics
  Handoff defect rate (how many engineering questions per handoff)
  Designer NPS / satisfaction
```

### Design Team Rituals

```
Design critique (weekly, 60 min):
  Purpose: Get feedback on in-progress work early (before it's too polished to change)
  Format:
    1. Designer presents context (3 min): problem, constraints, goal of feedback
    2. Silent review (5 min): everyone looks without talking — writes down observations
    3. Discussion (20 min per designer): structured feedback round
    4. Designer summarizes what they're taking away (2 min)
  Rules:
    Critique the work, not the designer
    Feedback tied to specific design principles or user needs, not preferences
    Presenter sets the feedback goal: "I need help with the information hierarchy"

Design review (before shipping):
  Purpose: Gate for quality before handoff to engineering
  Attendees: Designer, PM, lead designer (or design system owner)
  Checks: WCAG contrast, spacing tokens, component usage, all states designed

Design system working group (bi-weekly):
  Purpose: Prioritize system work, review proposals, manage versioning
  Attendees: System designers, system engineers, representatives from product teams

Retrospective (monthly or per sprint):
  Review design process, not the work — what's slowing us down?
```

### Design Ops Tooling Stack

```
Design:         Figma (single source of truth for design files)
Tokens:         Tokens Studio → Style Dictionary → code
Components:     Storybook (documentation + QA)
Handoff:        Figma Dev Mode or Zeplin
Version control: Git (for tokens/specs), Abstract (for Sketch files)
Prototyping:    Figma / Framer / ProtoPie
Research:       Notion / Confluence (research repository)
Async:          Loom (record design walkthrough videos for async reviews)
Tracking:       Linear / Jira (design issues alongside engineering)
```

### Scaling Design Processes

```
When team is small (1–3 designers):
  One person can know everything — informal processes are fine
  Focus: doing great work, not process overhead

When team grows (4–8 designers):
  Inconsistency emerges — someone designs a component differently
  Process needs: Design system, component library, shared critique ritual

When team is large (9+ designers):
  Knowledge siloing — designers don't know what others are building
  Process needs: Full Design Ops function, dedicated system team, governance model

Signs you need Design Ops:
  Engineers ask the same design questions repeatedly (knowledge gap)
  Different screens look like they're from different products (consistency gap)
  Handoff takes > 2 days from design complete to engineering starting
  New designers take > 3 weeks to be productive
  Design decisions aren't documented anywhere
```

### Measuring Design Ops Health

```
Metric                          | Target       | Warning
--------------------------------|--------------|----------
Handoff-to-start time           | < 24 hours   | > 3 days
Design questions per feature    | < 3          | > 8
Time to first productive PR     | < 2 weeks    | > 4 weeks
Design system token adoption %  | > 85%        | < 70%
Critique attendance             | > 80%        | < 60%
```

### Outputs
- Design process documentation (onboarding + rituals)
- Tool stack specification + onboarding guide
- Design velocity dashboard
- Governance model for design system contributions

---

## 2. Inclusive Design

**Purpose:** Design products that work for the full diversity of human experience — including people with disabilities, people with different cultural backgrounds, and users in varied situational or environmental contexts.

**When to use:** Every design project. Inclusion is not a feature to add at the end — it's a perspective to apply throughout.

### The Inclusive Design Framework (Microsoft)

```
Three principles:
  1. Recognize exclusion: Identify who is being left out by the current design
  2. Learn from diversity: The people most excluded often have insights that improve it for everyone
  3. Solve for one, extend to many: A solution for a permanent disability often helps situational users too

The spectrum of disability:
  Permanent:   One arm amputated, blind in one eye, deaf
  Temporary:   Arm in cast, eye infection, ear infection after concert
  Situational: Holding a baby, bright sunlight, loud environment

Example: Closed captions
  Designed for: Deaf users (permanent)
  Also helps: Noisy cafe (situational), non-native language speaker (situational),
              concentration difficulties (permanent), silent office (situational)
```

### Who Gets Excluded and Why

```
Disability categories:
  Vision:   Blind, low vision, color blindness, light sensitivity
  Motor:    One hand, tremors, limited fine motor, use only keyboard
  Hearing:  Deaf, hard of hearing, cognitive audio processing differences
  Cognitive: Dyslexia, ADHD, autism spectrum, memory, anxiety

Situational exclusion:
  Environment: Bright sun → low contrast unreadable
               Noisy → audio feedback inaudible
               Dark → high brightness uncomfortable
  Context:     Moving vehicle → touch precision reduced
               Borrowed device → unfamiliar, no saved settings
               Slow connection → heavy pages unusable
  Life stage:  New user → learning curve; elderly → different tech fluency

Cultural exclusion:
  Left-to-right vs. right-to-left languages (Arabic, Hebrew)
  Cultural color meanings (red = danger in West; luck in China)
  Date/number formats (MM/DD vs. DD/MM; comma vs. period as decimal)
  Names: single name, very long names, characters from non-Latin scripts
  Addresses: not all countries have states, ZIP codes, or street numbers
```

### Inclusive Design Checklist

```
Visual:
  ✅ Color contrast AA (4.5:1 text, 3:1 large text/UI)
  ✅ Color is not the only differentiator (always add icon or text)
  ✅ Text size respects system font scaling preferences
  ✅ Content is understandable at 200% zoom without horizontal scroll
  ✅ No flashing content > 3Hz

Motor:
  ✅ Touch targets ≥ 44×44pt (iOS) / 48×48dp (Android)
  ✅ Keyboard navigable (all interactions reachable without mouse)
  ✅ No time limits (or extendable by the user)
  ✅ No interactions requiring simultaneous multi-touch (unless alternative provided)

Cognitive:
  ✅ Plain language (Flesch-Kincaid grade 8 or lower for general audience)
  ✅ Consistent navigation (same menu, same order, every page)
  ✅ Error messages explain what to do, not just what went wrong
  ✅ Input purpose is clear (labels are visible, not just placeholders)
  ✅ No auto-playing video/audio without user control

Cultural:
  ✅ Date/number format respects locale
  ✅ Names/address fields accept a wide range of formats
  ✅ Imagery is representative (not all-white, all-young, all-able users)
  ✅ RTL language support (if relevant to market)
```

### Designing for Cognitive Diversity

```
Dyslexia:
  Use: Dyslexia-friendly sans-serif fonts (OpenDyslexic, or clean sans like Atkinson Hyperlegible)
  Avoid: Dense walls of text, italics, justified text (uneven spacing confuses)
  Line length: Max 60 characters
  Spacing: Generous paragraph spacing (1.5× body spacing)

ADHD:
  Reduce: Distractions (animations, auto-playing content, busy backgrounds)
  Chunk information: Short paragraphs, bullet points, clear visual sections
  Progress indicators: Show how far through a task/flow the user is
  Save progress: Don't force completion in one session

Anxiety:
  Clear error recovery: What went wrong, what to do, what the consequences are
  No surprise costs or commitments (subscription traps, hidden fees)
  Undo and soft deletes (don't make destructive actions permanent without warning)
  Gentle onboarding: Don't demand too much information upfront
```

### Outputs
- Exclusion audit: who is currently excluded by this design?
- Inclusive design checklist (applied to each screen)
- Alternative input and output modes (voice, large text, keyboard-only)
- Representation audit for imagery and language

---

## 3. Ethical Design

**Purpose:** Design products that respect users' time, attention, autonomy, and data — avoiding patterns that exploit psychological vulnerabilities for business metrics at the expense of user wellbeing.

**When to use:** Any design decision that could manipulate user behavior; when reviewing designs for potential dark patterns; when making privacy-related design choices.

### Dark Patterns — Taxonomy

Dark patterns are UI/UX choices that trick, coerce, or mislead users into doing things they wouldn't if they fully understood.

```
Roach motel:
  Easy to get in, hard to get out.
  Example: Subscribe in 2 clicks; cancel requires phone call during business hours.
  Ethical fix: Cancellation must be as easy as sign-up. Self-serve, immediate.

Confirmshaming:
  Using guilt or shame as the "decline" option text.
  Example: [Yes, I want to save money] / [No, I prefer to waste money]
  Ethical fix: Neutral decline option: "No thanks" or "Not now"

Hidden costs (drip pricing):
  Revealing additional fees only at the final checkout step.
  Example: Flight shown as $89, becomes $143 with fees at payment step.
  Ethical fix: Show total cost as early as possible. No surprise fees.

Disguised ads:
  Making ads look like content or navigation.
  Example: "Download" button that is actually an ad for another download.
  Ethical fix: Label all paid content and ads clearly and distinctly.

Forced continuity:
  Free trial ends and billing starts without a clear reminder.
  Ethical fix: Email reminder 3–7 days before trial ends. Make cancellation trivial.

Trick questions:
  Confusing wording to get opt-in by confusion.
  Example: "Uncheck to not receive emails" (double negative opt-out).
  Ethical fix: Affirmative, clear opt-in. "Yes, send me updates" with checkbox unchecked by default.

Misdirection:
  Visually emphasizing one option to push users away from another.
  Example: [Continue free trial] styled as ghost; [Subscribe now] styled as accent.
  Ethical fix: Both options receive equal visual weight when they're true alternatives.

Privacy zuckering:
  Designed to share more personal data than intended.
  Example: Default setting is "Share with everyone" with opt-out buried 5 menus deep.
  Ethical fix: Default to most private setting. Privacy controls in obvious location.

Urgency/scarcity manipulation:
  Fake countdown timers, fake low-stock warnings, fake "X people viewing now."
  Example: "Only 2 left!" shown on a product that's always available.
  Ethical fix: Only show real data. If it's always available, don't show scarcity.

Bait and switch:
  Advertised feature or price that isn't actually available.
  Example: "Free forever" plan that gets discontinued after users are locked in.
  Ethical fix: Be honest about what the product offers. Update claims when they change.
```

### The Ethical Design Hierarchy

```
From most to least critical:

Tier 1: Do not harm
  Don't create addictive loops that harm user wellbeing
  Don't exploit vulnerable users (elderly, grieving, addicted)
  Don't use dark patterns that directly deceive

Tier 2: Respect autonomy
  Users can easily leave, cancel, or opt out
  Default settings favor user interest, not business interest
  Consent is real (informed, specific, revocable)

Tier 3: Protect privacy
  Collect minimum necessary data
  Clear privacy controls
  Don't sell or share data without explicit consent

Tier 4: Design for wellbeing
  Time well spent, not just time spent
  Notifications that add value, not just engagement metrics
  Don't optimize for engagement at the expense of user mental health
```

### Privacy-Respectful Design

```
Privacy by default:
  The most private setting is the default — not the least private.
  Users must opt IN to share more, not opt OUT to protect themselves.

Permission requests:
  Ask for permissions at the moment they're needed, not upfront.
  Explain why the permission is needed before requesting.
  Gracefully handle denial — the app works without optional permissions.

Data transparency:
  Users can see what data you have about them (GDPR Article 15).
  Users can delete their data (GDPR Article 17 — "right to erasure").
  Export their data ("Download my data").
  These must be discoverable — not buried in settings.

Minimum data collection:
  Collect only what you need to provide the service.
  Delete data when it's no longer needed.
  Don't collect data "just in case it's useful later."
```

### Ethical Review Checklist

```
✅ No dark patterns (review list above — even one is too many)
✅ Default settings favor user privacy and control
✅ Subscription/commitment: clear, cancellable, no hidden renewal
✅ Opt-ins are real: explicit, informed, not pre-checked
✅ No fake urgency or scarcity
✅ Notifications: only valuable, opt-in explicitly
✅ Data: minimum necessary, transparent, user-controlled
✅ Copy: honest, no misleading headlines or CTA text
✅ Easy to leave: account deletion, data export, cancellation all trivially easy
```

### Outputs
- Dark pattern audit for existing designs
- Ethical review checklist applied per screen
- Privacy control design (settings screen, permission flows)
- Consent flow design (cookie consent, data sharing)

---

## 4. Sustainable Design

**Purpose:** Reduce the environmental impact of digital products — considering energy consumption, data transfer, carbon footprint, and longevity in design decisions.

**When to use:** When making technology, performance, or aesthetic choices that affect data transfer or processing; when the team has sustainability goals; when targeting markets with unreliable power or slow connectivity.

### Why Digital Has an Environmental Cost

```
The internet accounts for ~4% of global CO₂ emissions (comparable to aviation).

Sources of digital emissions:
  Data transfer: Every byte transferred = energy used in data centers + networks
  Processing: Client-side computation = device battery drain = energy
  Manufacturing: Device production has large embedded carbon cost
  End-of-life: Electronic waste from short product lifecycles

Designers control:
  Page/app weight (images, fonts, JavaScript bundles)
  Animation and computation intensity
  Data requests (number of API calls, size of responses)
  Push notifications (wake device from sleep)
  Rendering performance (heavy layouts, complex shadows/filters)
```

### Sustainable Design Principles

**1. Efficiency over excess**
```
Every element that adds visual weight adds data weight.
Large hero videos, 20MB stock photos, dozens of web fonts:
  → Not just slow — environmentally costly.

Sustainable alternatives:
  Hero video → Static image + CSS gradient animation
  Full-bleed 4K photo → WebP optimized image at correct dimensions
  5 font weights → Variable font (one file = all weights)
  Custom illustration → Simple SVG (1–5KB vs. 100KB+ PNG)
```

**2. Dark mode as energy reduction**
```
OLED screens (iPhone OLED, most modern Android): Black pixels = off = no power
A true dark mode on an OLED display uses ~30% less power for dark content.

Dark design + OLED = significant battery and energy benefit at scale.
Nexus is already designed with a dark-first aesthetic — this is a genuine sustainability benefit.
```

**3. Performance = sustainability**
```
Faster code = less processing = less energy.
60fps animations on the GPU: more efficient than JS-driven animations
Tree-shaking, code splitting: Less JS = less parsing = less energy
Image optimization: Serves correctly-sized images (not 2000px images at 400px)
Caching: Serves content from cache instead of re-fetching (network energy saved)

Sustainable design spec:
  Images: WebP at appropriate resolution, max 100KB for UI images
  Fonts: Variable fonts or system fonts; subset to used characters
  Icons: SVG sprite or component (not individual HTTP requests)
  Animations: transform/opacity only (GPU); no scroll-jacking
```

**4. Longevity and repairability**
```
Products that last longer reduce manufacturing emissions:
  Design for maintainability (clean code, documented systems)
  Use platform conventions (app feels familiar → less training needed)
  Don't design for planned obsolescence (features that expire artificially)
  Version gracefully (don't break old URLs, old API versions)
```

### Measuring Digital Carbon

```
Tools:
  Website Carbon Calculator (websitecarbon.com): Estimates CO₂ per page view
  Ecograder: Page weight, performance, and sustainability score
  Chrome DevTools Network panel: Total page weight in KB/MB
  Lighthouse: Performance score → correlates with energy efficiency

Targets:
  Page weight (web): < 1MB per page load (< 500KB is excellent)
  Time to interactive: < 3 seconds on 3G (less time loading = less energy)
  Requests: Fewer HTTP requests (bundle, cache, sprite)
```

### Sustainable Design Checklist

```
Images:
  ✅ WebP format used (30–35% smaller than PNG/JPEG same quality)
  ✅ Images sized correctly for their display dimensions (no 2×-too-large images)
  ✅ Lazy loading below the fold
  ✅ Appropriate quality (80% JPEG quality is usually sufficient)

Fonts:
  ✅ System fonts used where brand allows (no network request)
  ✅ Variable fonts instead of multiple weight files
  ✅ Font subsetting (only load characters actually used)
  ✅ Font-display: swap (text visible while font loads)

Code/performance:
  ✅ JS bundle size minimized (tree shaking, code splitting)
  ✅ Animations use transform/opacity (GPU, not CPU)
  ✅ No third-party scripts without purpose review
  ✅ Caching headers set correctly

Content decisions:
  ✅ Video used only when genuinely necessary (not as decoration)
  ✅ Autoplay video disabled by default
  ✅ Dark mode option provided (OLED energy benefit)
  ✅ Infinite scroll avoided where pagination would serve as well
```

### Outputs
- Carbon footprint estimate (websitecarbon.com baseline)
- Page weight audit (target < 1MB)
- Image optimization specification
- Sustainability score improvement roadmap

---

## 5. Service Design

**Purpose:** Map and design the complete experience of a service — including all customer touchpoints, backstage processes, and support systems — to create coherent, human-centered service experiences.

**When to use:** When a user's problem spans multiple channels (app, email, phone, in-person); when designing a new end-to-end product or service; when identifying the root cause of service failures.

### Service Design vs. UX Design

```
UX Design: Focuses on individual touchpoints (screens, flows, interactions).
           "How does this registration screen work?"

Service Design: Maps the entire journey across all touchpoints and backstage.
               "What happens before, during, and after the user registers?"
               Includes: Email notifications, support interactions, renewal process,
               offboarding, internal operations that affect the user experience.
```

### Service Blueprint

```
A service blueprint maps the end-to-end service across 4 layers:

Customer actions (top):
  Everything the customer does: decides to try, signs up, connects exchange, views dashboard, cancels.

Frontstage (touchpoints):
  Everything the customer directly sees/uses: app, website, emails, notifications.
  Line of interaction: separates customer from frontstage.

Backstage (support processes):
  Actions done by the company that the customer doesn't see but that directly support the interaction.
  Examples: Email delivery, exchange API polling, portfolio calculation, support ticket routing.
  Line of visibility: separates frontstage from backstage.

Support processes (infrastructure):
  Systems and tools that support backstage processes.
  Examples: Exchange APIs, database, payment processor, email service provider.

For each touchpoint, document:
  Customer goal at this moment
  What the customer sees/experiences
  Backend process that supports this
  Failure points and their impact
  Opportunities for improvement
```

### Key Service Design Artifacts

**Customer journey map:**
```
Focuses on the customer's experience over time.
Includes: Touchpoints, emotions (satisfaction curve), pain points, opportunities.
Scope: One journey (e.g., onboarding, resolving an issue) from start to end.

Columns (stages): Awareness → Consider → Sign up → Onboard → Use → Loyal/Advocate
Rows:
  Customer actions: What they do
  Thoughts: What they're thinking
  Emotions: Emotional curve (high/low)
  Touchpoints: Which channels at this moment
  Pain points: What's frustrating
  Opportunities: How to improve
```

**Ecosystem map:**
```
Who are all the actors in this service?
  User, company, partner (exchange APIs), payment processor, support team, etc.

How do they interact?
  Lines between actors show data/value flows

Use for: Understanding dependencies, identifying external parties that affect experience.
```

**Moments of truth:**
```
Critical moments where the service succeeds or fails decisively.
For Nexus:
  1. First portfolio view: Did it load correctly? Does it show real data?
  2. Price alert trigger: Did the notification arrive timely and accurately?
  3. Support contact: Did the user get a helpful response in time?
  4. Renewal: Was the billing expected, transparent, and fair?

Design these moments with extra care — they define long-term loyalty or churn.
```

### Service Failure Design

```
Service failures are inevitable — the design determines whether they destroy trust or rebuild it.

Recovery principles:
  1. Acknowledge quickly: Don't leave users in the dark
  2. Explain honestly: What happened, why, how long it will take
  3. Compensate proportionately: For significant failures, offer something
  4. Prevent recurrence: Fix the root cause, communicate the fix
  5. Follow up: Tell users when the issue is resolved

Status page design:
  Accessible URL: status.yourapp.com
  Incident levels: Operational, Degraded performance, Partial outage, Major outage
  Real-time updates (not a stale "all systems operational" page)
  Historical uptime (builds trust over time)

In-app failure communication:
  Don't show: Raw error codes or stack traces
  Do show: Plain English explanation + what the user can do
  Example: "We're having trouble reaching Binance right now.
           Your last sync was 14 minutes ago. We'll retry automatically."
```

### Outputs
- Service blueprint (full end-to-end map)
- Customer journey map (key journey)
- Moments of truth identification + design priority
- Service failure communication templates (in-app + email)

---

## 6. Design Thinking Facilitation

**Purpose:** Guide teams through structured problem-solving processes — creating shared understanding, generating ideas, and aligning on solutions through facilitated collaborative sessions.

**When to use:** Starting a new product or feature from scratch; teams are stuck and need fresh perspective; stakeholders need alignment; a problem needs divergent thinking before converging on a solution.

### Design Thinking Process

```
Empathize → Define → Ideate → Prototype → Test

Empathize:  Understand the people you're designing for (research, observation)
Define:     Synthesize research into a clear problem statement
Ideate:     Generate many ideas (quantity over quality at this stage)
Prototype:  Build cheap, fast representations of ideas
Test:       Get user feedback on prototypes (back to Empathize with learnings)

This is not linear — it's iterative.
Teams often loop back: testing reveals new empathy gaps; defining clarifies ideation.
```

### The Problem Statement (How Might We)

```
Format: "How might we [help user] [do goal] so that [outcome]?"

Examples:
  "How might we help crypto investors see their total portfolio value
   so that they don't have to manually check 3 exchanges?"

  "How might we help new users connect their first exchange
   so that they experience value within their first session?"

Rules for good HMW statements:
  Too broad:  "How might we improve crypto investing?" (not actionable)
  Too narrow: "How might we add a dark mode toggle?" (solves itself)
  Just right: Specific enough to guide ideation, open enough to allow creativity

Generate 5–10 HMW statements from research findings.
Vote on which to prioritize for the ideation session.
```

### Facilitation Techniques

**Warm-up exercises:**
```
30 circles (5 min):
  Each participant has a sheet with 30 empty circles.
  Draw something in as many circles as possible in 5 minutes.
  Purpose: Breaks "perfect first try" thinking; gets creativity flowing.

Worst possible idea (5 min):
  Brainstorm the WORST possible solution to the problem.
  Then reverse each bad idea into a potentially good one.
  Purpose: Reduces inhibition; often generates real insights.
```

**Brainstorming:**
```
Rules for effective brainstorming:
  Defer judgment: No criticism during generation (even "that won't work")
  Quantity over quality: More ideas = higher chance of a great one
  Encourage wild ideas: Extreme ideas can be tamed; safe ideas can't be made bold
  Build on others' ideas: "Yes, and..." not "Yes, but..."
  Stay focused: One person talks at a time (in verbal brainstorms)

Silent brainstorm (recommended for mixed-seniority groups):
  Everyone writes ideas individually on sticky notes (5–10 min)
  Share and cluster together
  Prevents HiPPO effect (Highest Paid Person's Opinion dominating)

Crazy 8s:
  Fold paper into 8 squares → sketch 8 interface ideas in 8 minutes
  Forces rapid generation, prevents over-investment in one idea
  Share and get dot votes on most interesting elements
```

**Voting and prioritization:**
```
Dot voting:
  Each participant gets 3–5 dots (sticky dots or drawn marks)
  Place dots on the ideas they find most promising
  Ideas with most votes float to top for discussion

Impact/effort matrix:
  Draw a 2×2 grid: Impact (low/high) on Y-axis, Effort (low/high) on X-axis
  Place ideas as sticky notes on the grid
  Prioritize: High impact, low effort = do first
              High impact, high effort = schedule for later
              Low impact, low effort = maybe
              Low impact, high effort = avoid

NUF test (Novel, Useful, Feasible):
  Rate each shortlisted idea 1–10 on each dimension
  Total score guides prioritization
```

**Storyboarding:**
```
Quick illustration of a user scenario (like a comic strip):
  6–8 panels showing: Before, trigger, the solution, the moment of value, after.
  Stick figures are perfect — this is about storytelling, not illustration.
  Purpose: Tests narrative coherence before building a prototype.
```

### Running a Design Sprint (5-Day Format)

```
Day 1 — Map (Monday):
  Long-term goal + sprint questions + how-might-we notes
  Map the customer journey
  Ask the experts (lightning talks from PM, engineer, support)
  Pick a target: which moment to focus on

Day 2 — Sketch (Tuesday):
  Lightning demos: competitors and inspiration (3 min each)
  Crazy 8s individual ideation
  Solution sketches (detailed, one idea per person)

Day 3 — Decide (Wednesday):
  "Art museum" display of all solution sketches
  Heatmap voting (sticky dots) in silence
  Speed critique: discuss top ideas
  Storyboard: 15-panel step-by-step plan for prototype

Day 4 — Prototype (Thursday):
  Build a realistic-looking prototype (Figma or simple webpage)
  Goal: Enough fidelity to get honest reactions from users
  Divide roles: Maker, writer, stitcher, interviewer

Day 5 — Test (Friday):
  5 user interviews (1 hour each, ~5 participants)
  Observe remotely; take notes
  Debrief: themes that emerged, what worked, what didn't

Rules:
  No phones/laptops in sprint (except Friday)
  Decisions by the Decider (not consensus)
  Time-box everything — done is better than perfect
```

### Remote Facilitation Adaptations

```
Tools:
  FigJam / Miro / MURAL: Virtual whiteboards (replace physical sticky notes)
  Loom: Pre-recorded presentations replace in-person talks
  Video call (breakout rooms): Small group brainstorms

Adjustments:
  Sessions max 90 min (vs. 4 hours in-person — video fatigue)
  More frequent breaks (10 min break every 60 min)
  Shorter activities: 3-minute brainstorm instead of 5
  Async beforehand: Share research and context before the session
  Camera on is requested (not required) — read the room

Remote-specific structures:
  Use timer visible to all (timeanddate.com timer in screen share)
  Assign a "chat monitor" to watch for contributions in chat
  Rotate who speaks first (prevents same voices dominating)
```

### Outputs
- Problem statement (HMW) + sprint question
- Ideation output (clustered sticky notes by theme)
- Prioritized concept list (dot vote results + impact/effort)
- Prototype brief (what to build and why)
- Research plan for testing (5 participants, key questions)
