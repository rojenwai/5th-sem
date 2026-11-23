# 5th Semester — Mid-Term & End-Sem Revision Notes

Chapter-wise notes for the mid-term and end-semester examinations, written from the class material in each subject's `source/` folder.

## Subjects

| Subject | Mid-term | End-sem (after-mid) | Status |
|---|---|---|---|
| [Optimization](Optimization/) | [Ch. 1–11](Optimization/notes/): up to **Duality** + 2 solved question banks | [Ch. 12–22](Optimization/notes/12-transportation-problem.md): **Transportation, Assignment, IP** + **Nonlinear** (extrema, Lagrange, KKT, convexity, Newton) | ✅ Complete |
| [Data Communication](Data%20Communication/) | [13 chapters + solved unit test](Data%20Communication/notes/) (Units 1–3) | *no after-mid material yet* | ✅ Mid complete |
| [Software Engineering](SE/) | [8 chapters + solved 2025 mid-sem](SE/notes/) | *no after-mid material yet* | ✅ Mid complete |
| [Compiler Design](CD/) | [Ch. 1–11](CD/notes/): NFA/DFA → predictive parsing + class examples + solved 2026 mid-sem | [Ch. 12–18](CD/notes/12-bottom-up-parsing-and-handles.md): **bottom-up, LR(0), SLR, YACC, ICG, optimisation, code generation** | ✅ Complete |
| [Operating Systems](OS/) | [Ch. 1–22](OS/notes/): process → deadlock | [Ch. 23–30](OS/notes/23-memory-management-linker-loader.md): **memory management, paging, virtual memory, EAT, disk scheduling** | ✅ Complete |

## How each subject is organised

```
<Subject>/
├── README.md     ← syllabus, chapter index, revision checklist
├── notes/        ← the actual revision notes, one file per chapter
└── source/       ← your original PDFs / DOCX / PPTX, untouched
```

Nothing was deleted. Every original file was moved into `source/` exactly as it was.

## How to use these notes

Each chapter follows the same shape, so you always know where to look:

| Section | What it is |
|---|---|
| 🎯 **In one line** | The single sentence to remember |
| **Concept** | Plain-language intuition before the jargon |
| **Definitions & formulas** | Tabulated for quick lookup |
| **Diagram** | ASCII waveforms/tableaux, or Mermaid flow diagrams |
| **Worked example** | Full numeric solution, every step shown |
| **Common exam questions** | What actually gets asked |
| ⚡ **Quick revision** | The 60-second recap — read this the night before |

> **Rendering:** open in VS Code (`Ctrl+Shift+V`), Obsidian, or GitHub. Mermaid diagrams and LaTeX maths both render in all three. In VS Code, install *Markdown Preview Mermaid Support* if diagrams show as code blocks.

> **Verification:** every after-mid numerical (transportation/MODI, Hungarian, branch & bound, SLR tables and traces, page replacement, EAT, disk scheduling, fit algorithms) was re-computed by a program. Where a handwritten answer disagrees, the chapter shows both and flags it ⚠️.

## Known gaps

- **Optimization (end-sem)**: the **nonlinear** chapters (18–22) follow `aftermid-syllabus.txt` but **no class notes for them have been supplied yet**, so they are written from standard theory and carry a ⚠️ banner. The Transportation/Assignment/IP chapters come from the class notes. **Homework Problem 2** (p. 19) has two blank cost rows in the notes; it is solved with the standard textbook data and flagged.
- **Compiler Design / OS (end-sem)**: there is **no end-sem syllabus file**; the scope is taken from the full-semester `Rati … full.pdf` notes.
- **OS (mid)**: class notes are now available (`Rati OS FULL.pdf` pp. 1–64), and the "no class material" banners have been replaced. Both open conventions are settled: **Round Robin** queues a new arrival before a preempted process, and **priority** direction is marked (H)/(L) per question (both are used in class).
- **SE** — Lecture 5 is missing from the folder; L1–L4, L6, L7, L7b are covered. The **2025 mid-sem paper** asks about Agile, UML, use-case/sequence diagrams and inheritance, none of which are in L1–L7. They are answered in full in [SE ch. 9](SE/notes/09-mid-sem-2025-paper-solved.md).
- **CD (mid)** — class notes (`Compiler notes.pdf`, `Rati CD full.pdf`) checked against chapters 1–11; the extra Thompson example $(ab\mid a^*)^*$ is in [CD ch. 10 §12](CD/notes/10-class-notes-worked-examples.md).
- **Data Communication** — `topology.pdf`, `Switching.pdf` and `guided_unguided.pdf` are **outside** the mid-term syllabus, so they have no notes. They remain in `source/` for the end-semester exam.

## Revision checklist

### Mid-term

- [ ] Optimization — chapters 1–9
- [ ] Optimization — ⭐ [class notes question bank](Optimization/notes/11-class-notes-question-bank.md) *(the teacher mainly sets exam questions from the class notes; every example is solved here)*
- [ ] Optimization — [assignment question bank](Optimization/notes/10-assignment-question-bank.md) *(teacher said to study this question pattern)*
- [ ] Data Communication — Unit 1 (ch. 1–3)
- [ ] Data Communication — Unit 2 (ch. 4–6)
- [ ] Data Communication — Unit 3 (ch. 7–13)
- [ ] Data Communication — [Unit Test 1, solved](Data%20Communication/notes/14-unit-test-1-solved.md) *(the teacher's question pattern)*
- [ ] Software Engineering — all 8 chapters
- [ ] Software Engineering — [2025 mid-sem paper, solved](SE/notes/09-mid-sem-2025-paper-solved.md) *(last year's actual paper)*
- [ ] Compiler Design — all 9 chapters
- [ ] Compiler Design — [class worked examples](CD/notes/10-class-notes-worked-examples.md) + [2026 mid-sem paper, solved](CD/notes/11-mid-sem-2026-paper-solved.md)
- [ ] Operating Systems — chapters 1–9 (process & CPU scheduling)
- [ ] Operating Systems — chapters 10–13 (system calls, PCB, fork/exec, threads)
- [ ] Operating Systems — chapters 14–18 (synchronization & semaphores)
- [ ] Operating Systems — chapters 19–21 (deadlock)
- [ ] Operating Systems — [numerical problem bank](OS/notes/22-numerical-problem-bank.md)

### End-sem

- [ ] Optimization — chapters 12–16 (transportation, assignment, integer programming)
- [ ] Optimization — ⭐ [transportation / assignment / IP question bank](Optimization/notes/17-transportation-assignment-ip-question-bank.md) *(every class example and homework, solved and verified)*
- [ ] Optimization — chapters 18–22 (nonlinear: extrema, Lagrange, KKT, convexity, Newton–Raphson)
- [ ] Compiler Design — chapters 12–15 (bottom-up, LR(0), ⭐ SLR table + `abb` trace, YACC)
- [ ] Compiler Design — chapters 16–18 (three-address code, ⭐ basic blocks & flow graph, code generation)
- [ ] Operating Systems — chapters 23–26 (linker/loader, fits, paging, multilevel paging)
- [ ] Operating Systems — chapters 27–29 (page replacement, EAT, disk scheduling)
- [ ] Operating Systems — ⭐ [end-sem numerical problem bank](OS/notes/30-end-sem-numerical-problem-bank.md)
