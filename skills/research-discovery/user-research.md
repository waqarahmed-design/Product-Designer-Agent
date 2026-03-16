# User Research Methods

## Table of Contents
1. [User Interviews](#1-user-interviews)
2. [Usability Testing](#2-usability-testing)
3. [Ethnographic Research](#3-ethnographic-research)
4. [Survey Design](#4-survey-design)
5. [A/B Testing](#5-ab-testing)
6. [Analytics Interpretation](#6-analytics-interpretation)
7. [Persona Development](#7-persona-development)
8. [Journey Mapping](#8-journey-mapping)
9. [Empathy Mapping](#9-empathy-mapping)
10. [Competitive Analysis](#10-competitive-analysis)

---

## 1. User Interviews

**Purpose:** Understand user needs, motivations, behaviors, and mental models in depth.

**When to use:** Early discovery, before designing solutions, when quantitative data lacks context.

### Interview Guide Structure

```
1. Warm-up (5 min)
   - "Tell me a little about yourself and what you do."

2. Context (10 min)
   - "Walk me through how you currently [do the task]."
   - "What tools or methods do you use?"

3. Core topics (25 min)
   - "Tell me about the last time you [did X]. What happened?"
   - "What was frustrating about that experience?"
   - "What would have made it easier?"

4. Probing patterns
   - "Can you tell me more about that?"
   - "Why did you do it that way?"
   - "What did you mean by [term]?"
   - "What happened next?"

5. Wrap-up (5 min)
   - "Is there anything else you'd like to share?"
   - "If you could change one thing, what would it be?"
```

### Key Rules
- Ask about past behavior, not hypothetical future behavior ("Tell me about a time..." not "Would you...?")
- Never ask leading questions — "Did you find that frustrating?" → "How did you feel about that?"
- Silence is productive — wait 3–5 seconds after an answer before responding
- Recruit 5–8 participants per segment; patterns emerge within 5 interviews

### Outputs
- Interview transcripts or notes
- Key quotes organized by theme
- Feed into Affinity Mapping and Empathy Mapping

---

## 2. Usability Testing

**Purpose:** Observe users attempting real tasks to identify where a design succeeds or fails.

**When to use:** Before launch, after major design changes, when NPS or support tickets signal confusion.

### Test Plan Template

```
Study: [Feature or flow being tested]
Goal: Identify [X] usability issues with [Y] flow
Participants: [N] users matching [persona criteria]
Method: [Moderated remote / Unmoderated / In-person]
Tasks: [list below]
Success metrics: Task completion rate, time on task, error count
```

### Writing Good Tasks

**Bad:** "Find the settings page and change your notification preferences."
*(Tells users where to go and what to call it)*

**Good:** "You've been getting too many emails from the app. What would you do?"
*(Scenario-based, uses user language, doesn't reveal the path)*

### Task Observation Framework

For each task, note:
- **Did they complete it?** (yes / no / partial)
- **Time taken**
- **Errors or wrong turns**
- **Think-aloud quotes** (what they said)
- **Observations** (what they did, facial expressions, hesitations)

### Severity Rating

| Rating | Criteria |
|--------|----------|
| 4 — Critical | Task impossible; users give up |
| 3 — Serious | Major difficulty; most users struggle |
| 2 — Moderate | Some difficulty; some users struggle |
| 1 — Minor | Small annoyance; most users succeed |
| 0 — Not an issue | Observed but doesn't affect success |

### Outputs
- List of usability issues ranked by severity
- Video clips of key failure moments
- Recommendations per issue

---

## 3. Ethnographic Research

**Purpose:** Observe users in their real environment to understand context, workarounds, and behaviors that users can't self-report.

**When to use:** When context matters (physical environment, social dynamics, interruptions), when users say one thing but do another.

### Observation Guide

```
Before visiting:
- Define what behaviors/artifacts to look for
- Get consent and explain you're observing, not evaluating them

During observation:
- Watch, don't direct — "I'm here to learn from you, not to test you"
- Note the environment (lighting, noise, devices, desk setup)
- Note workarounds ("I always do this extra step because...")
- Photograph artifacts (sticky notes, physical tools, paper forms)
- Ask "naive" questions: "Why do you do it that way?"

Field note categories:
- Actions (what they physically did)
- Context (environment, tools, interruptions)
- Quotes (exact words used)
- Interpretations (your inferences — mark clearly as [I])
```

### Key Insight Types to Look For
- **Workarounds** — extra steps users add to compensate for missing features
- **Mental models** — how users conceptualize the system (often wrong in useful ways)
- **Vocabulary** — the actual words users use (critical for copy and navigation labels)
- **Environmental constraints** — noisy office, bad lighting, one-handed use, interruptions

### Outputs
- Field notes and photographs
- List of observed workarounds
- Vocabulary and terminology users actually use

---

## 4. Survey Design

**Purpose:** Gather quantitative feedback from a large number of users to identify trends and measure sentiment.

**When to use:** When you need statistical confidence, want to prioritize features by user demand, or need to segment findings across demographics.

### Question Types

| Type | Use For | Example |
|------|---------|---------|
| Likert scale (1–5/7) | Satisfaction, agreement | "How easy was it to complete this task?" |
| NPS (0–10) | Overall loyalty | "How likely are you to recommend?" |
| Multiple choice | Categorization | "Which of these describes your role?" |
| Ranking | Priority | "Rank these features by importance" |
| Open text | Depth, context | "What would you change about this feature?" |
| Matrix | Multiple items at once | Rate these 5 features on ease of use |

### Survey Design Rules
- **Start with easy questions** — demographics or simple multiple choice first
- **One concept per question** — "Was it fast and easy?" is two questions
- **Avoid double negatives** — "I do not disagree that..." confuses respondents
- **Provide a neutral option** — include "Neither agree nor disagree" on Likert scales
- **Keep it under 10 minutes** — response quality drops sharply after that
- **Test the survey first** — run it with 3 internal people before distributing

### Sample Size Guidelines

| Goal | Min. Sample |
|------|-------------|
| Directional trends | 50+ |
| Segment comparisons | 100+ per segment |
| Statistical significance | 200–400+ |
| NPS benchmark | 100+ |

### Outputs
- Quantitative findings with charts
- Open-text themes
- Segmented breakdowns by user type/behavior

---

## 5. A/B Testing

**Purpose:** Measure which of two design variants performs better on a defined metric.

**When to use:** When you have sufficient traffic (>1,000 sessions/week per variant), a clear success metric, and a testable hypothesis.

### Hypothesis Format

```
We believe that [change]
will result in [outcome]
for [user segment]
because [reasoning].

We'll know this is true when [metric] changes by [threshold]
over [duration] with [statistical confidence level].
```

**Example:**
> We believe that moving the CTA above the fold will result in higher sign-up conversions for first-time visitors because users will see it before scrolling. We'll know this is true when conversion rate increases by ≥5% over 2 weeks at 95% confidence.

### What Makes a Good A/B Test
- **One variable at a time** — changing multiple things makes results uninterpretable
- **Pre-define success metric** — don't look at data and then decide what counts
- **Calculate sample size before starting** — use a significance calculator; don't stop early
- **Run for full weeks** — capture weekday/weekend variation
- **Minimum detectable effect** — know what change is meaningful before you start

### Common Metrics
- Conversion rate (primary CTA clicks, sign-ups, purchases)
- Click-through rate
- Time on task
- Bounce rate
- Revenue per visitor

### Outputs
- Winning/losing variant with statistical significance
- Effect size (actual % change, not just "won")
- Segment breakdowns (did it win for all users or just some?)

---

## 6. Analytics Interpretation

**Purpose:** Extract behavioral insights from product data to understand what users do at scale.

**When to use:** Quantifying problem scope, identifying drop-off points, measuring feature adoption, before/after comparisons.

### Key Metrics to Analyze

| Metric | Tells You |
|--------|-----------|
| Funnel conversion rates | Where users drop off in a flow |
| Feature adoption rate | % of users who use a given feature |
| Session duration / depth | Engagement level |
| Retention cohorts | Whether users come back after Day 1/7/30 |
| Error/rage click events | Where users are frustrated |
| Search queries | What users look for but can't find |
| Exit pages | Where users leave the product |

### Analysis Framework

```
1. Define the question first
   "Why did sign-ups drop 20% last month?"

2. Form a hypothesis
   "The new sign-up form may be causing friction"

3. Find supporting/contradicting data
   - Funnel drop-off rates: where specifically did users leave?
   - Compare before/after the form change date
   - Segment by device (desktop vs. mobile form behavior)

4. Quantify the impact
   "Drop-off at email field went from 8% → 31% on mobile"

5. Generate design implications
   "Mobile keyboard may be obscuring the Continue button"
```

### Pitfalls to Avoid
- **Correlation ≠ causation** — users who use feature X are more retained, but X may not cause retention
- **Averages hide distribution** — an average session of 3 min may mean half are 30s and half are 6 min
- **Survivorship bias** — analytics only shows users who stayed; you're missing the ones who churned

### Outputs
- Annotated funnel or flow with drop-off rates
- Prioritized list of friction points
- Hypotheses for qualitative follow-up

---

## 7. Persona Development

**Purpose:** Create representative composite user archetypes from research data to align teams on who they're designing for.

**When to use:** After gathering qualitative and quantitative research, when team alignment on users is weak.

### Persona Template

```
[Name] — [Role/Archetype label]

Photo: [stock photo for humanization]

Quote: "One sentence that captures their worldview or core frustration."

Demographics
- Age, role, location, tech comfort level

Goals
- Primary goal (what they ultimately want to achieve)
- Secondary goals

Frustrations / Pain Points
- What currently fails them
- Workarounds they use

Behaviors
- How they currently do the thing you're designing for
- Tools and channels they use
- Frequency of use

Motivations
- What drives their decisions

Needs from your product
- What the product must do for them
```

### Rules for Good Personas
- **Data-driven, not assumed** — each trait should trace back to research (interview quotes, survey data)
- **Behavioral, not demographic** — "Power users who batch-process" is more useful than "35-year-old male"
- **2–4 max** — more than 4 personas are rarely all used in design decisions
- **Mark which is primary** — design decisions should optimize for the primary persona first

### Outputs
- 2–4 persona documents
- A primary persona designation
- Team alignment on "who we're designing for"

---

## 8. Journey Mapping

**Purpose:** Document the end-to-end experience a user has with a product or service to identify pain points and opportunities.

**When to use:** When problems span multiple touchpoints, when teams are siloed and lose sight of the full user experience.

### Journey Map Structure

```
Columns: Stages across the top (Awareness → Consideration → Onboarding → Use → Renewal)

Rows for each stage:
  User Actions    — what the user does
  Touchpoints     — which channels/surfaces they interact with
  Thoughts        — what they're thinking ("Is this secure?")
  Emotions        — how they feel (plot as a curve: frustrated, neutral, delighted)
  Pain Points     — specific friction in this stage
  Opportunities   — design interventions that could improve this stage
```

### Building the Map

1. **Scope the journey** — define start and end points (first ad impression → 90-day retained user)
2. **Source from research** — use interview data and analytics, not assumptions
3. **Map current state first** — document reality before ideating improvements
4. **Identify the emotional low points** — these are your highest-priority design opportunities
5. **Create a future-state version** — show how the journey looks after your design interventions

### Outputs
- Current-state journey map
- Identified pain points ranked by severity
- Opportunity areas for design

---

## 9. Empathy Mapping

**Purpose:** Synthesize research into a shared understanding of a user's thoughts, feelings, actions, and environment.

**When to use:** After interviews or observations, before ideation, to build team empathy for users.

### Empathy Map Quadrants

```
┌─────────────────┬─────────────────┐
│    THINKS       │     FEELS       │
│                 │                 │
│ What occupies   │ What emotions   │
│ their mind?     │ do they have?   │
│ Worries,        │ Fears, hopes,   │
│ beliefs, goals  │ frustrations    │
├─────────────────┼─────────────────┤
│    SAYS         │     DOES        │
│                 │                 │
│ Exact quotes    │ Observable      │
│ from research   │ behaviors and   │
│                 │ actions         │
└─────────────────┴─────────────────┘

Below the quadrants:
PAINS    — frustrations, obstacles, fears
GAINS    — wants, needs, measures of success
```

### How to Run an Empathy Mapping Session

1. Share research findings with the team (quotes, observations)
2. Each person writes one insight per sticky note
3. Place notes in the relevant quadrant
4. Cluster and discuss as a group
5. Identify tensions — things users say vs. do that contradict each other
6. Synthesize into pains and gains

### Outputs
- Completed empathy map for each key persona
- Identified tensions between says/does
- Input for persona development and ideation

---

## 10. Competitive Analysis

**Purpose:** Research competitor and analogous products to understand market conventions, gaps, and differentiation opportunities.

**When to use:** Early in a new product/feature, when evaluating positioning, when users complain about competitors.

### Analysis Framework

```
For each competitor:
  Product overview     — what it does, who it's for, pricing
  Key features         — what they do well
  UX patterns          — how they handle [the flow you're designing]
  Strengths            — where they lead
  Weaknesses           — where they fall short
  Differentiators      — what makes them distinctive
```

### Evaluation Dimensions

| Dimension | What to Look For |
|-----------|-----------------|
| Onboarding | Time to first value, setup friction |
| Core flow | How they solve the same problem you're solving |
| Information architecture | How they organize navigation |
| Visual design | Style, tone, quality |
| Mobile experience | Responsiveness, native app quality |
| Copy & messaging | Language, tone, clarity |
| Empty states | How they handle zero data |
| Error handling | How they communicate failures |
| Pricing & packaging | How they structure tiers |

### Analogous Inspiration

Beyond direct competitors, study products that solve similar problems in different domains:
- Designing a file organization system? Study how Spotify organizes playlists.
- Designing a financial dashboard? Study how weather apps present complex multi-variable data.

### Outputs
- Competitive matrix (feature comparison table)
- UX pattern inventory (screenshots annotated with observations)
- Gaps and opportunities specific to your product
