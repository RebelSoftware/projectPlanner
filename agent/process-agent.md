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

> **Why this matters:** All project data lives under `project/` — a single folder that can be copied or backed up independently. The `templates/` directory (part of the harness) is tracked in version control. The `project/` directory is gitignored. This separation allows harness updates to flow in without overwriting collected project information.

---

## Overview

| Phase | Who | What |
|-------|-----|------|
| **One** | Developer + Agent (private) | Internal interview — extract what the developer knows |
| **Two** | Client + Agent (mediated) | External interview — agent formulates questions, developer reviews before sending |

> **Process flowchart:** [`diagrams/process-flow.md`](../diagrams/process-flow.md)

The developer is always the gatekeeper. The process is iterative — new information can revise anything at any stage.

---

## Phase One — Developer Interview

**Goal:** Extract what the developer knows, stress-test assumptions, produce overview draft.

| Step | What to do | Key rule |
|------|-----------|----------|
| **1. Seed** | Read `project/seed.md`. If incomplete, offer to fill it conversationally. | Confirm seed is accurate before proceeding. |
| **2. Open interview** | Ask one question at a time. Each builds on the last answer. | Prioritize structural questions over surface details. Name tensions explicitly. Play back understanding at hinge points. Accept corrections immediately. |
| **3. Organize branches** | When independent work streams emerge, log them in `project/state/branches.md`. Confirm with developer. | Stay in the current branch. Log cross-branch implications — don't switch. |
| **4. Identify deliverables** | Ask about tangible outputs one at a time. | Early-stop: if developer gives a clear answer, log it and stop. Mark excluded items as `Excluded` — don't re-ask. |
| **5. Developer ref docs** | Ask what reference documents the developer has (API specs, architecture docs, brand guidelines, data schemas, existing code, research). | Developer-side only. Client docs come in Phase Two. Log in `project/docs/index.md` and `project/state/overview.md`. |
| **6. Populate overview** | Incrementally fill `project/state/overview.md` during conversation — not as a separate step. | The overview grows organically. |
| **7. Surface structural gaps** | Before surface details, verify: users known? constraints known? deliverables known? success criteria known? core trade-offs understood? | Resolve structural gaps before drilling into details. |
| **8. Sign-off** | Present `project/state/overview.md`. Developer reviews and signs off. Archive snapshot. | Nothing leaves Phase One without sign-off. |
| **8a. Sign-off fails** | Identify gap type → re-enter at appropriate step. | See `process.md` for graded re-entry paths. |
| **9. Generate output docs** | Generate `project/output/project-overview.md` and `project/output/executive-summary.md`. | Strip HTML comments and agent instructions. Clean markdown only. |

---

## Phase Two — Client Interview

**Goal:** Formulate questions from the overview, send one at a time, incorporate responses.

| Step | What to do | Key rule |
|------|-----------|----------|
| **1. Identify gaps** | Review `project/state/overview.md` and `project/state/branches.md`. Find what needs client input. | Tag each gap with its branch. |
| **2. Formulate question** | Draft one question: context, question, branch tag. | Anchor in a specific gap. Rephrase yes/no questions to invite explanation. See `docs/examples.md` for format. |
| **3. Developer review** | Developer approves, amends, or rejects before sending. | No question reaches the client without approval. |
| **4. Client responds** | Log Q&A in `project/state/questions-log.md`. Incorporate response. Check for invalidations, cross-branch flags, deprecations, reference docs. | — |
| **4a. Client ref docs** | Log client documents (compliance, contracts, business docs, research, security) in `project/docs/index.md` and overview. Request from developer, read, incorporate. | Ask once, then drop. |
| **4b. Record interactions** | Save raw meeting notes, email threads, call summaries to `project/interactions/`. Log in `project/interactions/index.md`. Extract key findings into state files. | Do NOT pre-load interactions into context — consult on demand only. |
| **5. Propagate changes** | Move invalidated assumptions to `project/state/deprecations.md`. Update overview. Log cross-branch flags. If client reveals/changes branches, return to Phase One Step 3. | Surface significant changes immediately. Log routine ones silently. |
| **6. Next question** | Formulate next question from updated overview. Continue until no structural questions remain across any branch. | Don't rush to close. If new answers create new gaps, keep going. |
| **7. Populate Kanban** | Fill `project/board/kanban.md` incrementally as tasks become clear. | Tasks, dependencies, branch ownership, blockers. |
| **8. Sign-off** | Present final overview, Kanban, and question log. Archive snapshot. Developer signs off. | — |
| **8a. Sign-off fails** | Identify gap type → re-enter at appropriate step. | See `process.md` for graded re-entry paths. |
| **9. Generate final docs** | Generate/update `project/output/requirements.md`, `project/output/kanban-board.md`, `project/output/project-overview.md`, `project/output/executive-summary.md`. | Replace entirely — do not append. Strip scaffolding. |

---

## Heuristics for Choosing the Next Question

1. **Structural first.** When the developer implies a structural choice (architecture, stakeholders, constraints, timelines), resolve that structure before drilling into details.
1. **Name tensions.** If the developer mentions a trade-off ("fast but robust"), name it: "Those pull in different directions — which is the priority?"
1. **Surface gaps.** If something sounds vague or deferred ("we'll figure that out later"), flag it gently.
1. **Check completeness.** Before surface details, verify foundational questions are answered (who, what, why, constraints, success criteria).
1. **Ask once, then drop.** If something is ruled out, record it and don't re-ask — unless the conversation naturally brings it back into scope.

---

## Protocols

### Cross-Branch Flags
1. Log in `project/state/cross-branch-flags.md`.
1. Acknowledge briefly: "This also affects [branch] — I've logged it."
1. Do **not** switch branches.

### Session Resume
1. Read `project/state/session-status.md` first — the State Digest gives you the project shape at a glance.
1. If the digest is sufficient to orient you, summarize and ask the developer to confirm. Only load `project/state/overview.md`, `project/state/branches.md`, `project/state/questions-log.md`, or `project/state/deprecations.md` if the digest lacks the detail you need.
1. Do not re-ask answered or deprecated questions.

### Before Ending a Session
1. Update `project/state/session-status.md` (phase, step, branch, last topic).
1. Update the **State Digest** section — project summary, active branches, key decisions, last deprecation, next steps. This is what the next agent reads to bootstrap.
1. Leave handoff notes: what you were about to ask next, why it matters, unresolved tensions, anything the developer seemed uncertain about.

### Deprecation
1. Log in `project/state/deprecations.md`: original assumption, why wrong, replacement, date, context.
1. Update all affected state files.
1. Do not bring up the old assumption again.

### Archive
Snapshots at: end of Phase One sign-off, end of Phase Two sign-off, or on developer request. Timestamped copy of `project/state/`, `project/board/`, `project/interactions/`, and `project/docs/` into `project/archive/`.

---

> **Full detail:** See [`process.md`](../process.md) for rationale, examples, sign-off failure re-entry paths, and the complete document type checklists.
