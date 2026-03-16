# AI UX Patterns & Design

## Conversational Design

### Chatbot & AI assistant patterns

**Conversation structure:**
- **System message** — Sets the AI's role, tone, and boundaries (invisible to user)
- **User turn** — User input (text, voice, image)
- **AI turn** — AI response (text, structured output, actions)
- **Follow-up** — Suggestions for next steps

### Dialogue flow design principles
1. **Start with intent detection** — Understand what the user wants before generating
2. **Confirm before acting** — For high-stakes actions, confirm intent
3. **Recover gracefully** — When AI misunderstands, offer correction paths
4. **Maintain context** — Reference previous turns naturally
5. **Know when to escalate** — Hand off to human when AI can't help

### Conversational UI components

| Component | Purpose | When to use |
|---|---|---|
| **Chat bubble** | Display conversation turns | Multi-turn dialogue |
| **Typing indicator** | Show AI is processing | Short wait times (<5s) |
| **Streaming text** | Show AI generating in real-time | Longer responses |
| **Suggestion chips** | Offer quick follow-up actions | After AI response |
| **Action cards** | Show structured results | When AI returns data/options |
| **Source citations** | Show where AI got information | Factual claims |
| **Feedback buttons** | Thumbs up/down on response | Every AI response |

### Conversation anti-patterns
- **Dead ends** — AI responds but offers no next step
- **Loops** — AI keeps asking the same clarifying question
- **Personality overdose** — Too much personality, not enough utility
- **Context amnesia** — AI forgets what was discussed earlier
- **Over-qualification** — "As an AI, I..." before every response

## Prompt Interface Design

### Input field patterns

**Simple prompt input:**
- Large, inviting text area with placeholder example
- Send button with keyboard shortcut indicator
- Character/token counter if limits exist

**Enhanced prompt input:**
- Attachment support (images, files, links)
- Prompt templates / starter prompts
- Context chips showing what's included (current page, selection, etc.)
- Model/mode selector if multiple options
- Tone/style controls

### Prompt design best practices
- **Placeholder text** — Show an example prompt, not "Type your message"
- **Auto-resize** — Text area grows with input (min 1 line, max 6 before scroll)
- **Submit on Enter** — Shift+Enter for newlines (show hint)
- **Draft persistence** — Save unsubmitted prompts across sessions
- **History** — Access to previous prompts for reuse

### Constraint communication
- Show character/token limits as progress bar, not number
- Surface relevant context automatically: "Using: [current document]"
- Indicate which model/mode is active
- Show estimated cost per interaction if usage-based pricing

## AI Onboarding

### First-time AI feature onboarding

**Progressive onboarding pattern:**
1. **Introduction** — What this AI can do (2-3 examples, not a feature list)
2. **Guided first interaction** — Pre-filled prompt or walkthrough
3. **Quick win** — Ensure first output is useful (curate the experience)
4. **Capabilities discovery** — Surface new capabilities over time via tooltips

### Onboarding anti-patterns
- Showing all capabilities at once (overwhelming)
- Technical language ("RAG-augmented with 128k context window")
- No example prompts (blank canvas intimidation)
- Skipping the AI disclosure (users don't realize it's AI)

### Onboarding content hierarchy
1. What it does (one sentence)
2. How to use it (one example)
3. What it can't do (one limitation)
4. How to give feedback (thumbs up/down)

## Transparency Design

### Showing how AI makes decisions

**Levels of transparency:**
- **Level 0: Black box** — No explanation (avoid this)
- **Level 1: Label** — "AI-generated" badge
- **Level 2: Summary** — "Based on your purchase history and similar users"
- **Level 3: Factors** — Show which inputs influenced the output
- **Level 4: Full explanation** — Detailed reasoning chain (for expert users)

### Transparency patterns
- **"Why this?" links** — Expandable explanation for AI recommendations
- **Source citations** — Inline references with links to original content
- **Influence indicators** — Visual showing which factors drove the decision
- **Confidence scores** — How sure the AI is about its output
- **Model disclosure** — Which AI model was used (for advanced users)

### When to show what
- Always: AI-generated label, feedback mechanism
- By default: Summary-level explanation
- On demand: Detailed factors, sources, confidence
- For experts: Full reasoning chain, model info

## Explainability UI

### Making AI outputs understandable

**Explanation patterns:**
- **Natural language explanation** — "I recommended this because you liked similar items"
- **Feature highlight** — Highlight which parts of input influenced output
- **Comparison** — "Option A scores higher on X, Option B on Y"
- **Confidence bands** — Visual range showing certainty level
- **Counterfactual** — "If you changed X, the recommendation would be Y"

