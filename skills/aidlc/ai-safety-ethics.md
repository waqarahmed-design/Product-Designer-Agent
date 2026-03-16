# AI Safety & Ethics Design

## Bias Mitigation UI

### Designing to surface and reduce bias

**Bias disclosure patterns:**
- **Diversity check** — For image generation: "Review generated images for representation"
- **Bias warning** — "This analysis may reflect biases in training data"
- **Demographic testing results** — "Tested across X demographics with Y% consistency"
- **Alternative viewpoints** — "Here's another perspective on this topic"

### Design strategies for bias reduction
1. **Diverse test sets** — Test AI with inputs from diverse user groups
2. **Bias indicators** — Flag when AI output may be biased (e.g., limited to one perspective)
3. **User correction** — Let users flag biased output with specific categories
4. **Prompt guardrails** — System prompts that instruct the model to be balanced
5. **Audit trails** — Track bias reports and resolution over time

### Bias categories to design for

| Bias type | Example | UI mitigation |
|---|---|---|
| **Gender** | Default "he" in generated text | Inclusive language checks, pronoun options |
| **Racial/ethnic** | Stereotypical image generation | Diversity controls, representation checks |
| **Cultural** | Western-centric advice | Locale-aware prompting, cultural context options |
| **Socioeconomic** | Assumptions about income/education | Avoid assumptions, ask for context |
| **Ability** | Ignoring accessibility needs | Inclusive default outputs, accessibility checks |
| **Age** | Ageist language or assumptions | Neutral language, diverse examples |

## Content Moderation

### Filtering harmful requests and outputs

**Moderation levels:**

| Level | What's filtered | Use case |
|---|---|---|
| **Strict** | Violence, explicit content, self-harm, illegal activity | Consumer products, children's products |
| **Standard** | Explicit content, self-harm, illegal activity | General consumer |
| **Moderate** | Self-harm, illegal activity only | Professional tools |
| **Custom** | Configurable per-deployment | Enterprise, API products |

### Input moderation design
- **Pre-submission check** — Warn before sending (reduces wasted API calls)
- **Soft redirect** — "I can't help with X, but I can help with Y"
- **Hard block** — "This request violates our usage policy" (minimal)
- **Silent filtering** — Remove problematic parts, process the rest (use sparingly)

### Output moderation design
- **Content warning** — "This response discusses [topic]. Show content?"
- **Redaction** — Blur or hide sensitive content with reveal option
- **Truncation** — Stop generation when harmful content detected
- **Replacement** — Substitute harmful content with safe alternative

### Moderation UX rules
- Don't lecture users — brief, clear explanation is enough
- Don't reveal the exact rules (prevents gaming the system)
- Offer an appeal path for false positives
- Log moderation events for compliance and improvement
- Never publicly shame users for triggering moderation

## Privacy Design

### Handling sensitive data in AI contexts

**Data flow transparency:**
- Show users what data is sent to the AI model
- Indicate if data leaves the device / goes to cloud
- Distinguish between "used for this response" vs "used for training"
- Allow users to see and delete their AI interaction history

**Privacy patterns:**

| Pattern | Description | When to use |
|---|---|---|
| **Local processing** | AI runs on-device | Maximum privacy, limited capability |
| **Encrypted transit** | Data encrypted to/from cloud AI | Standard for cloud AI |
| **Ephemeral processing** | Data not stored after response | Sensitive queries |
| **Opt-in data use** | Explicit consent for training data | Any data retention |
| **Data minimization** | Send only necessary context | Always (minimize tokens = minimize exposure) |
| **Anonymization** | Strip PII before sending to AI | When personal data is in context |

### Privacy-sensitive AI features
- **Conversation history** — Clear "delete all" and per-conversation delete
- **Learning/memory** — Transparent what AI remembers, easy to clear
- **Context sharing** — Show exactly what document/data the AI can see
- **Third-party models** — Disclose if data goes to external AI providers

## Consent Design

### Clear opt-in/opt-out for AI features

**Consent hierarchy:**
1. **First use** — Explain what AI does, ask for consent before first interaction
2. **Feature-level** — Separate consent for each AI capability (generation, analysis, suggestions)
3. **Data-level** — Consent for what data AI can access
4. **Training** — Separate consent for using interactions to improve AI

**Consent UI patterns:**
- **Informed consent screen** — Brief explanation + "Enable AI features" / "Not now"
- **Granular toggles** — Per-feature AI settings in preferences
- **Contextual consent** — Ask when user first encounters each AI feature
- **Progressive consent** — Start with basic AI, ask for more permissions over time

**Consent rules:**
- Pre-checked boxes for AI features = dark pattern — never do this
- Opt-out must be as easy as opt-in
- Revoking consent should stop AI immediately, not "after next billing cycle"
- Show what changes when AI is disabled

## Data Attribution

### Crediting sources in AI-generated content

**Attribution patterns:**
- **Inline citations** — [1], [2] references with expandable source list
- **Source sidebar** — Panel showing all sources alongside AI output
- **Confidence + source** — "Based on [source] (high confidence)"
- **Quote extraction** — Show the exact text AI drew from
- **Link to original** — Direct link to source document/page

**Attribution rules:**
- Always attribute when AI quotes or closely paraphrases
- Show the most relevant sources, not all sources
- Make source links clickable and verifiable
- Distinguish "inspired by" vs "directly quoted from"
- When no sources available, clearly state output is generated, not sourced

## Watermarking

### Identifying AI-generated content

**Watermarking approaches:**

| Approach | Visibility | Use case |
|---|---|---|
| **Visual label** | Visible "AI-generated" badge | All AI content in UI |
| **Metadata tag** | Hidden in file metadata | Exported content, images |
| **Invisible watermark** | Steganographic embedding | Images, audio |
| **Content provenance** | C2PA / Content Credentials | Published content |

**Design rules:**
- AI-generated content should always be identifiable
- Labels should be clear but not dominate the content
- When AI augments human content, label the AI-contributed parts
- Allow users to see AI contribution level ("80% AI-generated")

## Misuse Prevention

### Designing against harmful use cases

**Prevention layers:**
1. **Input guardrails** — Block harmful prompts before they reach the model
2. **Output filtering** — Filter harmful content from responses
3. **Rate limiting** — Prevent mass generation of harmful content
4. **Usage monitoring** — Detect patterns of misuse
5. **Account consequences** — Warnings, suspensions for repeated misuse

**Misuse-resistant design patterns:**
- Don't surface capabilities that invite misuse
- Default to safer modes; require explicit opt-in for powerful features
- Add friction to high-risk actions (e.g., confirm before generating sensitive content)
- Design outputs that are clearly AI-generated (harder to pass off as human)

## Transparency Documentation

### AI model cards and capability disclosures

**What to document publicly:**
- What AI model(s) power the feature
- What the AI can and cannot do (capability boundaries)
- How the AI was trained (at a high level)
- Known limitations and failure modes
- How user data is handled
- How to report issues

**Where to surface transparency info:**
- **In-product** — "About this AI" link accessible from every AI interaction
- **Help center** — Detailed AI documentation page
- **Settings** — AI preferences with explanations
- **First-use** — Brief transparency during onboarding

### Model card design
- Keep it scannable — bullet points, not paragraphs
- Use plain language — no ML jargon
- Include examples of what the AI does well AND poorly
- Update when models change
- Link to more detailed technical documentation for those who want it
