# Process Flow Diagram

<!--
This file contains the Mermaid flowchart for the project planning process.
It's extracted from `process.md` so the agent doesn't pay the context cost
of loading a diagram it can't render.

Developer: Open this file in VS Code's Markdown preview (Ctrl+Shift+V) to
see the rendered diagram.
-->

## Full Process Flow

```mermaid
flowchart TD
    S[Seed.md filled in] --> P1[Phase One: Developer Interview]
    P1 --> S1[Step 1: Seed review]
    S1 --> S2[Step 2: Open interview<br>One question at a time]
    S2 --> S3[Step 3: Organize branches]
    S3 --> S4[Step 4: Identify deliverables]
    S4 --> S5[Step 5: Identify developer<br>reference docs]
    S5 --> S6[Step 6: Populate overview]
    S6 --> S7[Step 7: Surface structural questions]
    S7 --> S8{Developer sign-off?}
    S8 -->|No, minor edits| S6
    S8 -->|No, structural gaps| S7
    S8 -->|No, major rework| S2
    S8 -->|Yes| S9[Step 9: Generate output docs]
    S9 --> P2[Phase Two: Client Interview]
    P2 --> T1[Step 1: Identify gaps]
    T1 --> T2[Step 2: Formulate one question]
    T2 --> T3{Developer approves?}
    T3 -->|No| T2
    T3 -->|Yes| T4[Step 4: Client responds<br>+ collect client docs]
    T4 --> T5[Step 5: Propagate changes<br>+ revise branches if needed]
    T5 --> T6{More questions?}
    T6 -->|Yes| T2
    T6 -->|No| T7[Step 7: Populate Kanban]
    T7 --> T8{Developer sign-off?}
    T8 -->|No, minor edits| T7
    T8 -->|No, structural gaps| T1
    T8 -->|No, major rework| T1
    T8 -->|Yes| T9[Step 9: Generate final docs]
    T5 -.->|Client adds/removes branch| S3
```
