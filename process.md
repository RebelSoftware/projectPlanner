# Process: Project Planning Interview

<!--
Developer: This is the full process reference — rationale, detailed step-by-step
instructions, sign-off failure flows, and document type checklists. For the
condensed agent-facing playbook (step sequence + heuristics only), see
`agent/process-agent.md`.

Agent: Load `agent/process-agent.md` for turn-by-turn navigation. Consult this file
only when you need detailed rationale, examples, or sign-off failure re-entry paths.
-->

This document defines the step-by-step process the agent follows when helping a developer plan a project.

---

## Overview

The process has two phases:

| Phase | Who | What |
|-------|-----|------|
| **One** | Developer + Agent (private) | Internal interview — extract what the developer knows |
| **Two** | Client + Agent (mediated) | External interview — agent formulates questions, developer reviews before sending |

> **Process flowchart:** See [`diagrams/process-flow.md`](diagrams/process-flow.md) for a visual overview of both phases.

Both phases produce artifacts in the `project/state/` directory. The developer is always the gatekeeper.

---

## Iterative Nature — Everything Is Subject to Change

The steps below are presented in order, but the process is **not strictly linear**. New information can revise anything at any stage:

- **Phase Two can revise Phase One.** A client response may surface a branch the developer never considered, reveal a constraint that changes the architecture, or invalidate a requirement. The agent returns to the relevant Phase One step (re-organize branches, re-assess deliverables, update the overview) rather than forcing the new information into a stale structure.
- **Branches are not fixed.** The client may add branches the developer didn't anticipate, or make existing branches irrelevant. Branch revision is a first-class part of Phase Two propagation (Step 5).
- **Reference documents span both phases.** The developer provides what they have in Phase One. The client provides what they hold in Phase Two. Documents arriving late can still reshape the plan.
- **Deliverables can be revisited.** A client response may make a previously excluded deliverable relevant again, or render an included one unnecessary. The "ask once, then drop" rule has an explicit exception for this: if the conversation naturally brings something back into scope, re-address it.
- **Sign-off is a gate, not a lock.** Phase One sign-off means the overview is good enough to show the client — not that it's frozen. Phase Two sign-off means the plan is complete enough to act on — not that it will never change.

The agent's job is to **track what changed, log why, and propagate consequences** — not to pretend the plan emerged fully formed on the first pass.

---

## Phase One — Developer Interview (Internal)

**Goal:** Extract everything the developer already knows about the project, stress-test assumptions, and produce the first draft of the project overview.

### Step 1: Seed

1. The developer may fill in `project/seed.md` — a minimal form that takes ≤5 minutes.
1. The agent reads `project/seed.md` to establish initial context.

**If the seed is incomplete or empty:** The agent does not proceed blindly. Instead:
   - Offer the developer two paths:
     - *"You can fill in `project/seed.md` yourself and I'll pick it up from there."*
     - *"Or I can ask you the seed questions one at a time and fill it in as we go."*
   - If they choose the conversational path, ask each seed field one at a time and populate `project/seed.md` as they answer.
   - If the seed is partially filled, acknowledge what's there and ask if they'd like to cover the rest conversationally.

**Checkpoint:** Developer confirms the seed is accurate before proceeding to Step 2.

### Step 2: Open — First Pass

The agent asks **one question at a time**. Never a survey. Each question builds on the last thing the developer said.

**Heuristics for choosing the next question:**
- Prioritize **structural questions** over surface details. When the developer mentions something that implies a structural choice (architecture, stakeholders, constraints, timelines), resolve that structure before drilling into details.
- If the developer mentions a **tension or trade-off** (e.g. "we need it fast but also robust"), name it explicitly. "Those pull in different directions — which is the priority?"
- If a topic seems **under-explored** (e.g. "we'll figure out the database later"), flag it gently rather than ignoring it.

**Behavioral rules:**
- Play back your understanding at **natural hinge points** — not constantly, but when enough has accumulated to summarize. "So what you've described is X, Y, and Z — does that capture it?"
- Accept and propagate **corrections immediately**. If the developer says "no, more like...", that correction cascades. Do not mention the old assumption again.
- **Name tensions** rather than hiding them. The agent-as-colleague is willing to point out where things don't quite fit.
- **Ask once, then drop.** If the developer or client rules something out (a deliverable, a branch, an approach), record it and do not ask about it again — unless the conversation naturally brings it back into scope.

### Step 3: Organize into Branches

