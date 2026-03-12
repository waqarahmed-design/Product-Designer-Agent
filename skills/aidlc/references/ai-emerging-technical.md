# Emerging AI Patterns & Technical Collaboration

## AI Personalization & Learning

### Adaptive UI

**Interfaces that learn from user behavior:**

| Adaptation type | Example | Design requirement |
|---|---|---|
| **Layout adaptation** | Frequently used features move to prominent positions | Show users why layout changed; allow manual override |
| **Content adaptation** | Personalized feed, relevant suggestions | "Why am I seeing this?" explanation |
| **Complexity adaptation** | UI simplifies for novices, adds power for experts | User-controlled complexity level toggle |
| **Timing adaptation** | Notifications at user's preferred times | Transparent schedule in settings |
| **Language adaptation** | Tone/vocabulary matches user's communication style | User can reset or choose preferred style |

**Adaptive UI design rules:**
- Never change UI without the user understanding why
- Always provide a way to revert to default
- Adapt gradually, not in sudden jumps
- Show users their "profile" — what the system has learned
- Adaptations should be deletable ("Forget this preference")

### Recommendation Systems

**Recommendation UI patterns:**
- **"For you" section** — Personalized content feed
- **"Similar to" suggestions** — Based on current item
- **"Users like you" signals** — Social proof + personalization
- **Contextual recommendations** — Based on current task/time/location
- **Discovery mode** — Deliberately diverse recommendations to expand horizons

**Recommendation design principles:**
- Explain why something is recommended (builds trust)
- Mix familiar and new (80% relevant, 20% discovery)
- Let users dismiss recommendations and learn from it
- Avoid filter bubbles — intentionally show diversity
- Show recommendations at the moment of need, not as interruptions

### User Preference Learning

**Preference capture patterns:**
- **Explicit** — Settings, preferences page, "I like/dislike" buttons
- **Implicit** — Usage patterns, time spent, items saved, items skipped
- **Conversational** — "What kind of X do you prefer?"
- **Onboarding** — Initial preference questionnaire

**Design principles:**
- Make implicit learning visible ("We noticed you prefer X")
- Allow users to correct wrong inferences
- Decay old preferences (tastes change)
- Separate "I viewed this" from "I like this"

### Feedback Loops

**Using user corrections to improve AI:**
1. **Collect** — Thumbs, edits, regenerations, corrections
2. **Aggregate** — Find patterns in feedback across users
3. **Improve** — Better prompts, RAG, fine-tuning, UI changes
4. **Close the loop** — Show users that feedback led to improvement

