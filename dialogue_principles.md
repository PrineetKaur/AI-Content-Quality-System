# Dialogue Principles

This document extends the four core tone principles in `system.md` (Clear, Reassuring, Concise, Human) with three principles specific to multi-turn conversation design. The original four still apply to every individual turn. These three govern how turns relate to each other across an exchange.

They are grounded in the flows mapped in `flows.md`; each example below references a specific state from that document.

---

## Relationship to Core Tone Principles

A single turn can be Clear, Reassuring, Concise, and Human, and still fail as part of a conversation, for example, by ignoring what the user just said, or by not knowing how to recover when the user goes off-script. The principles below don't replace the four core ones; they sit alongside them and apply at the level of the exchange rather than the message.

---

## 1. Continuity

- Each turn should acknowledge relevant context from prior turns, rather than treating every message as if it were the first.
- This does not mean repeating the full conversation history, only what's relevant to the user's current decision.

✅ Example (from Flow 2, Onboarding, S4 → S6):
```
User:  wait, actually, how do I update my billing plan?
Bot:   You can change your plan under Settings > Billing. Back to setup. 
       You were creating your first project for task tracking. Want to continue there?
```

❌ Example:
```
User:  Wait, actually, how do I update my billing plan?
Bot:   You can change your plan under Settings > Billing.
Bot:   Let's continue. What would you like to do next?
```
The second response answers the question but drops the thread entirely; the user now has to re-orient themselves back into onboarding with no help from the bot.

**Edge cases:**
- Continuity doesn't require referencing context that's no longer relevant if the user explicitly starts a new topic, the bot can follow them there without forcing a callback.
- Continuity can conflict with Conciseness (a core principle from `system.md`) if taken too far; restating unnecessary history to "prove" the bot remembers is itself a tone violation. The bar is relevance, not recall.

---

## 2. Recoverability

- When a user goes off-script, is misunderstood, or gives input that doesn't map to an expected next step, the conversation should degrade gracefully, narrowing toward understanding or a handoff rather than failing, looping, or blaming the user.

✅ Example (from Flow 3, Support Escalation, S4):
```
User:  it's just broken
Bot:   Sorry to hear that — can you tell me what specifically isn't working:
       exporting, logging in, or something else?
```

❌ Example:
```
User:  it's just broken
Bot:   I'm sorry, I didn't understand that. Could you rephrase your question?
User:  it doesnt work
Bot:   I'm sorry, I didn't understand that. Could you rephrase your question?
```
The second version repeats the same generic prompt without narrowing, which is what actually causes drop-off, not the initial ambiguity.

**Edge cases:**
- After roughly two failed attempts to understand the user, the flow should escalate to a human rather than keep re-asking (see Flow 3, S3 → S5); persistent re-prompting is itself a recoverability failure, not a fix for one.
- Ambiguous input ("it's just broken") and off-topic input ("how do I update my billing plan?") call for different recovery strategies; the first needs narrowing, the second needs a brief answer and an explicit return to the prior thread (Continuity). Treating both the same way undermines whichever principle actually applies.

---

## 3. Progressive Disclosure

- Information relevant to a multi-step process should be paced one meaningful chunk at a time, matched to where the user actually is, not delivered all at once regardless of relevance.

✅ Example (from Flow 2, Onboarding, S2 → S3):

`
Bot:   Got it. Let's start with creating your first project.
...
Bot:   Nice. Next, here's how to assign tasks to teammates.
`

❌ Example:
```
Bot:   Great! Here's everything: projects, task assignment, deadlines, integrations,
       notifications settings, and reporting dashboards. Let us know if you have questions.
```
This is the failure path traced in Flow 2: every feature is presented at once, disconnected from the goal the user actually stated ("tracking team tasks"), leaving them without a clear starting point.

**Edge cases:**
- Progressive disclosure shouldn't be forced pacing for users who signal they already know the material (e.g., a returning user asking to skip ahead); the principle is about matching pace to need, not imposing a fixed number of steps regardless of signal.
- Progressive disclosure is not the same as being vague. Withholding necessary information at a given step to "pace" the conversation is a Recoverability and Clarity problem, not good disclosure; each chunk should still be complete enough to act on.

---

## Key Principle

A conversation can satisfy every core tone principle turn-by-turn and still lose the user between turns. Continuity, Recoverability, and Progressive Disclosure describe the structural properties of an exchange, not the wording of any single message, which is why they need a multi-turn evaluator, not just a single-message check, to assess (see the Phase 2 addition to `prompts.md`).
