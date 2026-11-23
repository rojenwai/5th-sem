# 20. Karush–Kuhn–Tucker (KKT) Conditions (Inequality Constraints)

> ⚠️ **Written from standard course knowledge.** No class notes for this topic yet. The scope follows [`source/aftermid-syllabus.txt`](../source/aftermid-syllabus.txt) §4. All examples were verified by computer (symbolic solve + numerical optimizer).
> **Syllabus:** *Why we need KKT: the constrained vs unconstrained minimizer · feasible points, active vs inactive constraints · the four KKT conditions: stationarity, primal feasibility, dual feasibility, complementary slackness · step-by-step procedure, worked problems and a homework set*

---

## 🎯 In one line

KKT extends Lagrange to **inequality** constraints. At the optimum, $-\nabla f$ is a **non-negative** combination of the gradients of the **active** constraints, and every **inactive** constraint gets multiplier **zero** (complementary slackness).

---

## 1. Why we need KKT: constrained vs unconstrained minimiser ⭐

**1-D illustration.** Minimise $f(x) = (x - 3)^2$.

| Constraint | Unconstrained minimiser $x = 3$ | Constrained minimiser | $f'$ there | Constraint status |
|---|---|---|---|---|
| $x \le 5$ | feasible ✔ | $x^* = 3$ | $0$ | **Inactive** (slack) |
| $x \le 2$ | **infeasible** ✘ | $x^* = 2$ (the boundary) | $-2 \ne 0$ | **Active** (binding) |

In the second case $f'(x^*) \ne 0$, so "set the derivative to zero" **fails**. The minimum is pushed onto the boundary, where the objective still wants to go further (downhill is to the right) but the constraint stops it. KKT captures this balance: $f'(x^*) + \mu\, g'(x^*) = 0$, i.e. $-2 + \mu(1) = 0$, so $\mu = 2 \ge 0$.

**Lagrange** handles only **equalities** ([Ch. 19](19-lagrange-multipliers.md)). **KKT** handles $\le$ constraints, which may or may not be binding at the optimum.

---

## 2. Standard form and vocabulary

$$\text{Minimise } f(\mathbf x) \quad \text{s.t.} \quad g_i(\mathbf x) \le 0 \;\; (i = 1..m), \qquad h_j(\mathbf x) = 0 \;\; (j = 1..p)$$

> Convert first: $\max f \to \min(-f)$. $\;g(\mathbf x) \ge b \to b - g(\mathbf x) \le 0$. $\;g(\mathbf x) \le b \to g(\mathbf x) - b \le 0$.

| Term | Meaning |
|---|---|
| **Feasible point** | Satisfies every $g_i \le 0$ and $h_j = 0$ |
| **Active (binding) constraint** at $\mathbf x$ | $g_i(\mathbf x) = 0$: the point lies **on** that boundary |
| **Inactive constraint** at $\mathbf x$ | $g_i(\mathbf x) < 0$: there is slack, so it has no local effect |
| **Active set** $\mathcal A(\mathbf x)$ | The indices of the active inequalities (equalities are always active) |

**Lagrangian:**
$$\boxed{L(\mathbf x, \boldsymbol\mu, \boldsymbol\lambda) = f(\mathbf x) + \sum_{i=1}^{m} \mu_i\, g_i(\mathbf x) + \sum_{j=1}^{p} \lambda_j\, h_j(\mathbf x)}$$

---

## 3. The four KKT conditions ⭐⭐⭐

| # | Name | Condition | Meaning |
|---|---|---|---|
| 1 | **Stationarity** | $\nabla f(\mathbf x^*) + \sum_i \mu_i \nabla g_i(\mathbf x^*) + \sum_j \lambda_j \nabla h_j(\mathbf x^*) = \mathbf 0$ | Forces balance: $-\nabla f$ is a combination of the constraint normals |
| 2 | **Primal feasibility** | $g_i(\mathbf x^*) \le 0$, $\;h_j(\mathbf x^*) = 0$ | The point is feasible |
| 3 | **Dual feasibility** | $\mu_i \ge 0$ | Constraints can only **push**, never pull |
| 4 | **Complementary slackness** | $\mu_i\, g_i(\mathbf x^*) = 0$ for every $i$ | Either the constraint is active ($g_i = 0$) or its multiplier is zero ($\mu_i = 0$) |

($\lambda_j$ for equality constraints is **unrestricted in sign**, as in Lagrange.)

**Geometric picture (minimisation).** At $\mathbf x^*$ the descent direction $-\nabla f$ must point **out of** the feasible region. It must lie inside the cone spanned by the outward normals $\nabla g_i$ of the **active** constraints. If it pointed anywhere else, you could move a little and still decrease $f$.

```
         feasible region
        ┌────────────────┐
        │                │  g₁ ≤ 0 boundary
        │            x* ●│──► ∇g₁   (outward normal)
        │                │──► −∇f = μ₁∇g₁ ,  μ₁ ≥ 0
        └────────────────┘
```

