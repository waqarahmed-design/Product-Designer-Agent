# AI-Specific Research

## AI User Needs Discovery

### What makes AI research different
Traditional UX research asks "What do users want to do?" AI research adds: "Do users even know AI could help here?"

### Discovery methods for AI features

| Method | Purpose | Key questions |
|---|---|---|
| **Workflow shadowing** | Find AI opportunities | Where do users do repetitive work? Where do they struggle with volume? |
| **Pain point interviews** | Validate AI fit | Is this problem solvable by pattern recognition, generation, or prediction? |
| **Diary studies** | Understand context | When and where would users interact with AI? What's their mental state? |
| **Wizard-of-Oz testing** | Test AI value before building | Would users use this if a human provided the same output? |
| **Competitive testing** | Benchmark expectations | Have users tried AI features elsewhere? What do they expect? |

### Key questions for AI needs discovery
- What tasks take the most time but require the least creativity?
- Where do users make decisions based on large amounts of data?
- What content do users create repeatedly with minor variations?
- Where do users need expert knowledge they don't have?
- What would users do if they had a smart assistant available?

## Mental Model Research

### How users think about AI

**Common mental models:**
- **AI as magic** — Expects perfect, instant results with no guidance needed
- **AI as search** — Treats AI like Google, expects factual answers
- **AI as human** — Anthropomorphizes, expects empathy and memory
- **AI as tool** — Understands it needs input and direction, expects predictable behavior
- **AI as threat** — Fears replacement, surveillance, or manipulation

**Design implication:** Your UI must gently correct inaccurate mental models. Users who think AI is magic will be disappointed; users who think AI is a threat need reassurance.

### Researching mental models
- **Card sorting** — How do users categorize AI capabilities?
- **Think-aloud protocols** — What do users expect when they type a prompt?
- **Metaphor elicitation** — "If this AI feature were a person/animal/tool, what would it be?"
- **Expectation mapping** — Before using AI feature, write down what they expect. After, compare.

## Trust & Expectations Research

### Trust factors for AI features

| Factor | High trust | Low trust |
|---|---|---|
| **Accuracy** | Consistently correct, few errors | Frequent mistakes, hallucinations |
| **Transparency** | Explains reasoning, shows sources | Black box, no explanation |
| **Control** | User can edit, override, undo | No way to correct or modify |
| **Predictability** | Consistent behavior | Different results each time |
| **Stakes** | Low-risk suggestions | High-stakes decisions |
| **Familiarity** | User has AI experience | First-time AI user |

### Trust research methods
- **Trust scale surveys** — Measure trust before and after AI interactions
- **Behavioral trust indicators** — Do users accept AI suggestions? Edit them? Ignore them?
- **Trust recovery testing** — After an AI error, how quickly does trust rebuild?
- **Comparison testing** — Do users trust AI output more or less than human output?

### Trust calibration
The goal is **appropriate trust** — not blind trust or complete distrust:
- Users should trust AI for tasks it's good at
- Users should verify AI for tasks where errors are costly
- Design should make verification easy and natural

## AI Anxiety & Concerns

### Common user concerns

| Concern | Frequency | Design response |
|---|---|---|
| **Job replacement** | Very common | Frame AI as assistant, not replacement; emphasize human control |
| **Privacy / data use** | Very common | Clear data policies, opt-in, show what data AI uses |
| **Accuracy fears** | Common | Show confidence indicators, provide sources, enable verification |
| **Loss of skill** | Moderate | Offer "show me how" alongside "do it for me" |
| **Manipulation** | Moderate | Transparent AI labeling, no dark patterns |
| **Surveillance** | Lower but intense | Minimal data collection, clear deletion options |

### Researching AI anxiety
- **Pre-exposure surveys** — Measure anxiety before using AI features
- **Anxiety trigger mapping** — Which specific AI interactions cause discomfort?
- **Opt-in rate analysis** — Low opt-in signals high anxiety; investigate why
- **Support ticket analysis** — What AI-related concerns do users raise?

## Use Case Validation

### Is this a real AI use case?

**Validation checklist:**
- [ ] Users currently do this task manually (real pain point)
- [ ] AI quality is good enough to be useful (not just impressive)
- [ ] Users would trust AI for this specific task
- [ ] The cost of AI errors is manageable
- [ ] Users can verify and correct AI output
- [ ] The AI version is meaningfully faster/better than manual

### Validation methods
- **Fake door testing** — Show the AI feature in UI, measure click-through before building
- **Wizard-of-Oz** — Human provides AI-like output; measure user satisfaction
- **Concierge testing** — Manually deliver AI output to test the value proposition
- **Prototype testing** — Build minimal AI feature, test with real users
- **Smoke testing** — Announce AI feature, measure interest

## Prompt Engineering Research

### How users naturally interact with AI

**Research findings on user prompting behavior:**
- Most users write short, vague prompts (3-7 words)
- Users don't know what context to provide
- Users expect AI to "just know" what they want
- Iterative prompting feels like failure to most users
- Users mimic conversation style they've seen in demos

### Design implications
- **Don't rely on user prompt skill** — Provide templates, suggestions, and guardrails
- **Show examples** — "Try asking: [example prompt]" reduces blank-page anxiety
- **Progressive prompting** — Start simple, ask clarifying questions
- **Pre-fill context** — Auto-include relevant context (current page, selected text, user history)
- **Prompt suggestions** — Offer follow-up prompts after AI responds

### Research methods for prompt behavior
- **Prompt log analysis** — What do users actually type? (with consent)
- **Think-aloud prompting** — Watch users compose prompts, note hesitations
- **Prompt A/B testing** — Do users perform better with templates vs. free text?
- **Error analysis** — When AI fails, was it the prompt or the model?

## AI Literacy Assessment

### User AI literacy levels

| Level | Description | Design approach |
|---|---|---|
| **Novice** | No AI experience, may be anxious | Heavy onboarding, simple language, guided interactions |
| **Aware** | Has used ChatGPT or similar | Brief onboarding, show what's different about your AI |
| **Competent** | Understands prompting, knows limitations | Minimal onboarding, power features, keyboard shortcuts |
| **Expert** | Builds with AI, understands models | Advanced controls, API access, custom instructions |

### Assessing literacy
- **Self-report surveys** — "How would you rate your experience with AI tools?"
- **Behavioral indicators** — Prompt length, iteration count, feature adoption speed
- **Onboarding completion** — Do they skip or read AI tutorials?
- **Segmentation** — Different onboarding paths for different literacy levels
