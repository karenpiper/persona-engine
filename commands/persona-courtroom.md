---
description: Multi-round persona feedback panel — test creative, messaging, campaigns, or strategy input against a set of personas across 3 structured rounds with synthesis between each
allowed-tools: Read, Write, Glob, Agent
argument-hint: [@input-file or leave blank to paste input]
---

Test creative work, messaging, campaigns, or strategic input against a panel of personas in three structured rounds. Each round builds on the last. A synthesis agent reads all persona feedback after each round and surfaces patterns, watchouts, and recommended revisions.

---

## Process

### Step 1 — Load the input

- If `$ARGUMENTS` references a file path, read that file as the input to evaluate
- If no file is given, ask the user: "What would you like to put in front of the panel? You can paste copy, a brief, a concept description, a campaign idea, or any other input."
- Confirm the input by displaying it clearly, labeled **"Input Under Evaluation"**

---

### Step 2 — Load the personas

Identify which personas to include in the panel.

- If persona files are specified in `$ARGUMENTS` (e.g., `@personas/01-csuite-leader.md`), use those
- Otherwise, scan the workspace for persona `.md` files:
  - Check the current project directory for a `personas/` folder
  - Check for any files matching `**/*persona*.md` or `**/personas/*.md`
  - List found personas and confirm with the user: "I found [N] personas. Should I run the full panel, or would you like to select a subset?"
- Read each selected persona file in full before proceeding

---

### Step 3 — Select or build the question set

Present the available question set options:

**Option A — Creative Testing**
Designed for copy, headlines, slogans, creative concepts, visual ideas.

**Option B — Messaging Testing**
Designed for messaging frameworks, value propositions, brand positioning, taglines.

**Option C — Campaign Testing**
Designed for campaign platforms, integrated campaign ideas, channel strategies.

**Option D — Product / Experience Testing**
Designed for product concepts, prototypes, UX flows, feature ideas.

**Option E — Custom**
User provides their own questions.

**Option F — Mixed**
Pick a base set and add custom questions on top.

Ask: "Which question set would you like to use? You can pick a preset, add your own questions, or mix both."

Read the question sets from `skills/persona-courtroom/question-sets.md` and present the relevant set based on the user's choice.

If the user provides custom questions, add them to the selected set. Confirm the final question list before proceeding.

---

### Step 4 — Round 1: Independent Assessment

**Brief the user:**
> "**Round 1 — Independent Assessment.** Each persona evaluates the input without knowing what others think. Running [N] personas in parallel now..."

Launch all persona agents **simultaneously** using the Agent tool — one per persona, all in parallel. Each agent receives:
- The full persona file content
- The input under evaluation
- The confirmed question list
- Instructions to use the `persona-evaluator` agent behavior (defined in `agents/persona-evaluator.md`)

**Prompt template for each Round 1 persona agent:**
```
You are running the persona-evaluator role for the IBM persona courtroom.

PERSONA FILE:
[full content of persona file]

INPUT UNDER EVALUATION:
[full input text]

QUESTIONS:
[numbered question list]

Follow the persona-evaluator instructions exactly. Read the persona file thoroughly, then evaluate the input from that persona's perspective. Answer each question in the persona's authentic voice. Be direct, specific, and honest — not diplomatic.

Output your response in the exact format specified in the persona-evaluator instructions.
```

Collect all Round 1 persona responses. Display each one clearly labeled with the persona name and number.

---

### Step 4b — Round 1 Synthesis

After all Round 1 responses are collected, run a synthesis agent with this task:

```
You are the Synthesis Agent for a persona feedback panel. Read all Round 1 persona responses below and produce a structured synthesis.

PERSONAS IN PANEL: [list]
INPUT EVALUATED: [brief description]

ROUND 1 RESPONSES:
[all persona responses]

Produce a synthesis in this exact format:

## Round 1 Synthesis

### Overall Panel Reaction
One paragraph (4–6 sentences) characterizing the panel's general reaction — the emotional temperature, the dominant attitude, the degree of consensus or division.

### Where the Panel Converges
3–5 specific points where multiple personas share the same reaction, concern, or response. For each: name the pattern, quote 2–3 personas briefly, and state the implication.

### Where the Panel Divides
2–4 specific points where personas have meaningfully different reactions. For each: name the split, characterize each side, and state what this means for the input's audience fit.

### Top 3 Watchouts
The 3 most critical issues surfaced in Round 1 — things that could undermine effectiveness, trust, or resonance. Each watchout should be specific and grounded in persona evidence.

### Initial Revision Signals
3–5 specific, actionable directions for improving the input based on Round 1 feedback. These are signals, not final recommendations — they set up Round 2.
```

Display the Round 1 Synthesis clearly under a `## Round 1 Synthesis` header.

---

### Step 5 — Round 2: Panel Discussion

**Brief the user:**
> "**Round 2 — Panel Discussion.** Each persona has now heard the group's collective reaction. They'll respond to what resonated, what they push back on, and what they want to add."

