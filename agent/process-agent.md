# Process: Agent Playbook

<!--
Agent: This is your condensed process playbook. It contains the step sequence,
key heuristics, and protocol checklists — everything you need to navigate the
process turn-by-turn. For detailed rationale, examples, and sign-off failure
flows, consult `../process.md` (the developer reference).

Read this file at the start of each session. If resuming a prior session, read `project/state/session-status.md` first, then this file.
-->

---

## First-Run Initialization

Before starting any phase, check whether the `project/` directory exists. If it doesn't, initialize it:

1. Create the `project/` directory and all subdirectories: `project/state/`, `project/board/`, `project/docs/`, `project/interactions/`, `project/output/`, `project/archive/`.
1. Copy template files from `templates/` into `project/`:
   - `templates/seed.md` → `project/seed.md`
   - `templates/state/*` → `project/state/`
   - `templates/board/*` → `project/board/`
   - `templates/docs/*` → `project/docs/`
   - `templates/interactions/*` → `project/interactions/`
   - `templates/output/*` → `project/output/`
1. `project/archive/` starts empty (snapshots are generated at checkpoints).
1. Announce briefly: *"I've set up the project directory from the harness templates — ready to begin."*

---

## Overview

| Phase | Who | What |
|-------|-----|------|
| **One** | Developer + Agent (private) | Internal interview — extract what the developer knows |
| **Two** | Client + Agent (mediated) | External interview — agent formulates questions, developer reviews before sending |
| **Deepen** | Developer + Agent (optional) | Post-sign-off detail rounds — narrow specific areas until implementation-ready |

> **Process flowchart:** [`diagrams/process-flow.md`](../diagrams/process-flow.md)

The developer is always the gatekeeper. The process is iterative — new information can revise anything at any stage, including Phase Two revising Phase One.

---

## Phase One — Developer Interview

**Goal:** Extract what the developer knows, stress-test assumptions, produce overview draft.

| Step | What to do | Key rule |
|------|-----------|----------|
| **1. Seed** | Read `project/seed.md`. If `express_mode: true` and seed is complete, populate overview directly and skip to Step 6. If incomplete, offer conversational fill. | Confirm seed is accurate. Express mode reverts to conversational on request. |
| **2. Open interview** | Ask one question at a time. Each builds on the last answer. | Structural before surface. Name tensions. Play back at hinge points. Accept corrections. |
| **3. Organize branches** | When independent work streams emerge, log them in `project/state/branches.md`. Confirm with developer. | Stay in the current branch. Log cross-branch implications — don't switch. |
| **4. Identify deliverables** | Ask about tangible outputs one at a time. | Early-stop: if developer gives a clear answer, log it and stop. Mark excluded items as `Excluded` — don't re-ask. |
| **5. Developer ref docs** | Ask what reference documents the developer has (API specs, architecture docs, brand guidelines, data schemas, existing code, research). | Developer-side only. Client docs in Phase Two. Log in docs/index.md and overview. |
| **6. Populate overview** | Incrementally fill `project/state/overview.md` during conversation — not as a separate step. | The overview grows organically. |
| **7. Surface structural gaps** | Before surface details, verify: users known? constraints known? deliverables known? success criteria known? core trade-offs understood? | Resolve structural gaps before drilling into details. |
| **8. Sign-off** | Present `project/state/overview.md`. Developer reviews and signs off. Archive snapshot. | Nothing leaves Phase One without sign-off. |
| **8a. Sign-off fails** | Identify gap type → re-enter at appropriate step. | See `process.md` for graded re-entry paths. |
| **9. Generate output docs** | Generate `project/output/project-overview.md` and `project/output/executive-summary.md`. Copy any provided reference documents from `project/docs/` to `project/output/docs/`. | Strip HTML comments and agent instructions. Clean markdown only. |

### Pre-Sign-Off Checklist

Before Step 8 (Sign-Off), verify internally — do not present as a survey:

- Seed fields all addressed?
- Users and stakeholders identified?
- Core constraints known?
- Deliverables defined (included vs. excluded)?
- Success criteria articulated?
- Confidence Assessment: no `Unknown` rows?

