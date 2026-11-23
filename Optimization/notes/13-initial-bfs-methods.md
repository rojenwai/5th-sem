# 13. Finding the Initial Basic Feasible Solution (IBFS)

> **Syllabus:** After-mid. *Transportation problem: initial basic feasible solution*
> **Source:** Transportation class notes pp. 6, 8–9, 11, 13–14

---

## 🎯 In one line

All five methods fill the table cell by cell with $x_{ij} = \min(a_i, b_j)$ and then cross off the exhausted row or column. They differ only in **which cell they pick next**. **VAM** looks at the *penalty* for not using the cheapest cell, so it gives the best start.

---

## 1. The five methods (p. 8)

| # | Method | Picks the next cell by… | Looks at cost? |
|---|---|---|---|
| 1 | **North-West Corner Rule (NWCR)** | Position: top-left of what remains | ❌ No |
| 2 | **Row-minima** | Cheapest cell **in the current row** | Row only |
| 3 | **Column-minima** | Cheapest cell **in the current column** | Column only |
| 4 | **Matrix-minima / Least Cost Method (LCM)** | Cheapest cell **in the whole remaining table** | ✅ Yes |
| 5 | **Vogel's Approximation Method (VAM)** ⭐ | Cheapest cell in the row/column with the **largest penalty** | ✅✅ Yes, plus the *second* cheapest |

> **Why VAM is best (p. 6):** *"VAM takes into account not only the least cost $c_{ij}$ but also the costs that just exceed the least cost $c_{ij}$, and therefore yields a better initial solution than obtained from other methods."*

**Common allocation rule for every method:** allocate $x_{ij} = \min\{a_i, b_j\}$, subtract it from both rim values, and cross off the row (supply = 0) or column (demand = 0).

> If a row **and** a column are exhausted by the same allocation, cross off only one of them and leave a **0** in the other (or add $\varepsilon$ later). Otherwise the solution will have fewer than $m+n-1$ allocations, which makes it **degenerate**.

---

## 2. The running example (class Problem, p. 13)

| | A | B | C | D | Supply |
|---|---|---|---|---|---|
| **I** | 21 | 16 | 25 | 13 | 11 |
| **II** | 17 | 18 | 14 | 23 | 13 |
| **III** | 32 | 27 | 18 | 41 | 19 |
| **Demand** | 6 | 10 | 12 | 15 | **43** |

Total supply $= 43 =$ total demand, so the problem is **balanced**. $m+n-1 = 3+4-1 = 6$.

---

## 3. North-West Corner Rule (p. 8, p. 11)

**Steps:**
1. Start from the **top-left** cell.
2. Allocate the minimum of the available supply and the required demand.
3. If the destination's demand is satisfied, **move right**.
4. If the source's supply is exhausted, **move down**.
5. Continue until all supply and demand requirements are satisfied.

**On the example:**

| Step | Cell | Allocation | Remaining |
|---|---|---|---|
| 1 | (I, A) | $\min(11, 6) = 6$ | A done; I has 5 → move right |
| 2 | (I, B) | $\min(5, 10) = 5$ | I done; B needs 5 → move down |
| 3 | (II, B) | $\min(13, 5) = 5$ | B done; II has 8 → move right |
| 4 | (II, C) | $\min(8, 12) = 8$ | II done; C needs 4 → move down |
| 5 | (III, C) | $\min(19, 4) = 4$ | C done; III has 15 → move right |
| 6 | (III, D) | $\min(15, 15) = 15$ | all done |

$$Z_{NWCR} = 6(21) + 5(16) + 5(18) + 8(14) + 4(18) + 15(41) = 126 + 80 + 90 + 112 + 72 + 615 = \mathbf{1095}$$

6 allocations $= m+n-1$, so the solution is **non-degenerate**. It is a poor start, though, because the 41-cost cell got 15 units.

---

## 4. Row-minima method (p. 8, p. 11)

**Steps:**
1. Start with the **first row**.
2. Find the cell with the **minimum cost in that row** among destinations with remaining demand.
3. Allocate the maximum possible quantity.
4. If the source still has supply, choose the **next** minimum-cost cell in the **same row**.
5. When the source's supply is exhausted, **move to the next row**.
6. Continue until all supplies and demands are satisfied.

