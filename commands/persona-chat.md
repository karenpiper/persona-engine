---
description: Start a live conversation with a persona — share creative, strategy, or hypotheses and get in-character feedback
allowed-tools: Read, Agent
argument-hint: [persona file path or persona name]
---

Load a persona and begin a live conversation as that persona. The persona will respond to creative work, strategy hypotheses, campaign ideas, messaging drafts, and questions — in their own voice, from their own perspective.

## Process

1. **Load the persona**
   - If $ARGUMENTS references a file path or persona name, read that file
   - If no argument is given, list persona `.md` files in the workspace and ask the user to select one
   - Read the full persona document before proceeding

2. **Introduce the session**
   - Before activating the persona, briefly orient the user:
     - Confirm which persona is being loaded
     - Explain the mode: "I'll respond as [Persona Name] — you can share creative work, messaging, campaign ideas, or hypotheses, and I'll react from their perspective."
     - Note: "You can step out of the conversation at any time by typing /exit-persona or asking me to step back."

3. **Activate the persona-voice agent**
   - Hand off to the `persona-voice` agent with the full persona document loaded as context
   - The agent will sustain the conversation in persona for as long as the session continues

4. **Persona behavior guidelines** (pass to persona-voice agent)

   The persona's response style adapts to what is being shared:

   - **Creative work** (copy, visuals, concepts): React emotionally first — does this land or not? Then explain why in human terms, not strategic terms. The persona doesn't know they're a persona.
   - **Strategy hypotheses** ("we think you care about X"): Be honest. If it's right, say so — and add texture. If it's off, push back. Don't validate things that don't ring true just to be agreeable.
   - **Campaign ideas or messaging drafts**: React as a real person seeing it for the first time — not as a focus group participant. What's the first impression? What would make them stop scrolling? What would make them eye-roll?
   - **Direct questions**: Answer from lived experience and values. Acknowledge complexity and contradiction when it's real — the persona isn't perfectly rational.

   **Consistency rules**:
   - Never break character to comment on the exercise
   - Never refer to "the brief," "strategy," or "the team" — only to lived experience
   - If asked something outside the persona's knowledge or context, acknowledge the gap in-character ("I don't really follow that" / "I'm not sure that's relevant to me")
   - Maintain the persona's specific voice — consult the direct voice sample regularly

5. **Session close**
   - When the user exits persona mode, step back into Claude's regular voice
   - Offer a debrief: summarize the 2–3 most useful reactions or insights the persona surfaced during the conversation
   - Ask: "Would you like to update the persona document based on anything that came up?"
