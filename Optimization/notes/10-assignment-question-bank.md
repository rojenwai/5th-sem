# 10. Assignment Question Bank — Solved

> **Why this chapter exists:** *"For the mid-term examination, **study the question pattern given in this assignment**."* — teacher, 15/09/2026
> **Source:** `optimization__assignment_I.pdf` — *Assignment: Optimization — Linear Programming Problem up to the Duality*

Every question from the assignment, with a worked answer. Theory answers are short because the detail lives in the linked chapter.

---

## Part A — Theory (short answers)

### Q1. What is a Linear Programming Problem?

A Linear Programming Problem is a problem in which we **maximize or minimize a linear objective function**, subject to a set of **linear constraints** together with non-negative restrictions on the decision variables.
→ [Ch. 1](01-introduction-to-optimization-and-lpp.md)

---

### Q2. Write down the mathematical form of a general L.P.P.

Find $x_1, x_2, \dots, x_n$ which optimize

$$Z = c_1x_1 + c_2x_2 + \cdots + c_nx_n \tag{objective function}$$

subject to

$$a_{i1}x_1 + a_{i2}x_2 + \cdots + a_{in}x_n \le (=,\ge)\ b_i, \qquad i = 1,2,\dots,m \tag{constraints}$$

$$x_1, x_2, \dots, x_n \ge 0 \tag{non-negative restrictions}$$

**Matrix form:** Optimize $Z = CX$ subject to $AX \le (=,\ge) b$, $X \ge 0$, where $A$ is the **coefficient matrix**, $C$ the **cost (price) vector**, $b$ the **requirement (resource) vector**, $X$ the **decision variable vector**.

---

### Q3. What is the relation between the optimum value of a maximization problem and a minimization problem?

$$\boxed{\min Z = -\max(-Z)}$$

That is, minimizing $Z$ is equivalent to maximizing $Z^* = -Z$. **If $Z^*_{\max} = v$, then $Z_{\min} = -v$.** This is why every minimization problem can be converted to a maximization problem before applying the simplex method.

---

### Q4. Write down the standard form of a general L.P.P.

$$\text{Maximize } Z = c^Tx \qquad \text{subject to } Ax = b, \quad x \ge 0, \quad b \ge 0$$

**Requirements of standard form:**
1. The objective function is of **maximization** type.
2. All constraints are **equations** (achieved via slack / surplus / artificial variables).
3. All variables are **non-negative**.
4. All right-hand side constants $b_i$ are **non-negative**.

→ [Ch. 5](05-standard-form-slack-surplus.md)

---

## Part B — Formulation

### Q5. Factory producing A and B (moulding / grinding / polishing)

Let $x_1, x_2$ = units of A, B produced.

$$
\begin{aligned}
\text{Maximize } && Z &= 5x_1 + 3x_2 \\
\text{s.t. } && 2x_1 + 4x_2 &\le 20 &&\text{(moulding)} \\
&& 3x_1 + 2x_2 &\le 24 &&\text{(grinding)} \\
&& 4x_1 + 2x_2 &\le 13 &&\text{(polishing)} \\
&& x_1, x_2 &\ge 0
\end{aligned}
$$

→ full working in [Ch. 2 §3](02-lpp-formulation.md)

---

### Q6. Circuit boards, and the dietician problem

> ⚠️ The assignment text runs two separate problems together here. Both are answered.

**(a) Electronics workshop.** Let $x_1$ = standard boards, $x_2$ = premium boards per week.

$$
\begin{aligned}
\text{Maximize } && Z &= 50x_1 + 60x_2 \\
\text{s.t. } && 2x_1 + x_2 &\le 120 &&\text{(machining hours)} \\
&& x_1 + 3x_2 &\le 150 &&\text{(testing hours)} \\
&& x_2 &\le 40 &&\text{(at most 40 premium boards)} \\
&& x_1, x_2 &\ge 0
\end{aligned}
$$

**(b) Dietician.** Let $x_1, x_2$ = grams of food X, Y purchased per day.

