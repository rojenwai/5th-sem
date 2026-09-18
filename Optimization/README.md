# Optimization — Mid-Term Notes

> **Syllabus (from teacher):** *"Mid term syllabus: from the beginning up to duality."*
> *"For the Simplex Method and Revised Simplex Method portion, study **only from the class notes**."*
> *"Study the question pattern given in this assignment."*

That last instruction matters — [Chapter 10](notes/10-assignment-question-bank.md) works through every question in the assignment.

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