> **Regularity (constraint qualification).** KKT conditions are **necessary** at a local minimum if the active constraint gradients are linearly independent (LICQ), or if all constraints are linear, or if Slater's condition holds for a convex problem. They are **sufficient** when the problem is **convex** (see [Ch. 21 §8](21-convex-optimization.md)).

---

## 4. Step-by-step procedure for KKT problems ⭐⭐

1. **Standardise:** min form, every inequality as $g_i \le 0$.
2. **Write the Lagrangian** and the four conditions.
3. **Case analysis on the active set.** Each inequality is either active ($g_i = 0$) or inactive ($\mu_i = 0$). With $m$ inequalities there are $2^m$ cases. Usually start with "none active" (the unconstrained optimum).
4. For each case solve the stationarity equations plus the active constraints.
5. **Reject** a case if it violates primal feasibility (some $g_i > 0$) or dual feasibility (some $\mu_i < 0$).
6. The surviving points are the **KKT points**. Compare $f$ values. If the problem is convex, any KKT point is the **global** minimum.

---

## 5. Worked problems

### Example 1: one active constraint ⭐

$$\min\ f = (x-2)^2 + (y-1)^2 \quad \text{s.t.} \quad g = x + y - 2 \le 0$$

$L = (x-2)^2 + (y-1)^2 + \mu(x + y - 2)$. Stationarity gives $2(x-2) + \mu = 0$ and $2(y-1) + \mu = 0$.

- **Case A ($\mu = 0$, inactive):** $(x,y) = (2,1)$. Then $g = 2 + 1 - 2 = 1 > 0$, which is **infeasible**, so reject it.
- **Case B (active, $x + y = 2$):** $x = 2 - \mu/2$ and $y = 1 - \mu/2$, so $3 - \mu = 2$, giving $\mu = 1 \ge 0$ ✔ and $(x,y) = (1.5, 0.5)$.

**KKT point:** $(1.5, 0.5)$ with $\mu = 1$ and $f = 0.25 + 0.25 = 0.5$. The objective is a convex bowl and the constraint is linear, so this is the **global minimum**. It is the point of the half-plane nearest $(2,1)$.

### Example 2: a "≥" constraint

$$\min\ x^2 + y^2 \quad \text{s.t.} \quad x + y \ge 4 \;\;\Longrightarrow\;\; g = 4 - x - y \le 0$$

Stationarity: $2x - \mu = 0$ and $2y - \mu = 0$.
- $\mu = 0$ gives $(0,0)$, but $g = 4 > 0$, so it is infeasible.
- Active: $x = y = \mu/2$ with $x + y = 4$, so $\mu = 4 \ge 0$ ✔.

**Answer:** $(2,2)$, $f = 8$, $\mu = 4$.

### Example 3: a maximisation problem

$$\max\ 8x + 10y - x^2 - y^2 \quad \text{s.t.} \quad 3x + 2y \le 6,\;\; x, y \ge 0$$

Minimise $F = -8x - 10y + x^2 + y^2$ with $g_1 = 3x + 2y - 6 \le 0$, $g_2 = -x \le 0$ and $g_3 = -y \le 0$.

- **Unconstrained:** $(4, 5)$, but $3(4) + 2(5) = 22 > 6$, which is infeasible.
- **$g_1$ active, $x, y > 0$** (so $\mu_2 = \mu_3 = 0$):
  $$-8 + 2x + 3\mu_1 = 0, \qquad -10 + 2y + 2\mu_1 = 0, \qquad 3x + 2y = 6$$
  This gives $x = 4 - 1.5\mu_1$ and $y = 5 - \mu_1$, so $12 - 4.5\mu_1 + 10 - 2\mu_1 = 6$, i.e. $\mu_1 = \frac{32}{13} \ge 0$ ✔.
  $$x = \tfrac{4}{13} \approx 0.31, \qquad y = \tfrac{33}{13} \approx 2.54 \qquad (\text{both } > 0 \;✔)$$

**Answer:** $\max = \frac{277}{13} \approx 21.31$ at $(\frac{4}{13}, \frac{33}{13})$.

### Example 4: two inequality constraints, full case analysis ⭐⭐⭐

$$\min\ f = (x-3)^2 + (y-2)^2 \quad \text{s.t.} \quad g_1 = x^2 + y^2 - 5 \le 0, \qquad g_2 = x + 2y - 4 \le 0$$

Stationarity:
$$2(x-3) + 2\mu_1 x + \mu_2 = 0, \qquad 2(y-2) + 2\mu_1 y + 2\mu_2 = 0$$

