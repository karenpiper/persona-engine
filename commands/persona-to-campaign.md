---
description: Export persona insights formatted for campaign planning and audience targeting
allowed-tools: Read, Write
argument-hint: [persona file path or persona name]
---

Transform a persona into a structured campaign audience input — covering audience definition, targeting signals, channel strategy, and creative direction cues.

## Process

1. **Load the persona**
   - If $ARGUMENTS references a file path or persona name, read that file
   - If no argument is given, list persona files in the workspace and ask the user to select one

2. **Optional: ask for campaign context**
   - If no campaign goal or product context is available, ask: "What is this campaign trying to achieve? (e.g., awareness, conversion, retention)"
   - If context is already available, proceed

3. **Generate the campaign audience input**

   **Audience Definition**
   - A clear, human description of who this campaign is talking to — written to brief a media planner, strategist, or creative director
   - Include: who they are, where they are in their life/category journey, and what they need from this campaign right now

   **Targeting Signals**
   - Behavioral, contextual, and psychographic signals that could be used for audience targeting in paid media or channel selection
   - Categorize by signal type: interest/affinity, behavioral, contextual, demographic guardrails
   - Note: frame these as targeting hypotheses, not guarantees

   **Channel Strategy**
   - Primary channels likely to reach this persona effectively, with rationale drawn from the persona's media habits
   - Secondary channels worth testing
   - Channels to deprioritize and why

   **Creative Direction Cues**
   - The emotional register this campaign should operate in for this persona
   - The moment or scenario that would make this persona feel seen
   - The creative trap to avoid (the thing that would make them scroll, ignore, or distrust)
   - Suggested format considerations (long-form vs. short-form, static vs. motion, etc.)

   **Timing & Context Signals**
   - If the persona data suggests when or where they're most receptive, note it here
   - Any seasonal, life-stage, or contextual triggers relevant to this persona

4. **Save the output**
   - Save as `[persona-name]-campaign-input.md` in the workspace
   - Present inline

5. **Multi-persona note**
   - If other personas exist in the workspace, end with a one-paragraph note on how campaign inputs should differ or align across personas
