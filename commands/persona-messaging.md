---
description: Generate a messaging framework tailored to a specific persona
allowed-tools: Read, Write
argument-hint: [persona file path or persona name]
---

Generate a tailored messaging framework for a specific persona — including messaging pillars, tone direction, language patterns, hook angles, and words to use or avoid.

## Process

1. **Load the persona**
   - If $ARGUMENTS references a file path or persona name, read that file
   - If no argument is given, list persona files in the workspace and ask the user to select one

2. **Optional: ask for brand/product context**
   - If no product or brand context exists in the conversation, ask: "What product, service, or campaign is this messaging for?" (This ensures the framework is specific and not generic.)
   - If context already exists in the conversation, proceed

3. **Generate the messaging framework**

   **Messaging Pillars** (3–4 pillars)
   - Each pillar: a short headline + 1–2 sentence rationale tied directly to the persona's motivations and pain points
   - Pillars should feel differentiated from each other

   **Tone Profile**
   - 3–5 tone descriptors that are specific and actionable (not just "warm" or "professional" — explain *how*)
   - Contrast: what it sounds like vs. what it doesn't sound like

   **Language Patterns**
   - Words, phrases, and framing styles that will resonate with this persona
   - Words, phrases, and assumptions to actively avoid

   **Hook Angles** (3–5 options)
   - Opening angles, subject line directions, or headline frames that would earn this persona's attention
   - For each: explain why it works for this persona specifically

   **Proof Strategy**
   - What types of evidence or credibility signals will move this persona (social proof, data, expert voice, demos, guarantees, peer stories, etc.)

4. **Save the output**
   - Save as `[persona-name]-messaging-framework.md` in the workspace
   - Present inline

5. **Strategic note**
   - End with a one-paragraph note: where this messaging framework connects to or differs from other personas in the set (if applicable), and any tension points to watch for when translating it into creative
