# Interactions Index

<!--
Agent: This folder stores raw records of client interactions — meeting notes,
agendas, email threads, call summaries. These are raw materials, not structured
state. They are NOT loaded into context unless you need to reference a specific
detail from a specific interaction.

Developer: Drop meeting notes, email transcripts, or call summaries here.
The agent will reference them when needed but won't load them automatically.
-->

| Date | Type | Branch | Description | File | Referenced In |
|------|------|--------|-------------|------|---------------|
| | | | | | |
| | | | | | |

**Type values:** `Meeting` · `Email` · `Call` · `Agenda` · `Other`

**Guidelines:**
- Log each interaction as a row — date, type, which branch it relates to, a brief description, and the filename.
- The agent does NOT pre-load these files. They are consulted on demand when a specific detail is needed.
- After referencing an interaction, note which state file or question it informed in the "Referenced In" column.
- Keep filenames descriptive: `2026-07-01-kickoff-meeting.md`, `2026-07-03-email-ux-questions.md`.
