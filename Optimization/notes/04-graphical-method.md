# 4. Graphical Method

> **Syllabus:** From the beginning — up to duality
> **Source:** `OPTIMIZATION_CLASS_NOTE-1.pdf` (pp. 14–22), `optimization__assignment_I.pdf` (Q9)

---

## 🎯 In one line

For a **two-variable** LPP: draw the constraints, find the feasible region, evaluate $Z$ at every corner point, and pick the best — this works because of the **Fundamental Extreme Point Theorem**.

---

## 1. Concept

An LPP with two decision variables can be solved by drawing. A three-variable problem *can* be drawn, but it becomes difficult to visualise — so the graphical method is used mainly for **two variables**.

The method rests on the **Fundamental Extreme Point Theorem**: *if an optimal solution exists, it occurs at one of the corner (extreme) points of the feasible region.* So we never have to test the infinitely many interior points — the corners are enough.

### Two techniques

| Technique | Idea |
|---|---|
| **1. Corner Point Method** | Evaluate $Z$ at every corner, pick the best. *(Most reliable — use this in exams.)* |
| **2. Iso-Profit / Iso-Cost Method** | Draw lines $Z = ax+by = k$ and slide them until they last touch the region. |

---

## 2. Basic idea — the 5 steps

1. Draw the graph of each constraint.
2. Determine the region satisfying **all** constraints and the non-negative restrictions. This common region is the **feasible region**.
3. Find all the corner (extreme) points of the feasible region.
4. Evaluate the objective function at each corner point.
5. Select the corner point giving the maximum (or minimum) value.

```mermaid
graph LR
    A["Replace ≤/≥<br/>with ="] --> B["Draw each line<br/>via intercepts"]
    B --> C["Shade feasible<br/>region"]
    C --> D["Find all<br/>corner points"]
    D --> E["Evaluate Z<br/>at each corner"]
    E --> F["Pick best Z"]
    style A fill:#e8eaf6,stroke:#3f51b5,color:#1a237e
    style C fill:#e0f2f1,stroke:#00897b,color:#004d40
    style F fill:#fff8e1,stroke:#f9a825,color:#e65100
```

---

## 3. Procedure in detail

**Step 1.** Replace each inequality constraint by an **equality**.

**Step 2.** Draw the corresponding straight lines together with the coordinate axes. To draw $ax + by = c$, find its intercepts by putting $x = 0$ and $y = 0$, then join the two intercepts.

$$\text{Put } x = 0 \Rightarrow y = \tfrac{c}{b} \quad\text{(y-intercept)} \qquad \text{Put } y = 0 \Rightarrow x = \tfrac{c}{a}\quad\text{(x-intercept)}$$

**Step 3.** Determine the **feasible region** — the common region satisfying all constraints together with the non-negative restrictions.

**Step 4.** Find the optimal solution by the Corner Point Method or the Iso-Profit method.

### Working rule for finding the feasible region ⭐

Consider $ax + by \le c$. Draw the line $ax + by = c$. It divides the plane into two regions. **Substitute the test point $(0,0)$** into the inequality.

- If $(0,0)$ **satisfies** the inequality → the feasible region is the side **containing the origin**.
- If $(0,0)$ **does not satisfy** it → the feasible region is the side **opposite** to the origin.

The same test works for $ax + by \ge c$.

> 💡 $(0,0)$ is the easiest test point — but only if the line does not pass through the origin. If it does, use any other convenient point such as $(1,0)$.

---

## 4. Corner Point Method

1. Determine the feasible region.
2. Find all the corner (extreme) points.
3. Compute the objective function at each corner point.
4. Select the corner giving the maximum (or minimum) value.

> ⭐ **If two adjacent corner points give the same optimal value, then every point on the line segment joining them is also optimal.** The problem then has **infinitely many optimal solutions**.

---

## 5. Iso-Profit (Iso-Cost) Method

An equation of the form

$$Z = ax + by = k \qquad (k \text{ constant})$$

is an **iso-profit line** for a maximization problem, or an **iso-cost line** for a minimization problem. Every point on such a line gives the *same* value of $Z$.

**To solve:** draw one iso-profit line for a convenient $k$, then slide it **parallel to itself**:
- **away from** the origin for maximization,
- **towards** the origin for minimization,

until it touches the feasible region at the **last** point. That point is optimal.

