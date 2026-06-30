# AI Tone Consistency System  
### Scaling consistent product voice across distributed teams using AI

_(A promped-based framwork to evaluate and improve tone consistency in product UI copy at scale.)_

---

## Repository Structure

- `system.md` (systems thinking) → Tone principles and evaluation framework  
- `prompts.md` (AI capability) → AI prompts for tone analysis and rewriting  
- `examples.md` (practical application) → Real input/output examples  
- `usage.md` (real-world usability) → How teams can apply this system in workflows  

---

## Overview

In fast-moving product teams, UI copy is often written by multiple contributors: _Product Managers, Designers, and Engineers_. While this enables speed, it also leads to inconsistencies in tone, clarity, and user experience.

This project explores how a **scalable content system + AI layer** can help teams maintain a consistent voice without relying on centralized content review.

---

## Problem Statement

In a multi-team product environment:

- Product managers and Designers write UI copy independently 
- Tone varies across features (formal vs casual, verbose vs concise)  
- Content reviews become a bottleneck  
- Users experience inconsistency across journeys  

Example:

- “Your booking has not been confirmed”  
- “Oops! Something went wrong, your booking failed”  

These inconsistencies reduce user trust and product coherence.

---

## Objective

Design a scalable system that:

- Defines a clear tone framework
- Enables teams to self-evaluate content
- Uses AI to detect and improve inconsistencies

---

## Stakeholders (who are designing for)

- Product Designers → writing interface copy
- Product Managers → defining flows and messages
- Content Team → maintaining voice consistency
-  Localization Teams → translating content at scale

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

### 3. AI-Powered Checker

I created a prompt-based system that:

### Input:
- UI text  
- Context (error, success, onboarding, etc.)

### Output:
- Tone score (1–5)  
- Identified issues  
- Suggested improved version  

---

### Example

**Input:**
Your request has not been processed due to an unexpected error.

**Output:**
- Tone score: 2/5  
- Issues:
  - overly formal  
  - lacks guidance  
- Suggested rewrite:
Something went wrong. Please try again.

---

## Testing

I tested the system on:

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

This system enables:

- **Faster content creation**__ → teams don’t wait for reviews
- **Consistent voice**__ → across features and teams
- **Scalability**__ → usable across multiple products and languages

Potential business impact:

- Reduced user confusion
- Increased trust
- Fewer support tickets

---

## Scalability

This system can be extended to:

- Localization workflows  
- Design tools (e.g. Figma plugins)  
- Content QA pipelines  
- Other content types (emails, notifications)  

---

## Final Solution

A System that includes:

1. **A structured tone framework**  
2. **A reusable evaluation model**  
3. **An AI-powered tone checker**

Together, they enable teams to:
- Self-evaluate Content  
- Improve Clarity and Consistency  
- Reduce Dependency on the Content team

---

## How to Use This System

1. Copy the prompt from `prompts.md`  
2. Input your UI text and context  
3. Review tone evaluation and suggestions  
4. Apply the improved version  
5. Iterate if needed  

---

## Key Insight

Content consistency is not a writing problem — it is a **system design problem**.

AI becomes valuable when it enables teams to operate independently while maintaining quality standards.

---

## Next Steps

- Integrate into product design workflows  
- Expand prompt system for more contexts  
- Connect with localization and QA processes  

---