$$
\begin{aligned}
\text{Minimize } && Z &= 2x_1 + x_2 \\
\text{s.t. } && 7x_1 + 2x_2 &\ge 30 &&\text{(vitamin A)} \\
&& 5x_1 + 4x_2 &\ge 20 &&\text{(vitamin B)} \\
&& 2x_1 + 8x_2 &\ge 16 &&\text{(vitamin C)} \\
&& x_1, x_2 &\ge 0
\end{aligned}
$$

> 📌 Note the contrast: (a) is *maximize profit* → $\le$; (b) is *minimize cost with minimum requirements* → $\ge$.

---

### Q7. Firm with Grinding / Turning / Assembling / Testing

Let $x_1, x_2$ = units of A, B.

$$
\begin{aligned}
\text{Maximize } && Z &= 3x_1 + 2x_2 \\
\text{s.t. } && x_1 + 2x_2 &\le 30 &&\text{(grinding)} \\
&& 3x_1 + x_2 &\le 60 &&\text{(turning)} \\
&& 4x_1 + 3x_2 &\le 200 &&\text{(assembling)} \\
&& 5x_1 + 4x_2 &\le 200 &&\text{(testing)} \\
&& x_1, x_2 &\ge 0
\end{aligned}
$$

---

### Q8. Four metals, three commodities

> ⚠️ **Convert units first:** 1 metric ton = 1000 kg, 1 quintal = 100 kg → copper 500 kg, zinc 200 kg, manganese 200 kg.

Let $x_1, x_2, x_3$ = units of commodities A, B, C.

$$
\begin{aligned}
\text{Maximize } && Z &= 300x_1 + 200x_2 + 100x_3 \\
\text{s.t. } && 40x_1 + 70x_2 + 50x_3 &\le 1000 &&\text{(iron)} \\
&& 30x_1 + 14x_2 + 18x_3 &\le 500 &&\text{(copper)} \\
&& 7x_1 + 8x_3 &\le 200 &&\text{(zinc)} \\
&& 4x_1 + 9x_2 &\le 200 &&\text{(manganese)} \\
&& x_1,x_2,x_3 &\ge 0
\end{aligned}
$$

---

## Part C — Graphical Method

### Q9. Solve by the graphical method

**(1) & (2)** Maximize $Z = 5x_1+7x_2$ s.t. $x_1+x_2 \le 4$, $3x_1+8x_2 \le 24$, $10x_1+7x_2 \le 35$, $x_1,x_2 \ge 0$.

> 📌 Parts (1) and (2) are printed **identically** in the assignment — presumably a typo. The solution below answers both as printed.

| Corner | $Z = 5x_1+7x_2$ |
|---|---|
| $(0,0)$ | 0 |
| $(3.5,\ 0)$ | 17.5 |
| $(7/3,\ 5/3)$ | 23.33 |
| $(1.6,\ 2.4)$ | **24.8** ⭐ |
| $(0,\ 3)$ | 21 |

$$\boxed{Z_{\max} = 24.8 \text{ at } x_1 = 1.6,\ x_2 = 2.4}$$

**(3)** Maximize $Z = 8x_1+7x_2$ s.t. $3x_1+x_2 \le 66000$, $x_1+x_2 \le 45000$, $x_1 \le 20000$, $x_2 \le 40000$.

$$\boxed{Z_{\max} = 325{,}500 \text{ at } x_1 = 10{,}500,\ x_2 = 34{,}500}$$

→ full working for both in [Ch. 4 §7–8](04-graphical-method.md)

---

## Part D — Definitions

### Q10. Define each of the following

| # | Term | Definition |
|---|---|---|
| 1 | **Feasible solution** | A solution that satisfies all the constraints **and** the non-negative restrictions $x_j \ge 0$. |
| 2 | **Optimum solution** | A feasible solution that gives the **best** (max or min, as required) value of the objective function. |
| 3 | **Basic feasible solution** | A solution that is **both** a basic solution and a feasible solution — a basic solution with all variables $\ge 0$. |
| 4 | **Optimal basic feasible solution** | A BFS that gives the optimum value of the objective function among all feasible solutions. |
| 5 | **Non-degenerate BFS** | A BFS in which **all $m$ basic variables are strictly positive**. |
| 6 | **Degenerate BFS** | A BFS in which **one or more basic variables equals zero**. |

