---
name: aidlc
description: AI Design Lifecycle (AIDLC) — comprehensive skill for designing AI-powered product experiences. Covers AI product strategy, AI-specific user research, AI UX patterns (conversational UI, copilots, prompt interfaces, suggestion UI), AI interaction design (streaming, multi-turn, regeneration), AI states and edge cases (loading, hallucination, rate limiting, moderation), AI quality evaluation, AI safety and ethics (bias, consent, transparency, content moderation), AI personalization (adaptive UI, recommendations, feedback loops), emerging AI patterns (agents, generative UI, multimodal), and AI technical collaboration (prompt engineering, RAG, tokens, context windows). Use when designing any AI/ML feature, chatbot, copilot, recommendation system, generative AI interface, AI onboarding, AI error handling, or AI-assisted workflow. Triggers on: AI, ML, LLM, chatbot, copilot, conversational UI, prompt, generative AI, recommendation, suggestion, AI assistant, streaming response, hallucination, AI safety, AI ethics, bias, content moderation, AI onboarding, confidence indicator, human-in-the-loop, AI feedback, regenerate, AI agent, multimodal, RAG, fine-tuning, prompt engineering, AI personalization, adaptive UI, AI quality, AI testing.
---

# AI Design Lifecycle (AIDLC)

Design AI-powered experiences that are useful, trustworthy, and transparent. AI features have unique UX challenges — this skill provides the frameworks.

## When to load references

| User's task involves | Load |
|---|---|
| AI feature strategy, use case identification, AI business models, AI competitive analysis, AI roadmapping | [ai-product-strategy.md](references/ai-product-strategy.md) |
| Understanding AI user needs, trust research, AI mental models, AI anxiety, prompt research | [ai-research.md](references/ai-research.md) |
| Conversational UI, prompt interfaces, copilot patterns, AI onboarding, transparency, explainability, suggestion UI, confidence indicators | [ai-design-patterns.md](references/ai-design-patterns.md) |
| AI loading states, streaming UI, hallucination handling, error states, rate limiting, moderation, timeouts | [ai-states-quality.md](references/ai-states-quality.md) |
| AI bias, fairness, consent, privacy, content moderation, watermarking, misuse prevention, AI ethics | [ai-safety-ethics.md](references/ai-safety-ethics.md) |
| AI agents, generative UI, multimodal, AI personalization, adaptive UI, prompt engineering, RAG, AI technical collaboration | [ai-emerging-technical.md](references/ai-emerging-technical.md) |

## Core principle

AI features must earn user trust through **transparency**, **control**, and **graceful failure**. Users should always know:
1. When AI is acting vs. a deterministic system
2. How confident the AI is in its output
3. How to correct, override, or turn off the AI

## Quick reference: AI UX heuristics

- **Set expectations** — Tell users what the AI can and cannot do before they use it
- **Show your work** — Explain why the AI made a recommendation or decision
- **Fail gracefully** — AI will be wrong; design for recovery, not perfection
- **Keep humans in control** — AI suggests, user decides
- **Design for iteration** — First AI output is rarely final; enable refinement
- **Be honest about limitations** — Never hide uncertainty or pretend AI is human