| Case | Active | Solution | Check | Verdict |
|---|---|---|---|---|
| 1 | none ($\mu_1 = \mu_2 = 0$) | $(3, 2)$ | $g_1 = 8 > 0$ | ✘ infeasible |
| 2 | $g_1$ only ($\mu_2 = 0$) | $(\frac{3\sqrt{65}}{13}, \frac{2\sqrt{65}}{13}) \approx (1.86, 1.24)$ | $g_2 = 0.34 > 0$ | ✘ infeasible |
| 3 | $g_2$ only ($\mu_1 = 0$) | $(2.4, 0.8)$, $\mu_2 = 1.2$ | $g_1 = 1.4 > 0$ | ✘ infeasible |
| 4 | both | $x = 4 - 2y$ on the circle gives $5y^2 - 16y + 11 = 0$, so $y = 1$ or $\frac{11}{5}$ | see below | |

**Case 4a: $(2, 1)$.** $\nabla f = (-2, -2)$, $\nabla g_1 = (4, 2)$, $\nabla g_2 = (1, 2)$:
$$-2 + 4\mu_1 + \mu_2 = 0, \qquad -2 + 2\mu_1 + 2\mu_2 = 0 \;\Rightarrow\; \mu_1 = \tfrac13, \;\mu_2 = \tfrac23 \;\ge 0 \;✔$$

**Case 4b: $(-0.4, 2.2)$.** Solving gives $\mu_1 = -\frac73 < 0$, which **violates dual feasibility**, so reject it.

**Unique KKT point:** $(2, 1)$ with $f = 1 + 1 = \mathbf 2$. The problem is **convex** (a convex objective, a convex disc and a half-plane), so this is the **global minimum**. A numerical optimizer gives the same answer.

---

## 6. Homework set (with answers to check yourself)

| # | Problem | KKT point | Multiplier | Optimal value |
|---|---|---|---|---|
| H1 | $\min x^2 + y^2$ s.t. $x + y \ge 1$ | $(\frac12, \frac12)$ | $\mu = 1$ | $\frac12$ |
| H2 | $\min (x-1)^2 + (y-2)^2$ s.t. $x + y \le 1$ | $(0, 1)$ | $\mu = 2$ | $2$ |
| H3 | $\max xy$ s.t. $x + y \le 8$, $x, y \ge 0$ | $(4, 4)$ | $\mu = 4$ | $16$ |
| H4 | $\min x^2 - 4x$ s.t. $x \le 1$ | $x = 1$ (active) | $\mu = 2$ | $-3$ |
| H5 | $\min (x-3)^2$ s.t. $x \le 5$ | $x = 3$ (inactive) | $\mu = 0$ | $0$ |

> In H3, $\max xy$ is **not** a concave objective, but on this feasible set the KKT point (4,4) is still the global max: check the boundary $x + y = 8$, where $xy = x(8 - x)$ peaks at 16.

---

## 7. KKT ↔ Lagrange ↔ LP duality

| | Lagrange | KKT | LP duality |
|---|---|---|---|
| Constraints | $=$ only | $\le$ and $=$ | linear $\le$ |
| Multiplier sign | any | $\mu \ge 0$ for $\le$ | dual variables $\ge 0$ |
| Extra condition | – | **complementary slackness** | **complementary slackness** ([Ch. 9](09-duality.md)) |
| Meaning of the multiplier | shadow price | shadow price of the active constraint | shadow price |

---

## 8. Common exam questions

1. **Why do we need KKT conditions?** Use the constrained vs unconstrained minimiser of §1.
2. **Define feasible point, active and inactive constraints.** See §2.
3. **State the KKT conditions.** Give the four in §3, with their names.
4. **Explain complementary slackness.** $\mu_i g_i = 0$: slack ⇒ zero multiplier, positive multiplier ⇒ binding.
5. **Solve using KKT conditions.** Use Examples 1–4 with case analysis.
6. **Are KKT conditions necessary or sufficient?** Necessary under a constraint qualification, and sufficient for convex problems.

---

## ⚡ Quick revision

- Standardise: **min**, $g_i \le 0$.
- $L = f + \sum\mu_i g_i + \sum\lambda_j h_j$.
- **KKT:** ① $\nabla_x L = 0$ ② $g \le 0$, $h = 0$ ③ $\mu \ge 0$ ④ $\mu_i g_i = 0$.
- **Active** $g_i = 0$ (μ may be > 0). **Inactive** $g_i < 0$ ⇒ $\mu_i = 0$.
- Solve by **cases**: reject if infeasible or if any $\mu < 0$.
- **Convex problem ⇒ KKT point = global minimum.**
- Must-know: $(x-2)^2 + (y-1)^2$, $x + y \le 2$ gives $(1.5, 0.5)$, $\mu = 1$. The two-constraint example gives $(2, 1)$, $\mu = (\frac13, \frac23)$, $f = 2$.

---

**Previous:** [← 19. Lagrange Multipliers](19-lagrange-multipliers.md) · **Next:** [21. Convex Optimization →](21-convex-optimization.md)
