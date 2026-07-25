# Conversation Flows

This document maps representative multi-turn conversation flows as structured state sequences. It extends the single-message tone evaluation in `system.md` and `prompts.md` to sequences of turns, where each message depends on what came before.

Each flow below includes:

- A **state map** of the discrete states a conversation can be in, what triggers a transition, and where it can go next
- Three **traced paths** through that map *(Success, Failure, and Ambiguous/Clarification)* shown as actual turn-by-turn dialogue

These are representative flows for design review, not an exhaustive state machine and not a built or tested dialogue manager. The goal is to give the multi-turn evaluator (added to `prompts.md` in Phase 2) something concrete to check against, and to give `dialogue-principles.md` real states to point to when it defines Continuity, Recoverability, and Progressive Disclosure.

---

## Flow 1: Booking Confirmation / Failure

### Scenario
A user is booking a ride or reservation through a product's chat-style interface.

### State Map

| State | Description | Triggered By | Leads To |
|---|---|---|---|
| S0 — Request Submitted | User has provided initial booking details | User sends booking request | S1 |
| S1 — Availability Check | System checks whether the request can be fulfilled | Automatic, no user input | S2 (available) or S3 (unavailable) |
| S2 — Confirmed | Booking is successful | Availability check passes | S6 (end) |
| S3 — Failed | Booking cannot be completed (no availability, payment issue) | Availability check fails | S4 or S5 |
| S4 — Clarification Requested | System didn't get enough information to retry (e.g., user says "try again" with no new detail) | Ambiguous or incomplete user reply after S3 | S1 (retry) or S5 |
| S5 — Recovery Offer | System proposes alternatives (different time, different option) | After S3, or after S4 resolves | S1 (retry) or S6 (user declines, end) |
| S6 — End | Conversation resolves, confirmed or user disengages | S2 or S5 | — |

### Path A — Success

```
User:  Book me a table for 2 at 7pm tonight.                                     [S0]
Bot:   Checking availability for 7pm, party of 2...                              [S1]
Bot:   You're booked — table for 2 at 7pm. See you then.                    [S2 → S6]
```

### Path B — Failure

```
User:  Book me a table for 2 at 7pm tonight.                                     [S0]
Bot:   Checking availability for 7pm, party of 2...                              [S1]
Bot:   7pm is fully booked tonight, so I couldn't confirm that one.              [S3]
Bot:   I can get you in at 6pm or 8:30pm instead — want either of those?         [S5]
User:  8:30 works.
Bot:   Booked — table for 2 at 8:30pm.                                 [S1 → S2 → S6]
```

### Path C — Ambiguous Input / Clarification

```
User:  Book me a table for 2 at 7pm tonight.                                     [S0]
Bot:   Checking availability for 7pm, party of 2...                              [S1]
Bot:   7pm is fully booked tonight, so I couldn't confirm that one.              [S3]
User:  ugh ok whatever try again
Bot:   Happy to try again. Did you want a different time,
       or should I check nearby dates?                                           [S4]
User:  different time, 8:30
Bot:   Checking 8:30pm for 2...                                                  [S1]
Bot:   Booked — table for 2 at 8:30pm.                                      [S2 → S6]
```

Note where the flow could lose the user: at S3→S4, if the bot restated the same failed request without asking what "try again" means, it would repeat the failure and the user would likely abandon. This is the kind of breakpoint the multi-turn evaluator (Phase 2 addition to `prompts.md`) is meant to flag.

---

## Flow 2: Onboarding

### Scenario
A new user is being walked through initial product setup.

### State Map

| State | Description | Triggered By | Leads To |
|---|---|---|---|
| S0 — Welcome | Bot greets user, sets expectation for what onboarding covers | User starts onboarding | S1 |
| S1 — Goal Collection | Bot asks what the user is trying to accomplish | After S0 | S2 |
| S2 — Guided Walkthrough (Step 1) | Bot introduces one relevant feature at a time, based on goal from S1 | After S1 | S3, or S4 if user goes off-script |
| S3 — Guided Walkthrough (Step 2+) | Bot continues, referencing the goal stated in S1 (not repeating full context) | After S2 confirms understanding | S5, or S4 if interrupted |
| S4 — Off-Script Interruption | User asks something unrelated to the current step (e.g., a billing question) | User input doesn't match expected next step | S6 (answer + return), then back to S2/S3 |
| S5 — Setup Confirmation | Bot confirms setup is complete relative to the stated goal | After walkthrough steps complete | S7 |
| S6 — Redirect & Resume | Bot answers the interruption briefly, then explicitly returns to where onboarding left off | After S4 | S2 or S3 (resumed) |
| S7 — Completion | Onboarding ends | After S5 | — |

### Path A — Success (with progressive disclosure)

