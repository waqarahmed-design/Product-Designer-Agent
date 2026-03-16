# AI States, Edge Cases & Quality Evaluation

## Loading States

### AI processing takes longer than traditional UI

| Duration | User perception | Design response |
|---|---|---|
| **0-300ms** | Instant | No indicator needed |
| **300ms-2s** | Brief wait | Typing indicator / pulse animation |
| **2-10s** | Noticeable wait | Progress message ("Analyzing your data...") |
| **10-30s** | Long wait | Step-by-step progress ("Reading documents... Generating summary...") |
| **30s+** | Very long | Background processing with notification when done |

### Loading state patterns
- **Typing indicator** — Three dots animation (conversational UI)
- **Skeleton + shimmer** — Placeholder showing expected output shape
- **Step indicator** — "Step 1 of 3: Reading your document..."
- **Progress narration** — Descriptive messages that update: "Searching 1,247 articles..."
- **Cancel button** — Always provide a way to abort long-running AI requests

### Loading state copy
- Be specific: "Analyzing 3 documents" not "Loading..."
- Use active verbs: "Searching", "Writing", "Comparing"
- Set expectations: "This usually takes 10-15 seconds"
- Show progress: "Found 12 relevant results, generating summary..."

## Streaming States

### Token-by-token generation UI

**Streaming design principles:**
1. **Start immediately** — Show first token as soon as it arrives
2. **Smooth rendering** — Buffer slightly to avoid character-by-character jitter
3. **Show cursor** — Blinking cursor at generation point indicates "still working"
4. **Allow scrolling** — User should be able to scroll up while generation continues
5. **Enable early stopping** — "Stop generating" button visible during streaming

**Streaming patterns:**
- **Chat-style streaming** — Text appears in chat bubble, grows as content arrives
- **Document streaming** — Content fills into document/editor area
- **Structured streaming** — Headers/sections appear as structure emerges
- **Code streaming** — Syntax highlighting applies progressively

**Streaming anti-patterns:**
- Auto-scrolling that fights user's manual scrolling
- No way to stop generation mid-stream
- Layout shifting as content length changes
- Hiding action buttons until generation completes

## Error States

### AI-specific error types and design responses

| Error | User sees | Design |
|---|---|---|
| **Model unavailable** | "AI is temporarily unavailable" | Graceful fallback, retry button, non-AI alternative |
| **Rate limited** | "You've reached your limit" | Usage meter, upgrade path, time until reset |
| **Content filtered** | "I can't help with that" | Brief explanation, suggest alternative phrasing |
| **Context too long** | "Input is too long" | Character count, suggest trimming, auto-summarize option |
| **Timeout** | "This is taking too long" | Retry, simplify request suggestion, background option |
| **Invalid input** | "I didn't understand that" | Examples, suggest rephrasing, template |
| **Low quality output** | AI responds but poorly | Regenerate button, refine prompt suggestion |

### Error design principles
- **Never show raw error codes** — Translate technical errors to human language
- **Always offer a next step** — Retry, rephrase, try alternative, contact support
- **Preserve user input** — Never lose what the user typed when an error occurs
- **Degrade gracefully** — If AI fails, offer non-AI fallback when possible

## Hallucination Handling

### Detecting and mitigating incorrect AI outputs

**Design strategies for hallucination:**

| Strategy | Implementation | Trade-off |
|---|---|---|
| **Source citations** | Show references for factual claims | Adds UI complexity, requires RAG |
| **Confidence indicators** | Show certainty level | Users may over-trust "high confidence" |
| **Verification prompts** | "Would you like me to verify this?" | Adds friction |
| **Disclaimer** | "AI can make mistakes — verify important info" | Easily ignored |
| **Fact-check links** | Link to authoritative sources | Requires source database |
| **Edit/correct UI** | Let users flag and fix incorrect outputs | Needs feedback pipeline |

### Hallucination severity tiers