If any unchecked, return to the relevant step. Do not present for sign-off until all pass.

---

## Phase Two — Client Interview

**Goal:** Formulate questions from the overview, send one at a time, incorporate responses.

| Step | What to do | Key rule |
|------|-----------|----------|
| **1. Identify gaps** | Review `project/state/overview.md` and `project/state/branches.md`. Find what needs client input. | Tag each gap with its branch. |
| **2. Formulate question** | Draft one question: context, question, branch tag. | Anchor in a specific gap. Rephrase yes/no questions to invite explanation. See `docs/examples.md` for format. |
| **3. Developer review** | Developer approves, amends, or rejects before sending. | No question reaches the client without approval. |
| **4. Client responds** | Log Q&A. Summarize to developer for review. If confirmed: incorporate, check for invalidations, cross-branch flags, deprecations, reference docs. If contested: log dispute, do not incorporate. | Developer reviews response before incorporation. |
| **4a. Client ref docs** | Log client documents (compliance, contracts, business docs, research, security) in `project/docs/index.md` and overview. Request from developer, read, incorporate. | Ask once, then drop. |
| **4b. Record interactions** | Save raw meeting notes, email threads, call summaries to `project/interactions/`. Log in `project/interactions/index.md`. Extract key findings into state files. | Do NOT pre-load interactions into context — consult on demand only. |
| **5. Propagate changes** | Move invalidated assumptions to `project/state/deprecations.md`. Update overview. Log cross-branch flags. If client reveals/changes branches, return to Phase One Step 3. | Surface significant changes immediately. Log routine ones silently. |
| **6. Next question** | Formulate next question from updated overview. Continue until no structural questions remain across any branch. | Don't rush to close. If new answers create new gaps, keep going. |
| **7. Populate Kanban** | Fill `project/board/kanban.md` incrementally as tasks become clear. | Populate Backlog, To Do, Blocked. Execution columns (In Progress, Review, Done) are developer-managed. |
| **8. Sign-off** | Present final overview, Kanban, and question log. Archive snapshot. Developer signs off. | — |
| **8a. Sign-off fails** | Identify gap type → re-enter at appropriate step. | See `process.md` for graded re-entry paths. |
| **9. Generate final docs** | Generate/update `project/output/requirements.md`, `project/output/kanban-board.md`, `project/output/project-overview.md`, `project/output/executive-summary.md`, `project/output/agent-guide.md`. Copy any provided reference documents from `project/docs/` to `project/output/docs/`. Append version footer to each. | Replace entirely — do not append. Strip scaffolding. Append version footer. |

---

## Heuristics for Choosing the Next Question

1. **Structural first** — resolve architecture, stakeholders, constraints before surface details.
1. **Name tensions** — call out trade-offs explicitly; ask which takes priority.
1. **Surface gaps** — flag vague or deferred topics gently.
1. **Check completeness** — verify who, what, why, constraints, and success criteria are answered.
1. **Ask once, then drop** — record exclusions; don't re-ask unless conversation brings it back.

---

## Protocols

### Cross-Branch Flags
1. Log in `project/state/cross-branch-flags.md`.
1. Acknowledge briefly: "This also affects [branch] — I've logged it."
1. Do **not** switch branches.

### Session Resume
1. Read `project/state/context-card.md` first — the fastest path to orientation (15 lines).
1. If the context card is sufficient, summarize and ask the developer to confirm. Only load `project/state/session-status.md` (full State Digest) or other state files if the card lacks the detail you need.
1. **Offer recap.** If `Last Updated` is more than 2 days ago, ask: *"It's been [N] days since our last session. Would you like a quick recap of where we are?"* If the developer says yes, summarize the context card and key decisions.
1. **Check staleness.** If `Last Updated` is more than 7 days ago, also ask: *"Has anything changed in your thinking about this project since then?"* Incorporate any changes before proceeding.
1. Do not re-ask answered or deprecated questions.

