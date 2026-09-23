# 5th Semester — Mid-Term Revision Notes

Chapter-wise notes for the mid-term examination, written from the class material in each subject's `source/` folder.

## Subjects

| Subject | Notes | Syllabus | Status |
|---|---|---|---|
| [Optimization](Optimization/) | [10 chapters](Optimization/notes/) | Up to **Duality** | ✅ Complete |
| [Data Communication](Data%20Communication/) | [13 chapters + solved unit test](Data%20Communication/notes/) | Units 1–3 | ✅ Complete |
| [Software Engineering](SE/) | [7 chapters + solved 2025 mid-sem](SE/notes/) | No syllabus file — scoped to lectures | ✅ Complete |
| [Compiler Design](CD/) | [9 chapters](CD/notes/) | NFA/DFA → Predictive Parsing | ✅ Complete |
| [Operating Systems](OS/) | [22 chapters](OS/notes/) | Process → Deadlock | ✅ Complete |

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

## Known gaps

- **OS** — no class material supplied; notes written from the **topic list you provided** (saved in `OS/source/midterm-syllabus.txt`) using standard OS theory. Each OS file carries a banner saying so. Two conventions to confirm against your class notes: **lower number = higher priority**, and the Round Robin queue rule (a new arrival is enqueued **before** a process preempted at the same instant).
- **SE** — Lecture 5 is missing from the folder; L1–L4, L6, L7 are covered. The **2025 mid-sem paper** asks about Agile, UML, use-case/sequence diagrams and inheritance, none of which are in L1–L7. They are answered in full in [SE ch. 8](SE/notes/08-mid-sem-2025-paper-solved.md).
- **CD** — no class material supplied; notes written from the syllabus using standard compiler theory. Each CD file carries a banner saying so.
- **Data Communication** — `topology.pdf`, `Switching.pdf` and `guided_unguided.pdf` are **outside** the mid-term syllabus, so they have no notes. They remain in `source/` for the end-semester exam.

## Revision checklist

- [ ] Optimization — all 10 chapters
- [ ] Optimization — [assignment question bank](Optimization/notes/10-assignment-question-bank.md) *(teacher said to study this question pattern)*
- [ ] Data Communication — Unit 1 (ch. 1–3)
- [ ] Data Communication — Unit 2 (ch. 4–6)
- [ ] Data Communication — Unit 3 (ch. 7–13)
- [ ] Data Communication — [Unit Test 1, solved](Data%20Communication/notes/14-unit-test-1-solved.md) *(the teacher's question pattern)*
- [ ] Software Engineering — all 7 chapters
- [ ] Software Engineering — [2025 mid-sem paper, solved](SE/notes/08-mid-sem-2025-paper-solved.md) *(last year's actual paper)*
- [ ] Compiler Design — all 9 chapters
- [ ] Operating Systems — chapters 1–9 (process & CPU scheduling)
- [ ] Operating Systems — chapters 10–13 (system calls, PCB, fork/exec, threads)
- [ ] Operating Systems — chapters 14–18 (synchronization & semaphores)
- [ ] Operating Systems — chapters 19–21 (deadlock)
- [ ] Operating Systems — [numerical problem bank](OS/notes/22-numerical-problem-bank.md)