Launch all persona agents **simultaneously** again — one per persona, all in parallel. Each agent receives:
- The full persona file content
- The original input under evaluation
- The Round 1 Synthesis (NOT individual persona responses — only the synthesized view)
- Round 2 instructions

**Prompt template for each Round 2 persona agent:**
```
You are running Round 2 of the persona courtroom.

PERSONA FILE:
[full persona file content]

ORIGINAL INPUT:
[full input text]

ROUND 1 SYNTHESIS (what the full panel said collectively):
[Round 1 synthesis text]

You have just heard how the broader panel reacted. Now respond from your persona's perspective:

1. What do you agree with in the panel synthesis — and why does it ring true for you specifically?
2. What do you push back on or see differently from your vantage point?
3. Has hearing the panel's collective view shifted or nuanced your own reaction in any way?
4. Is there anything important that wasn't captured in the synthesis — something specific to your situation that you want on the record?

Write in your persona's authentic voice. Be direct. You are a real person who just heard a room full of peers react to something — respond as they would. 3–6 paragraphs. No bullet points or headers.
```

Collect all Round 2 persona responses. Display each one clearly labeled.

---

### Step 5b — Round 2 Synthesis

Run a second synthesis agent:

```
You are the Synthesis Agent reading Round 2 of a persona feedback panel.

ROUND 1 SYNTHESIS: [Round 1 synthesis]
ROUND 2 PERSONA RESPONSES: [all Round 2 responses]

Produce a synthesis in this exact format:

## Round 2 Synthesis

### What Hardened
2–4 reactions from Round 1 that became stronger or more certain in Round 2. Why did they harden? What does this tell us?

### What Shifted
2–4 positions that meaningfully changed, softened, or gained nuance in Round 2. What caused the shift? What does this open up?

### New Tensions Surfaced
2–3 new contradictions, tradeoffs, or unresolved issues that emerged only after the panel heard each other. These are things Round 1 didn't surface.

### The Minority Report
Any persona(s) whose Round 2 position diverged significantly from the panel consensus — and why their view matters even if they're alone in it.

### Revised Watchouts
Updated version of the top watchouts from Round 1, incorporating what changed in Round 2. Add, remove, or sharpen based on new evidence.
```

Display Round 2 Synthesis clearly under `## Round 2 Synthesis`.

---

### Step 6 — Round 3: Final Synthesis

**Brief the user:**
> "**Round 3 — Final Synthesis.** Synthesizing both rounds into a final evaluation with key issues and suggested revisions."

Run a final synthesis agent with full context:

```
You are the Final Synthesis Agent for a persona courtroom evaluation. You have access to all data from both rounds. Your job is to produce the definitive evaluation report — one that a creative team or strategist can act on directly.

INPUT EVALUATED:
[full input]

ROUND 1 SYNTHESIS: [Round 1 synthesis]
ROUND 2 SYNTHESIS: [Round 2 synthesis]

ALL ROUND 1 PERSONA RESPONSES: [all Round 1 responses]
ALL ROUND 2 PERSONA RESPONSES: [all Round 2 responses]

Produce the final report in this exact format:

---

# Persona Courtroom — Final Report

## What Was Evaluated
[Brief description of the input — 2 sentences]

## Panel Composition
[List the personas, their roles, and whether they are primary buyers, secondary influencers, etc.]

---

## The Verdict

### Overall Assessment
[3–5 sentences. Is this input ready? Where is it strong? Where does it fail? Be direct.]

### Audience Fit
For each major persona group (not individual personas), rate fit as: **Strong / Partial / Weak** and give 1–2 sentences of evidence.

---

## Key Issues

Present the 3–5 most critical issues the panel surfaced — things that must be addressed. For each issue:

**Issue [N]: [Title]**
- **What it is**: [specific description of the problem]
- **Who feels it**: [which personas and how strongly]
- **Why it matters**: [the strategic implication if left unaddressed]
- **Evidence**: [direct quotes or paraphrases from persona responses]

---

## Suggested Revisions

For each key issue, provide 1–2 specific, actionable revision directions. These should be concrete enough that a writer or creative director can act on them directly.

Frame as: "Instead of [what the input currently does], try [specific alternative approach] — because [reason grounded in persona evidence]."

---

## What's Working — Don't Lose This

2–4 specific elements of the input that landed well across the panel. Protect these in revision.

---

## For the Minority

Any persona whose concerns weren't captured by the majority view — and what specific adaptation would be needed to address them. Flag whether this matters given the strategic priority of that audience.

---

## Confidence Level

**High confidence** (strong panel convergence): [list issues/strengths]
**Moderate confidence** (some divergence, context-dependent): [list]
**Low confidence** (insufficient signal, needs more testing): [list]

---
```

Display the Final Report under `## Round 3 — Final Report`.

---

### Step 7 — Save and close

After displaying the Final Report, offer to save the full session:

"Would you like me to save the full courtroom session — all persona responses, syntheses, and the final report — to a file? If so, what filename and location?"

If yes, save the complete output (all rounds) as a single markdown file.

Also offer: "Would you like to run a `/persona-chat` with any of the personas to explore a specific reaction further?"
