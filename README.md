# Project Planning Harness

This repo is a **project planning harness** for GitHub Copilot in VS Code. Clone it as the starting point for your project, and Copilot becomes a structured project planning partner — guiding you through a conversational interview process to turn a loose idea into a complete, actionable plan.

## What's Inside

### Harness (tracked in version control)

| File | Purpose |
|------|---------|
| `.gitignore` | Ignores `project/` — a single rule that keeps the harness tracked and project data local |
| `AGENTS.md` | Auto-loaded by Copilot — bootstraps the harness by pointing to `agent/system-prompt.md` |
| `agent/` | Agent-facing files — `system-prompt.md` (behavioral constitution) and `process-agent.md` (step playbook). Developers can ignore this folder. |
| `process.md` | Full developer reference — rationale, examples, and detailed instructions. Read this to understand the system. |
| `diagrams/process-flow.md` | Mermaid flowchart — visual overview of both phases (open in Markdown preview) |
| `docs/examples.md` | Format examples for agent output (questions, deprecations, Kanban tasks) |
| `output/README.md` | Instructions for exporting generated documents to PDF |
| `templates/` | Starter templates for all working files — copied into `project/` on first use (includes `seed.md`, state files, Kanban, etc.) |

### Project Directory (gitignored — all project-specific data in one place)

The `project/` folder contains everything collected or generated during planning:

| Subdirectory | Purpose |
|-------------|---------|
| `project/seed.md` | Your filled-in seed form |
| `project/state/` | Living state files (overview, branches, questions log, session status, etc.) |
| `project/board/kanban.md` | Task board populated as the plan takes shape |
| `project/docs/` | Reference documents (API specs, compliance, brand guidelines, etc.) — uploaded by developer or client |
| `project/interactions/` | Raw client interaction records — meeting notes, email threads, call summaries |
| `project/output/` | Generated printable documents — clean markdown ready for PDF export |
| `project/archive/` | Timestamped snapshots at checkpoints |

> **How it works:** The `templates/` directory holds the empty starter files (part of the harness). On first use, the agent copies them into `project/`. The entire `project/` folder is gitignored, so your project data stays local. Because all project data is under one folder, you can copy or back it up independently. When the harness is updated, you get the improvements without overwriting anything you've collected.

## How to Use This Harness

### Step 1: Clone the Repo

Clone this repo as the starting point for your project, or copy all files into an existing project directory.

### Step 2: Open Copilot Chat

In VS Code, open Copilot Chat. GitHub Copilot automatically reads `AGENTS.md` files — no prompt needed. The harness will bootstrap itself.

If your agent doesn't auto-load `AGENTS.md`, tell it:

> *"Read `AGENTS.md`"*

### Step 3: Fill in the Seed

The agent will set up the `project/` directory and prompt you to fill in `project/seed.md`. Keep it brief — 5 minutes max. Rough answers are fine; the agent will explore them with you. You can also ask the agent to interview you through the seed questions one at a time.

> **Already have a codebase?** Set the `codebase_path` field in `project/seed.md` to the absolute path of your project. The agent scans your project structure, config files, and README to pre-populate the seed and overview automatically — no manual form-filling needed. Nothing is copied or linked; the agent reads directly from your codebase. See the Brownfield Path section in `process.md` for full details.

### Step 4: Get Interviewed

The agent will ask you **one question at a time**, building on your last answer. The conversation should feel natural — like working with a colleague who's helping you think things through.

### Step 5: Sign Off

When Phase One is complete, review `project/state/overview.md` and give sign-off. The agent archives a snapshot.

### Step 6: Client Interview (If Applicable)

If you need client or stakeholder input, the agent formulates questions grounded in the overview. You review each before it goes out.

## Key Principles

- **You are the gatekeeper.** Nothing leaves the room without your approval.
- **One question at a time.** The agent will never send you a survey.
- **Structure emerges.** The agent doesn't impose branches, Kanban columns, or registers upfront — they appear when the conversation demands them.
- **No code.** This harness produces markdown plans, not code scaffolding.

## For Best Results

- Read `process.md` once to understand the full process and design rationale.
- Open `diagrams/process-flow.md` in VS Code's Markdown preview (Ctrl+Shift+V) for a visual overview.
- See `docs/examples.md` for examples of the formats the agent uses (questions, deprecations, Kanban tasks).
- Be honest with the agent — correct it when it drifts.
- The seed is meant to be quick. If you're stuck, write "not sure yet" — the agent will help you figure it out.

## Version Control

The included `.gitignore` already handles the separation: harness files are tracked, project data is ignored. Commit everything — the `.gitignore` ensures only harness files go into version control, not your project-specific data.

To update the harness (e.g., after improvements are made upstream), pull or copy the updated harness files into your repo. Your project data in `project/` will be untouched.

## Project Structure

```
.                        # Your project root — harness files live alongside your code
├── .gitignore           # Single rule: /project/ — keeps harness tracked
├── AGENTS.md            # Auto-loaded by Copilot — bootstraps the harness
├── README.md            # This file
├── process.md           # Step-by-step process definition
├── agent/               # Agent-facing instructions
│   ├── system-prompt.md     # Agent's behavioral constitution
│   └── process-agent.md     # Condensed process playbook
├── diagrams/            # Visual references
│   └── process-flow.md      # Mermaid flowchart
├── docs/                # Harness reference (examples.md only — tracked)
│   └── examples.md          # Format examples for the agent
├── output/              # Harness reference (README.md only — tracked)
│   └── README.md            # PDF export instructions
├── templates/           # Starter templates (tracked — copied to project/ on first use)
│   ├── seed.md              # Seed form template
│   ├── state/               # Empty state file templates
│   ├── board/               # Empty Kanban template
│   ├── docs/                # Empty reference doc tracker
│   ├── interactions/        # Empty interaction tracker
│   └── output/              # Output document templates
│
└── project/             # All project data in one folder (gitignored)
    ├── seed.md              # Your filled-in seed
    ├── state/               # Living project state files
    ├── board/               # Populated Kanban board
    ├── docs/                # Reference documents (API specs, compliance, etc.)
    ├── interactions/        # Raw client interaction records
    ├── output/              # Generated printable documents
    └── archive/             # Checkpoint snapshots
```
