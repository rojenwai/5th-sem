# Software Engineering — Mid-Term Notes

> ⚠️ **No syllabus file was supplied for this subject.** These notes are scoped to the **lectures actually present** in `source/`. If your teacher gives a syllabus, check it against this chapter list.

**Course:** NIT-CS3501 · **Instructor:** Dr. Prahlada Rao B B, ANRF PM Professor, CSE Department, NIT Manipur

## Chapters

| # | Chapter | Lecture | Source file |
|---|---|---|---|
| 1 | [Introduction to Software Engineering](notes/01-introduction-to-software-engineering.md) | **L1** (22-07-2026) | `1.pdf` |
| 2 | [Software Life Cycle Models](notes/02-software-life-cycle-models.md) | **L2** | `pdf  L2-Life Cycle Models-Prahlad 2ppg.pdf` |
| 3 | [Requirements Analysis & Specification (SRS)](notes/03-requirements-analysis-and-srs.md) | **L3** (12-08-2026) | `Lecture 3- Requirements Analysis and Specification -PDF.md` |
| 4 | [Decision Tables & Decision Trees](notes/04-decision-tables-and-trees.md) | **L3** | same as above |
| 5 | [Formal Specification of Systems](notes/05-formal-specification-of-systems.md) | **L4** (18-08-2026) | `Lecture 4- Formal Specification of Systems 2pg  pdf.md` |
| 6 | [Software Design Fundamentals](notes/06-software-design-fundamentals.md) | **L6** (28-08-2026) | `Lecture 6 Software Design-Prahlad-NIT-CS3501.md` |
| 7 | [Function-Oriented Design](notes/07-function-oriented-design.md) | **L7** (09-09-2026) | `Lecture 7 Function Oriented Design-Prahlad-NIT-CS3501.md` |
| 8 | [Structured Design — Examples & Structure Charts](notes/08-structured-design-examples-and-structure-charts.md) | **L7b** (15–18-09-2026) | `8.pdf` |
| 9 | [Mid-Sem 2025 Paper — Solved](notes/09-mid-sem-2025-paper-solved.md) ⭐ *last year's actual paper* | — | `MID-SEM- SE_2025.pdf` |

## Exam pattern (from the 2025 paper)

**30 marks · 1:30 hours.** Q1 has six 1-mark definitions. Then come four 6-mark questions, with an **either/or** choice between Waterfall (Q3) and Agile (Q4). Questions are tagged **CO1** (intro, life cycle models) and **CO2** (requirements, UML).

## ⚠️ Known gaps

- **Lecture 5 is missing** from the folder. L1–L4, L6, L7 and L7b are covered. If you get L5 material, it slots between chapters 5 and 6.
- **The 2025 paper asks about topics not in L1–L7:** **Agile**, **UML**, **use case diagrams**, **sequence diagrams**, **inheritance** and **structured programming**. They account for **9 compulsory marks** (Q1 ii, iv, v and Q6). Agile is the Q4 alternative, so you can avoid it by answering Waterfall. Full answers are in [Ch. 9](notes/09-mid-sem-2025-paper-solved.md). They may be in the missing L5 or a later OO-design lecture, so check with your teacher whether they are in this year's mid-sem.

## About the source files

`8.pdf` (L7b) is a scanned slide deck with no text layer; it was read page by page. The four `.md` files in `source/` are **raw OCR dumps of the lecture slides** — the reading order is scrambled, strikethrough artefacts remain, and slide numbers appear mid-sentence. They are kept as reference so any point can be traced back, but they are **not** usable for revision. The chapters in `notes/` are the rewritten, readable versions.

## Revision checklist

- [ ] Why software engineering exists — the effort–size curve, Art → Craft → Engineering
- [ ] **Abstraction** and **decomposition** — the two fundamental principles
- [ ] Classical vs **Iterative** Waterfall; the shortcomings of the classical model
- [ ] Prototyping, Evolutionary/Incremental, Spiral models + when to use each
- [ ] Comparison table of all life cycle models
- [ ] Functional vs non-functional requirements
- [ ] SRS characteristics and IEEE structure; the three types of SRS problems
- [ ] Draw a **decision table** and a **decision tree** for a given problem
- [ ] Formal specification: model-oriented vs property-oriented; axiomatic vs algebraic
- [ ] **Cohesion** — all 7 levels, in order
- [ ] **Coupling** — all 5 levels, in order
- [ ] Functional independence — why high cohesion + low coupling
- [ ] DFD symbols, levels (context/level-0, level-1, …), balancing, data dictionary
- [ ] Structure charts; transform vs transaction analysis
- [ ] **L7b:** TAS context diagram + level-1 DFD + data dictionary · the 7 DFD guidelines · the **9 common DFD errors** · DFD shortcomings · Ward and Mellor
- [ ] **L7b:** structure-chart symbols (library module, selection, repetition) and rules · flow chart vs structure chart · the RMS, Tic-tac-toe and TAS structure charts
- [ ] **2025 paper:** software crisis (1960s) · Agile model + manifesto · SRS organization **with an example** · "Renew book" use case + **sequence diagram**
- [ ] One-line definitions: feasibility study, structured programming, decision tree, inheritance, UML, functional requirements

## The two facts most likely to be asked

$$\textbf{Good design} = \textbf{High Cohesion} + \textbf{Low Coupling}$$

| Cohesion — 7 levels (worst → best) | Coupling — 5 levels (worst → best) |
|---|---|
| 7. Coincidental | 5. Content |
| 6. Logical | 4. Common |
| 5. Temporal | 3. Control |
| 4. Procedural | 2. Stamp |
| 3. Communicational | **1. Data** ⭐ *(best)* |
| 2. Sequential | |
| **1. Functional** ⭐ *(best)* | |

*Degree of cohesiveness **increases** from Coincidental to Functional. Degree of coupling **increases** from Data to Content.*