**On the example:**

| Row | Allocations (cheapest first) |
|---|---|
| I | (I, D) $c=13$: $\min(11,15) = 11$. Row I done |
| II | (II, C) $c=14$: $\min(13,12) = 12$. C done. Then (II, A) $c=17$: $\min(1,6) = 1$. Row II done |
| III | (III, B) $c=27$: 10. (III, A) $c=32$: 5. (III, D) $c=41$: 4 |

$$Z = 11(13) + 12(14) + 1(17) + 10(27) + 5(32) + 4(41) = \mathbf{922}$$

---

## 5. Column-minima method

This is the same idea **column by column**: in the first column pick the cheapest cell, allocate, and move to the next column once that column's demand is met.

| Column | Allocations |
|---|---|
| A | (II, A) $c=17$: 6 |
| B | (I, B) $c=16$: 10 (I has 1 left) |
| C | (II, C) $c=14$: 7 (II done). Then (III, C) $c=18$: 5 |
| D | (I, D) $c=13$: 1. Then (III, D) $c=41$: 14 |

$$Z = 6(17) + 10(16) + 7(14) + 5(18) + 1(13) + 14(41) = \mathbf{1037}$$

---

## 6. Matrix-minima / Least Cost Method (LCM)

**Steps:** pick the **cheapest cell in the entire remaining table** (break ties by the larger possible allocation), allocate, cross off, and repeat.

| Order | Cell | $c_{ij}$ | Allocation |
|---|---|---|---|
| 1 | (I, D) | 13 | 11 → row I done |
| 2 | (II, C) | 14 | 12 → column C done |
| 3 | (II, A) | 17 | 1 → row II done |
| 4 | (III, B) | 27 | 10 |
| 5 | (III, A) | 32 | 5 |
| 6 | (III, D) | 41 | 4 |

$$Z_{LCM} = \mathbf{922}$$

*(The order happens to match row-minima here. In general they differ.)*

---

## 7. Vogel's Approximation Method (VAM) ⭐⭐⭐

### Steps (p. 6, p. 9, p. 11)

1. **Check** whether the problem is balanced. If not, add a **dummy** source or destination.
2. **Calculate row and column penalties:**
   $$\boxed{\text{Penalty} = \text{second-smallest cost} - \text{smallest cost}}$$
   Write row penalties in brackets to the right of each row and column penalties below each column.
3. **Identify** the row or column with the **maximum penalty**.
4. **Allocate:** in that row or column, choose the cell with the **minimum cost** and allocate $x_{ij} = \min\{a_i, b_j\}$. *In case of a tie (equal penalties), allocate to the cell associated with the lower cost.*
5. **Update** supply and demand. If a source's supply becomes 0, remove that row. If a destination's demand becomes 0, remove that column.
6. **Recalculate** the penalties for the reduced table.
7. **Repeat** steps 3–6 until all rim requirements are satisfied.
8. **Verify** the BFS: the number of allocations should be $m+n-1$.

### VAM on the example (exactly as in the class notes, pp. 13–14)

**Table 1.** Penalties: rows I: $16-13 = 3$, II: $17-14 = 3$, III: $27-18 = 9$. Columns A: $21-17 = 4$, B: $18-16 = 2$, C: $18-14 = 4$, **D: $23-13 = 10$**.

```
            A     B     C     D      supply (pen)
   I       21    16    25   [11]13    11  (3)
   II      17    18    14    23       13  (3)
   III     32    27    18    41       19  (9)
  demand    6    10    12    15
  (pen)    (4)   (2)   (4)  (10) ← largest
```

The largest penalty is 10 (column D). Its cheapest cell is $c_{14} = 13$, so $x_{14} = \min\{11, 15\} = \mathbf{11}$. **Row I is crossed off.**

**Table 2.** Remaining rows II, III and columns A–D (D now needs 4). Penalties: rows II: 3, III: 9. Columns A: $32-17 = 15$, B: $27-18 = 9$, C: $18-14 = 4$, **D: $41-23 = 18$**. The largest is 18 (column D), cheapest cell $c_{24} = 23$, so $x_{24} = \min\{13, 4\} = \mathbf{4}$. **Column D is crossed off.**