| Tier | Impact | Design response |
|---|---|---|
| **Critical** | Medical, legal, financial advice | Strong disclaimers, mandatory human review, link to professional |
| **High** | Factual claims about real entities | Source citations, verification UI |
| **Medium** | Recommendations, analysis | Confidence indicators, "verify" nudge |
| **Low** | Creative content, brainstorming | Minimal — errors are less consequential |

### Design rules for hallucination
- Never present AI output as verified fact without sources
- Make it easy to report and correct errors
- Don't anthropomorphize ("I know" → "Based on available information")
- For critical domains, require human verification before acting on AI output

## Rate Limiting

### Designing for usage caps and quotas

**Rate limit communication:**
- Show current usage: "12 of 50 messages used today"
- Warn before hitting limit: "5 messages remaining"
- At limit: Clear explanation + when it resets or how to get more
- Never: Silent failure or confusing error

**Rate limit UI patterns:**
- **Usage meter** — Visual bar showing consumption
- **Countdown** — "Resets in 4 hours"
- **Upgrade prompt** — "Need more? Upgrade to Pro for unlimited"
- **Queue position** — "You're #12 in line" (for shared resources)
- **Smart rationing** — Warn users to save messages for important tasks

## Timeout Handling

### Long-running AI requests

**Timeout tiers:**
- **30s** — Show "still working" message with option to wait or cancel
- **60s** — Offer to continue in background with notification
- **120s+** — Auto-background, notify when complete

**Design patterns:**
- Always show elapsed time for long requests
- Offer "notify me when done" for background processing
- Preserve partial results if timeout occurs mid-generation
- Auto-retry once silently, then surface error to user

## Degraded Performance

### Fallback experiences when AI is slow or unavailable

**Graceful degradation ladder:**
1. **Full AI** — Normal experience
2. **Cached AI** — Serve previous/similar results with "may not be current" label
3. **Simplified AI** — Use faster, less capable model
4. **Rule-based fallback** — Non-AI heuristic (search, templates, defaults)
5. **Manual** — Show the non-AI way to accomplish the task
6. **Informational** — "AI unavailable, try again later" with status page link

### Design principles
- Users shouldn't need to know there's a fallback in place
- Always communicate current capability level
- Never silently downgrade quality — tell users if they're getting a simpler model

## Empty States

### First-time AI feature use

**Empty state content:**
1. **What this does** — One clear sentence
2. **How to start** — Example prompt or action button
3. **Example output** — Show what good output looks like
4. **Privacy note** — Brief reassurance about data handling

**Empty state patterns:**
- Starter prompts: 3-4 clickable example prompts
- Demo mode: Show pre-populated example conversation
- Template gallery: Browse use-case templates
- Quick-start wizard: Guided 3-step first interaction

## Moderation & Safety

### Handling inappropriate requests

**Request filtering design:**
- Soft block: "I can't help with that, but I can help you with [alternative]"
- Hard block: "This request goes against our usage policy"
- Never: Lecture, shame, or over-explain why the request was blocked

**Output filtering design:**
- Content warning before potentially sensitive output
- Blur/redact with option to reveal
- Report button accessible from every output
- Audit log for enterprise compliance

---

# AI Quality & Evaluation

## Output Quality Assessment

### Quality dimensions for AI output

| Dimension | Definition | How to measure |
|---|---|---|
| **Accuracy** | Factually correct | Human evaluation, automated fact-checking |
| **Relevance** | Addresses the user's actual request | Task completion rate, user satisfaction |
| **Completeness** | Covers all aspects of the request | Checklist evaluation, follow-up question rate |
| **Coherence** | Logically structured, well-written | Readability scores, human evaluation |
| **Helpfulness** | Actually helps the user achieve their goal | Task success rate, thumbs up/down ratio |
| **Safety** | No harmful, biased, or inappropriate content | Automated safety checks, human review |

### Quality feedback loop
1. Collect feedback (thumbs, edits, regenerations)
2. Analyze patterns (which types of requests get poor feedback?)
3. Improve (better prompts, RAG, fine-tuning, UI changes)
4. Measure improvement (A/B test, quality score trend)

