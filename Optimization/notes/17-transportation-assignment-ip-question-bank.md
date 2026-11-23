# 17. Transportation, Assignment & IP: Class-Notes Question Bank (solved) ⭐

> **Source:** Transportation/Assignment/IP class notes, every solved example, homework problem and theory question (pp. 13–23).
> **Every number in this chapter was re-computed by computer** (VAM/MODI implementation + LP solver). Where the notes and the computation disagree, it is flagged ⚠️.

---

## 🎯 How to use this chapter

The teacher's question pattern (p. 19): *"Find the IBFS using NWCR, RM and VAM, apply MODI, construct improvement loops if required, and determine the optimal solution."* Practise **that whole chain** on each problem below. The methods are explained in [Ch. 13](13-initial-bfs-methods.md) (IBFS) and [Ch. 14](14-modi-method.md) (MODI).

| # | Problem | Initial (VAM) | Optimal | Special feature |
|---|---|---|---|---|
| A | Class Problem (p. 13) | 796 | **796** | VAM already optimal |
| B | Cement factories (p. 15) | ₹10,200 | **₹10,000** | Tie in Δ; 2 MODI iterations |
| C | 3×5 problem (pp. 8, 18) | 68 | **67** ⚠️ | Notes stop at 68 |
| D | Homework 1 (p. 19) | 360 | **360** | **Degenerate** IBFS |
| E | Homework 2 (p. 19) | 779 | **743** | Data incomplete in notes ⚠️ |
| F | Homework 3 (p. 19) | 630 | **630** | VAM optimal, unique |
| G | Homework 4 (p. 19) | 585 | **540** | **Unbalanced** + **alternative optima** |
| H | Assignment (p. 20) | – | **9** | Hungarian |
| I | Integer programming (p. 21) | LP 21 | **20** | Branch & Bound |

---

## A. Class Problem (p. 13): VAM → 796, optimal

Fully solved in [Ch. 13 §7](13-initial-bfs-methods.md) (VAM) and [Ch. 14 §3](14-modi-method.md) (MODI).

**Answer:** $x_{14}=11$, $x_{21}=6$, $x_{22}=3$, $x_{24}=4$, $x_{32}=7$, $x_{33}=12$, $Z_{\min} = 796$. All $\Delta_{ij} < 0$, so the optimum is **unique**. For comparison, NWCR gives 1095, row-minima 922, LCM 922 and column-minima 1037.

---

## B. Cement factories (p. 15): ₹10,200 → ₹10,100 → ₹10,000

Fully solved in [Ch. 14 §4](14-modi-method.md).

**Answer:** F1 → P2: 5, F1 → P3: 1, F2 → P3: 1, F3 → P1: 7, F3 → P3: 1, F3 → P4: 2, giving $Z_{\min} = 100 \times 100 = \mathbf{₹10{,}000}$.

> The notes label the 2nd BFS (₹10,100) "Table 4" and the final one ₹10,000. Don't stop at ₹10,100, because (1,3) still has $\Delta = +1$ there.

---

## C. The 3×5 problem (p. 8 table ②, solved on p. 18): NWCR 153 · LCM 78 · VAM 68 · optimum 67

| | D1 | D2 | D3 | D4 | D5 | Supply |
|---|---|---|---|---|---|---|
| **O1** | 2 | 11 | 10 | 3 | 7 | 4 |
| **O2** | 1 | 4 | 7 | 2 | 1 | 8 |
| **O3** | 3 | 9 | 4 | 8 | 12 | 9 |
| **Demand** | 3 | 3 | 4 | 5 | 6 | **21** |

The problem is balanced and $m+n-1 = 7$.

### (1) NWCR (p. 18, solution ①)

$x_{11}=3,\ x_{12}=1,\ x_{22}=2,\ x_{23}=4,\ x_{24}=2,\ x_{34}=3,\ x_{35}=6$

$$Z = 6 + 11 + 8 + 28 + 4 + 24 + 72 = \mathbf{153}$$

### (2) Least-cost (p. 18, solution ②)

The allocations drawn in the notes are $x_{11}=3,\ x_{14}=1,\ x_{24}=2,\ x_{25}=6,\ x_{32}=3,\ x_{33}=4,\ x_{34}=2$:

