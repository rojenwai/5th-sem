# 19. Lagrange Multipliers (Equality Constraints)

> ⚠️ **Written from standard course knowledge.** No class notes for this topic yet. The scope follows [`source/aftermid-syllabus.txt`](../source/aftermid-syllabus.txt) §3. All examples were verified with a computer algebra system.
> **Syllabus:** *Where the method comes from (∇f parallel to ∇g) · building the auxiliary function (Lagrangian) and solving it step by step · bordered Hessian: interpretation and determinant test for constrained max/min · worked examples and classifying a point as local or global optimum*

---

## 🎯 In one line

At a constrained optimum the level curve of $f$ **touches** the constraint curve $g = c$, so their gradients are **parallel**: $\nabla f = \lambda \nabla g$. Solve that together with $g = c$, and classify each point with the **bordered Hessian**.

---

## 1. The problem

$$\text{Optimize } f(x_1, \dots, x_n) \quad \text{subject to} \quad g_j(x_1, \dots, x_n) = c_j, \quad j = 1, \dots, m \;\; (m < n)$$

Sometimes you can solve the constraint for one variable and substitute (as on the triangle edges in [Ch. 18](18-nlp-and-unconstrained-extrema.md)). Often you can't, or doing so is messy. Lagrange's method handles all variables symmetrically.

---

## 2. Where the method comes from: $\nabla f \parallel \nabla g$ ⭐⭐

Walk along the constraint curve $g(x,y) = c$ and watch the value of $f$.
- If the curve **crosses** a level curve $f = k$, you can keep walking to increase (or decrease) $f$, so this point is **not** an extremum.
- At a constrained max or min, the constraint curve must **just touch** (be **tangent** to) a level curve of $f$.

Two curves that are tangent have the same normal direction. The normal to a level curve is its **gradient**. Therefore:

$$\boxed{\nabla f = \lambda\, \nabla g} \qquad (\lambda = \text{Lagrange multiplier})$$

```
          f = 25 (touches) ← optimum
       ╲      ↗ ∇f
        ╲   ●(5,5)
  f = 16 ╲ ↗ ∇g        constraint  x + y = 10
          ╲
```

**Equivalently**, build the **Lagrangian** (auxiliary function)

$$\boxed{L(x, y, \lambda) = f(x,y) - \lambda\,[\,g(x,y) - c\,]}$$

and set **all** its partial derivatives to zero:

$$L_x = f_x - \lambda g_x = 0, \qquad L_y = f_y - \lambda g_y = 0, \qquad L_\lambda = -(g - c) = 0$$

The first two equations say $\nabla f = \lambda \nabla g$, and the third gives back the constraint. A constrained problem in $n$ variables becomes an **unconstrained stationary-point problem in $n + m$ variables**.

> **Sign convention:** some books write $L = f + \lambda(g - c)$. That only flips the sign of $\lambda$. The points found and the bordered-Hessian test are the same.

---

## 3. Step-by-step procedure

1. Write the constraint as $g(\mathbf x) = c$.
2. Form $L = f - \lambda(g - c)$ (with $\lambda_1, \dots, \lambda_m$ for $m$ constraints).
3. Solve $\partial L / \partial x_i = 0$ for all $i$ and $\partial L / \partial \lambda_j = 0$ for all $j$.
4. For each solution, classify it with the bordered Hessian (§4), or compare values if the constraint set is closed and bounded.
5. Interpret $\lambda$ if asked (§6).

---

## 4. The bordered Hessian ⭐⭐⭐

For $n$ variables and $m$ constraints, **border** the Hessian of $L$ with the constraint gradients:

$$H_B = \begin{bmatrix} \mathbf{0}_{m\times m} & \mathbf{J}_g \\ \mathbf{J}_g^T & \nabla^2_{xx} L \end{bmatrix} \qquad (\text{size } (m+n)\times(m+n))$$

**Two variables, one constraint** (the common exam case):

$$H_B = \begin{vmatrix} 0 & g_x & g_y \\ g_x & L_{xx} & L_{xy} \\ g_y & L_{xy} & L_{yy} \end{vmatrix}$$

