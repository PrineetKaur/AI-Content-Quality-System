# Examples

This document shows real input/output examples using the tone consistency system; both single-message evaluations (using Prompt 1) and full conversation transcripts (using Prompt 6, Phase 2).

---

## Example 1: Error Message

**Input:**
Your request has not been processed due to an unexpected error.

**Output:**
- Clarity: 3/5
- Tone: 2/5
- Conciseness: 3/5
- Actionability: 1/5

**Issues:**
- Overly formal
- No guidance
- Slightly verbose

**Improved Version:**
Something went wrong. Please try again.

---

## Example 2: Payment Failure

**Input:**
Transaction unsuccessful. Please verify your payment credentials and attempt again.

**Output:**
- Clarity: 3/5
- Tone: 2/5
- Conciseness: 2/5
- Actionability: 3/5

**Issues:**
- Too formal
- Slightly complex wording

**Improved Version:**
Payment failed. Check your details or try another method.

---

## Example 3: Empty State

**Input:**
No records found.

**Output:**
- Clarity: 3/5
- Tone: 2/5
- Conciseness: 5/5
- Actionability: 1/5

**Issues:**
- No guidance
- Cold tone

**Improved Version:**
No bookings yet. Start by searching for a ride.

---

## Example 4: Overly Casual Tone

**Input:**
Oops! We totally messed up 😅

**Output:**
- Clarity: 3/5
- Tone: 1/5
- Conciseness: 4/5
- Actionability: 1/5

**Issues:**
- Too casual
- Not reassuring
- No next step

**Improved Version:**
Something went wrong. Please try again.

---

## Example 5: Success Message

**Input:**
Your request has been successfully processed.

**Output:**
- Clarity: 4/5
- Tone: 3/5
- Conciseness: 3/5
- Actionability: 2/5

**Issues:**
- Slightly formal
- Could be more natural

**Improved Version:**
You're all set!

---

## Key Takeaway (Single-Message Examples)

Consistent improvements follow predictable patterns:
- simplify language
- reduce formality
- add guidance
- align tone

These patterns hold for individual messages. The examples below extend the same evaluation logic to full conversations, where the unit of analysis is the exchange, not any one message.

---

## Example 6: Onboarding — Progressive Disclosure (from Flow 2)

**Scenario:** onboarding

**Transcript (Before):**
```
Bot:   Welcome — let's get you set up. First, what are you hoping to use this for?
User:  Mainly tracking team tasks.
Bot:   Great! Here's everything: projects, task assignment, deadlines, integrations,
       notifications settings, and reporting dashboards. Let us know if you have questions.
User:  ...ok I'm lost, where do I even start?
```

**Output:**
- Continuity: 2/5
- Recoverability: 2/5
- Progressive Disclosure: 1/5
- Tone Consistency: 3/5

**Issues:**
- Turn 3 abandons the stated goal ("tracking team tasks") and lists every feature at once
- No pacing — six features delivered in a single message with no clear starting point
- User's confusion in turn 4 is a direct, predictable result of turn 3

**Flagged Breakpoint:** Turn 3 → Turn 4. A user this early in onboarding is unlikely to recover from an unpaced info-dump; this is where a real user would most likely abandon setup.

**Transcript (After):**
```
Bot:   Welcome — let's get you set up. First, what are you hoping to use this for?
User:  Mainly tracking team tasks.
Bot:   Got it. Let's start with creating your first project.
User:  Done.
Bot:   Nice. Next, here's how to assign tasks to teammates.
User:  Done.
Bot:   You're set up for task tracking. Anything else you want to configure now, or should we stop here?
```

**Output:**
- Continuity: 5/5
- Recoverability: 5/5 (not tested, no recovery needed)
- Progressive Disclosure: 5/5
- Tone Consistency: 5/5

**Why It Works:** Each step ties back to the goal stated in turn 2 ("tracking team tasks"), and features are introduced one at a time, matching Progressive Disclosure as defined in `dialogue-principles.md`.

---

## Example 7: Support Escalation — Continuity at Handoff (from Flow 3)

**Scenario:** support escalation

**Transcript (Before):**
```
User:  My export keeps failing partway through.
Bot:   That usually happens with files over 50MB. Try splitting the export into two batches. Want steps?
User:  I already tried that, still fails
Bot:   I'm sorry you're having trouble. You're being transferred to an agent.
```

**Output:**
- Continuity: 1/5
- Recoverability: 3/5
- Progressive Disclosure: 4/5
- Tone Consistency: 4/5

**Issues:**
- Turn 4 hands off without passing along what's already been tried (file size, batching, still failing)
- The user will likely have to repeat their entire issue to the human agent

**Flagged Breakpoint:** Turn 4. Not a drop-off risk in the same way as Example 6, but a trust and efficiency failure — the user did the work of describing and troubleshooting the issue, and the handoff discards it.

**Transcript (After):**
```
User:  My export keeps failing partway through.
Bot:   That usually happens with files over 50MB. Try splitting the export into two batches. Want steps?
User:  I already tried that, still fails
Bot:   Sorry that didn't fix it. I'm bringing in a support agent. They'll see that your
       export fails on files over 50MB even after splitting the batch.
Bot:   You're connected. Agent has the full context above, no need to repeat it.
```

**Output:**
- Continuity: 5/5
- Recoverability: 5/5
- Progressive Disclosure: 4/5
- Tone Consistency: 5/5

**Why It Works:** The handoff in turn 4 explicitly restates what's already been tried, so Continuity carries through the escalation instead of resetting at the exact moment the user is already frustrated.

---

## Example 8: Booking — Ambiguous Input Handling (from Flow 1)

**Scenario:** booking

**Transcript:**
```
User:  Book me a table for 2 at 7pm tonight.
Bot:   Checking availability for 7pm, party of 2...
Bot:   7pm is fully booked tonight, so I couldn't confirm that one.
User:  ugh ok whatever try again
Bot:   Happy to try again — did you want a different time, or should I check nearby dates?
User:  different time, 8:30
Bot:   Checking 8:30pm for 2...
Bot:   Booked — table for 2 at 8:30pm.
```

**Output:**
- Continuity: 5/5
- Recoverability: 5/5
- Progressive Disclosure: 4/5
- Tone Consistency: 4/5

**Issues:**
- None flagged as breakpoints; the vague retry request in turn 4 ("try again") is met with a narrowing question rather than a repeat of the failed request, which is the correct Recoverability response

**Flagged Breakpoint:** None. Included as a positive reference example, this is the shape a Recoverability response should take when user input is ambiguous rather than off-topic.

**Why It Works:** Rather than re-attempting the same failed 7pm request, or asking a generic "can you clarify?", the bot narrows to the two concrete options (different time or different date) that would actually resolve the ambiguity.

---

## Key Takeaway (Multi-Turn Examples)

Multi-turn failures rarely come from any single bad message  Examples 6–8 all contain individually well-formed turns. The failures come from what happens *between* turns: dropped context, unpaced information, or generic recovery that doesn't narrow toward a resolution. This is why Prompt 6 evaluates the transcript as a whole rather than scoring turns independently.