$$Z = 6 + 3 + 4 + 6 + 27 + 16 + 16 = \mathbf{78}$$

> ⚠️ **The notes write "$Z = 83$"** next to this table, but the allocations shown add up to **78**. Re-add them in the exam.

### (3) VAM (p. 18, solution ③)

| Round | Row penalties | Column penalties | Max | Allocation |
|---|---|---|---|---|
| 1 | 1, 0, 1 | 1, 5, 3, 1, **6** | 6 (D5) | $x_{25} = \min(8, 6) = 6$ |
| 2 | 1, 1, 1 | 1, **5**, 3, 1 | 5 (D2) | $x_{22} = \min(2, 3) = 2$, so O2 is done |
| 3 | 1, 1 | 1, 2, **6**, 5 | 6 (D3) | $x_{33} = \min(9, 4) = 4$ |
| 4 | 1, **5** | 1, 2, **5** | 5 (tie) | $x_{14} = \min(4, 5) = 4$ (cost 3), so O1 is done |
| 5 | only O3 is left | | | $x_{31} = 3$, $x_{32} = 1$, $x_{34} = 1$ |

$$Z_{VAM} = 4(3) + 2(4) + 6(1) + 3(3) + 1(9) + 4(4) + 1(8) = \mathbf{68}$$

This matches the notes. 7 allocations $= m+n-1$, so it is non-degenerate.

### (4) MODI ⚠️ The notes stop here, but 68 is not optimal

Set $u_1 = 0$. The potentials are $u = (0, 0, 5)$ and $v = (-2, 4, -1, 3, 1)$.

| Empty cell | (1,1) | (1,2) | (1,3) | (1,5) | (2,1) | (2,3) | **(2,4)** | (3,5) |
|---|---|---|---|---|---|---|---|---|
| $\Delta$ | −4 | −7 | −11 | −6 | −3 | −8 | **+1** | −6 |

(2,4) enters. The loop is $(2,4)^+ \to (2,2)^- \to (3,2)^+ \to (3,4)^-$ with $\theta = \min(2, 1) = 1$, so $x_{34}$ leaves.

New solution: $x_{14}=4,\ x_{22}=1,\ x_{24}=1,\ x_{25}=6,\ x_{31}=3,\ x_{32}=2,\ x_{33}=4$.

Potentials: $u = (0, -1, 4)$, $v = (-1, 5, 0, 3, 2)$. All $\Delta \le 0$ (the largest is $\Delta_{34} = -1$), so the solution is **optimal**.

$$Z_{\min} = 12 + 4 + 2 + 6 + 9 + 18 + 16 = \boxed{67}$$

> ✔ LP solver: optimum = 67. This problem is a ready-made answer to *"Does VAM always give an optimal solution?"* **No:** 68 vs 67.

---

## D. Homework Problem 1 (p. 19): a degenerate IBFS

| | D1 | D2 | D3 | Supply |
|---|---|---|---|---|
| **S1** | 8 | 6 | 10 | 20 |
| **S2** | 9 | 7 | 4 | 30 |
| **S3** | 8 | 4 | 2 | 25 |
| **Demand** | 10 | 35 | 30 | **75** |

The problem is balanced and $m+n-1 = 5$.

**NWCR:** $x_{11}=10,\ x_{12}=10,\ x_{22}=25,\ x_{23}=5,\ x_{33}=25$, giving $Z = 80+60+175+20+50 = \mathbf{385}$ (5 allocations).

**Row-minima:** S1 → D2 (6): 20. S2 → D3 (4): 30. S3 → D2 (4): 15, then D1 (8): 10. $Z = 120+120+60+80 = \mathbf{380}$. Only 4 allocations, so it is **degenerate**.

**VAM:**

| Round | Row penalties | Column penalties | Allocation |
|---|---|---|---|
| 1 | 2, **3**, 2 | 0, 2, 2 | Row S2 → $c_{23} = 4$: $x_{23} = \min(30, 30) = 30$. **Row S2 and column D3 are both exhausted** |
| 2 | 2, **4** | 0, 2 | Row S3 → $c_{32} = 4$: $x_{32} = 25$ |
| 3 | only S1 is left | | $x_{12} = 10$, $x_{11} = 10$ |

$$Z_{VAM} = 10(8) + 10(6) + 30(4) + 25(4) = \mathbf{360}$$