**Feedback loop design:**
- Low friction collection (one-tap thumbs, not multi-question surveys)
- Batch feedback for training (don't retrain on every thumbs down)
- A/B test improvements before rolling out
- Thank users for feedback that led to specific improvements

### Memory Management

**Designing what AI remembers about users:**

| Memory type | Scope | User control |
|---|---|---|
| **Session memory** | Current conversation only | Auto-clears |
| **Cross-session memory** | Persists across conversations | View, edit, delete |
| **User profile** | Stable preferences and facts | Full CRUD in settings |
| **Team memory** | Shared organizational context | Admin controls |

**Memory design rules:**
- Show users what AI remembers about them (transparency)
- Provide "forget" for any individual memory
- Provide "forget everything" nuclear option
- Don't remember sensitive information by default
- Distinguish between "remembering" and "training on"

### Customization vs. Automation

**Balancing user control and AI intelligence:**

| Spectrum | Description | Best for |
|---|---|---|
| **Full manual** | No AI, user does everything | Simple tasks, control-critical |
| **AI suggests** | AI offers options, user picks | Creative tasks, personal preference |
| **AI defaults + override** | AI picks, user can change | Routine tasks with occasional exceptions |
| **AI auto + review** | AI acts, user reviews after | High-volume tasks, low stakes |
| **Full auto** | AI handles end-to-end | Truly routine, zero-stakes tasks |

**Design principle:** Default to "AI suggests" and let users graduate to more automation as trust builds.

---

## Emerging AI Patterns

### Multimodal AI

**Combining text, image, audio, video:**

**Input patterns:**
- **Text + image** — "What's in this image?" / "Edit this photo to..."
- **Voice + screen** — "What am I looking at?" (screen context + voice)
- **Camera + AI** — Point camera, get real-time information
- **Document + chat** — Upload file, ask questions about it

**Output patterns:**
- **Text + image** — Generated explanation with diagrams
- **Text + audio** — Written response with voice narration option
- **Text + code** — Explanation with runnable code snippets
- **Rich cards** — Structured multi-element responses

**Multimodal design rules:**
- Let users choose their preferred input mode
- Show which modes are available (microphone icon, camera icon, attach)
- Handle mode switching gracefully (start typing, switch to voice)
- Output should match the richness of input when appropriate

### AI Agents

**Autonomous AI taking actions on behalf of users:**

**Agent patterns:**
- **Task agent** — "Book me a flight to NYC next Tuesday"
- **Research agent** — "Find the best CRM for our team and compare top 3"
- **Workflow agent** — "Every morning, summarize my unread emails"
- **Monitoring agent** — "Alert me when competitor X launches a new feature"

**Agent design principles:**
1. **Confirmation before action** — Always show plan before executing
2. **Progress visibility** — Show what the agent is doing in real-time
3. **Interruptibility** — User can pause or stop agent at any point
4. **Audit trail** — Full log of all actions taken
5. **Scope limits** — Clear boundaries on what agent can and cannot do
6. **Error recovery** — Agents will fail; design for graceful recovery

**Agent UI patterns:**
- **Plan preview** — "I'll do A, then B, then C. Proceed?"
- **Live activity feed** — Step-by-step log with timestamps
- **Checkpoint confirmation** — Pause for approval at critical steps
- **Result summary** — What was accomplished, what failed, what needs human attention

### AI Copilots

**Side-by-side AI collaboration:**

**Copilot layout patterns:**
- **Side panel** — AI assistant in right/left drawer alongside main workspace
- **Inline** — AI suggestions appear directly in the content (ghost text, highlights)
- **Floating** — Small AI widget user can position anywhere
- **Command palette** — Ctrl+K / Cmd+K to invoke AI actions
- **Contextual** — AI appears near the cursor/selection when relevant

**Copilot interaction patterns:**
- **Accept/reject** — Tab to accept, Esc to dismiss
- **Partial accept** — Accept word-by-word or line-by-line
- **Edit and accept** — Modify AI suggestion then apply
- **Ask for alternatives** — "Show me another option"
- **Explain** — "Why did you suggest this?"

### Generative UI

**AI creating interface elements dynamically:**

**Patterns:**
- **Dynamic forms** — AI generates form fields based on context
- **Adaptive dashboards** — AI creates relevant widgets/charts
- **Generated reports** — Custom layouts based on data
- **Smart templates** — AI modifies templates to fit user's needs

**Design guardrails for generative UI:**
- Generated UI must follow the existing design system
- User should be able to edit/customize generated UI
- Maintain consistency — generated elements shouldn't look foreign
- Progressive: Start with simple generated elements, add complexity over time
- Always allow manual creation as alternative

### Real-time AI

**Instant AI feedback and suggestions:**

| Pattern | Latency target | Example |
|---|---|---|
| **Autocomplete** | <100ms | Search suggestions, code completion |
| **Inline suggestions** | <500ms | Grammar fixes, smart compose |
| **Real-time analysis** | <1s | Sentiment as you type, live translation |
| **Background insights** | <5s | "You might also want to..." |

**Real-time design principles:**
- Suggestions must not disrupt typing/flow
- Visually distinct from user content (ghost text, different color)
- Dismissible with zero effort (keep typing = dismiss)
- No flicker — debounce suggestions to avoid visual noise

### AI Workflows

**Chaining multiple AI operations:**

**Workflow UI patterns:**
- **Pipeline view** — Visual flow showing AI steps: Input → Step 1 → Step 2 → Output
- **Progress tracker** — Which step is currently running, which completed
- **Intermediate results** — Show output of each step (not just final result)
- **Branch points** — Where human decision is needed between AI steps

**Workflow design rules:**
- Show the full pipeline upfront so users understand the process
- Let users inspect intermediate results
- Allow users to modify and re-run individual steps
- Save successful workflows as reusable templates

### AI Canvas/Workspaces

**Spatial interfaces for AI interaction:**

**Canvas patterns:**
- **Node-based** — AI operations as connected nodes (like Figma's FigJam or ComfyUI)
- **Card-based** — AI outputs as movable cards on infinite canvas
- **Thread-based** — Branching conversation trees
- **Artifact-based** — AI generates objects user can arrange spatially

### Voice AI Design

**Natural language voice interfaces:**

**Voice interaction design:**
- **Wake word** — Clear activation phrase or button
- **Listening indicator** — Visual feedback that system is hearing
- **Transcription display** — Show what was understood (allows correction)
- **Response modes** — Voice reply, text reply, or both
- **Fallback to text** — When voice isn't practical, easy text input switch

**Voice design rules:**
- Confirm understanding before acting ("I heard 'book flight to NYC'. Correct?")
- Keep voice responses concise (max 2-3 sentences)
- Provide visual accompaniment for complex responses
- Handle ambient noise gracefully
- Always have a non-voice alternative

---

## AI Technical Collaboration

### Prompt Engineering

**What designers should know about prompts:**

**Prompt components:**
- **System prompt** — Sets AI behavior, tone, constraints (invisible to user)
- **User prompt** — What the user types
- **Context** — Additional information injected (documents, data, history)
- **Examples** — Few-shot examples showing desired behavior

**Design-relevant prompt concepts:**
- **Temperature** — Higher = more creative/random, Lower = more deterministic/predictable
- **Max tokens** — Controls response length; design should handle variable-length outputs
- **Stop sequences** — When AI should stop generating
- **System prompt** — Designers should help craft the "personality" and constraints

### RAG (Retrieval-Augmented Generation)

**Designing for context injection:**

**What RAG means for design:**
- AI can reference specific documents/data (more accurate, less hallucination)
- UI should show which sources were consulted
- Users may need to manage their knowledge base (upload, delete, organize documents)

**RAG UI patterns:**
- **Source panel** — Show connected documents/data sources
- **Citation links** — Inline references to specific source passages
- **Knowledge base manager** — Upload, organize, search connected documents
- **Source selection** — Let users choose which sources AI should consult
- **Relevance indicators** — Show how closely sources match the query

### AI API Understanding

**Concepts designers should understand:**

| Concept | What it means | Design impact |
|---|---|---|
| **Tokens** | Units of text (~4 chars) that models process | Input length limits, cost per interaction |
| **Context window** | Maximum tokens model can process at once | How much history/context fits in a conversation |
| **Rate limits** | Maximum requests per time period | Queue design, retry logic, usage caps |
| **Latency** | Time between request and first response | Loading state design, streaming vs. batch |
| **Cost per token** | Price of processing text | Usage-based pricing UI, cost visibility |
| **Temperature** | Randomness/creativity of output | Consistency expectations, creative controls |
| **Streaming** | Receiving response token by token | Progressive display, cancel mid-generation |

### Model Versioning

**Handling AI model updates:**

**Design implications of model updates:**
- Output quality may change (better or worse for specific tasks)
- Response format may shift slightly
- Latency characteristics may change
- New capabilities may become available

**Design strategies:**
- Version pin for stability ("Using Model v2.1")
- Gradual rollout with A/B testing
- User notification when model changes
- Ability to roll back if quality regresses
- Test all AI-dependent UI flows when model updates

### Performance Optimization

**Balancing quality vs. speed vs. cost:**

| Strategy | Speed | Quality | Cost | When to use |
|---|---|---|---|---|
| **Cache common queries** | +++ | Same | --- | FAQ, repeated questions |
| **Smaller model for drafts** | ++ | - | -- | Real-time suggestions |
| **Streaming** | ++ (perceived) | Same | Same | Long responses |
| **Batch processing** | - | Same | -- | Non-urgent tasks |
| **Pre-compute** | +++ | Same | + | Predictable queries |
| **Progressive generation** | ++ | Improving | Same | Complex outputs |

### AI DevTools Integration

**Design awareness for AI infrastructure:**

| Tool | What it does | Design relevance |
|---|---|---|
| **LangChain/LlamaIndex** | Orchestrates AI workflows | Multi-step AI flows, chain visualization |
| **Vector databases** | Store and search embeddings | Semantic search UI, "similar items" |
| **Prompt management** | Version and A/B test prompts | Quality consistency, experimentation |
| **Observability** | Monitor AI performance | Admin dashboards, quality metrics |
| **Evaluation frameworks** | Automated quality testing | Design for testable AI interactions |

**Designer's role in AI technical decisions:**
- Advocate for user-facing quality metrics (not just technical accuracy)
- Push for streaming and low-latency where UX demands it
- Ensure error states and fallbacks are designed for every AI failure mode
- Request observability data that informs design decisions (what prompts fail? where do users give thumbs down?)