```
Bot:   Welcome — let's get you set up. First,
       what are you hoping to use this for?                                 [S0 → S1]
User:  Mainly tracking team tasks.
Bot:   Got it. Let's start with creating your first project.                     [S2]
       (single step shown, not the full feature list)
User:  Done.
Bot:   Nice. Next, here's how to assign tasks to teammates.                      [S3]
User:  Done.
Bot:   You're set up for task tracking. Anything else you want to configure,
       or should we stop here?                                              [S5 → S7]
```

### Path B — Failure (context dumped, no continuity)

```
Bot:   Welcome — let's get you set up. First,
       what are you hoping to use this for?                                 [S0 → S1]
User:  Mainly tracking team tasks.
Bot:   Great! Here's everything: projects, task assignment, deadlines,
       integrations, notification settings, and reporting dashboards.
       Let us know if you have questions.        [S2 — breaks progressive disclosure]
User:  ...ok I'm lost, where do I even start?
```
This path fails at S2: dumping all steps at once instead of pacing them, and not tying the walkthrough back to "tracking team tasks," is the kind of breakpoint the multi-turn evaluator should flag as a Progressive Disclosure violation.

### Path C — Ambiguous Input / Off-Script Interruption

```
Bot:   Welcome — let's get you set up. First,
       what are you hoping to use this for?                                 [S0 → S1]
User:  Mainly tracking team tasks.
Bot:   Got it. Let's start with creating your first project.                     [S2]
User:  Wait, actually, how do I update my billing plan?
Bot:   You can change your plan under Settings > Billing. Back to setup:    [S4 → S6]
       You were creating your first project for task tracking.
       Want to continue there?
User:  Yes
Bot:   Great, go ahead and name your project.                            [S2 resumed]
```

Note the resume line explicitly restates the goal ("task tracking"). This is what distinguishes a Continuity-preserving recovery from one that just drops the user back in with no context.

---

## Flow 3: Support Escalation

### Scenario
A user reports a problem to a support bot; the bot attempts self-serve resolution before involving a human agent.

### State Map

| State | Description | Triggered By | Leads To |
|---|---|---|---|
| S0 — Issue Reported | User describes a problem | User message | S1 |
| S1 — Bot Attempts Resolution | Bot offers a troubleshooting step based on the described issue | After S0 | S2 (resolved), S3 (unresolved), or S4 (unclear) |
| S2 — Resolved | User confirms the issue is fixed | User confirms after S1 | S7 (end) |
| S3 — Unresolved | User indicates the step didn't help, or expresses frustration | User reply after S1 | S5 |
| S4 — Clarification Needed | Bot cannot map the user's description to a known issue | User description is vague or doesn't match known categories | S0 (re-ask) or S5 |
| S5 — Escalate to Human Agent | Bot hands off, passing the conversation context forward | After S3 or repeated S4 | S6 |
| S6 — Handoff Confirmation | Bot confirms handoff and what the agent will see | After S5 | S7 |
| S7 — End | Conversation resolves, self-serve or handed off | S2 or S6 | — |

### Path A — Success (self-serve resolution)

```
User:  My export keeps failing partway through.                                  [S0]
Bot:   That usually happens with files over 50MB.
       Try splitting the export into two batches — want steps?                   [S1]
User:  yes
Bot:   [steps provided]
User:  That worked, thanks.
Bot:   Glad that fixed it.                                                  [S2 → S7]
```

### Path B — Failure → Escalation (with continuity preserved at handoff)

```
User:  My export keeps failing partway through.                                  [S0]
Bot:   That usually happens with files over 50MB.
       Try splitting the export into two batches — want steps?                   [S1]
User:  I already tried that, still fails
Bot:   Sorry that didn't fix it. I'm bringing in a support agent.           [S3 → S5]
       They'll see that your export fails on files over 50MB even
       after splitting the batch.
Bot:   You're connected. Agent has the full context above,                  [S6 → S7]
       no need to repeat it.  
```

### Path C — Ambiguous Input / Clarification

```
User:  it's just broken                                                          [S0]
Bot:   Sorry to hear that. Can you tell me what specifically isn't working:
       exporting, logging in, or something else?                                 [S4]
User:  exporting
Bot:   Got it. Are you seeing an error message,
       or does it just stop partway through?                                     [S4]
User:  stops partway
Bot:   That usually happens with files over 50MB.
       Try splitting the export into two batches. Want steps?                    [S1]
```

Note the breakpoint risk at S4: if the bot asked a second broad question instead of narrowing ("what specifically isn't working" → "error or stops?"), a frustrated user is likely to drop off. The multi-turn evaluator should flag repeated open-ended clarification as a Recoverability failure, distinct from a single well-scoped clarifying question.

---

## What These Flows Are (and Aren't)

- They are: worked examples showing how a sequence of turns can be mapped as states, used to ground the multi-turn tone evaluator and the conversation-specific principles in `dialogue-principles.md`.
- They are not: a complete specification for a production dialogue manager, an exhaustive list of edge cases, or implemented/tested conversational logic. Real systems would need many more states (timeouts, multi-issue conversations, repeated failures beyond one retry, etc.) — these three are illustrative, not comprehensive.