**Degeneracy:** there are only 4 positive allocations but $m+n-1 = 5$. Put **$\varepsilon$** in the least-cost independent empty cell, **(3,3)** with $c = 2$.

**MODI** ($u_1 = 0$): $v_1 = 8$, $v_2 = 6$, $u_3 = -2$, $v_3 = 4$ (from the ε cell), $u_2 = 0$.

| Empty cell | (1,3) | (2,1) | (2,2) | (3,1) |
|---|---|---|---|---|
| $\Delta$ | −6 | −1 | −1 | −2 |

All $\Delta < 0$, so the solution is **optimal**, with $Z_{\min} = \mathbf{360}$: S1 → D1: 10, S1 → D2: 10, S2 → D3: 30, S3 → D2: 25.

---

## E. Homework Problem 2 (p. 19) ⚠️ Rows S2 and S3 are blank in the notes

The notes give only row S1 (19, 30, 50, 10), supplies 7, 9, 18 and demands 5, 8, 7, 14. These rim values and row 1 are exactly the **standard textbook problem**, whose missing rows are S2 = (70, 30, 40, 60) and S3 = (40, 8, 70, 20). **Confirm with your teacher**. The solution below uses those values.

| | D1 | D2 | D3 | D4 | Supply |
|---|---|---|---|---|---|
| **S1** | 19 | 30 | 50 | 10 | 7 |
| **S2** | 70 | 30 | 40 | 60 | 9 |
| **S3** | 40 | 8 | 70 | 20 | 18 |
| **Demand** | 5 | 8 | 7 | 14 | **34** |

**NWCR:** $x_{11}=5,\ x_{12}=2,\ x_{22}=6,\ x_{23}=3,\ x_{33}=4,\ x_{34}=14$, giving $Z = \mathbf{1015}$.

**LCM:** $x_{14}=7,\ x_{21}=2,\ x_{23}=7,\ x_{31}=3,\ x_{32}=8,\ x_{34}=7$, giving $Z = \mathbf{814}$.

**VAM:**

| Round | Row penalties | Column penalties | Allocation |
|---|---|---|---|
| 1 | 9, 10, 12 | 21, **22**, 10, 10 | $x_{32} = 8$ (c = 8) |
| 2 | 9, 20, 20 | **21**, 10, 10 | $x_{11} = 5$ (c = 19) |
| 3 | 40, 20, **50** | 10, 10 | $x_{34} = 10$ (c = 20) |
| 4 | 40, 20 | 10, **50** | $x_{14} = 2$ (c = 10) |
| 5 | only S2 is left | | $x_{23} = 7$, $x_{24} = 2$ |

$$Z_{VAM} = 95 + 20 + 280 + 120 + 64 + 200 = \mathbf{779}$$

**MODI, iteration 1** ($u_1 = 0$): $u = (0, 50, 10)$, $v = (19, -2, -10, 10)$. $\Delta_{22} = 50 - 2 - 30 = \mathbf{+18}$ and every other Δ is negative. The loop is $(2,2)^+ \to (2,4)^- \to (3,4)^+ \to (3,2)^-$ with $\theta = \min(2, 8) = 2$, so $x_{24}$ leaves.

**Iteration 2:** $x_{11}=5,\ x_{14}=2,\ x_{22}=2,\ x_{23}=7,\ x_{32}=6,\ x_{34}=12$. The potentials are $u = (0, 32, 10)$, $v = (19, -2, 8, 10)$, and all $\Delta < 0$, so the solution is **optimal**.

$$Z_{\min} = 779 - 2 \times 18 = \boxed{743}$$

---

## F. Homework Problem 3 (p. 19): VAM optimal, unique

| | D1 | D2 | D3 | D4 | Supply |
|---|---|---|---|---|---|
| **S1** | 12 | 7 | 9 | 15 | 30 |
| **S2** | 8 | 11 | 6 | 10 | 40 |
| **S3** | 14 | 9 | 12 | 5 | 20 |
| **Demand** | 20 | 25 | 30 | 15 | **90** |

*(Cell S2–D2 is overwritten in the notes. It reads as 11.)*

**NWCR:** $x_{11}=20,\ x_{12}=10,\ x_{22}=15,\ x_{23}=25,\ x_{33}=5,\ x_{34}=15$, giving $Z = \mathbf{760}$.

