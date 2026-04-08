---
name: microinteractions-animation
description: "Micro-interactions and animation — covers Saffer's Trigger-Rules-Feedback-Loops framework, signature moments, scoring, motion principles, animation patterns, advanced techniques, and performance. Use when designing or auditing microinteractions, implementing loading animations, hover effects, button feedback, page transitions, scroll animations, pull-to-refresh, swipe gestures, toggles, modals, or toasts. Also covers physics-based motion, spring animations, Lottie, SVG animation, morphing, easing curves, orchestration, and 60fps performance with prefers-reduced-motion support. Triggers on: microinteraction, animation, motion, easing, spring physics, timing, duration, loading spinner, skeleton screen, hover effect, button press, page transition, scroll animation, parallax, pull-to-refresh, swipe gesture, toggle switch, modal animation, toast, Lottie, SVG animation, morphing, reduced motion, 60fps, orchestration, state transition."
---

# Micro-interactions & Animation

From the conceptual framework (why and what to design) to the technical implementation (how to animate it). Covers Saffer's four-part design structure, signature moments, and case studies — plus motion principles, animation patterns, advanced techniques, and performance.

## Method Selection Guide

| Question | Reference |
|----------|-----------|
| What is a microinteraction and how do I design one? | `.claude/skills/microinteractions-animation/design-framework.md` → Core Principle |
| How do I score/audit a microinteraction? | `.claude/skills/microinteractions-animation/design-framework.md` → Scoring + Quick Diagnostic |
| How do I design the trigger? | `.claude/skills/microinteractions-animation/design-framework.md` → Triggers |
| How do I design rules and state? | `.claude/skills/microinteractions-animation/design-framework.md` → Rules |
| How do I design feedback for an interaction? | `.claude/skills/microinteractions-animation/design-framework.md` → Feedback |
| How do I handle loops and modes? | `.claude/skills/microinteractions-animation/design-framework.md` → Loops and Modes |
| How do I create a signature/iconic moment? | `.claude/skills/microinteractions-animation/signature-moments.md` |
| How do I design a form submission interaction? | `.claude/skills/microinteractions-animation/case-studies.md` → Case Study 1 |
| How do I design a toggle/switch? | `.claude/skills/microinteractions-animation/case-studies.md` → Case Study 2 |
| How do I design pull-to-refresh? | `.claude/skills/microinteractions-animation/case-studies.md` → Case Study 3 |
| How do I design loading states? | `.claude/skills/microinteractions-animation/case-studies.md` → Case Study 4 |
| How do I design toast notifications? | `.claude/skills/microinteractions-animation/case-studies.md` → Case Study 5 |
| What easing curve should I use? | `.claude/skills/microinteractions-animation/motion-principles.md` → Timing & Easing |
| How long should this animation be? | `.claude/skills/microinteractions-animation/motion-principles.md` → Duration |
| How do I sequence multiple animations? | `.claude/skills/microinteractions-animation/motion-principles.md` → Orchestration |
| How do I transition between two states? | `.claude/skills/microinteractions-animation/motion-principles.md` → State Transitions |
| How do I build a loading state? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Loading Animations |
| How do I add hover effects? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Hover Effects |
| How do I animate button presses? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Click/Tap Feedback |
| How do I animate between screens? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Page Transitions |
| How do I trigger animations on scroll? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Scroll-Based Animation |
| How do I implement pull-to-refresh? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Pull-to-Refresh |
| How do I animate swipe actions? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Swipe Gestures |
| How do I animate toggles and switches? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Toggle Animations |
| How do I animate modals and dialogs? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Modal Animations |
| How do I animate toast notifications? | `.claude/skills/microinteractions-animation/animation-patterns.md` → Toast Notifications |
| How do I morph between shapes? | `.claude/skills/microinteractions-animation/advanced-animation.md` → Morphing |
| How do I use spring physics? | `.claude/skills/microinteractions-animation/advanced-animation.md` → Physics-Based Animation |
| How do I use Lottie animations? | `.claude/skills/microinteractions-animation/advanced-animation.md` → Lottie Animations |
| How do I animate SVGs? | `.claude/skills/microinteractions-animation/advanced-animation.md` → SVG Animation |
| How do I make loading feel faster? | `.claude/skills/microinteractions-animation/advanced-animation.md` → Loading Optimism |
| How do I use motion to guide attention? | `.claude/skills/microinteractions-animation/advanced-animation.md` → Attention Direction |
| How do I express brand through motion? | `.claude/skills/microinteractions-animation/advanced-animation.md` → Personality Expression |
| How do I keep animations at 60fps? | `.claude/skills/microinteractions-animation/performance-accessibility.md` → Animation Performance |
| How do I respect reduced motion? | `.claude/skills/microinteractions-animation/performance-accessibility.md` → Reduced Motion |
| How do I treat animation as enhancement? | `.claude/skills/microinteractions-animation/performance-accessibility.md` → Progressive Enhancement |

## Domain Sequencing

```
Motion Principles (the rules behind all motion)
  └── Timing & Easing → Duration → Orchestration
      → Continuity → State Transitions

Animation Patterns (apply principles to specific UI elements)
  └── Loading → Hover → Click/Tap → Page Transitions
      → Scroll → Pull-to-Refresh → Swipe → Toggle
      → Modal → Toast

Advanced Animation (specialized techniques)
  └── Morphing → Physics-Based → Lottie → SVG
      → Loading Optimism → Attention Direction → Personality

Performance & Accessibility (make it fast and inclusive)
  └── Animation Performance → Reduced Motion
      → Progressive Enhancement
```

## Reference Files

- **Design framework** — Read `.claude/skills/microinteractions-animation/design-framework.md` for: Saffer's Trigger-Rules-Feedback-Loops structure, state design, scoring (0–10), diagnostic checklist, common mistakes
- **Signature moments** — Read `.claude/skills/microinteractions-animation/signature-moments.md` for: what makes a moment signature, iconic examples (Slack, Stripe, Facebook Like), where to invest, creation process
- **Case studies** — Read `.claude/skills/microinteractions-animation/case-studies.md` for: detailed breakdowns of form submission, toggle, pull-to-refresh, loading states, toast notifications — with edge cases and platform notes
- **Motion principles** — Read `.claude/skills/microinteractions-animation/motion-principles.md` for: timing & easing, duration, orchestration, continuity, state transitions
- **Animation patterns** — Read `.claude/skills/microinteractions-animation/animation-patterns.md` for: loading, hover, click/tap, page transitions, scroll, pull-to-refresh, swipe, toggle, modal, toast
- **Advanced animation** — Read `.claude/skills/microinteractions-animation/advanced-animation.md` for: morphing, physics-based, Lottie, SVG, loading optimism, attention direction, personality expression
- **Performance & accessibility** — Read `.claude/skills/microinteractions-animation/performance-accessibility.md` for: 60fps performance, reduced motion, progressive enhancement
