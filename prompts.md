# AI Prompts for Tone Consistency

This file contains reusable prompts for evaluating and improving UI content and for evaluating multi-turn conversation flows.

---

## Prompt 1: Tone Evaluation

You are a content quality assistant.

Evaluate the following UI text based on these criteria:

- Clarity
- Tone (aligned with: clear, reassuring, concise, human)
- Conciseness
- Actionability

Provide:

1. A score (1–5) for each category
2. A short explanation of issues
3. A suggested improved version

Context:
{{context}}

Text:
{{text}}

---

## Prompt 2: Tone Improvement

You are a UX writer.

Rewrite the following UI text to align with this tone:

- Clear
- Reassuring
- Concise
- Human

Rules:

- Avoid jargon
- Keep it short
- Guide if needed
- Do not be overly casual

Context:
{{context}}

Text:
{{text}}

---

## Prompt 3: Error Message Generator

You are a UX writer designing error messages.

Given an error scenario, generate a user-friendly message that:

- Explains what happened
- Avoids technical language
- Suggests a clear next step
- Uses a calm and reassuring tone

Input:
{{error_description}}

---

## Prompt 4: Tone Consistency Check (Batch)

You are a content reviewer.

Analyze the following list of UI messages.

Tasks:

- Identify inconsistencies in tone
- Highlight messages that do not match the tone system
- Suggest improved versions

Messages:
{{list_of_texts}}

---

## Prompt 5: Localization Readiness Check

You are a localization-aware content reviewer.

Check if the following text:

- Is unambiguous
- Avoids idioms or cultural references
- Is easy to translate

Suggest improvements if needed.

Text:
{{text}}

---

## Prompt 6: Multi-Turn Conversation Evaluator (Phase 2)

You are a conversation design reviewer.

Evaluate the following conversation transcript (a full exchange of user and bot turns, not a single message) based on these criteria:

- **Continuity** — does each bot turn acknowledge relevant context from prior turns, rather than treating each message as the first
- **Recoverability** — when the user goes off-script, is ambiguous, or isn't understood, does the conversation degrade gracefully rather than loop or fail
- **Progressive Disclosure** — is information paced appropriately across turns, rather than delivered all at once
- **Tone Consistency** — does tone (Clear, Reassuring, Concise, Human, per `system.md`) hold steady across every bot turn, not just the first or last

Provide:

1. A score (1–5) for Continuity, Recoverability, Progressive Disclosure, and overall Tone Consistency
2. A short explanation of issues found, referencing specific turns by number
3. Flagged breakpoints — the specific turn(s) where a real user would likely disengage, and why
4. A suggested revised version of the turns that need it (not necessarily the full transcript)

Context:
{{scenario_type}} (e.g. booking, onboarding, support escalation)

Transcript:
{{conversation_transcript}}

### Notes on this prompt

- This prompt evaluates a full transcript, not a single message — it's meant to run alongside Prompt 1 (Tone Evaluation), not replace it. Use Prompt 1 for individual messages; use Prompt 6 to review how a full exchange holds together.
- Like the flows in `flows.md`, this checks against representative scenario types (booking, onboarding, support escalation) rather than an exhaustive taxonomy — extend `{{scenario_type}}` as new flow types are added.
- This is a design/review prompt, not a live conversation manager — it's meant for evaluating transcripts after the fact (or in design review), not for generating bot responses in real time.

---

## Usage Notes

- Replace placeholders (`{{text}}`, `{{context}}`, `{{error_description}}`, `{{list_of_texts}}`) before using Prompts 1–5
- For Prompt 6, replace `{{scenario_type}}` and `{{conversation_transcript}}` with a full multi-turn exchange, not a single message
- Use context to improve output quality
- Iterate prompts for better results
