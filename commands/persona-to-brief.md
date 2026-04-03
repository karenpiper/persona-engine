---
description: Export persona insights formatted for a strategy or creative brief
allowed-tools: Read, Write
argument-hint: [persona file path or persona name]
---

Extract and reformat a persona's most strategically relevant insights into a brief-ready audience section.

## Process

1. **Load the persona**
   - If $ARGUMENTS references a file path or persona name, read that file
   - If no argument is given, list all `.md` files in the workspace that appear to be personas and ask the user to select one

2. **Extract brief-relevant content**
   - From the persona, extract and synthesize:
     - **Who they are** (2–3 sentence human portrait — use the snapshot and refine)
     - **What they're trying to do** (motivations, aspirations)
     - **What's in their way** (pain points, tensions)
     - **How they relate to the category** (mental model, unmet needs)
     - **What will move them** (what resonates, proof types, hook types)
     - **Tone guidance** (voice, language style, what to avoid)

3. **Format for brief insertion**
   - Output as a clean, brief-ready "Target Audience" section using plain prose, not bullet lists
   - Write it as if it's already inside a brief — ready to hand to creative or strategy teams
   - Keep it tight: under 400 words total

4. **Save the output**
   - Save as `[persona-name]-brief-section.md` in the workspace
   - Also present inline

5. **Note what's missing**
   - If the persona is thin in any area that would matter for a brief (e.g., weak on tone guidance, no category insight), flag it with a one-line note at the end
