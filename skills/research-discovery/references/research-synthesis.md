# Research Synthesis Methods

## Table of Contents
1. [Affinity Mapping](#1-affinity-mapping)
2. [Insight Generation](#2-insight-generation)
3. [Stakeholder Interviews](#3-stakeholder-interviews)
4. [Jobs-to-be-Done Framework](#4-jobs-to-be-done-framework)
5. [Heuristic Evaluation](#5-heuristic-evaluation)

---

## 1. Affinity Mapping

**Purpose:** Organize raw research data (quotes, observations, facts) into emergent themes and patterns.

**When to use:** After interviews, usability tests, or any qualitative research session. Run before generating insights.

### Process

```
1. Capture raw data (post-it notes or digital cards)
   - One observation, quote, or fact per card
   - Use exact user language — don't interpret yet
   - Aim for 100–200 cards from 5–8 interviews

2. Sort silently
   - Team members move cards into groups without talking
   - No pre-defined categories — let themes emerge
   - Cards that don't fit anywhere stay isolated

3. Name the clusters
   - Write a header that captures what all cards in the cluster share
   - Use a user-centered statement: "Users feel confused when..." not "Confusion"

4. Create hierarchy (optional)
   - Group related clusters into higher-level themes
   - Creates a 2–3 level hierarchy: Theme → Cluster → Card

5. Discuss and adjust
   - Walk through each cluster as a team
   - Move cards that belong elsewhere
   - Split clusters that are too broad
```

### Digital Tools
- FigJam, Miro, MURAL — for remote teams
- Physical sticky notes — best for co-located workshops

### What Good Clusters Look Like

**Too broad:** "Problems with the app"
**Too narrow:** "User couldn't find the export button on Tuesday"
**Right level:** "Users don't know their data was saved"

### Outputs
- Themed clusters of research data
- 3–7 top-level themes
- Input for Insight Generation

---

## 2. Insight Generation

**Purpose:** Translate research themes into actionable, design-relevant insights that point toward solutions.

**When to use:** After Affinity Mapping, to brief design teams or stakeholders.

### Insight Formula

```
[User group] [verb — struggle, need, expect, believe]
[specific observation]
because [underlying reason].
```

**Weak finding:** "Users are confused by the navigation."
**Strong insight:** "First-time users expect to find account settings under their profile photo because every other app they use puts it there — so our top-nav gear icon gets ignored."

The strong insight:
- Names a specific user group
- States a specific, concrete observation
- Explains the *why* (mental model, context, behavior pattern)
- Points toward a design direction without prescribing a solution

### Insight Categories

| Type | Description | Example trigger |
|------|-------------|-----------------|
| **Mental model gap** | User expects X, product does Y | "Users think..." |
| **Unmet need** | Something users want that doesn't exist | "Users wish they could..." |
| **Workaround** | Users compensating for missing functionality | "Users use [workaround] because..." |
| **Trust/safety** | User hesitates due to concern | "Users are reluctant to... because..." |
| **Vocabulary mismatch** | Product uses different words than users | "Users call this [term], not [our term]" |
| **Context constraint** | Environment affects how product is used | "Users use this in [context] which means..." |

### How to Prioritize Insights

Score each insight on:
- **Frequency** — how many users said/did this? (1–5)
- **Severity** — how much does it affect their goal? (1–5)
- **Actionability** — can design address this? (1–5)

Prioritize insights with high frequency + high severity first.

### Outputs
- 5–10 prioritized insight statements
- Supporting evidence (quotes, observations) for each
- Design implications (1–2 sentences per insight pointing toward opportunities)

---

## 3. Stakeholder Interviews

**Purpose:** Gather business requirements, constraints, success metrics, and organizational context that shapes what design can and cannot do.

**When to use:** At the start of any project, before talking to users, when navigating organizational complexity.

### Interview Guide

```
1. Business context
   - "What is the business goal this project is meant to achieve?"
   - "How will you measure success 6 months from now?"
   - "What happens if this doesn't ship?"

2. Constraints
   - "What are the non-negotiables — things the design must or must not do?"
   - "What technical constraints should I be aware of?"
   - "What has been tried before? What happened?"

3. Users
   - "Who do you think the primary user is for this?"
   - "What do you know about what they need?"
   - "Where do your assumptions about users come from?"

4. Stakeholders and politics
   - "Who else has a strong opinion about this project?"
   - "Whose approval is needed before this ships?"
   - "Are there any teams that might push back?"

5. Definition of done
   - "What would a successful outcome look like to you personally?"
   - "What would make you say 'this is wrong'?"
```

### Key Patterns to Identify

- **Alignment gaps** — where stakeholders contradict each other
- **Assumed knowledge** — business goals stated as if they're user needs
- **Risk areas** — where constraints will force difficult design trade-offs
- **Champions** — who will advocate for good design decisions
- **Blockers** — whose approval could kill a good design

### Synthesis

After all stakeholder interviews, map:
1. **Agreed goals** — things everyone aligned on
2. **Tensions** — conflicting priorities between stakeholders
3. **Unknowns** — open questions that need resolution before design begins

### Outputs
- List of business requirements and constraints
- Stakeholder alignment map
- Open questions for the team to resolve

---

## 4. Jobs-to-be-Done Framework

**Purpose:** Understand the underlying progress users are trying to make in their lives — the real "job" they hire your product to do, beyond surface-level feature requests.

**When to use:** When defining product strategy, when features aren't sticking, when users churn unexpectedly, when you want to find unmet market opportunities.

### The JTBD Statement Format

```
When [situation/trigger],
I want to [motivation — what they're trying to do],
so I can [desired outcome — the progress they want to make].
```

**Feature-level (weak):** "Users want to filter search results."

**Job-level (strong):** "When I'm shopping for a new laptop for work, I want to quickly eliminate options that are out of my budget, so I can focus my decision-making energy on comparing the right options — not wasting time on things I'd never buy."

The job-level statement reveals:
- The trigger (shopping for a laptop for work)
- The functional job (eliminate wrong options fast)
- The emotional job (reduce decision anxiety)
- The social job (implicit — "for work" signals professional identity)

### Job Dimensions

| Dimension | Question |
|-----------|----------|
| Functional | What are they trying to accomplish practically? |
| Emotional | How do they want to feel (or not feel)? |
| Social | How do they want to be perceived by others? |

### Finding Jobs: Research Techniques

**Switch interviews** — talk to users who recently started or stopped using your product:
- "What were you using before?"
- "What happened that made you look for something different?"
- "When did you first think 'I need to find a solution to this'?"
- "What almost stopped you from switching?"

**Timeline interview:**
- Walk backward from the decision to use your product
- "Take me back to the moment you first realized you had this problem."
- Map the chain of events that led to the switch

### Job Map Structure

```
Job: [The overarching progress the user wants to make]

Stages:
1. Define     — User figures out what they need
2. Locate     — User finds resources/inputs needed
3. Prepare    — User sets up to execute the job
4. Confirm    — User verifies they're ready
5. Execute    — User performs the core job
6. Monitor    — User evaluates progress
7. Modify     — User adjusts course
8. Conclude   — User wraps up and evaluates success
```

Identify which stages are underserved — those are design opportunities.

### Outputs
- 2–5 JTBD statements per key user segment
- Job map with stages and current pain points per stage
- Opportunity areas where the job is currently poorly served

---

## 5. Heuristic Evaluation

**Purpose:** Assess an interface against established usability principles to identify issues without user testing.

**When to use:** Early design review, before usability testing (to catch obvious issues first), auditing existing products, when time/budget doesn't allow full user research.

### Nielsen's 10 Heuristics

| # | Heuristic | Key Question |
|---|-----------|-------------|
| 1 | **Visibility of system status** | Does the user always know what's happening? |
| 2 | **Match between system and real world** | Does the interface use language/concepts users know? |
| 3 | **User control and freedom** | Can users easily undo mistakes and exit unwanted states? |
| 4 | **Consistency and standards** | Are similar things named and styled the same way? |
| 5 | **Error prevention** | Does the design prevent errors before they happen? |
| 6 | **Recognition over recall** | Are options visible rather than requiring memorization? |
| 7 | **Flexibility and efficiency** | Can expert users find shortcuts? |
| 8 | **Aesthetic and minimalist design** | Is every element earning its place? |
| 9 | **Help users recognize, diagnose, recover from errors** | Are error messages plain-language and actionable? |
| 10 | **Help and documentation** | Is help easy to find and task-focused? |

### Evaluation Process

```
1. Define scope
   - Which flows/screens to evaluate
   - Which user tasks to walk through

2. Walk through each task per heuristic
   - Evaluate every screen in the flow against all 10 heuristics
   - Note issues, not solutions — separate evaluation from redesign

3. Rate severity per issue
   0 — Not a problem
   1 — Cosmetic only (fix if time permits)
   2 — Minor (low priority)
   3 — Major (important to fix)
   4 — Catastrophic (must fix before launch)

4. Consolidate (if multiple evaluators)
   - Each evaluator works independently first
   - Combine findings and remove duplicates
   - Discuss severity disagreements
```

### Issue Documentation Format

```
Issue: [Short title]
Heuristic violated: [#N — Name]
Severity: [0–4]
Location: [Screen/page/component]
Description: [What is wrong and where]
Impact: [How this affects the user]
Recommendation: [Suggested fix direction — brief]
```

### Common High-Severity Patterns to Look For

- No loading/progress feedback (H1)
- Technical jargon in error messages (H2, H9)
- No confirmation before destructive actions (H3, H5)
- Inconsistent button labels for same action (H4)
- Required fields only revealed after form submission (H5)
- Actions hidden in menus when frequently used (H6, H7)
- Cluttered screens where secondary content competes with primary (H8)
- Error messages that say "Error 403" with no guidance (H9)

### Outputs
- List of issues ranked by severity
- Heuristic violation breakdown (which heuristics fail most)
- Quick wins (severity 3–4 issues with easy fixes)
- Input for usability test script (major issues worth validating with users)