→ [Ch. 3](03-basic-solutions-and-bfs.md)

---

### Q11. Differentiate between a feasible solution and a basic feasible solution

| Feasible Solution | Basic Feasible Solution |
|---|---|
| Satisfies all constraints and $x \ge 0$ | Same, **plus** it is a basic solution |
| Can be **any** point of the feasible region | Only a **corner (extreme) point** |
| **Infinitely many** exist | **At most $\binom{n}{m}$** — finitely many |
| At most $n$ non-zero variables | **At least $n-m$ variables are zero** |
| Column vectors of non-zero variables may be linearly **dependent** | Column vectors of non-zero variables are linearly **independent** |
| The optimum need not be found here | The optimum is **guaranteed** to be among these |

---

## Part E — Basic Solutions

### Q12. Find all the basic solutions of $x_1+2x_2+x_3=4$, $2x_1+x_2+5x_3=5$, and prove they are non-degenerate

$$A = \begin{bmatrix}1&2&1\\2&1&5\end{bmatrix},\quad b = \begin{bmatrix}4\\5\end{bmatrix}, \quad m=2,\ n=3 \Rightarrow \binom{3}{2}=3 \text{ cases}$$

| Case | Basis columns | $B$ | $\det B$ | $X_B = B^{-1}b$ | Basic solution |
|---|---|---|---|---|---|
| 1 | 1, 2 | $\begin{bmatrix}1&2\\2&1\end{bmatrix}$ | $-3$ | $(2,\ 1)$ | $(2,\ 1,\ 0)$ |
| 2 | 1, 3 | $\begin{bmatrix}1&1\\2&5\end{bmatrix}$ | $3$ | $(5,\ -1)$ | $(5,\ 0,\ -1)$ |
| 3 | 2, 3 | $\begin{bmatrix}2&1\\1&5\end{bmatrix}$ | $9$ | $\left(\tfrac53,\ \tfrac23\right)$ | $\left(0,\ \tfrac53,\ \tfrac23\right)$ |

**Proof of non-degeneracy:** In each of the three cases **both basic variables are non-zero** ($2,1$; $5,-1$; $\tfrac53,\tfrac23$). Since no basic variable equals zero, **all three basic solutions are non-degenerate**. ∎

*(Of these, cases 1 and 3 are also **feasible**, so there are 2 basic feasible solutions.)*

→ full matrix working in [Ch. 3 §7](03-basic-solutions-and-bfs.md)

---

### Q13. Find all basic feasible solutions of $2x_1+6x_2+2x_3+x_4 = 3$, $6x_1+4x_2+4x_3+6x_4=2$

$$A = \begin{bmatrix}2&6&2&1\\6&4&4&6\end{bmatrix},\ b = \begin{bmatrix}3\\2\end{bmatrix},\quad m=2,\ n=4 \Rightarrow \binom42 = 6 \text{ cases}$$

| Case | Basis | $\det B$ | $X_B = B^{-1}b$ | Solution | Feasible? |
|---|---|---|---|---|---|
| 1 | $x_1,x_2$ | $-28$ | $(0,\ \tfrac12)$ | $(0,\ \tfrac12,\ 0,\ 0)$ | ✅ **BFS** (degenerate) |
| 2 | $x_1,x_3$ | $-4$ | $(-2,\ \tfrac72)$ | $(-2,\ 0,\ \tfrac72,\ 0)$ | ❌ $x_1 < 0$ |
| 3 | $x_1,x_4$ | $6$ | $(\tfrac83,\ -\tfrac73)$ | $(\tfrac83,\ 0,\ 0,\ -\tfrac73)$ | ❌ $x_4 < 0$ |
| 4 | $x_2,x_3$ | $16$ | $(\tfrac12,\ 0)$ | $(0,\ \tfrac12,\ 0,\ 0)$ | ✅ **BFS** (degenerate) |
| 5 | $x_2,x_4$ | $32$ | $(\tfrac12,\ 0)$ | $(0,\ \tfrac12,\ 0,\ 0)$ | ✅ **BFS** (degenerate) |
| 6 | $x_3,x_4$ | $8$ | $(2,\ -1)$ | $(0,\ 0,\ 2,\ -1)$ | ❌ $x_4 < 0$ |