**Table 3.** Rows II (9 left), III (19). Columns A, B, C. Penalties: rows II: $17-14 = 3$, III: $27-18 = 9$. Columns **A: $32-17 = 15$**, B: 9, C: 4. The largest is 15 (column A), cheapest cell $c_{21} = 17$, so $x_{21} = \min\{9, 6\} = \mathbf{6}$. **Column A is crossed off.**

**Table 4.** Rows II (3 left), III (19). Columns B (10), C (12). Penalties: rows II: $18-14 = 4$, III: $27-18 = 9$. Columns B: $27-18 = 9$, C: $18-14 = 4$. There is a **tie at 9** (row III and column B). The notes pick column B, whose cheapest cell is $c_{22} = 18$, so $x_{22} = \min\{3, 10\} = \mathbf{3}$. **Row II is crossed off.**

**Table 5.** Only row III remains: $x_{32} = \mathbf{7}$ and $x_{33} = \mathbf{12}$.

> Choosing row III at the tie instead ($x_{33} = 12$ first) ends with the **same** final allocation here.

**Final IBFS (Table 6):**

| | A | B | C | D | Supply |
|---|---|---|---|---|---|
| **I** | 21 | 16 | 25 | **[11]** 13 | 11 |
| **II** | **[6]** 17 | **[3]** 18 | 14 | **[4]** 23 | 13 |
| **III** | 32 | **[7]** 27 | **[12]** 18 | 41 | 19 |
| **Demand** | 6 | 10 | 12 | 15 | |

$$x_{14}=11,\; x_{21}=6,\; x_{22}=3,\; x_{24}=4,\; x_{32}=7,\; x_{33}=12$$
$$Z_{VAM} = 11(13) + 6(17) + 3(18) + 4(23) + 7(27) + 12(18) = 143 + 102 + 54 + 92 + 189 + 216 = \mathbf{796}$$

6 allocations $= m+n-1$, so the IBFS is **non-degenerate**. MODI ([Ch. 14](14-modi-method.md)) shows that **796 is already optimal**.

---

## 8. Comparison on the same problem ⭐

| Method | Initial cost | Distance from optimum (796) |
|---|---|---|
| NWCR | 1095 | +299 |
| Column-minima | 1037 | +241 |
| Row-minima | 922 | +126 |
| LCM | 922 | +126 |
| **VAM** | **796** | **0 (already optimal)** |

The same pattern holds for the 3×5 homework problem on p. 18: **NWCR 153 → LCM 78 → VAM 68**, with true optimum **67** (see [Ch. 17](17-transportation-assignment-ip-question-bank.md)).

> **Does VAM always give the optimum?** **No.** It usually lands close, but the 3×5 problem (VAM 68, optimum 67) and the cement problem (VAM ₹10,200, optimum ₹10,000) both need MODI iterations. That is a homework question on p. 18 and p. 23.

---

## 9. Common exam questions

1. **Find the IBFS by NWCR / LCM / VAM** and compare the costs. This is the core numerical (§3–§8).
2. **Explain VAM. Why does it give a better IBFS?** It uses the penalty, the regret of not using the cheapest cell (§7).
3. **What is a penalty in VAM?** It is the second-smallest cost minus the smallest cost in a row or column.
4. **How are ties handled in VAM?** Allocate to the cell with the lower cost.
5. **Does VAM always produce an optimal solution?** No (§8).
6. **What should you check after the IBFS?** That the number of allocations $= m+n-1$, i.e. non-degeneracy.

---

## ⚡ Quick revision

- Every method: $x_{ij} = \min(a_i, b_j)$, then cross off the exhausted line.
- **NWCR:** top-left; move **right** when demand is met and **down** when supply runs out. It ignores cost.
- **Row-/Column-minima:** cheapest cell in the current row or column.
- **LCM:** cheapest cell in the whole table.
- **VAM:** **penalty = 2nd smallest − smallest**. Take the **largest penalty**, allocate to its **cheapest cell**, break ties by the lower cost, and recompute the penalties every round.
- Class answers: **NWCR 1095 · LCM 922 · VAM 796** (optimal).
- Always check **allocations = $m+n-1$** before MODI.

---

**Previous:** [← 12. Transportation Problem](12-transportation-problem.md) · **Next:** [14. MODI Method →](14-modi-method.md)