**Row-minima:** $x_{12}=25,\ x_{13}=5,\ x_{21}=15,\ x_{23}=25,\ x_{31}=5,\ x_{34}=15$, giving $Z = \mathbf{635}$.

**VAM:**

| Round | Row penalties | Column penalties | Allocation |
|---|---|---|---|
| 1 | 2, 2, 4 | 4, 2, 3, **5** | $x_{34} = 15$ (c = 5) |
| 2 | 2, 2, 3 | **4**, 2, 3 | $x_{21} = 20$ (c = 8) |
| 3 | 2, **5**, 3 | 2, 3 | $x_{23} = 20$ (c = 6), so S2 is done |
| 4 | 2, 3 | 2, 3 (tie) | $x_{13} = 10$ (c = 9) *(the row-S3 choice gives the same end result)* |
| 5 | – | – | $x_{12} = 20$, $x_{32} = 5$ |

$$Z_{VAM} = 140 + 90 + 160 + 120 + 45 + 75 = \mathbf{630}$$

**MODI** ($u_1 = 0$): $u = (0, -3, 2)$, $v = (11, 7, 9, 3)$.

| Empty cell | (1,1) | (1,4) | (2,2) | (2,4) | (3,1) | (3,3) |
|---|---|---|---|---|---|---|
| $\Delta$ | −1 | −12 | −7 | −10 | −1 | −1 |

All $\Delta < 0$, so the solution is **optimal and unique**, with $Z_{\min} = \mathbf{630}$.

---

## G. Homework Problem 4 (p. 19): unbalanced + alternative optima ⭐⭐

| | D1 | D2 | D3 | D4 | D5 | Supply |
|---|---|---|---|---|---|---|
| **S1** | 9 | 12 | 9 | 6 | 9 | 40 |
| **S2** | 7 | 3 | 7 | 7 | 5 | 30 |
| **S3** | 6 | 5 | 9 | 11 | 8 | 20 |
| **S4** | 6 | 8 | 11 | 2 | 2 | 10 |
| **Demand** | 20 | 25 | 25 | 20 | 20 | |

**Step 0: balance.** Supply is $40+30+20+10 = 100$ and demand is $20+25+25+20+20 = 110$. Supply < demand, so add a **dummy source S5** with supply **10** and cost **0** in every cell. Now $m+n-1 = 5+5-1 = 9$.