**Sample calculation (Case 1):**
$$B = \begin{bmatrix}2&6\\6&4\end{bmatrix},\ \det = 8-36 = -28,\quad B^{-1} = \frac{1}{-28}\begin{bmatrix}4&-6\\-6&2\end{bmatrix}$$
$$X_B = \frac{1}{-28}\begin{bmatrix}4&-6\\-6&2\end{bmatrix}\begin{bmatrix}3\\2\end{bmatrix} = \frac{1}{-28}\begin{bmatrix}12-12\\-18+4\end{bmatrix} = \frac{1}{-28}\begin{bmatrix}0\\-14\end{bmatrix} = \begin{bmatrix}0\\ \tfrac12\end{bmatrix}$$

### ✅ Answer

There is exactly **one** basic feasible solution:

$$\boxed{(x_1,x_2,x_3,x_4) = \left(0,\ \tfrac12,\ 0,\ 0\right)}$$

It is **degenerate** — it is reached from three different bases (cases 1, 4, 5), and in each the second basic variable takes the value zero.

**Convex combination of the extreme points.** Since there is only **one** extreme point, the general convex combination degenerates to that single point:

$$x = \lambda_1 x^{(1)} = \left(0,\ \tfrac12,\ 0,\ 0\right), \qquad \lambda_1 = 1$$

---

### Q14. Show that $x_1=2, x_2=3, x_3=1$ is a feasible solution

**Problem:** Maximize $Z = x_1+2x_2+4x_3$ s.t. $2x_1+x_2+4x_3=11$, $3x_1+x_2+5x_3=14$, $x_j \ge 0$.

**Check constraint 1:** $2(2)+3+4(1) = 4+3+4 = 11$ ✓
**Check constraint 2:** $3(2)+3+5(1) = 6+3+5 = 14$ ✓
**Check non-negativity:** $x_1=2 \ge 0$, $x_2=3 \ge 0$, $x_3=1 \ge 0$ ✓

Hence $(2,3,1)$ **is a feasible solution**, with $Z = 2 + 6 + 4 = 12$. ∎

> ⭐ **Follow-up often asked:** *is it basic?* Here $m=2$, $n=3$, so a basic solution needs at least $n-m = 1$ variable equal to zero. All three variables are non-zero, so this is a feasible but **non-basic** solution.

---

### Q15. Reduce the feasible solution $x_1=2, x_2=4, x_3=1$ to a B.F.S.

**System:** $2x_1 - x_2 + 2x_3 = 2$, $\ x_1 + 4x_2 = 18$, $\ x_j \ge 0$.

**Step 1 — verify feasibility.** $2(2)-4+2(1) = 2$ ✓ and $2+4(4) = 18$ ✓, all $\ge 0$ ✓

**Step 2 — set up the column vectors.**

$$\alpha_1 = \begin{bmatrix}2\\1\end{bmatrix},\quad \alpha_2 = \begin{bmatrix}-1\\4\end{bmatrix},\quad \alpha_3 = \begin{bmatrix}2\\0\end{bmatrix},\quad b = \begin{bmatrix}2\\18\end{bmatrix}$$

$$2\alpha_1 + 4\alpha_2 + 1\alpha_3 = b \tag{2}$$

Three vectors in $\mathbb{R}^2$ are linearly **dependent**, so this is not a basic solution.

**Step 3 — express the dependence.** Let $\alpha_1 = a\alpha_2 + b\alpha_3$:

$$\begin{bmatrix}2\\1\end{bmatrix} = a\begin{bmatrix}-1\\4\end{bmatrix} + b\begin{bmatrix}2\\0\end{bmatrix} = \begin{bmatrix}-a+2b\\4a\end{bmatrix}$$

