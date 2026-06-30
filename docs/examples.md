# Format Examples

<!--
Developer reference: This file shows examples of the formats the agent uses
when formulating questions, logging deprecations, and flagging cross-branch
concerns. These examples are extracted from the working state files so the
agent doesn't pay the context cost of loading them on every turn.

Agent: If you need to see the exact format for a question, deprecation entry,
or cross-branch flag, consult this file. Otherwise, skip it.
-->

---

## Phase Two Question Format

When the agent formulates a question for the client (Phase Two, Step 2), it uses this structure:

> **Context:** [One sentence summarizing what we understand so far about this topic.]
>
> **Question:** [The single question to ask the client. Specific, neutral, answerable.]
>
> **Branch:** [Branch name]

**Example of a well-formed question:**

> **Context:** The mobile app needs to function in rural areas where connectivity is unreliable. We've identified the core features users need most frequently.
>
> **Question:** What parts of the app do your field workers need to access without an internet connection, and what should happen when they regain connectivity?
>
> **Branch:** UX / Mobile

**Guidelines for formulating questions:**
- Anchor each question in a specific gap from Step 1. Do not ask generic "anything else?" questions.
- The context should be just enough to orient the client — not a full briefing.
- If a question could be answered yes/no, rephrase it to invite explanation. Instead of "Do you need offline support?", ask "What parts of the app do users need to access without an internet connection?"
- After the client answers, do not re-ask a variation of the same question unless the answer genuinely opened a new angle.

---

## Deprecation Register Entry

When an assumption is proven wrong and replaced, the agent logs it in `project/state/deprecations.md`:

| Original Assumption | Why It Was Wrong | Replacement | Date | Decision Context |
|--------------------|-------------------|-------------|------|------------------|
| Users will self-administer via a web portal | Client interview revealed users expect hands-on onboarding | Onboarding includes an initial setup call with the team | 2026-06-29 | Phase Two — UX branch, client response #3 |

**What to look for:** Each entry captures what changed, why it changed, what replaces it, and enough context for someone reading later to understand the reasoning without needing the full conversation.

---

## Cross-Branch Flag Entry

When a decision in one branch affects another, the agent logs it in `project/state/cross-branch-flags.md`:

| Flag ID | Originating Branch | Affected Branch(s) | Description | Severity | Status |
|---------|---------------------|---------------------|-------------|----------|--------|
| CF-001 | UX / Mobile | Backend / API | Offline sync requirements will need API versioning support | Warning | Open |

**Severity levels:**
- **Info** — Something to be aware of; no action required yet
- **Warning** — May require coordination or adjustment
- **Blocker** — Cannot proceed in affected branch until resolved

---

## Kanban Task Entry

Each task on the Kanban board follows this schema:

| Task | Branch | Deliverable | Priority | Effort | Dependencies | Completed | Link to Overview |
|------|--------|-------------|----------|--------|--------------|-----------|------------------|
| Design offline sync protocol | Backend / API | MVP | P1 | M | UX branch: connectivity requirements | | § Architecture |

**Priority levels:** `P0` (critical) · `P1` (high) · `P2` (medium) · `P3` (low)

**Effort levels:** `S` (small — hours) · `M` (medium — days) · `L` (large — weeks) · `XL` (extra large — months) · `?` (unknown)