| Sign of $\det H_B$ at the point | Conclusion |
|---|---|
| $\det H_B > 0$ | **Local (constrained) maximum** |
| $\det H_B < 0$ | **Local (constrained) minimum** |
| $\det H_B = 0$ | Inconclusive |

**General rule** ($n$ variables, $m$ constraints). Look at the **last $n - m$ leading principal minors** of $H_B$, i.e. those of order $2m+1, 2m+2, \dots, m+n$:

| Pattern | Conclusion |
|---|---|
| All have the sign of $(-1)^m$ | **Local min** |
| They alternate in sign, the first (order $2m+1$) having the sign of $(-1)^{m+1}$ | **Local max** |

*Check:* with $n = 2$ and $m = 1$ there is one minor (order 3). Min needs sign $(-1)^1 < 0$ and max needs sign $(-1)^2 > 0$, which matches the table above.

> **Why "bordered"?** The ordinary Hessian tests curvature in **all** directions, but along a constraint we can only move in directions **tangent** to $g = c$. The border of constraint gradients restricts the test to those directions.

---

## 5. Worked examples

### Example 1: maximise $f = xy$ subject to $x + y = 10$ ⭐

$$L = xy - \lambda(x + y - 10)$$
$$L_x = y - \lambda = 0, \qquad L_y = x - \lambda = 0, \qquad L_\lambda = -(x + y - 10) = 0$$

So $x = y = \lambda$ and $2x = 10$, giving $x = y = 5$, $\lambda = 5$ and $f = 25$.

**Bordered Hessian** ($g_x = g_y = 1$, $L_{xx} = 0$, $L_{xy} = 1$, $L_{yy} = 0$):

$$\det H_B = \begin{vmatrix} 0 & 1 & 1 \\ 1 & 0 & 1 \\ 1 & 1 & 0 \end{vmatrix} = 0 - 1(0 - 1) + 1(1 - 0) = 2 > 0 \;\Rightarrow\; \textbf{maximum}$$

**Answer:** max $f = 25$ at $(5, 5)$.

### Example 2: minimise $f = x^2 + y^2$ subject to $x + 2y = 5$

$L = x^2 + y^2 - \lambda(x + 2y - 5)$. Then $2x = \lambda$ and $2y = 2\lambda$, so $y = 2x$. Substituting, $x + 4x = 5$, so $x = 1$, $y = 2$, $\lambda = 2$ and $f = 5$.

$$\det H_B = \begin{vmatrix} 0 & 1 & 2 \\ 1 & 2 & 0 \\ 2 & 0 & 2 \end{vmatrix} = -1(2 - 0) + 2(0 - 4) = -10 < 0 \;\Rightarrow\; \textbf{minimum}$$

*(Geometrically, $(1,2)$ is the point on the line nearest the origin, at distance $\sqrt5$.)*

### Example 3: extremes of $f = xy$ on the circle $x^2 + y^2 = 8$: local vs global ⭐⭐

$L = xy - \lambda(x^2 + y^2 - 8)$:
$$y = 2\lambda x, \qquad x = 2\lambda y \;\Rightarrow\; y = 4\lambda^2 y \;\Rightarrow\; \lambda = \pm\tfrac12 \;(y \ne 0)$$
- $\lambda = \frac12$: $y = x$, so $2x^2 = 8$ and the points are $(2,2)$, $(-2,-2)$ with $f = 4$.
- $\lambda = -\frac12$: $y = -x$, giving the points $(2,-2)$, $(-2,2)$ with $f = -4$.

| Point | $\lambda$ | $\det H_B$ | Nature | $f$ |
|---|---|---|---|---|
| $(2,2)$, $(-2,-2)$ | $\tfrac12$ | $+64$ | **max** | 4 |
| $(2,-2)$, $(-2,2)$ | $-\tfrac12$ | $-64$ | **min** | $-4$ |

**Local or global?** The circle is **closed and bounded**, and $f$ is continuous, so absolute extrema exist and must be among the Lagrange points. Comparing values: the **global max is 4** and the **global min is −4**.

### Example 4: three variables, minimise $f = x^2 + y^2 + z^2$ subject to $x + y + z = 3$

$2x = 2y = 2z = \lambda$, so $x = y = z = 1$, $\lambda = 2$ and $f = 3$.

