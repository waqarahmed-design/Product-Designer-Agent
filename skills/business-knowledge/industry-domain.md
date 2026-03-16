# Industry & Domain Knowledge

## Industry Trends

### Staying current — what to track

**Technology trends affecting design:**
- AI/ML integration — conversational UI, predictive features, personalization
- Voice and multimodal interfaces — designing beyond screens
- Spatial computing (AR/VR) — 3D interaction patterns
- Edge computing — faster, offline-capable experiences
- Web3/blockchain — wallet UX, decentralized identity

**UX trends:**
- Personalization at scale — adaptive interfaces, smart defaults
- Accessibility as default — not an afterthought
- Ethical design — transparency, user control, no dark patterns
- Sustainability — reduced data transfer, energy-efficient design
- AI-assisted creation — co-pilot features, smart suggestions

**Business model trends:**
- Usage-based pricing replacing flat subscriptions
- Product-led growth (PLG) replacing sales-led
- Vertical SaaS — deep domain solutions over horizontal platforms
- Creator economy — tools for individual creators and small businesses
- Embedded finance — financial services inside non-financial products

### How trends affect design decisions
- Don't chase trends for their own sake
- Evaluate each trend: Does it serve our users? Does it align with our business model?
- Early adoption = competitive advantage. Late adoption = table stakes.

## Regulatory Compliance

### GDPR (General Data Protection Regulation) — EU

**Design requirements:**
- **Consent:** Explicit opt-in for data collection. No pre-checked boxes. Clear language.
- **Right to access:** Users must be able to see what data you have about them
- **Right to delete:** "Delete my account" must actually delete data
- **Data portability:** Users can export their data in a standard format
- **Privacy by design:** Collect minimum data necessary. Don't track what you don't need.
- **Cookie consent:** Banner with real choices (not just "Accept all")

**Design implications:**
- Cookie consent UI that doesn't use dark patterns
- Privacy settings page with granular controls
- Data export feature
- Account deletion flow that's findable and functional
- Clear privacy policy in plain language

### CCPA (California Consumer Privacy Act) — US

**Design requirements:**
- "Do Not Sell My Personal Information" link in footer
- Disclosure of what data is collected and why
- Right to delete personal information
- Non-discrimination for users who exercise privacy rights

### Accessibility Laws

**ADA (Americans with Disabilities Act)** — US
- Digital products must be accessible to people with disabilities
- WCAG 2.1 AA is the de facto standard

**EAA (European Accessibility Act)** — EU (effective June 2025)
- Products and services must meet accessibility requirements
- Covers websites, mobile apps, e-commerce, banking, transport

**Design baseline:**
- WCAG 2.1 AA compliance minimum
- Keyboard navigation for all interactive elements
- Screen reader compatibility
- 4.5:1 contrast ratio for text
- 44x44px minimum touch targets
- Captions for video, alt text for images

### Industry-Specific Regulations

| Industry | Key regulations | Design impact |
|---|---|---|
| **Fintech** | PSD2, KYC/AML, SEC | Identity verification flows, transaction confirmations, risk disclosures |
| **Healthcare** | HIPAA, HITECH | Data encryption indicators, consent forms, audit trails |
| **Education** | FERPA, COPPA | Parental consent flows, age gates, data minimization |
| **E-commerce** | PCI-DSS, consumer protection | Secure checkout indicators, clear pricing, return policies |
| **Insurance** | State regulations, NAIC | Quote transparency, policy clarity, claims process |

## Domain Expertise

### Building domain knowledge for design

**For any new domain:**
1. **Talk to users** — 5 user interviews reveal 80% of pain points
2. **Shadow experts** — Watch domain professionals do their work
3. **Learn the vocabulary** — Every domain has jargon. Learn it to build credibility.
4. **Map the workflow** — Before designing screens, understand the end-to-end process
5. **Study the data** — What data matters most? What decisions do users make from it?

### Domain-specific design principles

**Fintech:**
- Trust is everything — security indicators at every step
- Numbers must be precise and instantly readable
- Transaction history is the most-used feature
- Regulatory compliance drives many design constraints
- Read-only vs. transactional permissions affect UI complexity

