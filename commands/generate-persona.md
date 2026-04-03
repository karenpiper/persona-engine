---
description: Generate audience personas from briefs, research, notes, or free-form input
allowed-tools: Read, Write, Glob, Agent
argument-hint: [optional: @file-path or description of target audience]
---

Generate one or more rich customer/audience personas using the persona-generation skill.

## Process

### Step 1: Assess the input

- If $ARGUMENTS includes file references (e.g., `@brief.pdf`, `@notes.md`), read those files
- If $ARGUMENTS is a free-form description of a target audience, treat it as a starting point
- If no arguments are provided, ask: "What audience should I build personas for? You can describe them, upload documents, or give me a segment name or role — and I'll research the rest."

### Step 2: Determine research mode

**Rich input (multiple documents, transcripts, research reports, agent findings)**
→ Invoke `persona-researcher` in synthesis mode to extract and organize signals from the provided materials before generating.

**Thin input (a sentence or two, a job title, a segment name, or nothing)**
→ Invoke `persona-researcher` in research mode. The agent will conduct active web research across Reddit, LinkedIn, professional forums, analyst reports, product reviews, job postings, trade publications, and analogous audiences to build a grounded audience picture from scratch. This typically takes a few minutes — let the user know research is underway.

**Mixed input (some documents + gaps)**
→ Invoke `persona-researcher` to synthesize what exists, then extend with targeted web research to fill the gaps identified. Flag which signals came from documents vs. research.

Always invoke `persona-researcher` first. Do not generate personas directly from thin or unprocessed input.

### Step 3: Clarify before generating

After the researcher returns its synthesis, check:
- Is the number of personas to generate clear? If not, ask.
- Do multiple distinct segments emerge from the research? Name them and confirm which to build.
- Is there a specific segment framework or naming convention to follow?

### Step 4: Generate the persona(s)

Apply the full two-part persona template:
- **Part 1** (Standard Persona): Name, Archetype, Demographics, Psychographics, Lifestyle & Interests, Motivations & Decision Criteria, Direct Voice Sample, Segment Context, Within-Segment Variation, Source Notes
- **Part 2** (AI Simulation Extension): Operational Context, Decision-Making Framework, Core Beliefs, Frictions, Activation Triggers, Simulation Guardrails

Meet all quality checklist criteria. Each persona must be grounded in evidence from the researcher's synthesis — label any inferences clearly.

### Step 5: Save the output

- Save each persona as `[archetype-kebab-case].md` in the workspace folder
- Present inline in the conversation
- For multiple personas, also create `persona-set-overview.md` summarizing the set and highlighting contrasts

### Step 6: Close with context

Briefly note:
- What sources informed the personas (documents, research, or both)
- Confidence level in the output (strongly evidenced vs. inferred in places)
- What additional research or input would sharpen them
- What the persona set is best suited for next (brief, messaging, campaign, persona-chat)
