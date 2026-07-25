# AI Tone-and-Conversation Framework

### Scaling consistent product voice and conversational flow across distributed teams using AI

_(A prompt-based framework to evaluate and improve tone consistency and conversation design in product content at scale.)_

---

## Repository Structure

- `system.md` _(systems thinking)_ → Tone principles and evaluation framework
- `prompts.md` _(AI capability)_ → AI prompts for tone analysis, rewriting, and multi-turn conversation evaluation
- `examples.md` _(practical application)_ → Real input/output examples, single-message and multi-turn
- `usage.md` _(real-world usability)_ → How teams can apply this system in workflows
- `flows.md` _(conversation architecture)_ → Structured conversation flow maps: success paths, failure paths, clarification paths
- `dialogue-principles.md` _(conversation design)_ → Conversation-specific principles extending the core tone framework: continuity, recoverability, progressive disclosure

---

## Overview

In fast-moving product teams, UI copy and conversational content are often written by multiple contributors: _Product Managers, Designers, and Engineers_. While this enables speed, it also leads to inconsistencies in tone, clarity, and user experience, and in conversational and chatbot-driven products, inconsistencies in how a dialogue actually flows from one turn to the next.

This project explores how a **scalable content framework plus an AI layer** can help teams maintain a consistent voice and coherent conversation design, without relying on centralized content review.

---

## Problem Statement

In a multi-team product environment:

- Product managers and Designers write UI copy and conversational content independently
- Tone varies across features (formal vs casual, verbose vs concise)
- Content reviews become a bottleneck
- Users experience inconsistency across journeys, and in conversational interfaces, across individual exchanges

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
- Tone score (1 to 5)
- Identified issues
- Suggested improved version

**Example**

Input: Your request has not been processed due to an unexpected error.

Output:
- Tone score: 2/5
- Issues: overly formal, lacks guidance
- Suggested rewrite: Something went wrong. Please try again.

---

### 4. Conversation Design Layer

A single-message checker evaluates one piece of content in isolation. It does not account for how a message performs in context, whether it acknowledges what a user just said, or how a conversation recovers when something goes wrong mid-exchange.

This layer extends the framework with:

- **`flows.md`** → representative conversation flows mapped as structured state sequences (success path, failure path, clarification path), for scenarios such as booking confirmation, onboarding, and support escalation. Each flow includes a full state map and three traced dialogue paths.
- **`dialogue-principles.md`** → three conversation-specific principles extending the four tone principles above:
  - **Continuity** → does each turn acknowledge context from prior turns
  - **Recoverability** → does the flow degrade gracefully when a user goes off-script or isn't understood
  - **Progressive disclosure** → is information paced across an exchange, rather than delivered all at once
- **A multi-turn evaluator prompt** (Prompt 6 in `prompts.md`) → input is a full conversation transcript, output includes scores for Continuity, Recoverability, Progressive Disclosure, and overall Tone Consistency, plus flagged breakpoints where a real user would likely disengage.

These are representative flows and principles for design review, not an exhaustive state machine and not a built or tested dialogue manager. See `flows.md` for the explicit scope note on what these are and are not.

---

## Testing

I tested the tone framework on:

- onboarding messages
- error states
- transactional notifications

I tested the conversation design layer against three representative flows, booking, onboarding, and support escalation, each traced through a success path, a failure path, and an ambiguous input path (see `flows.md` and `examples.md`).

Findings:

- Improved clarity across all single-message cases
- Reduced verbosity
- More consistent tone across flows
- Multi-turn failures traced back to specific, nameable causes: dropped context, unpaced information, or generic recovery that does not narrow toward resolution, rather than any single badly worded message (see Examples 6 to 8 in `examples.md`)

---

## Iteration

Key improvements:

- Added context-aware prompting
- Refined tone scoring criteria
- Introduced edge-case handling (legal, safety messages)
- Extended evaluation from single messages to full conversation transcripts, with a dedicated multi-turn prompt and scoring model

---

## Impact

This framework enables:

- **Faster content creation** → teams don't wait for reviews
- **Consistent voice** → across features, teams, and full conversational exchanges
- **Scalability** → usable across multiple products, languages, and conversational surfaces

Potential business impact:

- Reduced user confusion
- Increased trust
- Fewer support tickets
- Fewer conversational drop-offs at identifiable breakpoints

---

## Scalability

This framework can be extended to:

- Localization workflows
- Design tools (e.g. Figma plugins)
- Content QA pipelines
- Other content types (emails, notifications)
- Additional conversation flow types beyond the three mapped here (timeouts, multi-issue conversations, repeated failures)

---

## Final Solution

A framework that includes:

1. **A structured tone framework**
2. **A reusable evaluation model**
3. **An AI-powered tone checker**
4. **A conversation design layer**, flow mapping, dialogue principles, and multi-turn evaluation

Together, they enable teams to:
- Self-evaluate content and conversation flows
- Improve clarity and consistency across single messages and full exchanges
- Reduce dependency on the content team

---

## How to Use This Framework

1. Copy the relevant prompt from `prompts.md`, Prompt 1 for a single message, Prompt 6 for a full transcript
2. Input your UI text and context, or a full conversation transcript
3. Review the evaluation and suggestions
4. Apply the improved version
5. Iterate if needed

---

## Key Insight

Content consistency is not a writing problem; it is a **system design problem**. 
The same is true of conversation design. A chatbot that loses context mid-exchange is not a scripting failure; it is a **structural failure**.

AI becomes valuable when it enables teams to operate independently while maintaining quality standards, across both individual messages and full conversational exchanges.

---

## Next Steps

- Expand prompt system for more contexts and additional flow types
- Connect with localization and QA processes
- Integrate into product design workflows
