# Branch Register

<!--
Agent: Create this file when the developer naturally distinguishes
independent streams of work. Do not impose branches — let them emerge.

If no branches are needed, leave this file empty.
-->

| Branch | Owner | Stakeholder | Source | Status | Depends On | Description |
|--------|-------|-------------|--------|--------|------------|-------------|
| | | | | | | |
| | | | | | | |
| | | | | | | |

**Status values:** `Active` · `Blocked` · `Complete` · `Dormant` · `Deprecated`

**Source values:** `Developer` (identified in Phase One) · `Client` (revealed in Phase Two)

**Guidelines:**
- Each branch should be independently workable with its own stakeholder.
- A branch may be in Phase Two (client interview) while another is still in Phase One.
- Cross-branch dependencies are tracked in `cross-branch-flags.md`.
- The client may reveal branches the developer never considered — add them here with source `Client` and return to Phase One Step 3 to integrate them properly.
- If a branch becomes irrelevant, mark it `Deprecated` rather than deleting it — preserve the decision trace.