### Explainability design rules
- Use the user's language, not model terminology
- Lead with the most important factor
- Keep explanations concise (1-2 sentences default, expandable)
- Visual explanations > text for complex decisions
- Don't explain the obvious — only explain the surprising

## Confidence Indicators

### Showing AI certainty/uncertainty

| Confidence level | Visual pattern | When to show |
|---|---|---|
| **High** (>90%) | No indicator needed, or subtle green check | Factual answers, classifications |
| **Medium** (60-90%) | Yellow/amber indicator, "likely" language | Recommendations, predictions |
| **Low** (<60%) | Orange/red indicator, explicit caveat | Novel queries, ambiguous requests |
| **Unknown** | "I'm not sure" + suggestion to verify | Out-of-domain questions |

### Design approaches
- **Verbal** — "I'm fairly confident..." / "This might be..." / "I'm not sure, but..."
- **Visual** — Color-coded indicators, progress bars, meter gauges
- **Structural** — Multiple options with scores, "best guess" vs "alternatives"
- **Behavioral** — Auto-suggest verification for low-confidence outputs

### Rules
- Never show false confidence — if the AI doesn't know, say so
- Don't show raw probability numbers to non-expert users
- Map confidence to actionable guidance: high = trust, medium = verify, low = don't rely

## Human-in-the-Loop Design

### Enabling human oversight and correction

**HITL patterns:**

| Pattern | Description | Use when |
|---|---|---|
| **Review before publish** | AI drafts, human approves | Content generation, emails |
| **Edit after generate** | AI outputs, human refines | Code generation, reports |
| **Approve/reject** | AI suggests, human decides | Recommendations, classifications |
| **Escalation** | AI handles routine, escalates edge cases | Support, moderation |
| **Teaching** | Human corrects AI, AI learns | Feedback loops, fine-tuning |

### HITL design principles
- Make the "edit" path as easy as the "accept" path
- Show what AI changed so humans can review efficiently (diff view)
- Track human corrections to improve AI over time
- Don't make HITL feel like extra work — frame as quality control

## AI Feedback Mechanisms

### Core feedback patterns

**Explicit feedback:**
- **Thumbs up/down** — Simplest signal, lowest friction
- **Star rating** — More granular but higher friction
- **Regenerate** — Implicit "this wasn't good enough"
- **Edit output** — What the user changed reveals what was wrong
- **Report** — Flag harmful, inaccurate, or inappropriate output

**Implicit feedback:**
- **Copy/use** — User copied or applied the output (positive signal)
- **Ignore** — User didn't engage with AI suggestion
- **Time spent** — How long user spent reading/editing output
- **Follow-up prompt** — What user asked next (refinement = not satisfied)

### Feedback UI placement
- Thumbs up/down: End of every AI response
- Regenerate: Prominent button near output
- Edit: Inline editing on AI-generated content
- Report: Secondary action (overflow menu or small link)

### Feedback loop closure
- Show users that their feedback matters: "Thanks — this helps improve responses"
- Periodically show improvement: "We've improved X based on feedback like yours"

## Copilot Patterns

### AI as assistant, not replacement

**Copilot design principles:**
1. **User drives** — Human sets direction, AI helps execute
2. **Suggestions, not insertions** — AI proposes, user accepts/modifies/rejects
3. **Side by side** — AI works in a panel, not taking over the main canvas
4. **Context-aware** — Copilot understands what user is working on
5. **Dismissible** — Easy to hide, not in the way when not needed
6. **Learns from use** — Adapts to user's style and preferences

**Copilot UI patterns:**
- **Inline suggestions** — Ghost text that appears as you type (GitHub Copilot)
- **Side panel** — AI assistant in a drawer/sidebar
- **Command palette** — Ctrl+K style AI action menu
- **Contextual tooltip** — AI suggestion appears near cursor/selection
- **Chat thread** — Persistent conversation alongside work

### Copilot anti-patterns
- Taking over the cursor or canvas
- Showing suggestions that interrupt the user's flow
- Requiring users to switch contexts to use AI
- Making AI feel mandatory rather than optional

## Suggestion UI

### Displaying AI recommendations effectively

**Suggestion formats:**
- **Single suggestion** — One clear recommendation with explanation
- **Ranked list** — Multiple options ordered by relevance
- **Grouped options** — Categories of suggestions
- **Comparison table** — Side-by-side with pros/cons
- **Progressive** — Start with top suggestion, reveal more on request

**Suggestion design rules:**
- Lead with the best option, not all options
- Show why this suggestion is relevant to the user
- Make accepting a suggestion one click/tap
- Make dismissing a suggestion equally easy
- Don't repeat dismissed suggestions immediately
- Show variety — don't always suggest the same type of thing
