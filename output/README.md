# Output Documents

<!--
Agent: Generate clean, self-contained, print-ready markdown documents here
after each sign-off. These are for sharing with stakeholders — no comments,
no agent instructions, no scaffolding markup.

The developer or any stakeholder can open these in VS Code, preview as HTML,
and print to PDF (File > Print... or Ctrl+P in the preview tab).
-->

This directory contains generated printable documents. Each file is a clean,
self-contained markdown document ready for export to PDF or sharing.

## Document Types

| Document | When Generated | Audience |
|----------|---------------|----------|
| `project-overview.md` | After Phase One sign-off | All stakeholders |
| `executive-summary.md` | After Phase One sign-off | Non-technical stakeholders |
| `requirements.md` | After Phase Two sign-off | Development team |
| `kanban-board.md` | After Phase Two sign-off | Project team |
| `agent-guide.md` | After Phase Two sign-off | AI agents assisting with implementation |

## How to Export to PDF

VS Code does not have a built-in Markdown-to-PDF converter. Use one of these options:

**Option A — Browser Print (no extensions needed):**
1. Open the document in VS Code
1. Right-click the editor tab → **Open Preview** (or Ctrl+Shift+V)
1. Right-click the preview → **Open Preview to the Side**
1. Right-click the preview → **Copy** (or select all + copy)
1. Paste into Google Docs, Word, or any document editor and print to PDF

**Option B — VS Code Extension (recommended):**
- Install **Markdown PDF** (`yzane.markdown-pdf`) from the extensions marketplace
- Right-click any `.md` file → **Markdown PDF: Export (pdf)**

**Option C — Command line (pandoc):**
```bash
pandoc document.md -o document.pdf --pdf-engine=weasyprint
```
