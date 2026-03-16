# Growth & Monetization

## Growth Loops

### Types of growth loops

**Viral loop** — User invites others → new users → they invite others
- Design: Share buttons, referral rewards, collaborative features, social proof
- Metric: Viral coefficient (K-factor). K > 1 = exponential growth
- Example: Dropbox "invite a friend, get free storage"

**Content loop** — User creates content → content attracts new users → they create content
- Design: SEO-friendly pages, embeddable content, creator tools, templates
- Metric: Content created per user, organic traffic from content
- Example: Pinterest pins appearing in Google image search

**Paid loop** — Revenue funds acquisition → new users generate revenue → fund more acquisition
- Design: Optimize conversion to maximize revenue per user, reduce CAC through better onboarding
- Metric: CAC payback period, ROAS (Return on Ad Spend)
- Requirement: LTV > CAC with positive unit economics

**Product loop** — User gets value → user builds more data/connections → switching cost increases → retention
- Design: Data import, integrations, customization, history, saved preferences
- Metric: Depth of usage, integration count, data volume
- Example: Spotify recommendations improving with more listening history

### Designing for growth loops
1. Identify which loop type fits your product
2. Map the full cycle: trigger → action → output → distribution → new user → trigger
3. Reduce friction at every step in the loop
4. Measure the loop's cycle time (faster = better)

## Conversion Rate Optimization

### Funnel optimization framework

For each step in a conversion funnel:
1. **Measure** — What % of users complete this step?
2. **Benchmark** — How does this compare to industry standards?
3. **Identify friction** — Why are users dropping off? (analytics, recordings, surveys)
4. **Hypothesize** — What change would reduce drop-off?
5. **Test** — A/B test the change with statistical rigor
6. **Ship or iterate** — If significant improvement, ship. If not, new hypothesis.

### Common conversion killers and design fixes

| Killer | Fix |
|---|---|
| Too many form fields | Remove non-essential fields, use progressive profiling |
| Unclear value proposition | Rewrite headline to focus on user benefit, not feature |
| No social proof | Add testimonials, user counts, trust badges near CTAs |
| Confusing pricing | Simplify tiers, highlight recommended plan, show savings |
| Slow loading | Optimize images, lazy load, show skeleton screens |
| Decision paralysis | Reduce options, add "most popular" badge, provide defaults |
| Hidden costs | Show total cost early, no surprises at checkout |
| Weak CTA | Specific action words ("Start free trial" not "Submit"), high contrast |

### A/B testing principles
- Test one variable at a time
- Run until statistically significant (p < 0.05, typically 1-2 weeks minimum)
- Minimum sample size: 1000+ per variant for meaningful results
- Don't stop tests early on positive results (regression to mean)
- Document every test — wins AND losses

## Onboarding Optimization

### Time-to-value framework

**Goal:** Get users to their "aha moment" as fast as possible.

**Aha moment examples:**
- Slack: Sending 2000 messages as a team
- Dropbox: Putting a file in a shared folder
- Facebook: Adding 7 friends in 10 days

### Onboarding patterns

**Progressive onboarding** — Reveal features as users need them, not all at once
- Best for: Complex products with many features
- Design: Contextual tooltips, coach marks, empty state guidance

**Checklist onboarding** — Show users a list of setup steps to complete
- Best for: Products requiring configuration before value
- Design: Progress bar, numbered steps, skip options, celebration on completion

**Personalized onboarding** — Ask users about their goals, customize the experience
- Best for: Products serving multiple use cases
- Design: "What's your role?" or "What do you want to accomplish?" flow

**Template/sample data onboarding** — Show the product filled with realistic data
- Best for: Empty-state-heavy products (dashboards, project tools)
- Design: Pre-populated templates, sample projects, demo data

### Onboarding metrics
- **Activation rate** — % of signups who reach the aha moment
- **Time to activate** — How long from signup to aha moment
- **Setup completion rate** — % who complete onboarding steps
- **D1 retention of activated users** — Validates the aha moment is real

