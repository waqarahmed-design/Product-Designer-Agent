# Project Planning Methods

## Table of Contents
1. [Design Scoping](#1-design-scoping)
2. [Resource Planning](#2-resource-planning)
3. [Risk Assessment](#3-risk-assessment)
4. [Design Sprint Facilitation](#4-design-sprint-facilitation)
5. [Workshop Facilitation](#5-workshop-facilitation)

---

## 1. Design Scoping

**Purpose:** Estimate the effort, timeline, and deliverables for design work so the team can plan realistically and stakeholders can set expectations.

**When to use:** At the start of any project or feature, before committing to a timeline.

### Design Work Breakdown

Break design work into concrete deliverable types:

| Deliverable | Typical effort range |
|-------------|---------------------|
| Research plan + recruitment | 0.5–1 day |
| User interviews (per interview) | 2–3 hours |
| Research synthesis + report | 1–3 days |
| User flow diagram | 0.5–1 day |
| Wireframes (per screen) | 2–4 hours |
| High-fidelity mockups (per screen) | 4–8 hours |
| Interactive prototype | 1–3 days |
| Usability test (plan + run + report) | 3–5 days |
| Design system component | 4–8 hours |
| Handoff + dev support | 10–20% of design time |
| Stakeholder review rounds | 2–4 hours each |

### Scoping Template

```
Project: [Name]
Scope: [What's included and explicitly excluded]

Phase 1: Discovery (X days)
  - Stakeholder interviews: X sessions × Y hours
  - User interviews: X sessions × Y hours
  - Research synthesis: Z days

Phase 2: Definition (X days)
  - User flows: X screens
  - Wireframes: X screens
  - Review round 1: X hours

Phase 3: Design (X days)
  - High-fidelity mockups: X screens
  - Interactive prototype: Y flows
  - Review round 2: X hours

Phase 4: Validation (X days)
  - Usability testing: X sessions
  - Iteration based on findings: X days

Phase 5: Handoff (X days)
  - Spec documentation
  - Dev handoff sessions
  - QA support

Total: X weeks design time
Buffer (20%): Y days
Total with buffer: Z weeks
```

### Estimation Rules
- **Always add 20% buffer** — design almost always involves unexpected rounds of feedback
- **Scope complexity multipliers**: First-time design (1.5×), major redesign (1.3×), greenfield (1.4×), iteration (1.0×)
- **Account for review cycles** — each stakeholder review round = 2–4 hours design + meeting time
- **Never scope in isolation** — get PM and engineering estimates first to calibrate assumptions

### Scoping Conversations

Questions to ask before scoping:
- "How many stakeholders need to approve the design?"
- "How defined is the problem — do we need discovery or is it already known?"
- "Are there existing patterns/components we can reuse or is this greenfield?"
- "How much design debt or accessibility work is bundled in?"
- "What's the deadline and how firm is it?"

### Outputs
- Phased work breakdown with effort estimates
- Explicit list of what's in and out of scope
- Risk flags that could affect the estimate

---

## 2. Resource Planning

**Purpose:** Coordinate the right people, skills, and time to deliver design work effectively across functions.

**When to use:** Starting a new project, when team capacity is constrained, when cross-functional coordination is needed.

### RACI Matrix

Define who is Responsible, Accountable, Consulted, and Informed for each decision:

```
                        Designer  PM    Eng   Research  Exec
Problem definition         R       A      C       C       I
Research plan              A       C      I       R       I
Design direction           R       C      C       I       A
Technical feasibility      I       C      A       I       I
Final design approval      C       C      I       I       A
Engineering handoff        R       C      A       I       I
Launch decision            I       A      C       I       R
```

R = Responsible (does the work)
A = Accountable (owns the outcome, final decision)
C = Consulted (input needed, two-way communication)
I = Informed (kept updated, one-way communication)

**Rule:** Every decision should have exactly one Accountable. Multiple A's cause gridlock.

### Capacity Planning

```
Designer weekly capacity:
  Total hours: 40
  Meetings/admin: −8 hours
  Unplanned work/interruptions: −4 hours
  Available for project work: 28 hours/week

For a project requiring 200 design hours:
  At 28h/week = ~7 weeks calendar time
  Add 20% buffer = ~8.5 weeks
  With 2 designers: ~4–5 weeks
```

### Cross-functional Touchpoints

Design typically needs input from:

| Function | When | What for |
|----------|------|----------|
| **Engineering** | Early discovery | Feasibility check, API constraints |
| **Engineering** | Wireframes complete | Technical review before hi-fi investment |
| **PM** | Continuously | Problem alignment, scope management |
| **Data/Analytics** | Pre-design | Baseline metrics, usage patterns |
| **Legal/Compliance** | Before final | Privacy, accessibility, regulatory review |
| **Marketing** | Brand touchpoints | Tone, messaging, visual alignment |
| **Customer Success** | Discovery | User pain point intel, support ticket themes |

### Onboarding Design Contributors

When bringing in additional designers:
```
Day 1: Product walkthrough + user research review
Day 2: Design system orientation + component library tour
Day 3: Stakeholder context + team norms
Week 1: Shadow reviews, no independent decisions
Week 2+: Paired work, then independent with review
```

### Outputs
- RACI matrix for the project
- Capacity plan with designer allocation
- Cross-functional meeting cadence
- Onboarding plan for new contributors

---

## 3. Risk Assessment

**Purpose:** Identify threats to design quality, timeline, or adoption before they occur so the team can mitigate them proactively.

**When to use:** Project kickoff, at the start of each phase, before major commitments.

### Risk Categories

| Category | Examples |
|----------|---------|
| **Scope** | Requirements change mid-project, "just one more thing" requests |
| **Stakeholder** | Late stakeholder feedback, conflicting approvals, unavailable reviewers |
| **Technical** | Feasibility constraints discovered late, API limitations, platform restrictions |
| **Research** | Can't recruit users, research findings contradict existing direction |
| **Timeline** | Engineering dependencies delayed, hard launch dates with fixed scope |
| **Quality** | Insufficient testing time, accessibility not checked, design system debt |
| **Organizational** | Team changes mid-project, strategy pivot, budget cuts |

### Risk Register

```
Risk: [Short description]
Category: [Scope / Stakeholder / Technical / Research / Timeline / Quality / Org]
Likelihood: [High / Medium / Low]
Impact: [High / Medium / Low]
Priority: [Likelihood × Impact = H×H=Critical, H×M or M×H=High, etc.]
Mitigation: [What to do before it happens]
Contingency: [What to do if it happens anyway]
Owner: [Who monitors this risk]
```

### Common Design Risks + Mitigations

**"We discover technical constraints after hi-fi is complete"**
- Mitigation: Engineering feasibility review after wireframes, before investing in hi-fi
- Contingency: Wireframe-quality designs shipped as a "phase 1" while alternatives are explored

**"Stakeholder feedback arrives after development has started"**
- Mitigation: Mandatory sign-off gates before each phase; calendar stakeholder reviews at project start
- Contingency: Change control process — changes after sign-off require explicit scope negotiation

**"Usability testing reveals the design doesn't work"**
- Mitigation: Test low-fidelity prototypes early, before hi-fi investment
- Contingency: Time-boxed iteration sprint; identify which issues are critical vs. backlog

**"Design system components don't exist for what we need"**
- Mitigation: Audit design system at scoping phase; flag new component needs as project requirements
- Contingency: Build the component as part of the project with design system team involvement

**"Recruitment fails — can't get users to test with"**
- Mitigation: Start recruitment 2 weeks before testing is needed; have backup panel or guerrilla testing plan
- Contingency: Internal user proxies or expert review as a substitute

### Risk Review Cadence
- Full risk register review: at each phase gate
- Weekly: check top 3 priority risks for new developments
- Escalation trigger: any risk moves from Medium to High likelihood

### Outputs
- Risk register for the project
- Top 3 critical risks with mitigation plans
- Phase gate criteria (what must be true to move forward)

---

## 4. Design Sprint Facilitation

**Purpose:** Solve a focused design problem and validate a solution prototype with real users in 5 days, before committing to full design and development.

**When to use:** Stuck on a critical design problem, need to align diverse stakeholders on a direction, want to validate before major engineering investment.

### 5-Day Structure

**Monday — Map**
- Morning: Expert interviews (PM, Eng, CS, domain experts)
- Afternoon: Map the problem space, identify the critical moment to focus on
- Output: Sprint goal, target customer, target moment in the user journey

**Tuesday — Sketch**
- Morning: Lightning demos (5 min each — inspiration from analogous products)
- Afternoon: Individual sketching (4-step sketch: notes → ideas → crazy 8s → solution sketch)
- Output: 4 solution sketches per participant

**Wednesday — Decide**
- Morning: Sticky decision (silent review, heat map vote, speed critique, straw poll)
- Afternoon: Storyboard the winning concept (15–20 frames = the prototype script)
- Output: One clear concept to prototype; storyboard with every screen defined

**Thursday — Prototype**
- All day: Build a realistic-looking prototype (not a real product — just the facade)
- Tools: Figma, Keynote, or even printed screens
- Goal: "Goldilocks" fidelity — real enough that users react authentically, fake enough to build in one day
- Output: Testable prototype + interview guide

**Friday — Test**
- 5 user interviews × 60 minutes each
- Two-room setup: interviewer + participant in one room, team watching (live or recorded) in another
- Note patterns in real-time: look for moments of delight and confusion
- Output: Validated or invalidated concept with specific findings

### Sprint Facilitation Rules

- **Limit participants to 7** — larger groups slow decisions and dilute the work
- **Phones away during sprints** — distraction kills creative momentum
- **"How might we" notes** — capture problems heard in expert interviews as HMW opportunities
- **One decider** — identify the person with authority to make final calls before the sprint starts
- **Protect Thursday** — prototype day gets crushed if Wednesday runs over; keep Wednesday's decide phase time-boxed
- **No perfectionism on Friday** — 5 users is enough to see patterns; it's directional, not statistically valid

### When Not to Run a Sprint

- Problem isn't well-scoped yet (run discovery research first)
- No access to real users for Friday testing
- Team isn't co-located or able to commit full 5 days
- Solution is already decided (sprint becomes theater)

### Outputs
- Validated or invalidated prototype
- User testing insights with direct quotes
- Recommended next steps (invest, pivot, or kill)
- Sprint documentation for stakeholders who weren't present

---

## 5. Workshop Facilitation

**Purpose:** Lead structured collaborative sessions that produce specific outputs — alignment, ideas, decisions, or prioritization — from a group of participants.

**When to use:** Kickoff sessions, ideation workshops, retrospectives, alignment meetings, co-design sessions with stakeholders or users.

### Workshop Design Framework

Before any workshop, define:

```
Purpose: What decision or output must exist by the end?
Participants: Who needs to be in the room and why?
Duration: How long? (90 min max for ideation; 3 hours max for full-day)
Format: Remote / in-person / hybrid
Pre-work: What should participants do before arriving?
Outputs: What tangible artifacts leave the room?
```

### Common Workshop Activities

**Icebreaker (5–10 min)**
Keep it short and relevant. "Share one word that describes your biggest challenge with [topic]" is better than unrelated games.

**Rose / Thorn / Bud (10–15 min)**
Individual reflection before group discussion:
- Rose: What's working well?
- Thorn: What's a pain point or problem?
- Bud: What's an opportunity you see?

**How Might We (20–30 min)**
- Share research or problem context (5 min)
- Each person writes HMW questions on sticky notes (1 per note, 8–10 min)
- Group and dot-vote on the most important HMWs

**Crazy 8s (10 min)**
- Each person folds paper into 8 panels
- 1 minute per panel: sketch one idea
- Share and discuss — volume over quality, defer judgment

**Affinity Grouping (20–30 min)**
- Team silently reads all sticky notes
- Group into themes without discussion
- Name each cluster, then discuss as a group

**Dot Voting / Prioritization (10 min)**
- Each participant gets 3–5 votes (dots or digital equivalents)
- Vote on ideas, problems, or directions
- Discuss top-voted items; decider makes final call

**Retrospective: Start / Stop / Continue (30 min)**
- What should we start doing?
- What should we stop doing?
- What should we continue doing?
- Vote and commit to 1–3 actions with owners

### Facilitation Principles

- **Separate divergence from convergence** — never judge ideas while generating them
- **Timebox everything** — display a visible timer; keep energy up with pace
- **Silence before discussion** — give individuals 3–5 min to write before open discussion (prevents groupthink)
- **Capture everything** — someone takes notes and photographs throughout
- **End with clear commitments** — who does what by when; if no one owns it, it doesn't happen
- **Parking lot** — capture off-topic ideas separately so discussion stays focused

### Remote Facilitation Specifics
- Use Miro, FigJam, or Mural for collaborative digital boards
- Send pre-work 48 hours in advance (participants arrive with context)
- Assign a co-facilitator to manage chat and technical issues
- Build in 5-min breaks every 60 minutes
- Shorter, more frequent workshops beat 4-hour marathon remote sessions

### Outputs
- Workshop artifacts (affinity maps, prioritized ideas, decision records)
- Summary document with decisions made, ideas captured, and action items with owners
- Photos or digital export of all boards
