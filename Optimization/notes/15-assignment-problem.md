# 15. The Assignment Problem: the Hungarian Method

> **Syllabus:** After-mid. *Assignment problem*
> **Source:** Transportation/Assignment/IP class notes p. 20 (method + 3×3 example) and p. 23 (homework). Worked examples 2–3 below are **added** to cover the line-covering and maximisation steps that the class example never reaches. They are marked 🆕 and verified by computer.

---

## 🎯 In one line

Transportation asks **"how much to allocate?"**. Assignment asks **"who should do which task?"**. Reduce every row and column so that each has a zero, cover the zeros with the fewest lines, and when $n$ lines are needed, pick one independent zero per row and column.

---

## 1. Assignment as a special transportation problem (p. 20)

> **Can we consider an assignment problem as a transportation problem?** **Yes.** Each source has **supply 1** and each destination has **demand 1**.

An **assignment problem** is a special type of optimization problem in which **agents are assigned to tasks**, generally **one agent per task**, to **minimise total cost** or **maximise total benefit**.

Unlike the transportation problem, where $x_{ij}$ could be 20 or 50 units, here $x_{ij}$ is a **yes-or-no decision**:

$$x_{ij} = \begin{cases} 1 & \text{if agent } i \text{ performs task } j \\ 0 & \text{otherwise} \end{cases} \qquad c_{ij} = \text{cost of assigning agent } i \text{ to task } j$$

$$\boxed{\text{Minimize } Z = \sum_{i=1}^{n}\sum_{j=1}^{n} c_{ij}x_{ij}} \quad \text{s.t.} \quad \sum_{j=1}^{n} x_{ij} = 1 \;(\text{each agent one task}), \quad \sum_{i=1}^{n} x_{ij} = 1 \;(\text{each task one agent}), \quad x_{ij} \in \{0, 1\}$$

| | Transportation | Assignment |
|---|---|---|
| Question | How much to allocate? | Who does which task? |
| $x_{ij}$ | Any quantity $\ge 0$ | 0 or 1 |
| Supply / demand | $a_i$, $b_j$ | All equal to **1** |
| Matrix | $m \times n$ | Square $n \times n$ (after balancing) |
| Basic cells in a BFS | $m+n-1$ | $2n-1$, but only $n$ are positive. **Always highly degenerate** |
| Method | VAM + MODI | **Hungarian method** |

> Because only $n$ of the $2n-1$ basic variables are non-zero, MODI would have to fight $n-1$ ε's. The Hungarian method avoids this.

---

## 2. Why reductions work (p. 23 Q5)

**Theorem.** If a constant is subtracted from (or added to) every element of a row or column of the cost matrix, the **optimal assignment is unchanged**.

*Reason:* every feasible assignment uses **exactly one** cell from each row and each column. Subtracting $k$ from row $i$ lowers the cost of **every** assignment by exactly $k$, so the ranking of assignments does not change. Once the matrix is non-negative, an assignment made entirely of **zeros** costs 0 in the reduced matrix, which is the smallest possible. It is therefore optimal for the original matrix too.

---

## 3. The Hungarian method: steps ⭐⭐⭐

