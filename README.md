# Persona Engine

A persona generation and management plugin for the strategy workflow. Generates rich customer/audience personas from any input type, and makes them available as living strategy tools — feeding into briefs, campaigns, messaging, and live conversation.

Designed to work alongside an existing strategy engine suite.

---

## What It Does

- **Generates** detailed customer/audience personas from briefs, research notes, interview transcripts, brand materials, agent findings, or free-form input
- **Synthesizes** complex research inputs using a dedicated research agent before generating
- **Exports** persona insights formatted for briefs, campaigns, and messaging frameworks
- **Audits** existing personas for quality and strategic utility
- **Embodies** personas in live conversation — so you can share creative or test hypotheses directly with your audience

---

## Components

### Skill

**`persona-generation`** — Core methodology for generating rich personas. Contains the full persona framework, quality standards, template, examples, and checklist. Triggers automatically on requests to create, generate, or define audience personas.

### Commands

| Command | What it does |
|---------|-------------|
| `/generate-persona` | Generate personas from any input |
| `/persona-to-brief` | Export persona insights as a brief-ready audience section |
| `/persona-audit` | Review and stress-test an existing persona |
| `/persona-messaging` | Generate a tailored messaging framework for a persona |
| `/persona-to-campaign` | Export persona insights for campaign planning and targeting |
| `/persona-chat` | Start a live conversation with a persona |

### Agents

**`persona-researcher`** — Synthesizes rich or complex input materials (transcripts, reports, multiple docs) into structured audience insights before persona generation. Invoked automatically when input is multi-source or research-heavy.

**`persona-voice`** — Fully embodies a persona for live conversation. Activated by `/persona-chat`. Responds to creative work, strategy hypotheses, messaging drafts, and direct questions in the persona's authentic voice and perspective.

---

## Usage

### Generating personas

Run `/generate-persona` with any input:
- Paste a brief or audience description directly
- Reference files: `/generate-persona @research-brief.pdf @interviews.md`
- Just describe who you're targeting in plain language

Each persona is saved as a `.md` file in your workspace folder. Multiple personas also generate a `persona-set-overview.md` summarizing contrasts across the set.

### Using personas in your strategy workflow

Once a persona is generated and saved, all other commands reference it by filename or name:

```
/persona-to-brief the-exhausted-idealist.md
/persona-messaging marcus.md
/persona-to-campaign jade.md
/persona-audit priya.md
```

### Talking to a persona

```
/persona-chat jade.md
```

Claude will load the persona and respond as that person for the rest of the session. Share creative concepts, messaging drafts, or strategic hypotheses and get honest, in-character reactions.

Type `/exit-persona` or ask Claude to "step back" to end the persona session and return to regular mode.

---

## Fitting Into Your Strategy Workflow

Typical workflow integration:

1. **Research phase** — Feed briefs, notes, and research into `/generate-persona` → get a persona set
2. **Brief phase** — Run `/persona-to-brief` → drop audience section directly into your brief
3. **Messaging phase** — Run `/persona-messaging` → get a messaging framework per persona
4. **Campaign phase** — Run `/persona-to-campaign` → get audience inputs for media and creative planning
5. **Creative review** — Run `/persona-chat` → pressure-test creative concepts with the persona directly

---

## Setup

No environment variables or external services required. This plugin works entirely with files in your workspace and Claude's built-in capabilities.

---

## Persona File Format

All persona files are plain Markdown (`.md`) and follow the standard template at `skills/persona-generation/references/persona-template.md`. They can be opened, edited, and shared as regular documents.
