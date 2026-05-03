# Focs-pipeline-simulator
Interactive pipeline hazard simulator

# Plaksha Orbital Pipeline Deck
CS2011 — Foundations of Computer Systems · Assignment 2

**Kashika Kapoor · Jahnavi S · Vansh Jain**

A browser-based pipeline hazard simulator. Input instructions and watch them move cycle-by-cycle through a 4-stage or 5-stage pipeline, with RAW hazard detection, stall insertion, and data forwarding.

---

## Features

- **4-stage and 5-stage** pipeline modes
- **Supported instructions** — `ADD`, `SUB`, `MUL`, `DIV`, `AND`, `OR`, `ORI`, `LW`, `SW`, `SLT`
- **RAW hazard detection** with automatic stall insertion
- **Data forwarding** toggle (EX→EX and MEM→EX paths)
- **Load-use hazard** handling 
- **Side-by-side comparison** — total cycles, stall cycles, RAW hazards, forwarding events, and stalls eliminated, shown for both forwarding and no-forwarding on the same instruction sequence
- **Step / Auto / Run All** execution controls
- Up to 10 instructions per simulation

---

## Files

| File | Description |
|---|---|
| `applet.html` | Open this in any browser to run the simulator |
| `code.rtf` | Full source code of the simulator ,The code is using html+javascript+css|
| `FOCS_Report.pdf` | Detailed report — design decisions, assumptions, test cases |

---
## To Use it

[▶ Open Live Demo](https://yourusername.github.io/repo-name/applet.html)

---

## Quick Start

Download `code.html` and open it in your browser.For the code.

---

## Learn More

For a full explanation of the pipeline model, hazard handling, forwarding logic, and test case analysis — see **`FOCS_Report.pdf`**.