From the second component $4a = 1 \Rightarrow a = \tfrac14$. From the first: $-\tfrac14 + 2b = 2 \Rightarrow b = \tfrac98$.

$$\alpha_1 - \tfrac14\alpha_2 - \tfrac98\alpha_3 = 0 \tag{4}$$

so $\lambda_1 = 1$, $\lambda_2 = -\tfrac14$, $\lambda_3 = -\tfrac98$.

**Step 4 — apply the rule.**

$$\nu = \max_i\left(\frac{\lambda_i}{x_i}\right) = \max\left(\frac{1}{2},\ \frac{-1/4}{4},\ \frac{-9/8}{1}\right) = \max\left(0.5,\ -0.0625,\ -1.125\right) = \frac12 = \frac{\lambda_1}{x_1}$$

The maximum corresponds to $x_1$, so **$x_1$ is set equal to zero**.

**Step 5 — eliminate $\alpha_1$** between (2) and (4). From (4), $\alpha_1 = \tfrac14\alpha_2 + \tfrac98\alpha_3$. Substituting into (2):

$$2\left(\tfrac14\alpha_2 + \tfrac98\alpha_3\right) + 4\alpha_2 + \alpha_3 = \left(\tfrac12 + 4\right)\alpha_2 + \left(\tfrac94+1\right)\alpha_3 = \tfrac92\alpha_2 + \tfrac{13}{4}\alpha_3 = b$$

**Step 6 — verify.** The columns $\alpha_2, \alpha_3$ of the new non-zero variables:

$$\begin{vmatrix} -1 & 2 \\ 4 & 0\end{vmatrix} = 0 - 8 = -8 \ne 0 \quad\Rightarrow\quad \text{linearly independent} \ \checkmark$$

### ✅ Answer

$$\boxed{x_1 = 0,\qquad x_2 = \tfrac92,\qquad x_3 = \tfrac{13}{4}}$$

**Check:** $2(0) - \tfrac92 + 2\left(\tfrac{13}{4}\right) = -4.5 + 6.5 = 2$ ✓ · $0 + 4\left(\tfrac92\right) = 18$ ✓ · both $\ge 0$ ✓

---

## Part F — Simplex Theory

### Q16. Give three advantages of the simplex method over the graphical method

1. **Any number of variables.** The graphical method is restricted to **two** decision variables (three is drawable but impractical); the simplex method handles **any** number.
2. **Systematic algebraic procedure.** No drawing and no reading values off a graph, so there is no loss of accuracy — the result is exact.
3. **Automatic detection of special cases.** The simplex table reveals **unboundedness** ($\Delta_k>0$ but all $y_{ik}\le0$), **infeasibility** (positive artificial variable at the optimum) and **alternative optima** (non-basic $\Delta_j=0$) without any extra work. It also extends naturally to duality and sensitivity analysis.

---

### Q17. Define slack variable and surplus variable

| | **Slack variable** | **Surplus variable** |
|---|---|---|
| Constraint | $a^Tx \le b$ | $a^Tx \ge b$ |
| Operation | **Added**: $a^Tx + s = b$ | **Subtracted**: $a^Tx - s = b$ |
| Meaning | **Unused capacity** | Amount **above a minimum requirement** |
| Sign | $s \ge 0$ | $s \ge 0$ |
| Gives a unit column? | ✅ Yes — usable as an initial basic variable | ❌ No — its column is $-1$ |

---

### Q18. When are artificial variables introduced in an LPP?

Artificial variables are introduced when a constraint **does not supply a convenient basic unit column**, i.e. for:

- **$\ge$ constraints:** after subtracting a surplus variable, the column is $-1$. Setting the other variables to zero gives $s = -b < 0$, violating $s \ge 0$. So we add $A_i$: $\ a^Tx - s_i + A_i = b_i$.
- **$=$ constraints:** neither slack nor surplus exists, so no basic column is produced at all. Add $A_i$: $\ a^Tx + A_i = b_i$.