```
   y
   │╲    ╲    ╲     ← iso-profit lines, all parallel
   │ ╲    ╲    ╲       Z = k₁ < k₂ < k₃
   │  ╲────╲    ╲
   │  │▓▓▓▓│╲    ╲
   │  │▓▓▓▓│ ╲    ╲     slide outward →
   │  │▓▓▓▓│  ●    ╲    ● = last touch = OPTIMAL
   │  └────┘   ╲    ╲
   └──────────────────── x
      feasible region
```

---

## 6. Special cases you must be able to name ⭐

| Situation | What the graph looks like | Conclusion |
|---|---|---|
| **Unique optimum** | Iso-profit line touches exactly **one** corner | One optimal solution |
| **Multiple optima** | Iso-profit line is **parallel to a constraint edge** — two adjacent corners give the same $Z$ | Infinitely many optimal solutions along that edge |
| **Unbounded** | Feasible region extends infinitely in the improving direction | $Z$ can be increased indefinitely — **unbounded solution** |
| **Infeasible** | Constraints have **no common region** | No feasible solution exists |
| **Redundant constraint** | A constraint lies entirely outside the region formed by others | Removing it does not change the answer |

---

## 7. Worked Example 1 (Assignment Q9.1) ⭐

$$
\begin{aligned}
\text{Maximize } && Z &= 5x_1 + 7x_2 \\
\text{subject to } && x_1 + x_2 &\le 4 \\
&& 3x_1 + 8x_2 &\le 24 \\
&& 10x_1 + 7x_2 &\le 35 \\
&& x_1, x_2 &\ge 0
\end{aligned}
$$

### Step 1–2: intercepts of each line

| Constraint | Put $x_1=0$ | Put $x_2=0$ | Line through |
|---|---|---|---|
| $x_1 + x_2 = 4$ | $x_2 = 4$ | $x_1 = 4$ | $(0,4)$ and $(4,0)$ |
| $3x_1 + 8x_2 = 24$ | $x_2 = 3$ | $x_1 = 8$ | $(0,3)$ and $(8,0)$ |
| $10x_1 + 7x_2 = 35$ | $x_2 = 5$ | $x_1 = 3.5$ | $(0,5)$ and $(3.5,0)$ |

Test $(0,0)$ in each: $0 \le 4$ ✓, $0 \le 24$ ✓, $0 \le 35$ ✓ — so all three feasible regions **contain the origin**.

### Step 3: the feasible region

```
 x₂
  5 ┤●(0,5)                      ← 10x₁+7x₂=35
    │ ╲
  4 ┤●╲(0,4)                     ← x₁+x₂=4
    │▓▓╲╲
  3 ┤●▓▓▓╲╲                      ← 3x₁+8x₂=24
    │▓▓▓▓▓╲╲
 2.4┤▓▓▓▓▓▓●(1.6, 2.4)  ★ OPTIMAL
    │▓▓▓▓▓▓│╲╲
 1.67┤▓▓▓▓▓▓│ ●(2.33, 1.67)
    │▓▓▓▓▓▓│  │╲
    │▓▓▓▓▓▓│  │ ╲
  0 ┼──────┴──●───╲──────── x₁
    0     1  2  3 (3.5,0)  4
        ▓ = feasible region
```

### Step 4: corner points and $Z$ values

Corner points are found by intersecting pairs of boundary lines:

- $x_1+x_2=4$ ∩ $3x_1+8x_2=24$: substitute $x_1 = 4-x_2$ → $3(4-x_2)+8x_2=24$ → $5x_2 = 12$ → $x_2 = 2.4,\ x_1 = 1.6$.
  *Check third constraint:* $10(1.6)+7(2.4) = 32.8 \le 35$ ✓ feasible.
- $x_1+x_2=4$ ∩ $10x_1+7x_2=35$: $10(4-x_2)+7x_2=35$ → $40-3x_2=35$ → $x_2 = \tfrac53,\ x_1 = \tfrac73$.
  *Check:* $3(\tfrac73)+8(\tfrac53) = 7 + \tfrac{40}{3} \approx 20.33 \le 24$ ✓ feasible.
- $3x_1+8x_2=24$ ∩ $10x_1+7x_2=35$: gives $x_1 \approx 1.898,\ x_2 \approx 2.288$.
  *Check:* $x_1+x_2 = 4.186 > 4$ ✗ **not feasible** — reject.

| Corner point | $Z = 5x_1 + 7x_2$ |
|---|---|
| $(0,\ 0)$ | $0$ |
| $(3.5,\ 0)$ | $17.5$ |
| $\left(\tfrac73,\ \tfrac53\right) \approx (2.33,\ 1.67)$ | $\tfrac{35}{3}+\tfrac{35}{3} = \tfrac{70}{3} \approx 23.33$ |
| $(1.6,\ 2.4)$ | $8 + 16.8 = \mathbf{24.8}$ ⭐ |
| $(0,\ 3)$ | $21$ |