## Accuracy Metrics

### Understanding AI accuracy for designers

| Metric | What it means | Design implication |
|---|---|---|
| **Precision** | Of items AI flagged as positive, how many actually are? | High precision = fewer false alarms |
| **Recall** | Of all actual positives, how many did AI catch? | High recall = fewer missed items |
| **F1 Score** | Balance of precision and recall | Overall quality indicator |
| **Hallucination rate** | % of outputs containing fabricated info | Determines need for citations/verification |
| **Task completion rate** | % of requests where AI successfully helps | Core quality metric |

### Accuracy thresholds by use case
- **Search/discovery** — 80%+ relevance acceptable
- **Classification/tagging** — 90%+ accuracy expected
- **Content generation** — Quality is subjective; measure via satisfaction
- **Factual Q&A** — 95%+ accuracy required; design for verification below that
- **Safety-critical** — 99%+ accuracy or mandatory human review

## AI Testing Methods

### Testing AI features from a design perspective

**Prompt testing:**
- Test with diverse prompt styles (short/long, formal/casual, vague/specific)
- Test edge cases (empty input, very long input, non-English, special characters)
- Test adversarial inputs (prompt injection attempts, off-topic requests)
- Test across user personas (novice vs expert prompters)

**Output testing:**
- Compare outputs across same prompt (consistency check)
- Test formatting (does structured output render correctly?)
- Test streaming (does incremental rendering work smoothly?)
- Test error states (what happens when model fails?)

**Integration testing:**
- Test feedback mechanisms (do thumbs work, does regenerate work?)
- Test rate limiting (graceful degradation at limits?)
- Test with slow network (streaming behavior, timeouts?)
- Test with concurrent users (performance under load?)

## Bias Detection

### Identifying bias in AI outputs

**Types of bias to test:**
- **Demographic bias** — Different quality for different user groups
- **Cultural bias** — Assumptions based on Western/English-centric norms
- **Representation bias** — Image generation shows limited diversity
- **Language bias** — Better performance for English vs. other languages
- **Recency bias** — Overweighting recent information

**Bias testing approach:**
1. Define protected attributes relevant to your use case
2. Create test sets that vary only the protected attribute
3. Compare AI output quality across groups
4. Flag disparities above threshold
5. Document and address in prompt engineering or model selection

## User Satisfaction Metrics

### Measuring AI feature satisfaction

| Metric | How to collect | Target |
|---|---|---|
| **Thumbs up ratio** | Thumbs up / (thumbs up + thumbs down) | >80% for good quality |
| **Regeneration rate** | Regenerate clicks / total responses | <15% (lower is better) |
| **Edit rate** | % of outputs users edited before using | Context-dependent |
| **Abandonment rate** | % of AI interactions with no follow-up action | <30% |
| **CSAT** | Post-interaction survey | >4.0 / 5.0 |
| **Task success rate** | % of tasks completed using AI | >70% |
| **Return rate** | % of users who use AI feature again within 7 days | >50% |

## Continuous Evaluation

### Monitoring AI performance over time

**Dashboard metrics:**
- Response quality score (rolling average of feedback)
- Error rate by error type
- Latency (p50, p95, p99)
- Usage volume and growth
- Cost per interaction
- User satisfaction trend

**Alerting thresholds:**
- Quality score drops >10% week-over-week
- Error rate exceeds 5%
- P95 latency exceeds 10s
- Negative feedback ratio exceeds 25%

## A/B Testing AI Features

### Testing different AI implementations

**What to A/B test:**
- Different prompts / system messages
- Different models (fast vs. capable)
- Different UI patterns (chat vs. inline vs. sidebar)
- Different explanation levels (none vs. brief vs. detailed)
- Different feedback mechanisms (thumbs vs. stars vs. edit)

**A/B testing AI challenges:**
- Outputs are non-deterministic — need larger sample sizes
- User learning effects — users improve at prompting over time
- Quality is subjective — use multiple metrics, not just one
- Model updates may invalidate results — note model version in test data
