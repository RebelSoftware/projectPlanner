<!-- AGENT: DO NOT READ. Harness version history — irrelevant to project planning. -->

# Changelog

## 0.3.0 — 2026-07-07

### Added
- **Implicit roles** — Interviewer, Scribe, Analyst, Gatekeeper mapped to process steps (`system-prompt.md`)
- **Brownfield intake** — `codebase_path` field in seed; agent scans existing codebase to pre-populate plan
- **Stakeholder register** — named individuals with roles; agent uses names throughout the plan (`templates/state/stakeholders.md`)
- **Context card** — 15-line bootstrap for fast session resume (`templates/state/context-card.md`)
- **Agent guide output** — generated document telling AI agents how to navigate and act on the plan (`templates/output/agent-guide.md`)
- **Version footer on output** — all generated docs carry harness version and date
- **Agent guide directives** — "Before You Start Coding" (confirm environment), "Keep the Plan Alive" (update docs as you work)

### Changed
- **Session resume** now loads context card first; session-status.md is secondary
- **Staleness check** tiered: 2-day recap offer, 7-day change check
- **One-question rule** relaxed: small-cluster exception (2-3 coupled questions) and agenda mode (client meetings)
- **Kanban scope** clarified: planning artifact, not execution tracker; execution columns are developer-managed

### Added (process)
- Confidence assessment in output project overview
- Brownfield intake documented in `process.md` and `README.md`

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