### ✅ Answer

$$\boxed{Z_{\max} = 24.8 \text{ at } x_1 = \tfrac{8}{5} = 1.6,\quad x_2 = \tfrac{12}{5} = 2.4}$$

> 📌 At the optimum both $x_1+x_2 \le 4$ and $3x_1+8x_2 \le 24$ are **binding** (hold with equality), while $10x_1+7x_2 = 32.8 < 35$ has slack of $2.2$.

---

## 8. Worked Example 2 (Assignment Q9.3)

$$
\begin{aligned}
\text{Maximize } && Z &= 8x_1 + 7x_2 \\
\text{subject to } && 3x_1 + x_2 &\le 66{,}000 \\
&& x_1 + x_2 &\le 45{,}000 \\
&& x_1 &\le 20{,}000 \\
&& x_2 &\le 40{,}000 \\
&& x_1, x_2 &\ge 0
\end{aligned}
$$

### Corner points

- $3x_1+x_2 = 66{,}000$ ∩ $x_1+x_2 = 45{,}000$: subtract → $2x_1 = 21{,}000$ → $x_1 = 10{,}500,\ x_2 = 34{,}500$. Both bounds satisfied ✓
- $x_1 + x_2 = 45{,}000$ ∩ $x_2 = 40{,}000$ → $(5{,}000,\ 40{,}000)$. Check $3(5000)+40000 = 55{,}000 \le 66{,}000$ ✓
- $x_1 = 20{,}000$ ∩ $3x_1+x_2 = 66{,}000$ → $x_2 = 6{,}000$ → $(20{,}000,\ 6{,}000)$ ✓
- Plus $(0,0)$, $(20{,}000, 0)$, $(0, 40{,}000)$

| Corner point | $Z = 8x_1 + 7x_2$ |
|---|---|
| $(0,\ 0)$ | $0$ |
| $(20{,}000,\ 0)$ | $160{,}000$ |
| $(20{,}000,\ 6{,}000)$ | $160{,}000 + 42{,}000 = 202{,}000$ |
| $(10{,}500,\ 34{,}500)$ | $84{,}000 + 241{,}500 = \mathbf{325{,}500}$ ⭐ |
| $(5{,}000,\ 40{,}000)$ | $40{,}000 + 280{,}000 = 320{,}000$ |
| $(0,\ 40{,}000)$ | $280{,}000$ |

### ✅ Answer

$$\boxed{Z_{\max} = 325{,}500 \text{ at } x_1 = 10{,}500,\quad x_2 = 34{,}500}$$

---

## 9. Common exam questions

1. **Solve the following LPP by the graphical method.** *(Assignment Q9 — the main one)*
2. **State the Fundamental Extreme Point Theorem.**
3. **Give three advantages of the simplex method over the graphical method.**
   - Graphical handles only **2 variables**; simplex handles **any number**.
   - Simplex is a **systematic algebraic procedure** — no drawing, no reading values off a graph, so no accuracy loss.
   - Simplex **detects unboundedness and infeasibility automatically**, and extends to duality and sensitivity analysis.
4. **When does an LPP have infinitely many optimal solutions?** → When the iso-profit line is parallel to a binding constraint edge; two adjacent corners then give the same $Z$.
5. **Explain the working rule for identifying the feasible region.** → the $(0,0)$ test.

---

## ⚡ Quick revision

- Graphical method works for **2 variables** only (3 is drawable but impractical).
- Justified by the **Fundamental Extreme Point Theorem** — optimum sits at a corner.
- **Procedure:** inequality → equality → draw via intercepts → test $(0,0)$ → shade feasible region → list corners → evaluate $Z$ → pick best.
- **$(0,0)$ test:** satisfies ⇒ region contains origin; fails ⇒ region is on the far side.
- **Corner Point Method** = evaluate at all corners. **Iso-Profit** = slide $ax+by=k$ outward (max) / inward (min).
- ⚠️ **Always verify each candidate corner against *all* constraints** — an intersection of two lines can lie outside the region (that happened in Worked Example 1).
- Two adjacent corners with equal $Z$ ⇒ **infinitely many optima** along that edge.
- Region unbounded in the improving direction ⇒ **unbounded**. No common region ⇒ **infeasible**.

---

**Previous:** [← 3. Basic Solutions & BFS](03-basic-solutions-and-bfs.md) · **Next:** [5. Standard Form, Slack & Surplus →](05-standard-form-slack-surplus.md)
