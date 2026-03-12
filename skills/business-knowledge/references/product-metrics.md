# Product Metrics & Analytics

## KPI Definition

### Choosing the right KPIs

Good KPIs are:
- **Actionable** — The team can influence them through design/product decisions
- **Comparable** — Can be measured across time periods and cohorts
- **Understandable** — Everyone on the team knows what they mean
- **Rate or ratio** — Percentages and rates beat raw counts (they normalize for growth)

### KPI hierarchy
```
North Star Metric
├── Primary KPIs (3-5 metrics that drive the North Star)
│   ├── Leading indicators (predict future performance)
│   └── Lagging indicators (confirm past performance)
└── Feature-level metrics (per-screen or per-flow)
```

Design implication: Every screen should map to at least one KPI. If it doesn't, question why it exists.

## Funnel Analysis

### Standard product funnel (AARRR / Pirate Metrics)

| Stage | Definition | Key metric | Design focus |
|---|---|---|---|
| **Acquisition** | User arrives | Traffic, signups | Landing page, first impression |
| **Activation** | User experiences core value | Time-to-value, setup completion | Onboarding, first-run experience |
| **Retention** | User comes back | D1/D7/D30 retention | Habit loops, notifications, value reinforcement |
| **Revenue** | User pays | Conversion rate, ARPU | Pricing page, upgrade prompts, value demonstration |
| **Referral** | User invites others | Viral coefficient, share rate | Sharing features, referral rewards |

### Funnel design principles
1. Measure drop-off between every step
2. The biggest drop-off is your highest-leverage design opportunity
3. Reduce steps — every additional step loses 20-50% of users
4. Show progress indicators for multi-step flows
5. Allow skipping non-essential steps (collect data later)

## Cohort Analysis

### What cohort analysis reveals for designers

- **Onboarding changes** — Did the new onboarding improve D7 retention for the March cohort vs February?
- **Feature impact** — Did users who adopted Feature X have better retention curves?
- **Seasonal patterns** — Do holiday signups behave differently than organic signups?

### Reading cohort charts
- X-axis: Time since signup (Day 0, Day 1, Day 7, Day 30...)
- Y-axis: % of cohort still active
- Each row: A signup cohort (e.g., "Jan 2024 signups")
- Healthy: Curves flatten (users who stay past Day 7 tend to stay)
- Unhealthy: Curves keep declining (no retention floor)

## Retention Metrics

### Key retention metrics

**DAU / MAU (Daily/Monthly Active Users)**
- DAU/MAU ratio = "stickiness" — what % of monthly users come back daily
- Benchmarks: Social apps 50%+, SaaS tools 25-40%, e-commerce 10-20%

**Retention curves**
- D1 retention: Did the user come back the next day? (activation quality)
- D7 retention: Did the user form a habit? (core loop quality)
- D30 retention: Is the user a long-term user? (product-market fit signal)

**Benchmarks by category:**
| Category | D1 | D7 | D30 |
|---|---|---|---|
| Top social apps | 60%+ | 40%+ | 25%+ |
| Good SaaS | 80%+ | 60%+ | 40%+ |
| Mobile games | 35%+ | 15%+ | 5%+ |
| E-commerce | 25%+ | 12%+ | 8%+ |

### Design levers for retention
- **Habit loops** — Trigger → Action → Variable reward → Investment
- **Progress systems** — Streaks, levels, completion percentages
- **Content freshness** — New data, updates, recommendations
- **Social connections** — Following, teams, shared activity
- **Notifications** — Re-engagement with genuine value (not spam)

## Engagement Metrics

**Session length** — How long users spend per visit
**Session frequency** — How often users return
**Feature adoption** — % of users who use a specific feature
**Depth of engagement** — How many features used per session
**Time to value** — How quickly users reach the "aha moment"

### Design implications
- Short sessions + high frequency = utility tool (optimize for speed)
- Long sessions + low frequency = deep work tool (optimize for depth)
- Low feature adoption = discovery problem (improve navigation, onboarding)
- High drop-off at specific feature = usability problem (redesign that flow)

## North Star Metric

### Choosing a North Star

The North Star Metric captures the core value your product delivers. It should:
1. Reflect value delivered to the user (not just business revenue)
2. Be a leading indicator of revenue
3. Be measurable and actionable

### Examples by product type
| Product type | North Star Metric |
|---|---|
| Social network | Daily active users posting content |
| SaaS tool | Weekly active teams completing workflows |
| Marketplace | Transactions completed per week |
| Content platform | Time spent consuming content |
| Fintech | Assets under management / transactions processed |
| E-commerce | Purchase frequency per customer |

## Product-Market Fit

### Measuring PMF

**Sean Ellis test:** "How would you feel if you could no longer use this product?"
- 40%+ say "Very disappointed" = PMF achieved
- Below 40% = iterate on value proposition

**Retention curve flattening:** If your retention curve levels off (doesn't hit zero), you have PMF for that cohort.

**Organic growth:** Users telling other users without incentives.

### Design signals of poor PMF
- High signup rate but low activation — value proposition mismatch
- Good D1 but terrible D7 — initial interest but no sustained value
- Users only use one feature — product is too broad or core value unclear
- High support tickets — product is confusing or unreliable

## Data-Driven Decision Making

### Framework for design decisions

1. **Define the question** — What are we trying to learn?
2. **Choose the metric** — What number will answer the question?
3. **Set the baseline** — What is the current performance?
4. **Design the experiment** — A/B test, prototype test, or analytics analysis
5. **Analyze results** — Statistical significance, practical significance, edge cases
6. **Decide and document** — Ship, iterate, or kill. Record the reasoning.

### When to use data vs. intuition
- **Use data:** Optimizing existing flows, comparing alternatives, validating assumptions
- **Use intuition:** Novel product directions, 0→1 features, aesthetic decisions
- **Use both:** Most real decisions — data informs, designer decides