## Upselling & Cross-selling

### Upgrade path design principles

1. **Show the ceiling** — Let users see what they're missing (blurred premium features, usage limits)
2. **Trigger at natural moments** — Prompt upgrades when users hit limits, not randomly
3. **Demonstrate value first** — Let users try premium features temporarily before asking to pay
4. **Make downgrade easy** — Paradoxically increases trust and reduces churn anxiety

### Upsell UI patterns
- **Usage meters** — "You've used 80% of your free storage" with upgrade CTA
- **Feature gates** — Locked features visible but not usable, with "Upgrade to unlock"
- **Trial prompts** — "Try Pro free for 14 days" at natural upgrade moments
- **Comparison modals** — Side-by-side current plan vs. upgrade when user hits a limit
- **Success triggers** — "You're growing fast! Pro gives you X to keep scaling"

### Cross-sell patterns
- **Contextual suggestions** — "Users who use X also use Y"
- **Bundle discounts** — "Add Y for 30% off when bought together"
- **Workflow integration** — Surface related products where they naturally fit

## Retention Strategies

### Re-engagement design patterns

**Email/notification re-engagement**
- Trigger: User hasn't logged in for X days
- Content: Show what they're missing (new data, updates, activity)
- Rule: Provide value, not guilt. "3 things happened since you left" > "We miss you"

**Habit formation (Hook Model)**
1. **Trigger** — External (notification) or internal (boredom, anxiety)
2. **Action** — Simplest behavior in anticipation of reward
3. **Variable reward** — Unpredictable positive outcome (social validation, content, data)
4. **Investment** — User puts something in (data, connections, preferences) that improves next loop

**Streak mechanics**
- Show consecutive usage days/weeks
- Celebrate milestones (7-day streak, 30-day streak)
- Warning before breaking a streak
- Caution: Don't make streaks punishing — that drives churn, not retention

## Churn Reduction

### Churn signals to detect

| Signal | What it means | Design response |
|---|---|---|
| Declining session frequency | User is disengaging | Re-engagement notification with new value |
| Reduced feature usage | Core value fading | Surface unused features, show what's new |
| Support ticket spike | Frustration building | Fix UX issues, proactive help |
| Billing page visits | Considering cancellation | Show value summary, offer plan adjustment |
| Export/download data | Preparing to leave | Retention offer, remind of switching costs |

### Cancellation flow design
1. Ask why they're leaving (multiple choice, not open text)
2. Offer solutions based on reason (too expensive → downgrade, missing feature → roadmap)
3. Show what they'll lose (data, history, integrations, team access)
4. Offer a pause option instead of cancellation
5. Make cancellation possible — never dark pattern it (destroys trust, causes chargebacks)

## Pricing Page Design

### Layout principles

1. **3 tiers maximum** — Good / Better / Best (or Starter / Pro / Enterprise)
2. **Highlight the target plan** — Visual emphasis on the plan you want most users to choose
3. **Annual default** — Show annual pricing first, monthly as toggle (show savings %)
4. **Feature comparison** — Scannable rows, not walls of text. Group by category.
5. **Social proof** — Customer logos, testimonials, user counts near pricing
6. **FAQ below** — Address objections: "Can I cancel anytime?", "Is there a free trial?"
7. **Enterprise CTA** — "Contact sales" for high-value custom plans

### Pricing psychology
- **Anchoring** — Show the expensive plan first so the middle plan feels reasonable
- **Decoy effect** — The cheapest plan exists to make the middle plan look like the best deal
- **Price ending** — $49/mo feels cheaper than $50/mo (charm pricing)
- **Per-user vs. flat** — Per-user scales with team size; flat rate is simpler and preferred by buyers
- **Free tier** — Lowers acquisition barrier but must clearly limit to drive upgrades