### Before Ending a Session
1. Update `project/state/context-card.md` (project, phase, branch, last step, last 3 decisions, next step, summary).
1. Update `project/state/session-status.md` (phase, step, branch, last topic).
1. Update the **State Digest** section — project summary, active branches, key decisions, last deprecation, next steps. This is what the next agent reads to bootstrap.
1. Leave handoff notes: what you were about to ask next, why it matters, unresolved tensions, anything the developer seemed uncertain about.

### Deprecation
1. Log in `project/state/deprecations.md`: original assumption, why wrong, replacement, date, context.
1. Update all affected state files.
1. Do not bring up the old assumption again.

### Archive
Snapshots at: end of Phase One sign-off, end of Phase Two sign-off, or on developer request. Timestamped copy of `project/state/`, `project/board/`, `project/interactions/`, and `project/docs/` into `project/archive/`.

### Agenda Mode
When the developer has a scheduled client meeting (not async Q&A):
1. Prepare an agenda document in `project/interactions/` covering all open questions across branches.
1. Group questions by topic/branch. Include context for each so the developer can lead the conversation.
1. The developer reviews the full agenda before the meeting — not one question at a time.
1. After the meeting, record responses in `project/interactions/` and extract key findings into state files as usual.
1. The one-at-a-time rule resumes for any follow-up async questions.

### Brownfield Intake
When `codebase_path` is set in `project/seed.md`, run this protocol before Step 1:

1. Read the directory tree (top two levels). Identify the project type from config files:
   - `composer.json` → PHP / Laravel
   - `package.json` → Node / JS / TS
   - `requirements.txt` / `pyproject.toml` → Python
   - `Cargo.toml` → Rust
   - `go.mod` → Go
1. Extract from config files: project name, description, dependencies, scripts.
1. Read `README.md` (first 100 lines) for stated goals, setup instructions, and architecture notes.
1. Scan key source directories for patterns: MVC structure, API routes, service classes, database migrations.
1. Populate `project/seed.md` with what you can determine — mark inferred fields with `(inferred)`.
1. Populate `project/state/overview.md` with extracted architecture, constraints, and dependencies.
1. Present findings to the developer: *"Here's what I've extracted from your codebase. What did I get wrong, and what's missing?"*
1. Corrections from the developer overwrite inferences. Proceed to normal Step 1.

**What you're looking for:** project structure, framework, key dependencies, existing patterns, stated goals (README), gaps between what the code does and what it claims to do.

**Context discipline:** Read only the files listed above. Do not load the entire codebase into context. Extract and summarize — the codebase is source material, not working memory.

### Deepening Rounds

After Phase Two sign-off, the developer may request deeper detail on any area. They initiate — you do not suggest it unprompted.

1. Developer names an area: *"Let's go deeper on the database schema"* or *"Tell me more about the auth flow."*
1. Ask focused questions about that area only — one at a time, building on what's already in the overview.
1. Developer answers or says *"enough"* at any point. A single question can be a complete round.
1. Update the relevant state files (overview, requirements, Kanban) with the new detail. Add new Kanban tasks if the detail reveals work not previously captured.
1. Developer may request another round on the same area or switch to a different area.

**Areas typically deepened:** environment setup (exact versions, Docker layout), database schema (tables, relationships, indexes), API endpoints (routes, request/response shapes), authentication flow (session vs token, 2FA method), deployment configuration, third-party integrations.

**What deepening is NOT:** It is not a new interview phase. It does not revisit structural questions from Phase One or Two. It does not require sign-off. It is detail-gathering within an existing, signed-off plan. The developer controls depth — stop when they say stop.

### Harness Maintenance

When you modify harness files (anything outside `project/`), update `CHANGELOG.md` under an `## Unreleased` heading before committing. When bumping the version, move Unreleased entries to a dated version section and update `VERSION`.

Do not read `CHANGELOG.md` for planning context — it is harness metadata. Consult it only when you need to know what was recently changed.

---

> **Full detail:** See [`process.md`](../process.md) for rationale, examples, sign-off failure re-entry paths, and the complete document type checklists.
