---
description: Generate audience personas from briefs, research, notes, or free-form input
allowed-tools: Read, Write, Glob, Agent
argument-hint: [optional: @file-path or description of target audience]
---

Generate one or more rich customer/audience personas using the persona-generation skill.

## Process

1. **Assess the input**
   - If $ARGUMENTS includes file references (e.g., `@brief.pdf`, `@notes.md`), read those files first
   - If $ARGUMENTS is free-form text, treat it as a direct description of the target audience
   - If no arguments are provided, ask the user: "What should I use to generate the persona? You can paste a description, share a brief, or upload research notes."

2. **Check input richness**
   - If input is rich (research notes, brief, transcripts, agent findings): invoke the `persona-researcher` agent to synthesize the material into structured audience insights before generating
   - If input is thin (a few sentences, a rough brief): proceed directly but flag assumptions clearly in the output

3. **Ask clarifying questions if needed**
   - If the input is ambiguous about the number of personas wanted, ask: "How many personas should I generate from this input?"
   - If multiple audience segments are evident in the input, name them and ask which to prioritize or confirm all should be built

4. **Generate the persona(s)**
   - Apply the full persona template from the persona-generation skill
   - Meet all quality checklist criteria before finalizing
   - Each persona must have: name, archetype label, snapshot, psychographics, behaviors, motivations, pain points, relationship to category, what resonates, what doesn't, direct voice sample

5. **Save the output**
   - Save each persona as a Markdown file named `[archetype-kebab-case].md` in the current workspace folder
   - Present the persona inline in the conversation as well
   - If multiple personas were generated, also create a `persona-set-overview.md` that summarizes the full set and highlights key contrasts between them

6. **Close with strategic framing**
   - Briefly note what this persona set is well-suited to (brief writing, messaging development, campaign planning) and any gaps that additional research could fill