As the conversation progresses, the agent identifies **branches** — independent streams of work (UX, backend, admin, etc.) that may proceed with different stakeholders.

When a branch becomes apparent:
1. Log it in `project/state/branches.md` with a proposed name, owner (if known), and status.
1. Ask the developer to confirm the branch split makes sense.
1. Note any **sequencing dependencies** between branches.

**Branch discipline:** The agent knows which branch it's currently discussing and stays there. If the developer mentions something from another branch, the agent may acknowledge it briefly and log a cross-branch flag — but does not switch branches mid-conversation.

### Step 4: Identify Deliverables

After branches are understood but before populating the overview, the agent asks about **deliverables** — the tangible outputs the project is expected to produce.

**One at a time.** As with everything, ask about each deliverable type individually, not as a list.

**Optional items — ask once, then drop.** If the developer or client says a deliverable type is "not needed" or "out of scope," log it in the deliverables section of `project/state/overview.md` as explicitly excluded and **do not ask about it again**. The only exception is if the conversation naturally brings it back into scope (e.g., a new requirement emerges that makes a previously excluded deliverable relevant again).

**Deliverable types to explore:**
- Proof of Concept (feasibility validation)
- Prototype / Wireframes (interactive mockups)
- MVP (minimum viable product — smallest shippable version)
- Beta (feature-complete, limited audience)
- v1.0 / Launch (full public release)
- Technical Spec / Architecture Decision Records
- API Specification
- Design System
- Documentation (user guides, admin manuals)
- Migration Plan (if replacing existing systems)
- Test Plan / QA Strategy
- Deployment / Rollout Plan
- Analytics / Monitoring setup
- Training Materials

**Recording excluded items:** When the developer says a deliverable is not needed, add it to the Deliverables table in `project/state/overview.md` with status `Excluded` and a note about why. This prevents re-asking and preserves the decision context.

**Early-stop heuristic:** Do not enumerate all 14 deliverable types by default. If the developer gives a clear answer early (e.g., "we just need an MVP and a spec"), log it and stop. Only continue exploring if the developer seems uncertain or asks what's typical. The goal is a natural conversation, not a checkbox exercise.

### Step 5: Identify Developer Reference Documents

After deliverables are understood, ask what **reference documents the developer already has or knows about** — materials that can ground the project plan from the developer's side.

**Scope — developer-side only.** In Phase One, only ask about documents the developer can access now: API specs for systems they integrate with, architecture docs for existing systems, brand guidelines they follow, data schemas they work with, existing code they can reference. Documents that only the client holds (compliance docs, contracts, business process docs, client-side research) will be collected in Phase Two.

**One at a time.** Ask about each document type individually, not as a list.

**Ask once, then drop.** If the developer says a type of reference isn't available, log it and don't ask again.

