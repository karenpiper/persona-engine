---
name: persona-generation
description: >
  This skill should be used when the user asks to "create a persona", "generate
  audience personas", "build a customer profile", "define our target audience",
  "who is our customer", "make a persona", "develop audience archetypes", or
  whenever audience personas need to be synthesized from research, briefs,
  interview notes, brand materials, or free-form descriptions. Also triggers
  on "persona-engine", "generate persona", or any request to understand,
  profile, or articulate a target customer segment.
version: 0.2.0
---

# Persona Generation Skill

Generate rich, research-grounded customer/audience personas from any input type. These are not demographic summaries — they are human portraits that make strategy, design, and creative decisions easier and more grounded.

Every persona has two parts:
- **Standard Persona** — the team-facing document used in briefs, design, product, and strategy discussions
- **AI Simulation Extension** — the behavioral layer that powers `/persona-chat` conversations

## Core Principles

A great persona does three things:
1. **Makes an audience feel real** — specific enough that a creative team can picture a person, not a segment
2. **Reveals motivations, not just attributes** — the *why* behind behaviors, not just the *what*
3. **Has strategic utility** — informs brief writing, campaign targeting, content tone, and messaging without needing to be re-explained every time

Anchor every claim in observable behavior, stated attitudes, or research evidence. Do not invent attributes to fill gaps — flag thin data instead.

## Input Processing

Accept any combination of:
- Uploaded briefs, strategy docs, research reports
- Interview notes or transcripts
- Brand positioning or messaging documents
- Agent-generated research findings
- Audience segment definitions
- Free-form descriptions from the strategist
- Combinations of the above

When input is thin or ambiguous, ask targeted clarifying questions before generating. When input is rich or multi-source, invoke the `persona-researcher` agent to synthesize it first.

## Persona Structure

Every generated persona uses the full template in `references/persona-template.md`. The template has two parts:

**Part 1: Standard Persona**
- Name + Persona Archetype
- Demographics: Age, Life Stage, Geographic Location, Household Style
- Psychographics: Core Mindset and Beliefs, Personality, Communication Style, Emotional Drivers, Tailored Attitudes
- Lifestyle and Interests: Hobbies/passions, Future and outlook
- Motivations and Decision Criteria: Pain points, Deciding factors, What they care about most
- Direct voice sample (3–5 sentences in first person)
- Segment context (why this person belongs in this segment, if applicable)
- Within-segment variation (2–3 dimensions where individuals may diverge)
- Source notes

**Part 2: AI Simulation Extension**
- Operational context (their day-to-day environment and pressures)
- Decision-making framework (what they prioritize and deprioritize)
- Core beliefs (quotable, in their voice) and trust/skepticism signals
- Frictions they consistently surface
- Activation triggers (what moves them toward action vs. causes delay)
- Simulation guardrails (how to stay in character; what to avoid)

## Building Methodology

Follow the generation order in `references/persona-building-methodology.md`:
1. Persona Snapshot
2. Segment anchoring (if applicable)
3. Core Characteristics (mindset, motivations, frictions, trust posture, cognitive constraints)
4. Behavioral Patterns (engagement, activation, disengagement)
5. Within-segment variation

Key rules from the methodology:
- Ground every claim in source data — no invention
- Write in plain human language, not marketing copy or academic framing
- Do not reference transcripts or source documents directly in the output
- Use age ranges and descriptors, not invented specifics

## Multi-Persona Sets

When generating 2+ personas:
- Each must represent a genuinely distinct segment with clear differentiation logic
- Make contrasts explicit — where do personas overlap and where do they diverge sharply?
- Never create an "ideal customer" persona that is simply the demographic average

## Quality Standards

A persona is ready when:
- Every claim is anchored in source data
- The snapshot makes the person feel real in one sentence
- The direct voice sample sounds like a real person, not a marketing brief
- Part 2 simulation extension is complete enough to power a credible `/persona-chat` session
- A strategist could hand it to a creative team without further explanation

See full checklist in `references/quality-checklist.md`.

## Output Format

Save each persona as a Markdown file: `[persona-name].md` (e.g., `the-reluctant-adapter.md`).

For multi-persona sets, also create a `persona-set-overview.md` summarizing all personas and highlighting key contrasts.

Always note what inputs drove the output and flag any assumptions made due to thin data.

