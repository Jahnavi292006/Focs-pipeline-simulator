# Focs-pipeline-simulator
Interactive pipeline hazard simulator

# 🛰️ Plaksha Orbital Pipeline Deck

![Course](https://img.shields.io/badge/CS2011-FOCS-1d4ed8?style=flat-square) ![Assignment](https://img.shields.io/badge/Assignment-2-6d28d9?style=flat-square) ![Type](https://img.shields.io/badge/Pipeline-Simulation-0f766e?style=flat-square) ![Hazards](https://img.shields.io/badge/RAW-Hazards-c2410c?style=flat-square) ![Tech](https://img.shields.io/badge/Vanilla-JS-f59e0b?style=flat-square&logo=javascript&logoColor=white)

> CS2011 — Foundations of Computer Systems · Plaksha University  
> **Kashika Kapoor · Jahnavi S · Vansh Jain**

A browser-based interactive simulator for visualising instruction execution in a single-issue, in-order pipeline. Supports both 4-stage and 5-stage configurations with real-time RAW hazard detection, stall insertion, and data forwarding.

**[▶ Open Live Demo](https://yourusername.github.io/repo-name/applet.html)** ← _replace with your GitHub Pages link_

---

## Pipeline Architecture

```
5-Stage In-Order Pipeline
┌────┐   ┌────┐   ┌────┐   ┌─────┐   ┌────┐
│ IF │──▶│ ID │──▶│ EX │──▶│ MEM │──▶│ WB │
└────┘   └────┘   └────┘   └─────┘   └────┘
 Fetch   Decode  Execute   Memory   Writeback

4-Stage variant merges MEM+WB → MEM/WB

Hazard Resolution
  RAW detected at ID stage
  ├── Forwarding ON  → EX→EX or MEM→EX path (0 stalls*)
  └── Forwarding OFF → stall until producer finishes WB
  * load-use always requires exactly 1 stall cycle
```

---

## Features

| Feature | Details |
|---|---|
| Pipeline modes | 4-stage (IF ID EX MEM/WB) and 5-stage (IF ID EX MEM WB) |
| Hazard detection | RAW (Read After Write) only — WAR/WAW not needed in single-issue in-order |
| Hazard resolution | Stall insertion with optional EX→EX and MEM→EX data forwarding |
| Load-use handling | Always inserts 1 stall even with forwarding enabled |
| Execution modes | Run All · Step · Auto (550 ms/cycle) |
| Visualisation | Colour-coded stage cells, animated forwarding arrows, stall tooltips |
| Stats panel | Side-by-side comparison of total cycles, stalls, RAW hazards, forwarding events |
| Instruction builder | Dropdown-driven; supports ADD, SUB, AND, OR, SLT, LW, SW, ORI (up to 10 instructions) |

---

## Test Cases

| # | Instructions | Hazard | Stalls (no fwd) | Stalls (fwd) |
|:---:|---|---|:---:|:---:|
| 1 | `ADD R1,R2,R3` → `SUB R4,R5,R6` | None | 0 | 0 |
| 2 | `ADD R4,R5,R6` → `SUB R1,R4,R2` | RAW (ALU) | 2 | 0 |
| 3 | `LW R5,0(R3)` → `ADD R6,R5,R7` | Load-use | 2 | 1 |
| 4 | `LW R5` → `ADD R6,R5,R7` → `SUB R8,R6,R9` → `LW R10,4(R3)` | RAW chain + Load-use | 4+ | 1 |

---

## How to Run

No build step needed — it's a single self-contained HTML file.

```bash
git clone https://github.com/Jahnavi292006/repo-name.git
cd repo-name
open applet.html        # macOS
# or just double-click the file on Windows/Linux
```

Or host it instantly on GitHub Pages:  
`Settings → Pages → Branch: main → / (root) → Save`

---

## Implementation Notes

- **Stall propagation** — when an instruction stalls in ID, the instruction in IF is frozen for the same cycle to preserve in-order behaviour.
- **Forwarding detection** — checked at the cycle a consumer moves from ID to EX; if the producer is in EX (EX→EX) or MEM (MEM→EX) at that same cycle, the hazard is resolved with zero added stalls.
- **Load-use exception** — the loaded value is only ready at the end of MEM, one cycle after the consumer needs it at EX entry, so one stall is unavoidable.
- **Scope** — WAR and WAW hazards are not modelled (they cause no corruption in a single-issue in-order pipeline). Control and structural hazards are also out of scope.

---

## File Structure

```
.
├── applet.html   # entire simulator — HTML + CSS + JS, no dependencies
└── README.md
```

---

_Assignment 2 · CS2011 Foundations of Computer Systems · Plaksha University_