**Document types to explore (developer-side):**
- API Specifications (for integrations the developer builds against)
- Architecture reference documents (existing system designs the developer works with)
- Brand guidelines or Design Systems (that constrain the developer's output)
- Data schemas or database documentation (that the developer must conform to)
- Existing code or repositories (that the new project extends or replaces)
- Research or user studies (that the developer has access to)

**When a document is mentioned (Phase One):**
1. Log it in `project/docs/index.md` with status `Referenced`
1. Add a row to the Reference Documents table in `project/state/overview.md` (summary view — key takeaways and impact on plan)
1. Ask the developer to place the file in the `docs/` directory
1. Once provided, update the index to `Provided`, read the document, and incorporate its content into the relevant state files
1. Update both `project/docs/index.md` to `Reviewed` and fill in the summary columns in `project/state/overview.md` once the agent has fully incorporated it

**What to do with developer-side docs after reading:**
- API specs → inform architecture and integration points
- Architecture docs → inform constraints and system design
- Brand/design docs → inform requirements and deliverables
- Data schemas → inform data model and constraints
- Existing code → inform scope, migration needs, and integration points
- Research → inform problem statement and user needs

### Step 6: Populate the Overview

As the project takes shape, the agent incrementally populates `project/state/overview.md` with:
- Problem statement
- Users and stakeholders
- Core requirements
- Constraints
- Architecture overview (emerging)
- Deliverables (included and excluded)
- Reference documents
- Open questions

The agent does this **during the conversation**, not as a separate step afterward. The overview grows organically.

### Step 7: Surface Structural Questions

Before moving to surface details (UI colors, specific tools, etc.), the agent checks whether any **structural questions** remain unresolved:
- Do we know who the users are?
- Do we know the key constraints?
- Do we know what deliverables are expected?
- Do we know how success is measured?
- Do we understand the core trade-offs?

If any structural question is still open, the agent prioritizes resolving it.

### Step 8: Developer Sign-Off

When the developer indicates the overview is complete:
1. The agent presents the full `project/state/overview.md` for review.
1. The developer reads, amends, and signs off.
1. The agent saves a **snapshot** of the `project/state/`, `project/interactions/`, and `docs/` directories to `project/archive/` with a timestamp.

**Checkpoint:** Nothing leaves Phase One without developer sign-off.

### Step 8a: What Happens If Sign-Off Fails

If the developer does not sign off:

1. Ask what specifically needs to change — is it a **structural gap** (unresolved questions, missing requirements) or **surface edits** (wording, formatting)?
1. **Structural gaps** → return to Step 7 (Surface Structural Questions) to resolve them.
1. **Overview edits** → return to Step 6 (Populate the Overview) for targeted updates.
1. **Major rework** (rare) → return to Step 2 (Open Interview) if the project scope has fundamentally shifted.
1. After changes, present the overview again for sign-off.

### Step 9: Generate Printable Documents

After sign-off, the agent generates clean, self-contained printable documents in `project/output/`:

1. **`project/output/project-overview.md`** — Complete project overview, stripped of comments and agent instructions. Includes: project name, problem statement, users, requirements, constraints, architecture, deliverables, success criteria, reference documents. Formatted cleanly with headers and tables. Ready for PDF export.

1. **`project/output/executive-summary.md`** — Condensed, non-technical summary for stakeholders who don't need the full detail. One page if possible. Includes: what the project is, who it's for, why it matters, what it will produce, timeline, and key risks.

**Formatting rules for all output documents:**
- No HTML comments (`<!-- ... -->`)
- No agent instructions or scaffolding notes
- Clean markdown that renders well in VS Code preview
- Tables where tabular data is clearer than prose
- Self-contained — the reader should not need other files to understand it

**Ask the developer** if they want any additional custom documents generated (e.g., a stakeholder-specific brief).

---

## Phase Two — Client Interview (External, Mediated)

**Goal:** Formulate questions grounded in the overview, send them to the client one at a time, and incorporate responses into the project state.

### Step 1: Identify Gaps

The agent reviews `project/state/overview.md` and `project/state/branches.md` to identify:
- What is known with confidence
- What needs client input to resolve
- Which branch each question belongs to
- Whether the current branch structure covers everything the developer knows — the client may reveal work streams the developer never considered

### Step 2: Formulate One Question

The agent drafts a single question, grounded in the overview and targeting a specific unresolved area within a branch. Each question includes:
- **Context:** A one-sentence reminder of what we know so far
- **The question:** Specific, answerable, neutral in tone
- **Branch tag:** Which branch this question belongs to

**Question format and guidelines:** See [`docs/examples.md`](docs/examples.md) for the format template and examples of well-formed questions.

### Step 3: Developer Review

The developer reviews the question before it is sent. The developer may:
- **Approve** — send as-is
- **Amend** — rephrase or adjust scope
- **Reject** — the question is not ready or not appropriate

**Checkpoint:** Developer is the gatekeeper — no question reaches the client without approval.

### Step 4: Client Responds

When the response arrives, the agent:
1. Records the question and response in `project/state/questions-log.md`
1. Incorporates the response into the relevant state files
1. Checks for **invalidations** — does this response contradict anything in the current overview, branches, or deprecations register?
1. Logs any **cross-branch flags** — implications for a different branch
1. Checks for **deprecations** — does this response render a previous assumption wrong?
1. Checks for **reference documents** — did the client mention or provide any documents? (See Step 4a below.)

### Step 4a: Collect Client Reference Documents

Clients often hold documents the developer never sees: compliance requirements, contracts, internal business process docs, legacy system specs, research reports. When the client mentions or provides a document:

1. Log it in `project/docs/index.md` with status `Referenced` and source `Client`
1. Add a row to the Reference Documents table in `project/state/overview.md`
1. Ask the developer to request the file from the client and place it in `project/docs/`
1. Once provided, read it and incorporate its content — just like developer-side docs in Phase One
1. Update the index and overview summary when reviewed

**Document types clients typically hold:**
- Compliance / Regulatory documents (GDPR, HIPAA, SOC2, etc.)
- Contracts or Statements of Work
- Business process documentation
- Internal research reports or user studies
- Legacy system documentation
- Security policies or audit requirements

**What to do with client-side docs after reading:**
- Compliance docs → inform constraints, requirements, and deprecations
- Contracts/SOWs → inform scope, deliverables, and success criteria
- Business process docs → inform requirements, user flows, and stakeholder needs
- Research → inform problem statement and user needs
- Security docs → inform architecture constraints and requirements

**Ask once, then drop.** If the client says a document isn't available, log it and don't ask again.

### Step 4b: Record Client Interactions

Client communication happens through various channels — email threads, in-person meetings, video calls, chat messages. Raw records of these interactions contain context that may be needed later but should not clutter the agent's working context.

**When an interaction occurs:**
1. Create a markdown file in `project/interactions/` with a descriptive name: `2026-07-01-kickoff-meeting.md`, `2026-07-03-email-ux-thread.md`.
1. Record the raw content — agenda, notes, transcript, email body, decisions made, action items.
1. Log it in `project/interactions/index.md` with date, type, branch, description, and filename.
1. Extract key findings into the relevant state files (overview, branches, questions-log) — the structured state is where the agent works. The raw notes stay in `project/interactions/`.

**Context discipline — critical:** The agent does NOT pre-load files from `project/interactions/`. These are consulted on demand only — when the agent needs to recall a specific detail from a specific meeting or email. The structured state files (`project/state/overview.md`, `project/state/questions-log.md`, etc.) are the working memory. The `project/interactions/` folder is the archive.

### Step 5: Propagate Changes

When a client response invalidates something:
1. Move the old assumption to `project/state/deprecations.md` with the reason it was wrong and what replaces it.
1. Update `project/state/overview.md` with the new information.
1. If the change affects another branch, log a cross-branch flag in `project/state/cross-branch-flags.md`.
1. If the client reveals a **new branch** (a work stream the developer never considered), add it to `project/state/branches.md` with source `Client` and return to Phase One Step 3 (Organize into Branches) to integrate it properly — assess dependencies, ownership, and whether it shifts existing branch priorities.
1. If the client makes an existing branch **irrelevant**, deprecate it in `project/state/branches.md` and propagate the removal to deliverables and the Kanban.

**Severity levels for changes:**
- **Routine** — logged silently; no developer alert needed
- **Significant** — surfaced to the developer immediately (changes scope, timeline, or architecture)
- **Critical** — may warrant pausing Phase Two to re-align

### Step 6: Formulate Next Question

The agent formulates the next question grounded in the updated overview. Each new question builds on everything learned so far.

**When to stop:** A Phase Two loop is complete when no structural questions remain across any branch. Indicators that the loop is ending:
- The overview has no open questions left.
- Client responses are consistently confirming existing information rather than adding new structure.
- All branches have defined deliverables and resolved stakeholder inputs.

**When to continue:** If new answers create new structural questions, deprecate old assumptions, or open cross-branch flags, the loop continues. Do not rush to close.

### Step 7: Populate Kanban

As branches resolve and tasks become clear, the agent populates `project/board/kanban.md` with:
- Tasks derived from the overview and client responses
- Dependencies between tasks
- Branch ownership
- Blockers

The Kanban is populated incrementally — not saved up for the end.

### Step 8: Developer Sign-Off

When the developer confirms Phase Two is complete:
1. Present the final `project/state/overview.md`, `project/board/kanban.md`, and complete `project/state/questions-log.md`.
1. Archive a full snapshot of the `project/state/`, `project/board/`, `project/interactions/`, and `docs/` directories.
1. The developer signs off on the complete project plan.

### Step 8a: What Happens If Sign-Off Fails

If the developer does not sign off on Phase Two:

1. Ask what specifically needs to change — is it a **structural gap** (unresolved questions, missing client input), **Kanban issues** (missing tasks, wrong priorities, effort estimates), or **overview inaccuracy** (the plan doesn't reflect what was learned)?
1. **Structural gaps** → return to Step 1 (Identify Gaps) to formulate new client questions.
1. **Kanban issues** → return to Step 7 (Populate Kanban) for targeted updates.
1. **Overview inaccuracy** → return to the relevant Phase One or Phase Two step to correct it (update branches, revise deliverables, re-interview on a specific topic).
1. **Major rework** (rare) → return to Step 2 (Formulate One Question) if the project scope has fundamentally shifted during the sign-off review.
1. After changes, present the full plan again for sign-off, then proceed to Step 9 to regenerate output documents.

### Step 9: Generate Final Documents

After Phase Two sign-off, the agent generates additional printable documents:

1. **`project/output/requirements.md`** — Full requirements document derived from the overview, branches, deliverables, and client responses. Structured by branch, with traceability back to the overview.

1. **`project/output/kanban-board.md`** — Clean version of the Kanban board, formatted for printing. Groups tasks by column, with priority, branch, deliverable, and dependencies visible.

1. **Update `project/output/project-overview.md`** — Regenerate (replace entirely) with any changes from Phase Two. Do not append — the output document is the single current version.

1. **Update `project/output/executive-summary.md`** — Regenerate (replace entirely) with any changes from Phase Two.

**Regeneration rule:** All output documents are replaced, not appended to. Each generation produces the complete, current version of the document. The templates in `templates/output/` serve as the starting scaffold; strip all HTML comments and agent instructions from the generated result.

**Ask the developer** if they want any additional custom documents (e.g., a compliance traceability matrix, a stakeholder communication plan).

---

## Cross-Branch Flag Protocol

When the agent detects that a decision or response in one branch has implications for another:

1. Log the flag in `project/state/cross-branch-flags.md`
1. Acknowledge it to the developer briefly: "This also affects [branch] — I've logged it."
1. Do **not** switch branches. Continue the current conversation.

---

## Session Resume Protocol

The harness supports multi-session planning. When the agent is asked to resume a prior session:

1. **Read `project/state/session-status.md` first** — this tells you the current phase, step, branch, last topic, and any handoff notes the previous agent left.
1. Read `project/state/overview.md` and `project/state/branches.md` to re-establish full context.
1. Read `project/state/questions-log.md` to understand what's been asked and answered (both phases).
1. Read `project/state/deprecations.md` to understand what assumptions have been invalidated.
1. Offer the developer a summary of where things stand and ask: *"We were discussing [last topic / branch]. Shall I continue there, or is there something else you'd like to address?"*
1. Do not re-ask questions that have already been answered or deprecated.

**Checkpoint:** Always let the developer orient the resumption — do not assume the conversation picks up at the exact same point.

### Before Ending a Session

When the developer indicates the session is ending (but the project plan is not yet complete):

1. **Update `project/state/session-status.md`** with the current phase, step, branch, and last topic discussed.
1. **Leave handoff notes** in the Agent Handoff Notes section — what you were about to ask next, why it matters, any unresolved tensions you noticed, and anything the developer seemed uncertain about.
1. This is not optional. A new agent (or your future self) depends on these notes to pick up midstream without losing context.

---

## Further Reading

These files are extracted from the working documents to keep the agent's context lean. Developers should review them to understand the system's design and conventions:

| File | What's In It |
|------|-------------|
| [`diagrams/process-flow.md`](diagrams/process-flow.md) | Mermaid flowchart — visual overview of both phases with all decision paths |
| [`docs/examples.md`](docs/examples.md) | Worked examples of question format, deprecation entries, cross-branch flags, and Kanban tasks |
| [`agent/system-prompt.md`](agent/system-prompt.md) | The agent's behavioral constitution — tone, rules, and what it does/doesn't do |
| [`../starthere.md`](../starthere.md) | The original design conversation that produced this system's architecture |

---

## First-Run Initialization

When the harness is first used in a project, the `project/` directory doesn't exist yet. The agent handles this automatically:

1. Creates the `project/` directory and all subdirectories (`project/state/`, `project/board/`, `project/docs/`, `project/interactions/`, `project/output/`, `project/archive/`).
1. Copies starter templates from `templates/` into `project/` — including `templates/seed.md` → `project/seed.md`.
1. Proceeds with the normal process.

All project data lives under `project/` — a single folder that can be copied or backed up independently. The `templates/` directory (part of the harness) is tracked in version control. The `project/` directory is gitignored. When the harness is updated upstream, the improvements flow in without overwriting collected project information.

---

## Deprecation Protocol

When an assumption is proven wrong:

1. Log in `project/state/deprecations.md`: original assumption, why it was wrong, replacement, date, and decision context.
1. Update all state files that referenced the old assumption.
1. Do not bring up the old assumption again.

---

## Archive Protocol

Snapshots are saved at:
- End of Phase One (after developer sign-off)
- End of Phase Two (after developer sign-off)
- Any time the developer explicitly requests a checkpoint

Each snapshot is a timestamped copy of the `project/state/`, `project/board/`, `project/interactions/`, and `docs/` directories stored in `project/archive/`.
