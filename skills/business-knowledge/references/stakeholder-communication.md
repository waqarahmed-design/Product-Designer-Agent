# Stakeholder & Business Communication

## Business Case Development

### Structure of a design business case

1. **Problem statement** — What user/business problem are we solving?
2. **Opportunity size** — How many users affected? What's the revenue impact?
3. **Proposed solution** — What are we building? (High-level, not implementation)
4. **Expected impact** — Which metrics will move? By how much?
5. **Investment required** — Design time, engineering time, dependencies
6. **ROI calculation** — Expected return / investment cost
7. **Risk assessment** — What could go wrong? What's the mitigation?
8. **Timeline** — When will we see results?

### Quantifying design ROI

| Design improvement | Business metric | How to measure |
|---|---|---|
| Simplified onboarding | Activation rate | A/B test completion rates |
| Redesigned pricing page | Conversion rate | Revenue per visitor before/after |
| Improved search/discovery | Feature adoption | Usage analytics, task completion |
| Reduced form friction | Signup rate | Funnel drop-off analysis |
| Better error handling | Support tickets | Ticket volume before/after |
| Faster page load | Bounce rate, revenue | Performance metrics + revenue correlation |

### Framing design in business language

| Instead of saying | Say |
|---|---|
| "The UI needs to be cleaner" | "Reducing visual clutter will improve task completion by X%" |
| "Users are confused" | "40% of users abandon at step 3, costing $Xk/month in lost conversions" |
| "We need a design system" | "A component library will cut dev time by 30%, saving X hours per sprint" |
| "The onboarding is bad" | "Only 25% of signups reach activation — industry benchmark is 40%" |
| "We should redesign this page" | "This page has a 78% bounce rate vs. 45% benchmark — fixing it could recover $Xk/month" |

## Executive Presentations

### Presenting design to leadership

**Structure (10-minute format):**
1. **Context** (1 min) — What problem, who's affected, why now
2. **Data** (2 min) — Current metrics, what's broken, opportunity size
3. **Solution** (3 min) — What we're proposing, key design decisions, mockups
4. **Expected impact** (2 min) — Which metrics move, by how much, timeline
5. **Ask** (2 min) — What you need (resources, approval, alignment)

**Rules:**
- Lead with the business impact, not the design
- Show before/after, not process
- Use numbers — executives trust data more than aesthetic arguments
- Anticipate objections — have the "why not X?" answers ready
- Keep visuals large and simple — details are for follow-up

### Communicating design value to non-designers

- **To engineers:** Focus on component reusability, reduced rework, clear specifications
- **To product managers:** Focus on user outcomes, metric impact, competitive advantage
- **To executives:** Focus on revenue impact, cost savings, risk reduction
- **To sales:** Focus on customer stories, demo-ability, competitive differentiation
- **To support:** Focus on reduced ticket volume, clearer user self-service

## OKR / Goal Setting

### Aligning design with OKRs

**Objective:** Qualitative goal (what we want to achieve)
**Key Results:** Quantitative measures (how we know we achieved it)

### Design-aligned OKR examples

**Objective:** Improve new user activation
- KR1: Increase onboarding completion from 35% to 55%
- KR2: Reduce time-to-first-value from 8 minutes to 3 minutes
- KR3: Increase D7 retention of new users from 20% to 30%

**Objective:** Increase revenue per user
- KR1: Increase free-to-paid conversion from 3% to 5%
- KR2: Reduce pricing page bounce rate from 65% to 40%
- KR3: Increase average plan tier from $29 to $49

**Objective:** Reduce user friction
- KR1: Reduce support tickets about feature X by 50%
- KR2: Increase task completion rate from 60% to 85%
- KR3: Improve System Usability Scale (SUS) score from 65 to 80

### Setting design-specific goals
- Every design initiative should tie to at least one company OKR
- If it doesn't tie to an OKR, question its priority
- Measure design impact through behavior change, not design output

## Budget Management

### Understanding design costs

**Direct costs:**
- Design tools (Figma, prototyping tools, analytics)
- User research (recruiting, incentives, testing tools)
- Design assets (stock photos, icons, fonts, illustrations)

**Indirect costs:**
- Designer time (the biggest cost — make it count)
- Engineering time for implementation
- QA time for design fidelity

### Making the case for design investment
- Benchmark against industry: design team size vs. engineering ratio (typically 1:5 to 1:8)
- Show ROI of past design work: "The checkout redesign increased conversion by 15%, worth $Xk/year"
- Calculate cost of NOT investing: "Current churn rate costs $Xk/month — design improvements can reduce by Y%"

## Risk Assessment

### Design risk categories

| Risk type | Example | Mitigation |
|---|---|---|
| **Usability risk** | Users can't complete core task | User testing before development |
| **Adoption risk** | Users don't discover/use new feature | Progressive disclosure, onboarding |
| **Technical risk** | Design can't be built as specified | Early engineering collaboration |
| **Business risk** | Feature doesn't move target metric | Define success criteria upfront, kill criteria |
| **Brand risk** | Design damages brand perception | Brand guidelines review, user perception testing |
| **Accessibility risk** | Design excludes users with disabilities | WCAG audit, assistive technology testing |

### Risk communication framework
- **Probability:** How likely is this risk? (Low / Medium / High)
- **Impact:** How bad if it happens? (Low / Medium / High)
- **Mitigation:** What can we do to reduce probability or impact?
- **Detection:** How will we know if this risk materializes?

## Trade-off Analysis

### Common design trade-offs

| Trade-off | When to choose A | When to choose B |
|---|---|---|
| **Speed vs. quality** | Time-sensitive launch, can iterate later | High-stakes surface (payments, onboarding) |
| **Simplicity vs. power** | Broad audience, consumer product | Power users, professional tools |
| **Consistency vs. optimization** | Maintaining design system integrity | Clear data showing a variant performs better |
| **User needs vs. business needs** | Long-term retention, brand trust | Short-term revenue, survival |
| **Build vs. buy** | Core differentiator, unique UX | Commodity feature, faster time to market |

### Decision framework
1. State the trade-off explicitly
2. List what you gain and lose with each option
3. Identify which stakeholder each option serves
4. Check alignment with company strategy and OKRs
5. Make a recommendation with reasoning
6. Document the decision for future reference

## Opportunity Sizing

### Estimating design impact

**Formula:** Impact = Reach x Frequency x Value x Improvement

- **Reach:** How many users encounter this?
- **Frequency:** How often do they encounter it?
- **Value:** What's each interaction worth? (revenue, time saved, satisfaction)
- **Improvement:** What % improvement is realistic?

### Example
- Checkout flow has 10,000 users/month (Reach)
- Average 1.5 purchases/month (Frequency)
- Average order value $50 (Value)
- Redesign could improve conversion by 10% (Improvement)
- Impact: 10,000 x 1.5 x $50 x 0.10 = $75,000/month potential

### Prioritization with RICE

| Factor | Definition | Scale |
|---|---|---|
| **Reach** | How many users in a time period | Actual number |
| **Impact** | How much does it move the metric | 3=massive, 2=high, 1=medium, 0.5=low, 0.25=minimal |
| **Confidence** | How sure are we about estimates | 100%=high, 80%=medium, 50%=low |
| **Effort** | Person-months to ship | Actual estimate |

RICE Score = (Reach x Impact x Confidence) / Effort

Higher score = higher priority. Use to compare competing design initiatives.