**Healthcare:**
- Patient safety overrides convenience
- Clinical workflows are deeply ingrained — change carefully
- HIPAA constrains what can be shown on screens (shoulder surfing)
- Interoperability (HL7/FHIR) affects data display
- Accessibility is legally mandated, not optional

**SaaS / B2B:**
- Admin UX matters as much as end-user UX
- Onboarding must serve both individual and team setup
- Integrations drive adoption — API and webhook UI
- Role-based access control affects every screen
- Enterprise customers expect customization options

**E-commerce:**
- Reducing checkout friction = direct revenue impact
- Product photography quality > clever UI
- Trust signals (reviews, return policy, secure badge) drive conversion
- Mobile commerce requires thumb-friendly design
- Search and filtering are make-or-break features

**Education:**
- Engagement without manipulation (no dark patterns for "engagement")
- Progress tracking motivates learners
- Content accessibility for diverse learning needs
- Parental controls and age-appropriate design
- Offline capability for low-connectivity environments

## Competitive Intelligence

### Competitive analysis framework

For each competitor, evaluate:

**Product analysis:**
- Core features and differentiators
- UX quality (run a heuristic evaluation)
- Pricing model and tiers
- Platform coverage (web, iOS, Android, API)
- Integration ecosystem

**User perception:**
- App store reviews — what do users love and hate?
- Social media sentiment
- Support forums — common complaints
- G2/Capterra reviews for B2B products

**Business signals:**
- Funding and valuation (Crunchbase)
- Team growth (LinkedIn)
- Feature velocity — how fast are they shipping?
- Marketing positioning — who do they target?

### Competitive design opportunities
- Features competitors have but execute poorly — do it better
- Features no competitor has — first-mover advantage
- UX friction points across all competitors — industry-wide pain point
- Underserved segments — users competitors ignore

## Customer Segmentation

### Segmentation approaches

**Behavioral segmentation** (most useful for design)
- Power users vs. casual users → different feature exposure
- Creators vs. consumers → different interfaces
- Free vs. paid → different upgrade path visibility
- New vs. returning → different onboarding needs

**Value-based segmentation** (most useful for business)
- High-LTV customers → premium support, retention priority
- At-risk customers → re-engagement, churn prevention
- Growth potential → upsell opportunities

**Demographic/firmographic** (useful for targeting)
- Company size (SMB vs. enterprise) → feature complexity
- Industry vertical → domain-specific features
- Geography → localization, compliance
- Role/title → workflow and permission differences

### Design implications of segmentation
- Don't build one UI for all segments — use progressive disclosure
- Power users need efficiency (shortcuts, bulk actions, density)
- New users need guidance (onboarding, tooltips, defaults)
- High-value users may justify custom features or white-glove onboarding

## Market Research

### Primary research methods

| Method | Best for | Sample size | Design output |
|---|---|---|---|
| User interviews | Deep understanding | 5-8 per segment | Personas, journey maps |
| Surveys | Quantitative validation | 100+ | Feature prioritization, satisfaction scores |
| Usability tests | Identifying friction | 5-7 per round | Specific UX improvements |
| Card sorting | Information architecture | 15-30 | Navigation structure, labeling |
| Diary studies | Longitudinal behavior | 10-15 | Habit patterns, context of use |
| A/B tests | Comparing alternatives | 1000+ per variant | Winning design direction |

### Secondary research sources
- Industry reports (Gartner, Forrester, Nielsen Norman)
- App store reviews and ratings
- Social media and community forums
- Competitor product analysis
- Patent filings (signal future direction)
- Job postings (signal company priorities)

## Business Strategy

### How design supports business strategy

| Strategy | Design's role |
|---|---|
| **Market expansion** | Localization, new user segment flows, simplified onboarding |
| **Product-led growth** | Self-serve experience, viral features, in-product upgrade paths |
| **Platform strategy** | Developer experience, API docs, integration marketplace |
| **Vertical focus** | Domain-specific features, industry workflow support |
| **Cost leadership** | Efficiency-focused UX, self-service support, automation |
| **Differentiation** | Distinctive experience, premium feel, signature interactions |

### Strategic design thinking
- Always ask: "How does this design decision support the business strategy?"
- Short-term tactics (conversion optimization) must not undermine long-term strategy (brand trust)
- Design can be a moat — a superior experience is hard to replicate
