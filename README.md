# AI Tone-and-Conversation Framework
### Scaling consistent product voice and conversational flow across distributed teams using AI

_(A prompt-based framework to evaluate and improve tone consistency and conversation design in product content at scale.)_

---

## Repository Structure

- `system.md` (systems thinking) → Tone principles and evaluation framework
- `prompts.md` (AI capability) → AI prompts for tone analysis, rewriting, and multi-turn conversation evaluation
- `examples.md` (practical application) → Real input/output examples, single-message and multi-turn
- `usage.md` (real-world usability) → How teams can apply this system in workflows
- `flows.md` (Phase 2, planned) → Structured conversation flow maps: success paths, failure paths, clarification paths
- `dialogue-principles.md` (Phase 2, planned) → Conversation-specific principles extending the core tone framework: Continuity, Recoverability, Progressive disclosure

---

## Overview

In fast-moving product teams, UI copy and conversational content are often written by multiple contributors: _Product Managers, Designers, and Engineers_. While this enables speed, it also leads to inconsistencies in tone, clarity, and user experience. And, in conversational and chatbot-driven products, inconsistencies in how a dialogue actually flows from one turn to the next.

This project explores how a **scalable content framework + AI layer** can help teams maintain a consistent voice and coherent conversation design, without relying on centralized content review.

---

## Problem Statement

In a multi-team product environment:

- Product managers and Designers write UI copy and conversational content independently
- Tone varies across features (formal vs casual, verbose vs concise)
- Content reviews become a bottleneck
- Users experience inconsistency across journeys — and, in conversational interfaces, across individual exchanges

Example (tone inconsistency):

- "Your booking has not been confirmed"
- "Oops! Something went wrong, your booking failed"

Example (conversation inconsistency):

- A chatbot acknowledges context in one turn, then resets and asks the user to repeat themselves in the next
- A failure state offers no next step, leaving the user stuck mid-conversation

These inconsistencies reduce user trust and product coherence.

---

## Objective

Design a scalable framework that:

- Defines a clear tone framework
- Defines conversation design principles for multi-turn, agent-driven exchanges
- Enables teams to self-evaluate content and conversation flows
- Uses AI to detect and improve inconsistencies in both

---

## Stakeholders (who this is designed for)

- Product Designers → writing interface copy and conversational scripts
- Product Managers → defining flows and messages
- Content Team → maintaining voice consistency
- Localization Teams → translating content at scale
- Conversation/AI Designers → structuring multi-turn dialogue and chatbot logic

---

## Approach

### 1. Tone Framework Definition

I defined 4 core tone principles:

- **Clear** → Easy to understand, no jargon
- **Reassuring** → Affirmative, reduces user doubts or confusions
- **Concise** → Avoids unnecessary words
- **Human** → Conversational but not overly casual

Each principle is applied consistently across all product surfaces and includes:

- good vs bad examples
- edge cases
- usage guidelines

---

### 2. System Design

I designed a reusable evaluation structure:

Each piece of content is assessed on:

- Clarity
- Emotional tone
- Length
- Actionability

---

### 3. AI-Powered Checker (single message)

I created a prompt-based system that:

**Input:**
- UI text
- Context (error, success, onboarding, etc.)

**Output:**
- Tone score (1–5)
- Identified issues
- Suggested improved version

**Example**

Input: Your request has not been processed due to an unexpected error.

Output:
- Tone score: 2/5
- Issues: overly formal, lacks guidance
- Suggested rewrite: Something went wrong. Please try again.

---

### 4. Conversation Design Layer (Phase 2, planned)

The single-message checker above evaluates one piece of content in isolation. It does not account for how a message performs in context — whether it acknowledges what a user just said, or how a conversation recovers when something goes wrong mid-exchange.

Phase 2 extends this framework with:

- **`flows.md`** — representative conversation flows mapped as structured state sequences (success path, failure path, clarification path), for scenarios such as booking confirmation, onboarding, and support escalation.
- **`dialogue-principles.md`** — conversation-specific principles extending the four tone principles above:
  - **Continuity** → does each turn acknowledge context from prior turns
  - **Recoverability** → does the flow degrade gracefully when a user goes off-script or isn't understood
  - **Progressive disclosure** → is information paced across an exchange, rather than delivered all at once
- **A multi-turn evaluator prompt**, extending the existing AI-powered checker: input is a full conversation transcript (3–6 exchanges), output includes a continuity score, recovery-handling assessment, tone consistency across the full exchange, and flagged breakpoints where the flow would likely lose a user.

This layer is in active development. It is not yet part of the working framework below.

---

## Testing

I tested the tone framework on:

- onboarding messages
- error states
- transactional notifications

Findings:

- Improved clarity across all cases
- Reduced verbosity
- More consistent tone across flows

---

## Iteration

Key improvements:

- Added context-aware prompting
- Refined tone scoring criteria
- Introduced edge-case handling (legal, safety messages)

---

## Impact

This framework enables:

- **Faster content creation** → teams don't wait for reviews
- **Consistent voice** → across features and teams
- **Scalability** → usable across multiple products and languages

Potential business impact:

- Reduced user confusion
- Increased trust
- Fewer support tickets

---

## Scalability

This framework can be extended to:

- Localization workflows
- Design tools (e.g. Figma plugins)
- Content QA pipelines
- Other content types (emails, notifications)
- Conversational and chatbot-driven products (Phase 2)

---

## Final Solution

A framework that includes:

1. **A structured tone framework**
2. **A reusable evaluation model**
3. **An AI-powered tone checker**
4. **A conversation design layer** (Phase 2, planned) — flow mapping, dialogue principles, and multi-turn evaluation

Together, they enable teams to:
- Self-evaluate content and conversation flows
- Improve clarity and consistency across single messages and full exchanges
- Reduce dependency on the content team

---

## How to Use This Framework

1. Copy the prompt from `prompts.md`
2. Input your UI text and context (or, once Phase 2 is complete, a full conversation transcript)
3. Review the evaluation and suggestions
4. Apply the improved version
5. Iterate if needed

---

## Key Insight

Content consistency is not a writing problem — it is a **system design problem**. The same is true of conversation design: a chatbot that loses context mid-exchange isn't a scripting failure, it's a structural one.

AI becomes valuable when it enables teams to operate independently while maintaining quality standards, across both individual messages and full conversational exchanges.

---

## Next Steps

- Complete Phase 2: conversation flow mapping and multi-turn evaluation
- Integrate into product design workflows
- Expand prompt system for more contexts
- Connect with localization and QA processes