**VAM** (the dummy row's zero costs make its penalties 0, and column penalties use the 0 as the smallest cost):

| Round | Max penalty | Allocation |
|---|---|---|
| 1 | 7 (D3: 7−0) | $x_{53} = 10$ (dummy), so S5 is done |
| 2 | 4 (D4: 6−2) | $x_{44} = 10$ (c = 2), so S4 is done |
| 3 | 3 (tie, D5) | $x_{25} = 20$ (c = 5) |
| 4 | 4 (S2: 7−3) | $x_{22} = 10$ (c = 3), so S2 is done |
| 5 | 7 (D2: 12−5) | $x_{32} = 15$ (c = 5) |
| 6 | 5 (D4) | $x_{14} = 10$ (c = 6) |
| 7 | 3 (tie) | $x_{31} = 5$ (c = 6) |
| 8 | – | $x_{11} = 15$, $x_{13} = 15$ |

$$Z_{VAM} = 135 + 135 + 60 + 30 + 100 + 30 + 75 + 20 + 0 = \mathbf{585}$$

**Count:** 9 positive allocations $= m+n-1$, so it is non-degenerate. ✔

**MODI, iteration 1:** $u = (0, -5, -3, -4, -9)$, $v = (9, 8, 9, 6, 10)$. The positive Δ's are $\Delta_{15} = 1$, $\Delta_{45} = \mathbf{4}$ and $\Delta_{55} = 1$. (4,5) enters along the 8-corner loop
$(4,5)^+ (4,4)^- (1,4)^+ (1,1)^- (3,1)^+ (3,2)^- (2,2)^+ (2,5)^-$ with $\theta = \min(10, 15, 15, 20) = 10$, so $x_{44}$ leaves and $Z = 585 - 4 \times 10 = \mathbf{545}$.

**Iteration 2:** $\Delta_{15} = \Delta_{55} = 1$ is a tie, so take the lower cost, **(5,5)** ($c = 0$). The loop is $(5,5)^+ (5,3)^- (1,3)^+ (1,1)^- (3,1)^+ (3,2)^- (2,2)^+ (2,5)^-$ with $\theta = \min(10, 5, 5, 10) = 5$.
Both $x_{11}$ and $x_{32}$ hit 0. Only **one** may leave ($x_{32}$), and $x_{11}$ stays in the basis at **0**, which makes the new BFS degenerate. $Z = 545 - 5 = \mathbf{540}$.

**Iteration 3: optimal.** $u = (0, -4, -3, -7, -9)$, $v = (9, 7, 9, 6, 9)$. All $\Delta \le 0$, and $\Delta_{15} = \Delta_{51} = 0$.

| | D1 | D2 | D3 | D4 | D5 |
|---|---|---|---|---|---|
| **S1** | (0) | | 20 | 20 | |
| **S2** | | 25 | | | 5 |
| **S3** | 20 | | | | |
| **S4** | | | | | 10 |
| **S5 (dummy)** | | | 5 | | 5 |

$$Z_{\min} = 9(20) + 6(20) + 3(25) + 5(5) + 6(20) + 2(10) = \boxed{540}$$

**Interpretation:** the dummy row means **D3 and D5 are each 5 units short**.

**Multiple optima? Yes.** $\Delta = 0$ in non-basic cells (1,5) and (5,1). Entering (1,5) with $\theta = 5$ gives a different optimal plan with the **same cost 540**:
$x_{13}=15,\ x_{14}=20,\ x_{15}=5,\ x_{22}=25,\ x_{25}=5,\ x_{31}=20,\ x_{45}=10,\ x_{53}=10$. Here D3 alone is 10 short.

> ✔ LP solver: optimum = 540.

---

## H. Assignment (p. 20): Hungarian → 9

$C = \begin{bmatrix} 9 & 2 & 7 \\ 6 & 4 & 3 \\ 5 & 8 & 1 \end{bmatrix}$. Row-reduce, then column-reduce, to get $\begin{bmatrix} 4 & 0 & 5 \\ 0 & 1 & 0 \\ 1 & 7 & 0 \end{bmatrix}$. The assignment is 1 → 2, 2 → 1, 3 → 3, so $Z = 2 + 6 + 1 = \mathbf{9}$. Full steps are in [Ch. 15 §4](15-assignment-problem.md).

## I. Integer programming (p. 21): Branch & Bound → 20

$\max 5x_1 + 4x_2$ s.t. $6x_1 + 4x_2 \le 24$, $x_1 + 2x_2 \le 6$. The LP gives $(3, 1.5)$ with $Z = 21$. Branching gives $x_2 \le 1$: $(10/3, 1)$ → $x_1 \le 3$: $(3,1)$, $Z = 19$ · $x_1 \ge 4$: **$(4,0)$, $Z = 20$** · and $x_2 \ge 2$: $(2,2)$, $Z = 18$. **Optimum $(4, 0)$, $Z = 20$.** Full tree in [Ch. 16 §4](16-integer-programming.md).

---

## J. Theory homework: model answers

### "Think and answer" (p. 18) and Homework (p. 23)

**1. Why does a non-degenerate BFS of an $m \times n$ balanced TP contain exactly $m+n-1$ basic allocations?**
There are $m+n$ rim equations, but they are **linearly dependent**: the sum of the supply equations equals the sum of the demand equations (both are $\sum\sum x_{ij}$). The rank is $m+n-1$, so a basis has $m+n-1$ variables. "Non-degenerate" means every one of them is positive. Graphically, the occupied cells form a **spanning tree** on the $m$ row-nodes plus $n$ column-nodes, and a tree on $m+n$ nodes has $m+n-1$ edges.

**2. Does VAM always produce an optimal solution? Justify with an example.**
**No.** VAM is a **heuristic** that usually lands near the optimum. Counter-examples from these notes: problem C (VAM 68, optimum **67**) and the cement problem B (VAM ₹10,200, optimum **₹10,000**). For problems A and F, VAM happened to be optimal. Always test with MODI.

**3. Difference between a degenerate and a non-degenerate BFS.**

| Non-degenerate | Degenerate |
|---|---|
| Exactly $m+n-1$ **positive** allocations | Fewer than $m+n-1$ positive allocations (some basic variable is 0) |
| MODI works directly | $u_i, v_j$ cannot all be found. Add **ε** in an independent cell first |
| Example: problem A (6 = 6) | Example: problem D (4 < 5) |

It arises when one allocation exhausts a row **and** a column simultaneously (a partial sum of supplies equals a partial sum of demands).

**4. Can MODI be applied directly to a TP with unequal total supply and demand?**
**No.** The equalities $\sum_j x_{ij} = a_i$ and $\sum_i x_{ij} = b_j$ cannot both hold, so no feasible BFS exists to test. First **balance** it with a dummy row or column at zero cost (problem G), then apply MODI.

**5. State the MODI optimality condition for a minimisation TP.**
With $u_i + v_j = c_{ij}$ on the basic cells, the current BFS is optimal iff
$$\Delta_{ij} = u_i + v_j - c_{ij} \le 0 \quad \text{for every non-basic cell}.$$
(Equivalently, the reduced cost $c_{ij} - u_i - v_j \ge 0$.) $\Delta_{ij} = 0$ at the optimum means alternative optima.

**6. Why is a closed loop necessary for improving a transportation solution?**
Adding θ to the entering cell would break its row and column totals. Compensating with $-\theta$, $+\theta$, … at the other corners, turning only at occupied cells, keeps **every rim requirement satisfied**. Choosing θ = the smallest $(-)$ allocation keeps everything $\ge 0$ and drives exactly one basic variable to zero, so the result is again a BFS with $m+n-1$ cells.

**7. Why do row and column reductions preserve the optimal assignments?**
Every assignment picks exactly **one** cell in every row and column. Subtracting $k$ from a row lowers the cost of **all** assignments by the same $k$, so their order is unchanged ([Ch. 15 §2](15-assignment-problem.md)).

**8. How is an unbalanced assignment problem handled?**
Add **dummy rows or columns with zero cost** to make the matrix square. A dummy assignment means that agent is idle or that task is not done.

**9. Significance of covering zeros with the minimum number of lines (Hungarian).**
The minimum number of lines equals the **maximum number of independent zeros** (König). If it equals $n$, a complete zero-cost, and therefore optimal, assignment exists. If fewer, adjust: subtract the smallest uncovered element from the uncovered cells and add it at the intersections.

**10. Why can't we simply round the LP-relaxation solution?**
Rounding can be **infeasible** ($(3, 1.5) \to (3, 2)$ violates $6x_1 + 4x_2 \le 24$) or **sub-optimal** ($(3, 1)$ gives 19 < 20). With $n$ fractional variables there are $2^n$ roundings and none is guaranteed optimal.

**11. Conditions under which a node is fathomed in Branch and Bound.**
① its LP relaxation is **infeasible**; ② its LP optimum is **already integer** (update the incumbent); ③ its LP value is **no better than the current incumbent** (for max, $Z_{node} \le Z_{best}$).

**12. Can an IPP have a better optimal objective value than its LP relaxation?**
**No.** The IP feasible set is a subset of the LP feasible set, so for max $Z_{IP}^* \le Z_{LP}^*$ (here $20 \le 21$). They are equal only if the LP optimum is already integer.

---

## ⚡ Quick revision: the answers to memorise

| Problem | Answer |
|---|---|
| Class Problem (p. 13) | NWCR 1095 · LCM 922 · **VAM 796 = optimal** |
| Cement (p. 15) | **₹10,200 → ₹10,100 → ₹10,000** |
| 3×5 (p. 18) | NWCR 153 · LCM 78 · VAM 68 · **optimum 67** |
| HW 1 | VAM 360 (**degenerate**, ε at (3,3)) = optimal |
| HW 2 | VAM 779 → **743** (textbook data) |
| HW 3 | VAM **630** = optimal, unique |
| HW 4 | Dummy S5 (10) · VAM 585 → 545 → **540** · **alternative optima** |
| Assignment | **9** |
| IP | LP 21 → **(4, 0), Z = 20** |

---

**Previous:** [← 16. Integer Programming](16-integer-programming.md) · **Next:** [18. Nonlinear Programming & Unconstrained Extrema →](18-nlp-and-unconstrained-extrema.md)