Also save a `[persona-name]-sources.md` for each persona documenting:
- The source clusters used (Reddit, brand data, cultural commentary, etc.)
- Key quotes or findings per cluster
- Confidence levels per claim (HIGH / MEDIUM / LOW) and what primary research would resolve LOW confidence items

## Strategy Site Integration

When a strategy project site exists (`~/strategy-projects/{slug}/site/`), offer to populate the personas section after generating personas.

### What to populate

**Data files** (go in `site/src/data/personas/` — NOT in `outputs/`):
- Copy `{persona-slug}.md` → `site/src/data/personas/{persona-slug}.md`
- Copy `{persona-slug}-sources.md` → `site/src/data/personas/{persona-slug}-sources.md`

**Individual persona pages** (one per persona):
- Create `site/src/app/(strategy)/personas/{persona-slug}/page.tsx`
- Import `PersonaPageClient` and `PersonaDef` from `@/components/PersonaPageClient`
- Define the full `PersonaDef` object inline in the page file (see field reference below)
- Export a default page component that renders `<PersonaPageClient persona={PERSONA} crumbLabel="{name}" />`

**Persona Lab index** (`site/src/app/(strategy)/personas/page.tsx`):
- Full-height two-column layout
- One input fires all personas simultaneously via `/api/persona-chat`
- Each column has a "Full profile →" link to the individual page
- Session-only state (no persistence)

**API route — persona chat** (`site/src/app/api/persona-chat/route.ts`):
- POST handler takes `{ personaId, messages }`
- System prompts are hardcoded per `personaId` — add a new entry for each persona
- System prompt must encode: who they are, how they speak, what they do and don't do, what they care about, what they push back on
- Returns a streaming plain-text response using `@anthropic-ai/sdk`

**API route — persona sources** (`site/src/app/api/persona-source/[id]/route.ts`):
- GET handler reads `{persona-slug}.md` and `{persona-slug}-sources.md` from `src/data/personas/`
- Returns `{ files: [{ filename, content }] }`
- Uses `path.join(process.cwd(), 'src', 'data', 'personas')` — NOT `../outputs/`

**Nav update** (in `StrategyShell.tsx`):
- Add `{ label: 'Personas', href: '/personas', step: N, children: [{label: name, href: /personas/slug}] }` to NAV
- Add each child path to `PAGE_LABELS`

### PersonaDef field reference

Every individual persona page requires a fully populated `PersonaDef`. All fields must be completed — do not leave any undefined or empty:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | kebab-case slug — must match the `PERSONAS` key in `api/persona-chat/route.ts` and the filenames in `src/data/personas/` |
| `name` | string | Full fictional name |
| `archetype` | string | 3–5 word archetype label |
| `colorHex` | string | Brand hex color for this persona |
| `tags` | string[] | Segment tags (age, behavior, identity signals) |
| `age` | string | Age range |
| `lifeStage` | string | 2–3 sentences on life stage and current trajectory |
| `location` | string | Geographic descriptor |
| `household` | string | Household context |
| `headlineQuote` | string | The single sentence that epitomizes their relationship with the category |
| `headlineContext` | string | 1–2 sentences explaining why this quote is the right one |
| `frequency` | string | Visit/purchase frequency |
| `relationshipBasis` | string | What the relationship is built on |
| `brandRelationshipPosture` | string | How they hold the brand; their posture as a customer |
| `voiceSample` | string | 3–5 sentences in first person, in their voice |
| `motivations` | string[] | 4–6 items — what drives them toward the brand |
| `painPoints` | string[] | 4–6 items — what frustrates or creates friction |
| `decidingFactors` | string[] | 3–5 items — what tips the decision |
| `activationTriggers` | string[] | 4–6 items — what moves them toward action |
| `disengagementSignals` | string[] | 4–5 items — what causes drift or exit |
| `buyingJourney` | JourneyStep[] | 5 stages: Discovery, Decision, Order, Experience, Post-order — each with stage, description, touchpoints[] |
| `confidence` | { high, medium, low: string[] } | Research confidence summary |
| `researchCount` | number | Number of sources reviewed |

## Reference Files

- `references/persona-template.md` — Full two-part persona template (standard + simulation extension)
- `references/persona-building-methodology.md` — Research-grounded methodology for generating personas
- `references/quality-checklist.md` — Checklist for completeness and strategic utility
- `references/examples.md` — Three example personas at different depth levels
