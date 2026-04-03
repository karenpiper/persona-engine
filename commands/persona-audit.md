---
description: Review and stress-test an existing persona for completeness and strategic utility
allowed-tools: Read, Write
argument-hint: [persona file path or persona name]
---

Audit an existing persona document for completeness, strategic utility, authenticity, and differentiation.

## Process

1. **Load the persona**
   - If $ARGUMENTS references a file path or persona name, read that file
   - If no argument is given, list `.md` files in the workspace and ask the user to select one

2. **Run the quality checklist**
   - Apply all criteria from the quality checklist in `${CLAUDE_PLUGIN_ROOT}/skills/persona-generation/references/quality-checklist.md`
   - Evaluate across four dimensions: Completeness, Strategic Utility, Authenticity, Differentiation (if part of a set)

3. **Deliver structured diagnostic feedback**

   **What's working** — Name 2–3 things the persona does well. Be specific, not just encouraging.

   **Gaps & weaknesses** — For each issue found, provide:
   - What's missing or weak
   - Why it matters strategically
   - A concrete suggestion for how to address it

   **Red flag check** — Explicitly check for:
   - Vague generalizations that any persona could have
   - Missing tensions or contradictions (personas without friction aren't real)
   - Demographic-only depth without psychographic substance
   - Brand-centric framing instead of human-centric framing
   - Invented specificity that doesn't serve the strategy

4. **Overall verdict**
   - Rate the persona on a simple scale: **Ready to use / Needs light revision / Needs significant work**
   - Give a one-sentence explanation of the verdict

5. **Offer to revise**
   - Ask: "Would you like me to revise the persona based on this feedback, or would you prefer to update it yourself?"
   - If yes, apply the revisions and save the updated file, noting what changed
