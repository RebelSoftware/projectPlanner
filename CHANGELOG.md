<!-- AGENT: DO NOT READ. Harness version history — irrelevant to project planning. -->

# Changelog

## 0.2.0 — 2026-06-30

### Added
- Phase One pre-sign-off completeness checklist (`process-agent.md`)
- Developer review gate for client responses before incorporation (`process-agent.md`, `process.md`)
- Risk register template with client-authoritative dispute handling (`templates/state/risks.md`)
- Express mode for experienced users — skip conversational interview (`templates/seed.md`)
- Glossary template for shared terminology (`templates/state/glossary.md`)
- Interaction record template for meeting notes and emails (`templates/interactions/_template.md`)
- Deliverable types extracted to dedicated reference file (`docs/deliverable-types.md`)
- Harness version tracking (`VERSION`, `CHANGELOG.md`)
- Agent guard: "Files You Never Load" section in system prompt

### Changed
- Compressed heuristics in `process-agent.md` from full sentences to one-liners
- Removed rationale paragraph from First-Run Init in `process-agent.md`
- Tightened verbose Key rule cells in Phase One table (`process-agent.md`)
- Added explicit "Phase Two can revise Phase One" note to iterative rule

## 0.1.0 — Initial

- Two-phase planning process: Developer Interview + Client Interview
- Emergent structure philosophy — branches, Kanban, registers appear on demand
- Session resume protocol with state digest and handoff notes
- Deprecation and cross-branch flag tracking
- Printable output document generation
- Seed-based project initialization
