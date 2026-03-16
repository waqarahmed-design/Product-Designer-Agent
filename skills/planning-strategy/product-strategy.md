# Product Strategy Methods

## Table of Contents
1. [Problem Definition](#1-problem-definition)
2. [Opportunity Assessment](#2-opportunity-assessment)
3. [Feature Prioritization](#3-feature-prioritization)
4. [Roadmap Planning](#4-roadmap-planning)
5. [Success Metrics Definition](#5-success-metrics-definition)
6. [Value Proposition Design](#6-value-proposition-design)

---

## 1. Problem Definition

**Purpose:** Articulate the problem clearly enough that the right solution becomes obvious — and the wrong solutions stop being considered.

**When to use:** Before any design work begins. A poorly defined problem guarantees a poorly designed solution.

### Problem Statement Format

```
[User/customer type]
experiences [problem/friction/unmet need]
when [context/situation]
because [root cause].
This results in [consequence for the user or business].
```

**Weak:** "Users don't use the dashboard enough."
**Strong:** "Power users who manage multiple projects experience information overload when they log in each morning because the dashboard shows all activity regardless of relevance — so they learn to ignore it, missing time-sensitive items."

### Problem Framing Techniques

**5 Whys** — Dig to root cause, not symptoms:
```
Why do users abandon the checkout? → They're surprised by shipping costs
Why are they surprised? → Costs aren't shown until the final step
Why aren't they shown earlier? → The system calculates them late
Why does it calculate late? → Legacy API requires a complete address first
Why hasn't this been fixed? → No one has owned this problem
```

**How Might We (HMW)** — Reframe problems as opportunities:
- Problem: "Users can't find past orders"
- HMW: "How might we help users re-find something they bought before?"
- HMW: "How might we make order history feel more like a personal shopping record?"

**Problem vs. Solution framing check:**
- Problem: "Users need to see their order history" ✅
- Solution disguised as problem: "Users need a search bar in order history" ❌

### Problem Validation Checklist
- [ ] Is this a real problem (evidence from research, not assumption)?
- [ ] Is it a problem worth solving (frequency × severity × addressability)?
- [ ] Is it our problem to solve (in scope, aligned with business)?
- [ ] Have we separated problem from solution?
- [ ] Do stakeholders and team agree on this framing?

### Outputs
- 1–3 problem statements with supporting evidence
- HMW reframes for ideation
- Clear articulation of what's out of scope

---

## 2. Opportunity Assessment

**Purpose:** Identify and prioritize which problems or user needs represent the best design and business opportunities to pursue.

**When to use:** When multiple problems have been identified, before committing to a direction.

### Opportunity Scoring Matrix

Score each opportunity on these dimensions (1–5 scale):

| Dimension | Question |
|-----------|----------|
| **User impact** | How significantly does solving this improve the user's life? |
| **Business value** | How much does solving this contribute to business goals? |
| **Frequency** | How often do users encounter this problem? |
| **Feasibility** | How technically and organizationally achievable is a solution? |
| **Strategic fit** | How well does this align with where the product is headed? |
| **Differentiation** | Does solving this create competitive advantage? |

**Opportunity Score** = (User Impact × Frequency) + Business Value + Strategic Fit − (5 − Feasibility)

### Opportunity Sizing

For each candidate opportunity, estimate:
- **Addressable users** — how many users have this problem?
- **Current workaround cost** — what do users do instead, and what does it cost them?
- **Business upside** — conversion, retention, expansion revenue impact
- **Investment** — rough estimate of design + engineering effort

### Prioritization Output: Opportunity Canvas

```
Opportunity: [Short name]
Problem it solves: [1 sentence]
Evidence: [Research sources]
Users affected: [Segment + rough count]
Business impact: [Metric it moves + estimated magnitude]
Effort: [S / M / L / XL]
Score: [Calculated]
Recommended: [Pursue now / Next quarter / Watch / Deprioritize]
Rationale: [2-3 sentences]
```

### Outputs
- Ranked list of opportunities with scores and rationale
- Recommended focus areas for the quarter
- Opportunities explicitly deprioritized (with reasons — prevents revisiting)

---

## 3. Feature Prioritization

**Purpose:** Decide which features or improvements to build, in which order, using structured frameworks rather than gut feel or loudest voice.

**When to use:** Backlog grooming, quarterly planning, when the roadmap has more ideas than capacity.

### RICE Framework

**R**each × **I**mpact × **C**onfidence ÷ **E**ffort

| Factor | Definition | Scale |
|--------|------------|-------|
| Reach | Users affected per quarter | # of users |
| Impact | Effect on goal per user | 3=massive, 2=high, 1=medium, 0.5=low, 0.25=minimal |
| Confidence | How sure are you about estimates | 100%=high, 80%=medium, 50%=low |
| Effort | Person-months of work | # of person-months |

**RICE Score** = (Reach × Impact × Confidence) / Effort

Best for: Data-rich teams with enough users to estimate reach reliably.

### MoSCoW Framework

| Category | Definition | Guideline |
|----------|------------|-----------|
| **Must have** | Non-negotiable for launch; product fails without it | ≤60% of scope |
| **Should have** | High value; workaround exists but is painful | ~20% of scope |
| **Could have** | Nice to have; low impact if absent | ~20% of scope |
| **Won't have** | Explicitly out of scope this cycle | Document to prevent scope creep |

Best for: Scoping releases, managing stakeholder expectations, MVP definition.

**Critical rule:** "Must have" list always expands under pressure. Enforce the 60% cap ruthlessly — every new Must Have requires removing another.

### Kano Model

Classify features by how they affect satisfaction:

| Type | Description | Effect |
|------|-------------|--------|
| **Basic (Must-be)** | Expected — absence causes dissatisfaction, presence is neutral | Fix these first |
| **Performance** | More = better satisfaction, less = less | Invest proportionally |
| **Delighter (Excitement)** | Unexpected — presence delights, absence doesn't disappoint | These differentiate |
| **Indifferent** | Users don't care either way | Deprioritize |
| **Reverse** | Some users want it, others don't | Segment carefully |

Survey question pair per feature:
- Functional: "If this feature exists, how do you feel?" (Love it / Expect it / Neutral / Dislike it / Can live with it)
- Dysfunctional: "If this feature does NOT exist, how do you feel?" (same options)

Best for: Feature discovery, identifying delighters that create competitive moat.

### Prioritization Decision Table

| Use when... | Framework |
|-------------|-----------|
| You have usage data and want objective ranking | RICE |
| You're scoping a release or MVP | MoSCoW |
| You want to understand user delight vs. expectation | Kano |
| You need fast team alignment without data | MoSCoW (workshop) |
| You're deciding between qualitatively similar features | Kano |

### Outputs
- Ranked backlog with scores and framework used
- Explicit "won't do" list with reasons
- Next sprint or quarter scope defined

---

## 4. Roadmap Planning

**Purpose:** Communicate the design team's direction and planned work over time, aligned to business goals.

**When to use:** Quarterly planning, new project kickoff, when stakeholders need visibility into design work.

### Roadmap Levels

| Level | Horizon | Audience | Detail |
|-------|---------|----------|--------|
| **Strategy roadmap** | 12–18 months | Executives, board | Themes and goals, no features |
| **Product roadmap** | 3–6 months | Product, engineering, design | Initiatives and epics |
| **Design roadmap** | 4–8 weeks | Design team, PMs | Specific design tasks and deliverables |

### Roadmap Structure (Now / Next / Later)

```
NOW (current quarter — committed)
  Initiative: [Name]
  Goal: [What outcome we're driving]
  Design work: [Specific deliverables]
  Status: [In progress / Starting / Done]

NEXT (following quarter — planned)
  Initiative: [Name]
  Goal: [What outcome we're driving]
  Dependencies: [What must happen first]
  Confidence: [High / Medium / Low]

LATER (future — directional)
  Theme: [Broad area of focus]
  Rationale: [Why this matters when we get there]
  Open questions: [What we need to learn before committing]
```

### Roadmap Design Principles
- **Outcomes, not features** — "Reduce checkout abandonment by 15%" not "Add progress bar to checkout"
- **Show confidence levels** — Later items are directional, not committed
- **Include design debt** — Accessibility fixes, design system work, and research deserve explicit slots
- **Date ranges, not exact dates** — "Q3" is more honest than "August 14th" for anything beyond 6 weeks
- **Tie to company OKRs** — Every roadmap item should connect to a business objective

### Outputs
- Now/Next/Later roadmap document
- Quarterly design commitment with deliverables
- Stakeholder-facing summary (stripped of implementation detail)

---

## 5. Success Metrics Definition

**Purpose:** Establish measurable criteria that tell you whether a design decision is working — before you build it.

**When to use:** At the start of any feature or project, before design begins.

### Metric Hierarchy

```
Business metric (lagging)
  └── Product metric (leading)
        └── Feature metric (proximate)
              └── Interaction metric (immediate)

Example:
  Revenue growth
    └── Paid conversion rate
          └── Trial-to-paid conversion in onboarding flow
                └── Completion rate of setup wizard
```

Design work most directly influences interaction and feature metrics. Connect them explicitly to business metrics to earn organizational buy-in.

### Metric Types

| Type | Definition | Examples |
|------|------------|---------|
| **Completion** | Did users finish the task? | Task completion rate, funnel step completion |
| **Efficiency** | How quickly / with how little effort? | Time on task, clicks to complete, error rate |
| **Engagement** | Are users coming back and going deeper? | DAU/MAU, feature adoption rate, session depth |
| **Satisfaction** | Do users feel good about the experience? | CSAT, NPS, SUS score |
| **Business** | Is value being created? | Conversion rate, churn rate, revenue per user |

### OKR Format for Design

```
Objective: [Qualitative direction — what we're trying to improve]

Key Result 1: [Metric] from [baseline] to [target] by [date]
Key Result 2: [Metric] from [baseline] to [target] by [date]
Key Result 3: [Metric] from [baseline] to [target] by [date]
```

**Example:**
```
Objective: Make onboarding feel effortless for new users

KR1: Setup completion rate from 54% → 75% by end of Q3
KR2: Time to first meaningful action from 8 min → 4 min
KR3: Day-7 retention for onboarded users from 31% → 42%
```

### Guardrail Metrics

For every target metric, define a guardrail — a metric that must NOT get worse:
- If optimizing for sign-up conversion → guardrail: don't reduce 7-day retention
- If optimizing for feature adoption → guardrail: don't increase support ticket volume

### Outputs
- 2–4 key metrics with baselines and targets
- Guardrail metrics
- Measurement plan (how/when will you check these?)

---

## 6. Value Proposition Design

**Purpose:** Articulate why users would choose your product over alternatives — and ensure design decisions reinforce that proposition.

**When to use:** New product/feature launch, positioning work, when user acquisition or retention is struggling.

### Value Proposition Canvas

Two sides that must fit together:

```
CUSTOMER PROFILE (what exists)           VALUE MAP (what you offer)
┌─────────────────────────────┐         ┌─────────────────────────────┐
│ Customer Jobs                │         │ Products & Services          │
│ What they're trying to do   │ ◄──────► │ What you actually offer      │
│                              │         │                              │
│ Pains                        │         │ Pain Relievers               │
│ Frustrations, risks,         │ ◄──────► │ How you address specific     │
│ obstacles                    │         │ customer pains               │
│                              │         │                              │
│ Gains                        │         │ Gain Creators                │
│ Desired outcomes, benefits,  │ ◄──────► │ How you produce outcomes     │
│ aspirations                  │         │ customers want               │
└─────────────────────────────┘         └─────────────────────────────┘
```

**Fit** = your Pain Relievers address real Pains, and your Gain Creators produce desired Gains.

### Value Proposition Statement

```
For [target customer]
who [has this job/problem/need],
[product name] is a [product category]
that [key benefit / problem it solves].
Unlike [alternative/competitor],
our product [key differentiator].
```

### Design Implications of Value Proposition

Every value prop creates design obligations:

| Value Prop Claims... | Design Must... |
|---------------------|----------------|
| "Saves you time" | Minimize steps, show time saved, make speed visible |
| "Gives you control" | Surface settings, provide undo, show what changed |
| "Keeps you informed" | Make notifications meaningful, show data at a glance |
| "Earns your trust" | Show credentials, explain data use, make errors honest |
| "Works everywhere" | Prioritize cross-device, handle offline gracefully |

### Validation Questions
- Can a user explain the value proposition after 60 seconds in the product?
- Does the hero screen (first screen after login) deliver on the primary value prop?
- Are the three most-used features the ones that most directly deliver the core value?

### Outputs
- Completed Value Proposition Canvas
- Value proposition statement (1–2 sentences)
- Design obligations list derived from the proposition
