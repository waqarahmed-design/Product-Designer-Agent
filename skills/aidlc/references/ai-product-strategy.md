# AI Product Strategy

## AI Use Case Identification

### Recognizing AI opportunities

Not every feature needs AI. Use AI when:
- **Pattern recognition** — Finding patterns in large datasets humans can't process
- **Personalization at scale** — Adapting experiences to individual users
- **Automation of repetitive tasks** — Freeing users from tedious work
- **Natural language interaction** — Understanding intent from unstructured input
- **Prediction** — Anticipating what users need before they ask
- **Content generation** — Creating text, images, code, or other content

### When NOT to use AI
- Simple if/else logic handles it — don't overcomplicate
- Deterministic output is required (legal, financial compliance)
- User trust is fragile and errors have high cost
- The data doesn't exist to train or prompt the model
- A simpler heuristic achieves 90% of the value

### AI opportunity framework

| Signal | AI opportunity | Example |
|---|---|---|
| Users search/filter repeatedly | AI-powered recommendations | "You might also like..." |
| Users write the same content | AI drafting / templates | Email composer, report generator |
| Users classify or tag items | Auto-categorization | Expense categorization, ticket routing |
| Users ask the same questions | AI assistant / FAQ bot | Customer support chatbot |
| Users analyze complex data | AI insights / summaries | Dashboard insights, trend detection |
| Users do repetitive formatting | AI formatting / cleanup | Document formatting, data cleaning |

## AI Capabilities Assessment

### What current AI can do well
- **Text generation** — Drafting, summarizing, translating, reformatting
- **Classification** — Sentiment analysis, categorization, intent detection
- **Conversational interaction** — Multi-turn dialogue, Q&A, task completion
- **Code generation** — Writing, explaining, debugging code
- **Image generation & understanding** — Creating images from text, analyzing visual content
- **Search & retrieval** — Semantic search, recommendation, similar-item finding
- **Structured extraction** — Pulling structured data from unstructured text

### What current AI struggles with
- **Factual accuracy** — Hallucination remains an unsolved problem
- **Real-time data** — Models have knowledge cutoffs
- **Complex reasoning** — Multi-step logic chains with many variables
- **Consistency** — Same prompt can produce different outputs
- **Domain expertise** — Deep, specialized knowledge without fine-tuning or RAG
- **Understanding context** — Nuance, sarcasm, cultural context

### Design implication
Design for AI's actual capabilities, not marketing promises. Always have a fallback for when AI fails.

## AI Product Roadmapping

### AI feature maturity model

| Stage | Description | Design approach |
|---|---|---|
| **Exploration** | Testing if AI adds value | Wizard-of-Oz prototypes, manual-behind-the-scenes |
| **Assisted** | AI suggests, human decides | Copilot patterns, suggestion chips, "AI draft" |
| **Augmented** | AI handles routine, human handles edge cases | Auto-complete, auto-categorize with human override |
| **Autonomous** | AI handles end-to-end with human oversight | Automated workflows with audit trail |

### Roadmap principles
1. **Start assisted, earn autonomous** — Build trust before removing guardrails
2. **Ship the 80% version** — AI doesn't need to be perfect to be useful
3. **Instrument everything** — Every AI interaction should generate feedback data
4. **Plan for model updates** — AI capabilities improve; design flexible UI that can grow
5. **Budget for evaluation** — 30% of AI feature effort should be testing and tuning

## Model Selection Understanding

### Model types and their design implications

| Model type | Use case | Design patterns |
|---|---|---|
| **LLM (GPT, Claude, etc.)** | Text generation, conversation, analysis | Chat UI, prompt input, streaming output |
| **Computer vision** | Image recognition, OCR, visual search | Camera input, bounding boxes, annotation UI |
| **Recommendation systems** | Content/product discovery | Cards, carousels, "for you" sections |
| **Classification models** | Categorization, sentiment, intent | Labels, tags, confidence scores |
| **Speech/voice models** | Transcription, voice commands | Voice input UI, transcript display |
| **Embedding models** | Semantic search, similarity | Search interfaces, "similar items" |

### Cost-quality tradeoffs
- Larger models = better quality, higher cost, slower response
- Smaller models = faster, cheaper, but less capable
- Design should gracefully handle different quality levels
- Consider: Can you use a fast model for suggestions and a powerful model for final output?

## AI Ethics & Governance

### Design responsibilities

| Principle | Design action |
|---|---|
| **Fairness** | Test AI outputs across diverse user groups; surface bias when detected |
| **Transparency** | Label AI-generated content; explain how AI decisions are made |
| **Accountability** | Provide human override for every AI decision; maintain audit trails |
| **Privacy** | Minimize data collection; give users control over what AI learns about them |
| **Safety** | Content filtering, guardrails, misuse prevention |
| **Consent** | Explicit opt-in for AI features; easy opt-out |

### Governance checklist for AI features
- [ ] AI-generated content is clearly labeled
- [ ] Users can opt out of AI features
- [ ] Human override is available for AI decisions
- [ ] Bias testing has been conducted across user segments
- [ ] Data usage is transparent and documented
- [ ] Error/failure modes are designed and tested
- [ ] Usage limits and costs are communicated

## AI Business Models

### Monetizing AI features

| Model | Description | Design implication |
|---|---|---|
| **Usage-based** | Charge per AI interaction (tokens, requests) | Usage meters, cost visibility, "credits remaining" |
| **Tiered access** | Free tier with limits, premium for more | Feature gates, upgrade prompts at limit |
| **Premium feature** | AI as a paid add-on | Clear value demonstration before paywall |
| **Bundled** | AI included in existing subscription | Discovery and onboarding within existing product |
| **Data flywheel** | Free AI that improves with usage, monetize insights | Feedback mechanisms, data quality signals |

### AI cost considerations for design
- Token usage directly impacts cost — design concise prompts
- Streaming responses feel faster but may use same tokens
- Caching frequent responses reduces cost dramatically
- Rate limiting needs elegant UX, not just error messages
- Show users their usage when they're paying per interaction

## Competitive AI Analysis

### Framework for analyzing AI in competitor products

**Feature audit:**
- What AI features do they offer?
- How prominent are AI features in their product?
- What model/provider do they appear to use?
- What are users saying about AI quality in reviews?

**UX audit:**
- How do they handle AI onboarding?
- How do they communicate AI limitations?
- What feedback mechanisms do they provide?
- How do they handle errors and hallucinations?

**Business audit:**
- How do they price AI features?
- Is AI a differentiator or table stakes?
- How fast are they shipping AI improvements?

### Competitive positioning
- **AI-native** — AI is the core product (ChatGPT, Midjourney)
- **AI-enhanced** — AI augments existing product (Notion AI, GitHub Copilot)
- **AI-adjacent** — AI features added but not core (traditional SaaS adding AI)

Design implication: Your positioning determines how prominently AI should feature in the UX. AI-native products build the entire experience around AI. AI-enhanced products integrate AI into existing workflows.
