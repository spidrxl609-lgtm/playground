# Gemini Writers' Room — SillyTavern preset

A Chat Completion preset for Google Gemini in SillyTavern, built for long-form roleplay: slow-burn relationships,
autonomous NPCs, lore-aware worldbuilding, author-style prose and a hidden planning step (`<meeting>`) before each reply.

File: [`Gemini-Writers-Room.json`](Gemini-Writers-Room.json)

## Install

1. **API Connections** → *Chat Completion* → **Google AI Studio** (or Vertex AI) and connect your key.
2. Open the **AI Response Configuration** panel (the sliders icon) → **Import preset** → pick `Gemini-Writers-Room.json`.
3. When SillyTavern asks whether to allow the preset's **regex scripts**, click **Allow**. They fold the `<meeting>`
   block into a collapsible "📋 Writers' meeting" box and keep it out of the chat history sent back to the model.
4. Recommended model: `gemini-3.1-pro-preview` (set by the preset). `gemini-2.5-pro` works too.

## Defaults

| Setting | Value |
| --- | --- |
| Temperature / Top P / Top K | 1.0 / 0.95 / off |
| Context / max response | 128k / 16k tokens (room for Gemini's thinking + the meeting + the reply) |
| System instruction | on (all setup prompts go into Gemini's system instruction) |
| Streaming | on |
| Show Gemini's own thoughts | off |

Temperature 1.0 is Google's recommendation for Gemini 3; raise it to 1.1–1.2 if replies get repetitive rather than lowering it.

## Sections (Prompt Manager)

Entries marked *pick one* are alternatives: enable exactly one per group. ✅ = on by default.

- **📖 README** — the same notes inside SillyTavern. Keep it off; it is never sent.
- **CORE** — ✅ Narrator role, ✅ Language: English, ✅ `{{user}}` agency (never speaks or acts for you),
  ✅ Formatting (`"dialogue"`, `*thoughts*`, no OOC), POV *pick one*: ✅ third person past / second person present / first person `{{char}}`.
- **WORLD & LORE** — ✅ lore rules (canon is fixed, no info-dumps, living world, no meta knowledge), then the character card,
  persona, scenario, World Info and example dialogue, wrapped in tags Gemini parses well.
- **CHARACTERS** — ✅ NPC Autonomy (own goals, initiative, can refuse/lie/leave, only know what they've seen),
  ✅ Character Integrity (flaws stay, no positivity bias).
- **RELATIONSHIP PACING** *pick one* — ✅ Slow Burn, Balanced, Fast.
- **PLOT PACING** *pick one* — ✅ Organic, Driven, Slice of Life; plus ✅ Scene Endings (always hand the turn back to you).
- **GENRE & TONE** *stack any* — ✅ Follow the Card, Comedy, Romance, Drama, Adventure & Action, Fantasy, Sci-Fi, Horror,
  Mystery & Thriller, Slice of Life, Dark & Grimdark. Turn off "Follow the Card" when you pick genres yourself.
- **LENGTH** *pick one* — Short 150–250, ✅ Medium 300–500, Long 500–800, Very Long 800–1200 words (story only, not the meeting).
- **WRITING STYLE** — ✅ Prose Craft, ✅ Anti-Slop banned-phrase list, and an author voice *pick one*:
  ✅ Balanced Blend (Gaiman / King / Le Guin), Terry Pratchett, Douglas Adams, Jane Austen, Raymond Chandler, Stephen King,
  Shirley Jackson, Cormac McCarthy, Joe Abercrombie, Sally Rooney, Brandon Sanderson, Agatha Christie.
  The model imitates technique and rhythm only, never the author's actual text.
- **CONTENT** *optional* — Mature Themes (18+, adults only) or Fade to Black. Both off = follow the card.
- **EXTRAS** — ✅ Anti-Echo & Anti-Repetition, ✅ Continuity Tracking, Dialogue Focus, Status Block (location/time/weather line).
- **After chat history** — ✅ final reminder, ✅ 🧠 CoT: Writers' Meeting, ✅ 🧠 Prefill: `<meeting>`.

## The `<meeting>` CoT + prefill

Before each reply the model holds a short "writers' room meeting" inside `<meeting>…</meeting>`: continuity, what each
character wants, pacing stage, genre/style check, a beat plan and a length/POV check. The prefill starts Gemini's turn with
`<meeting>` so it reliably plans first. Both entries only fire on normal sends, swipes and regenerations — not on
Continue, Impersonate or background (quiet) generations.

- **Turn both off together** for faster, cheaper replies.
- **Gemini 3.6/3.7 Flash and 3.5 Flash-Lite reject prefills**; SillyTavern then sends it as a user message. On those models
  switch the *Prefill* entry off — the CoT entry still asks for the block.
- Prefer SillyTavern's reasoning box over the regex fold? Disable the two preset regex scripts and set
  **Advanced Formatting → Reasoning** prefix `<meeting>` / suffix `</meeting>` with *Auto-Parse* on.
- Renaming the tag: change it in the CoT entry, the Prefill entry and both regex scripts.