| Step | Name | Action |
|---|---|---|
| 0 | Balance | If the matrix is not square, add **dummy** rows or columns of **0** |
| 1 | **Row reduction** | Find the minimum cost in each row and subtract it from every entry in that row |
| 2 | **Column reduction** | Find the minimum of each column of the row-reduced matrix and subtract it from every entry in that column |
| 3 | **Cover zeros** | Draw the **minimum number of horizontal and vertical lines** that cover all the zeros |
| 4 | **Test** | If the number of lines $= n$, an optimal assignment exists, so go to step 6 |
| 5 | **Adjust** | If lines $< n$: find the **smallest uncovered** element $k$. **Subtract** $k$ from all uncovered elements and **add** $k$ at the **intersections** of two lines (covered-once elements don't change). Go back to step 3 |
| 6 | **Select independent zeros** | Choose zeros so that **exactly one zero is selected in every row and every column** |
| 7 | **Total cost** | Add up the **original** costs of the selected cells |

**How to draw the minimum lines (row/column scanning):**
1. **Row scan:** for each row with **exactly one** unmarked zero, box that zero (assign it) and cross out the other zeros in its column.
2. **Column scan:** for each column with exactly one unmarked zero, box it and cross out the other zeros in its row.
3. Repeat until no zeros are left unmarked. If a full set of $n$ boxes appears, you are done.
4. Otherwise tick the rows without a box, tick the columns that have zeros in ticked rows, tick the rows that have boxes in ticked columns, and repeat. Then draw lines through **un-ticked rows** and **ticked columns**.

> **Significance of covering zeros with the minimum number of lines (p. 23 Q7).** The minimum number of lines equals the **maximum number of independent zeros** (König's theorem). Fewer than $n$ lines means a complete zero-cost assignment does not yet exist, so the matrix must be adjusted to create new zeros without destroying the useful ones.

---

## 4. Worked example 1: the class example (p. 20) ⭐

$$C = \begin{bmatrix} 9 & 2 & 7 \\ 6 & 4 & 3 \\ 5 & 8 & 1 \end{bmatrix}$$

**Step 1: row reduction** (row minima 2, 3, 1):

$$\begin{bmatrix} 9-2 & 2-2 & 7-2 \\ 6-3 & 4-3 & 3-3 \\ 5-1 & 8-1 & 1-1 \end{bmatrix} = \begin{bmatrix} 7 & 0 & 5 \\ 3 & 1 & 0 \\ 4 & 7 & 0 \end{bmatrix}$$

**Step 2: column reduction** (column minima 3, 0, 0):

$$\begin{bmatrix} 7-3 & 0-0 & 5-0 \\ 3-3 & 1-0 & 0-0 \\ 4-3 & 7-0 & 0-0 \end{bmatrix} = \begin{bmatrix} 4 & 0 & 5 \\ 0 & 1 & 0 \\ 1 & 7 & 0 \end{bmatrix}$$

**Step 3: select independent zeros.** Row 1 has a single zero at column 2, so box it. Row 3 has a single zero at column 3, so box it. That forces row 2 to column 1.

$$\begin{bmatrix} 4 & \boxed{0} & 5 \\ \boxed{0} & 1 & 0 \\ 1 & 7 & \boxed{0} \end{bmatrix} \qquad \begin{aligned} c_1 &\to \text{job } 2 \\ c_2 &\to \text{job } 1 \\ c_3 &\to \text{job } 3 \end{aligned}$$

**Step 4: total cost from the original matrix:**

$$Z_{\min} = c_{12} + c_{21} + c_{33} = 2 + 6 + 1 = \mathbf{9}$$

---

## 5. Worked example 2 🆕: when lines < n (5 jobs × 5 machines)

$$C = \begin{bmatrix} 9 & 11 & 14 & 11 & 7 \\ 6 & 15 & 13 & 13 & 10 \\ 12 & 13 & 6 & 8 & 8 \\ 11 & 9 & 10 & 12 & 9 \\ 7 & 12 & 14 & 10 & 14 \end{bmatrix}$$

**Row reduction** (minima 7, 6, 6, 9, 7), then **column reduction** (column minima 0, 0, 0, 2, 0, so only column 4 changes):

$$\begin{bmatrix} 2 & 4 & 7 & 2 & 0 \\ 0 & 9 & 7 & 5 & 4 \\ 6 & 7 & 0 & 0 & 2 \\ 2 & 0 & 1 & 1 & 0 \\ 0 & 5 & 7 & 1 & 7 \end{bmatrix}$$

**Cover the zeros.** Rows 2 and 5 both have their **only** zero in column 1, so at most one of them can be assigned there. The minimum cover is **4 lines**: rows 1, 3, 4 and column 1.

```
          M1   M2   M3   M4   M5
   J1  ──  2────4────7────2────0──   (line)
   J2      0│   9    7    5    4
   J3  ──  6────7────0────0────2──   (line)
   J4  ──  2────0────1────1────0──   (line)
   J5      0│   5    7    1    7
           (line on column 1)
```

4 lines < 5, so the matrix must be **adjusted**. The smallest uncovered element is $k = 1$ (cell J5–M4).
- Subtract 1 from every **uncovered** element (rows 2 and 5, columns 2–5).
- Add 1 at the **intersections** (rows 1, 3, 4 × column 1).

$$\begin{bmatrix} 3 & 4 & 7 & 2 & \boxed{0} \\ \boxed{0} & 8 & 6 & 4 & 3 \\ 7 & 7 & \boxed{0} & 0 & 2 \\ 3 & \boxed{0} & 1 & 1 & 0 \\ 0 & 4 & 6 & \boxed{0} & 6 \end{bmatrix}$$

Now 5 lines are needed, which equals $n$, so the assignment is optimal:

| Job | Machine | Original cost |
|---|---|---|
| J1 | M5 | 7 |
| J2 | M1 | 6 |
| J3 | M3 | 6 |
| J4 | M2 | 9 |
| J5 | M4 | 10 |
| | **Total** | **38** |

---

## 6. Variations ⭐

### Unbalanced assignment (p. 23 Q6)

If the number of agents ≠ the number of tasks, add **dummy rows or columns with cost 0** to make the matrix square. An agent assigned to a dummy task is **idle**, and a task assigned to a dummy agent is **not done**.

### Maximisation 🆕

The Hungarian method minimises. To **maximise** profit, convert first:

$$c'_{ij} = (\text{largest element}) - p_{ij} \qquad \text{(or simply use } -p_{ij}\text{)}$$

**Example.** Profits $P = \begin{bmatrix} 16 & 10 & 14 \\ 12 & 13 & 15 \\ 14 & 16 & 12 \end{bmatrix}$. The largest element is 16:

$$C' = \begin{bmatrix} 0 & 6 & 2 \\ 4 & 3 & 1 \\ 2 & 0 & 4 \end{bmatrix} \xrightarrow{\text{row red.}} \begin{bmatrix} \boxed{0} & 6 & 2 \\ 3 & 2 & \boxed{0} \\ 2 & \boxed{0} & 4 \end{bmatrix}$$

So A1 → J1, A2 → J3, A3 → J2, and the **maximum profit** is $16 + 15 + 16 = \mathbf{47}$. Checking all $3! = 6$ assignments confirms 47 is the largest.

### Prohibited (restricted) assignments

If agent $i$ cannot do task $j$, set $c_{ij} = M$ (a very large number) so that it is never chosen.

---

## 7. Common exam questions

1. **Formulate the assignment problem as an LPP.** See §1, with $x_{ij} \in \{0,1\}$.
2. **Is assignment a special case of transportation? Explain.** Yes: every supply and demand is 1 (§1).
3. **Solve by the Hungarian method.** Use the §4 and §5 templates.
4. **Why do row and column reductions preserve the optimal assignment?** Every assignment uses one cell per row and column (§2) (p. 23 Q5).
5. **How is an unbalanced assignment problem handled?** With dummy rows or columns of 0 (p. 23 Q6).
6. **What is the significance of covering zeros with the minimum number of lines?** Lines = maximum number of independent zeros. $n$ lines means optimal (p. 23 Q7).
7. **How is a maximisation assignment problem solved?** Subtract every entry from the largest (§6).

---

## ⚡ Quick revision

- Assignment = TP with **all supplies and demands 1**, $x_{ij} \in \{0,1\}$, a square matrix.
- **Hungarian:** ① row-reduce → ② column-reduce → ③ cover zeros with the **minimum lines** → ④ lines $= n$? → ⑤ if not, **subtract the min uncovered from uncovered, add it at intersections** → ⑥ one zero per row and column → ⑦ add up the **original** costs.
- Reductions don't change the optimum because every assignment uses one cell per row and column.
- Unbalanced → **dummy (0)**. Max → **largest − $p_{ij}$**. Forbidden → **M**.
- Class answer: $C = [9\,2\,7;\, 6\,4\,3;\, 5\,8\,1]$ gives $Z_{\min} = 2 + 6 + 1 = \mathbf{9}$.

---

**Previous:** [← 14. MODI Method](14-modi-method.md) · **Next:** [16. Integer Programming →](16-integer-programming.md)