Their **only** purpose is to construct an initial basis; they have no physical meaning and must be driven to zero via the **Big-M** or **Two-Phase** method. If an artificial variable remains **positive** in the final solution, the LPP is **infeasible**.

→ [Ch. 7](07-big-m-and-two-phase.md)

---

### Q19. State the fundamental theorem of LPP

> **Fundamental Theorem of Linear Programming.** If an L.P.P. has an optimal feasible solution, then **at least one Basic Feasible Solution is optimal**.

**Related — Fundamental Extreme Point Theorem:** if an optimal solution of an LPP exists, then at least one optimal solution occurs at an **extreme point (corner point)** of the feasible region.

**Significance:** it is enough to search among the finitely many basic feasible solutions instead of the infinitely many feasible solutions — this is what makes the simplex method possible.

---

### Q20. Give the computational procedure for the simplex method

| Step | Procedure |
|---|---|
| 1 | Convert minimization to maximization using $Z^* = -Z$ if necessary. |
| 2 | Make every $b_i \ge 0$ (multiply a negative row by $-1$ and reverse the inequality). |
| 3 | Convert every constraint into an equation using slack, surplus and, when needed, artificial variables. |
| 4 | Find an initial basis and calculate $x_B = B^{-1}b$. If artificial variables occur, use Two-Phase or Big-M. |
| 5 | Construct the simplex table; calculate $Y_j$, $Z$ and every $\Delta_j = c_j - c_B^TY_j$. |
| 6 | **Optimality test:** if all $\Delta_j \le 0$, the current B.F.S. is optimal. |
| 7 | If some $\Delta_j > 0$, choose the column with the **largest positive** $\Delta_j$ as the entering column. |
| 8 | Choose the leaving row by the **minimum positive-ratio test** and pivot. |
| 9 | Recalculate reduced costs; repeat 6–8 until optimal, unbounded or infeasible. |

→ [Ch. 6](06-simplex-method.md)

---

## Part G — Duality

### Q21. Differentiate between a primal problem and its dual

| **Primal** | **Dual** |
|---|---|
| The original problem | The associated problem derived from it |
| Maximize $Z_P = c^Tx$ | Minimize $Z_D = b^Tw$ |
| $Ax \le b$, $x \ge 0$ | $A^Tw \ge c$, $w \ge 0$ |
| $m$ constraints, $n$ variables | $n$ constraints, $m$ variables |
| Coefficient matrix $A$ | Coefficient matrix $A^T$ |
| Asks: *how much of each product to produce?* | Asks: *what value to assign to each resource?* |
| Variables = activity levels | Variables = **shadow prices** of resources |

At optimality $Z_P^* = Z_D^*$ (Strong Duality), and **the dual of the dual is the primal**.

---

### Q22. Define primal and dual. Give an example of a primal and write its dual

**Definitions.** Every LPP (the **primal**) is associated with another LPP called its **dual**. They are two ways of viewing the same optimization problem.

**Example — primal:**

$$\text{Maximize } Z_P = 3x_1+2x_2 \quad\text{s.t.}\quad x_1+x_2 \le 4,\quad 2x_1+x_2 \le 6,\quad x_1,x_2 \ge 0$$

**Its dual** (two constraints → two dual variables $w_1, w_2$):

$$\text{Minimize } Z_D = 4w_1+6w_2 \quad\text{s.t.}\quad w_1+2w_2 \ge 3,\quad w_1+w_2 \ge 2,\quad w_1,w_2 \ge 0$$

→ full derivation in [Ch. 9 §2](09-duality.md)

---

### Q23. Write the dual of: Minimize $Z = 3x_1+x_2$, s.t. $2x_1+3x_2 \ge 2$, $x_1+x_2 \ge 1$, $x_1,x_2 \ge 0$

Already in standard minimization form (all $\ge$). $A^T = \begin{bmatrix}2&1\\3&1\end{bmatrix}$.