$$H_B = \begin{bmatrix} 0 & 1 & 1 & 1 \\ 1 & 2 & 0 & 0 \\ 1 & 0 & 2 & 0 \\ 1 & 0 & 0 & 2 \end{bmatrix}$$

Here $n = 3$ and $m = 1$, so check the last $n - m = 2$ minors, of orders $2m+1 = 3$ and 4:

$$\Delta_3 = \begin{vmatrix} 0 & 1 & 1 \\ 1 & 2 & 0 \\ 1 & 0 & 2 \end{vmatrix} = -4, \qquad \Delta_4 = \det H_B = -12$$

Both have the sign of $(-1)^m = -1$, so the point is a **minimum**, with $f_{\min} = 3$ at $(1,1,1)$.

### Example 5: two constraints

Minimise $x^2 + y^2 + z^2$ subject to $x + 2y + z = 1$ and $2x - y - 3z = 4$.

$L = x^2 + y^2 + z^2 - \lambda_1(x + 2y + z - 1) - \lambda_2(2x - y - 3z - 4)$:
$$2x = \lambda_1 + 2\lambda_2, \qquad 2y = 2\lambda_1 - \lambda_2, \qquad 2z = \lambda_1 - 3\lambda_2$$

Substituting into the two constraints gives $\lambda_1 = \frac{52}{75}$ and $\lambda_2 = \frac{18}{25}$, so
$$x = \tfrac{16}{15},\quad y = \tfrac13,\quad z = -\tfrac{11}{15},\quad f_{\min} = \tfrac{134}{75}$$

The $5\times5$ bordered Hessian has $\det = 150 > 0$, which is the sign of $(-1)^m = (-1)^2 = +$, so this is a **minimum**.

---

## 6. Meaning of $\lambda$ (sensitivity / shadow price)

$$\lambda^* = \frac{d f^*}{d c}$$

$\lambda$ is the **rate at which the optimal value changes** when the constraint constant $c$ is relaxed. It is the nonlinear analogue of the **dual variable / shadow price** in LP ([Ch. 9](09-duality.md)).

*Check with Example 1:* the optimum for $x + y = c$ is $f^* = c^2/4$, so $df^*/dc = c/2 = 5 = \lambda$ ✔. Raising $c$ from 10 to 11 raises $f^*$ from 25 to 30.25, roughly $+\lambda$.

---

## 7. Common exam questions

1. **Explain the geometric idea behind Lagrange multipliers.** Tangency, so $\nabla f = \lambda\nabla g$ (§2).
2. **Form the Lagrangian and find the stationary points of …** (Examples 1–2).
3. **What is a bordered Hessian? State the determinant test.** See §4.
4. **Find the max/min of $f$ subject to $g = c$ and classify the points.** Use Example 3 and decide local vs global.
5. **Three variables / two constraints.** Use Examples 4–5 with the minor-sign rule.
6. **Interpret the Lagrange multiplier.** See §6.

---

## ⚡ Quick revision

- **Tangency:** $\nabla f = \lambda \nabla g$ together with $g = c$.
- $L = f - \lambda(g - c)$. Set $L_x = L_y = L_\lambda = 0$.
- 2 variables, 1 constraint: $H_B = \begin{vmatrix} 0 & g_x & g_y \\ g_x & L_{xx} & L_{xy} \\ g_y & L_{xy} & L_{yy} \end{vmatrix}$. **$> 0$ ⇒ max**, **$< 0$ ⇒ min**.
- General: last $n - m$ minors. All $(-1)^m$ ⇒ min. Alternating, starting with $(-1)^{m+1}$ ⇒ max.
- Closed, bounded constraint set ⇒ compare $f$ at the Lagrange points for the **global** answer.
- $\lambda = df^*/dc$ is the **shadow price**.
- Must-know: $xy$ on $x + y = 10$ gives 25 (det = 2). $xy$ on $x^2 + y^2 = 8$ gives ±4.

---

**Previous:** [← 18. NLP & Unconstrained Extrema](18-nlp-and-unconstrained-extrema.md) · **Next:** [20. KKT Conditions →](20-kkt-conditions.md)
