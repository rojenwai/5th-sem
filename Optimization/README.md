# Optimization — Mid-Term Notes

> **Syllabus (from teacher):** *"Mid term syllabus: from the beginning up to duality."*
> *"For the Simplex Method and Revised Simplex Method portion, study **only from the class notes**."*
> *"Study the question pattern given in this assignment."*

That last instruction matters — [Chapter 10](notes/10-assignment-question-bank.md) works through every question in the assignment.

> ⭐ **The teacher mainly sets exam questions from the class notes.** [Chapter 11](notes/11-class-notes-question-bank.md) solves **every example, question and practice problem in Class Notes 1–5**, with full simplex tables checked against the teacher's answers. It also solves the problems the notes state but never solve (🆕 Big-M Ex 2 and duality Practice Problems 1–4). **Make Ch. 11 your main revision source**, with Ch. 10 second.

## Chapters

| # | Chapter | Source |
|---|---|---|
| 1 | [Introduction to Optimization & LPP](notes/01-introduction-to-optimization-and-lpp.md) | Class Note 1 |
| 2 | [LPP Formulation](notes/02-lpp-formulation.md) | Class Note 1 |
| 3 | [Basic Solutions & BFS](notes/03-basic-solutions-and-bfs.md) | Class Note 1, 2 |
| 4 | [Graphical Method](notes/04-graphical-method.md) | Class Note 1 |
| 5 | [Standard Form, Slack & Surplus](notes/05-standard-form-slack-surplus.md) | Class Note 2 |
| 6 | [Simplex Method](notes/06-simplex-method.md) | Class Notes 2, 3 |
| 7 | [Artificial Variables, Big-M & Two-Phase](notes/07-big-m-and-two-phase.md) | Class Notes 3, 4 |
| 8 | [Revised Simplex Method](notes/08-revised-simplex-method.md) | Class Note 4 |
| 9 | [Duality](notes/09-duality.md) | Class Note 5 |
| 10 | [Assignment Question Bank (solved)](notes/10-assignment-question-bank.md) | `optimization__assignment_I.pdf` |
| 11 | [**Class Notes Question Bank (solved)**](notes/11-class-notes-question-bank.md) ⭐ | All five class notes |

## Source files

| File | Content |
|---|---|
| `OPTIMIZATION_CLASS_NOTE-1.pdf` | Intro, classification, LPP, formulation, basic solutions, graphical method |
| `Optimization _Class Note_II.pdf` | Simplex: slack/surplus, standard matrix form, initial BFS |
| `OPtimization_class_notes_III.pdf` | Simplex table, computational steps, artificial variables |
| `optimization IV.pdf` | Revised simplex, artificial variable technique, Big-M |
| `class Note 5.pdf` | Duality |
| `optimization__assignment_I.pdf` | Assignment — **the stated question pattern** |

## Revision checklist

**Class-notes questions (highest priority — the teacher sets exams from these; see [Ch. 11](notes/11-class-notes-question-bank.md))**
- [ ] Formulate: shopkeeper, diet, lamps, tyres
- [ ] Basic solutions: Class Note 1 Ex 6–10 (including "show this is **not** a basic solution")
- [ ] Graphical: Ex 11 (min, $Z = 240$) and Ex 12 (max, $Z = 325500$)
- [ ] Reduce F.S. → B.F.S.: Class Note II Ex 2, 3, 5 (two answers) and 4/6 (tie → degenerate)
- [ ] Simplex: Class Notes III Ex 1–5 (1000 · 765/41 · −11 · 6 · 3600)
- [ ] Big-M: Ex 1 (52, alternative optima) · 🆕 Ex 2 (**infeasible**)
- [ ] Revised simplex: Ex 1 (5) · Ex 2 (13/7)
- [ ] Duality: Ex 1–4 · 🆕 Practice Problems 1–4

**General**
- [ ] Can classify an optimization problem (linear / nonlinear / integer / convex …)
- [ ] Can formulate a word problem into an LPP
- [ ] Know: solution vs feasible solution vs basic solution vs BFS vs optimal BFS
- [ ] Can find **all** basic solutions of a system and label degenerate / non-degenerate
- [ ] Can solve a 2-variable LPP graphically (corner point **and** iso-profit)
- [ ] Know when to add slack / surplus / artificial variables
- [ ] Can run a full simplex table to optimality
- [ ] Know the Big-M and Two-Phase procedures, and the infeasibility test
- [ ] Can compute a revised simplex iteration using $B^{-1}$
- [ ] Can write the dual of any primal (≤, ≥, =, unrestricted)
- [ ] Know the duality theorems and what $Z_P = Z_D$ means

## Formula sheet (the ones worth memorising)

$$x_B = B^{-1}b \qquad Y_j = B^{-1}\alpha_j \qquad Z = c_B^T x_B \qquad \Delta_j = c_j - c_B^T Y_j$$

| Rule | Statement |
|---|---|
| **Optimality** (max) | Optimal when $\Delta_j \le 0$ for all $j$ |
| **Entering variable** | Largest positive $\Delta_k = \max\{\Delta_j : \Delta_j > 0\}$ |
| **Leaving variable** | $\dfrac{x_{Br}}{y_{rk}} = \min_i \left\{ \dfrac{x_{Bi}}{y_{ik}} : y_{ik} > 0 \right\}$ |
| **Unbounded** | Entering column has $\Delta_k > 0$ but every $y_{ik} \le 0$ |
| **Infeasible** | Phase I ends with $W^* > 0$, or an artificial variable is positive at the Big-M optimum |
| **Min → Max** | $\min Z = -\max(-Z)$; if $\max(-Z) = v$ then $\min Z = -v$ |
