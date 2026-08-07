# Usage Guide

This guide explains how product teams can use the Tone Consistency System, for both individual messages and full conversation transcripts.

---

## Who This Is For

- Content Designers maintaining Voice Consistency
- Product Designers writing UI copy and conversational scripts
- Product Managers defining Product Flows
- Conversation/AI Designers structuring multi-turn dialogue and chatbot logic

---

## When to Use

Use this system when:

- Writing new UI content
- Reviewing existing content
- Preparing content for release
- Scaling across multiple features
- Designing or reviewing a multi-turn conversation flow (booking, onboarding, support escalation, or similar)

---

## Workflow

### Step 1 — Define Context

Identify:

- What type of message? (error, success, onboarding)
- What is the user trying to do?
- Is this a single message, or a full conversation exchange? If it's a conversation, which scenario type does it map to (see `flows.md`)?

---

### Step 2 — Evaluate Content

**For a single message:**
Use the Tone Evaluation Prompt (Prompt 1) from `prompts.md`
Check:
- clarity
- tone
- conciseness
- actionability

**For a full conversation transcript:**
Use the Multi-Turn Conversation Evaluator (Prompt 6) from `prompts.md`
Check:
- continuity — does each turn acknowledge prior context
- recoverability — does the flow degrade gracefully when the user goes off-script or isn't understood
- progressive disclosure — is information paced across turns
- tone consistency — does tone hold steady across every turn

See `dialogue-principles.md` for the definitions behind these, and `flows.md` for worked examples of the scenario types Prompt 6 checks against.

---

### Step 3 — Improve Content

- For a single message: apply suggestions, or use the Tone Improvement Prompt (Prompt 2)
- For a conversation transcript: apply the revised turns suggested by Prompt 6, focusing first on any flagged breakpoints — the turns where a real user would likely disengage

---

### Step 4 — Validate

Ensure:

- tone aligns with system
- message is clear and helpful
- user knows what to do next
- for conversations: context carries across turns, and the flow has a graceful path if the user goes off-script (see Recoverability in `dialogue-principles.md`)

---

### Step 5 — Document Patterns

If similar issues repeat:

- update system guidelines
- create reusable patterns
- if a recurring conversation breakpoint shows up across multiple flows, consider whether it points to a gap in `dialogue-principles.md` or a new flow type worth adding to `flows.md`

---

## Example Workflow

**Single message:**
1. PM writes error message
2. Designer reviews using Prompt 1
3. AI suggests improvements
4. Final version is applied
5. Pattern is reused across product

**Conversation transcript:**
1. Designer drafts or exports a multi-turn flow (e.g. onboarding)
2. Reviewer runs the transcript through Prompt 6
3. AI flags breakpoints and scores Continuity, Recoverability, Progressive Disclosure, and Tone Consistency
4. Flagged turns are revised
5. Pattern is checked against `flows.md` and reused across similar flow types

---

## Integration Opportunities

This system can be integrated into:

- design workflows (Figma)
- product documentation
- QA processes
- localization pipelines
- conversation/chatbot design reviews, using `flows.md` and Prompt 6 alongside existing message-level QA

---

## Best Practices

- Always include context when using prompts
- Avoid over-relying on AI without judgment
- Use system principles as the source of truth for single messages, and `dialogue-principles.md` as the source of truth for conversation flow
- Iterate and refine over time

---

## Key Principle

This system is not meant to replace content designers or conversation designers.
It is designed to:
→ enable teams
→ scale consistency across single messages and full conversations
→ reduce bottlenecks