$$
\begin{aligned}
\text{Maximize } && Z_D &= 2w_1 + w_2 \\
\text{s.t. } && 2w_1 + w_2 &\le 3 \\
&& 3w_1 + w_2 &\le 1 \\
&& w_1, w_2 &\ge 0
\end{aligned}
$$

---

### Q24. Write the dual of: Minimize $Z = 2x_2+5x_3$, s.t. $x_1+x_2 \ge 2$, $2x_1+x_2+6x_3 \le 6$, $x_1-x_2+3x_3 = 4$, $x_j \ge 0$

Convert to standard minimization form (all $\ge$): keep the first; multiply the second by $-1$; split the equality into two opposite inequalities. Then take the dual and set $w_3 = w_3' - w_3''$.

$$
\begin{aligned}
\text{Maximize } && Z_D &= 2w_1 - 6w_2 - 4w_3 \\
\text{s.t. } && w_1 - 2w_2 - w_3 &\le 0 \\
&& w_1 - w_2 + w_3 &\le 2 \\
&& -6w_2 - 3w_3 &\le 5 \\
&& w_1, w_2 &\ge 0,\qquad w_3 \text{ unrestricted in sign}
\end{aligned}
$$

→ full working in [Ch. 9 §7](09-duality.md)

---

### Q25. Give the dual of: Maximize $Z = 2x_1+3x_2+x_3$, s.t. $4x_1+3x_2+x_3 = 6$, $x_1+2x_2+5x_3 = 4$, $x_j \ge 0$

Two **equality** constraints → two dual variables, both **unrestricted in sign**.

$$
\begin{aligned}
\text{Minimize } && Z_D &= 6w_1 + 4w_2 \\
\text{s.t. } && 4w_1 + w_2 &\ge 2 \\
&& 3w_1 + 2w_2 &\ge 3 \\
&& w_1 + 5w_2 &\ge 1 \\
&& w_1, w_2 &\ \text{unrestricted in sign}
\end{aligned}
$$

---

### Q26. Find the dual of: Minimize $Z = x_1+x_2+x_3$, s.t. $x_1-3x_2+4x_3=5$, $x_1-2x_2 \le 3$, $2x_2-x_3 \ge 4$, $x_1,x_2 \ge 0$, $x_3$ unrestricted

**Step 1.** Replace the unrestricted $x_3 = x_3' - x_3''$, $x_3',x_3'' \ge 0$.
**Step 2.** Convert to standard minimization form (all $\ge$): split the equality into two, and flip $x_1-2x_2\le3$ to $-x_1+2x_2 \ge -3$.
**Step 3.** Take the dual and recombine $w_1 = w_1' - w_1''$ (unrestricted, coming from the primal equality).

$$
\begin{aligned}
\text{Maximize } && Z_D &= 5w_1 - 3w_2 + 4w_3 \\
\text{s.t. } && w_1 - w_2 &\le 1 \\
&& -3w_1 + 2w_2 + 2w_3 &\le 1 \\
&& 4w_1 - w_3 &= 1 \\
&& w_2, w_3 &\ge 0,\qquad w_1 \text{ unrestricted in sign}
\end{aligned}
$$

> ⭐ **The mirror rule at work:** the primal **equality** → unrestricted dual variable $w_1$; the primal **unrestricted variable** $x_3$ → dual **equality** constraint.

---

## ⚡ Question-pattern summary

What the assignment tells you about the exam:

| Pattern | Count | Where |
|---|---|---|
| **Short theory / definitions** | 8 | Q1–Q4, Q10, Q11, Q16–Q19, Q21 |
| **Formulation of an LPP** | 4 | Q5–Q8 |
| **Graphical method** | 3 | Q9 |
| **Basic solutions / BFS computation** | 4 | Q12–Q15 |
| **Writing the dual** | 4 | Q23–Q26 |

> 🎯 **Biggest scoring blocks:** definitions, formulation, and writing duals. All three are pure routine — practise the format and they are guaranteed marks. The graphical and basic-solution questions need care with arithmetic but follow a fixed template.

---

**Previous:** [← 9. Duality](09-duality.md) · **Back to:** [Optimization index](../README.md)
