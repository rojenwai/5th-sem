# 22. Numerical Methods: Newton–Raphson for Nonlinear Optimization

> ⚠️ **Written from standard course knowledge.** No class notes for this topic yet. The scope follows [`source/aftermid-syllabus.txt`](../source/aftermid-syllabus.txt) §6. Every iteration table below was produced by running the code in §7.
> **Syllabus:** *Why numerical methods are needed (e.g. eˣ + 2x − 4 = 0 has no closed-form solution) · gradient, Hessian, iterative methods, convergence and stopping criteria · Newton–Raphson: roots vs stationary points, working procedure, worked examples · Newton's method for two variables, damped Newton · Python code*

---

## 🎯 In one line

Replace the function by its **tangent** (for a root) or its **quadratic approximation** (for an optimum) and jump to where that model is zero or minimal: $x_{k+1} = x_k - \dfrac{f(x_k)}{f'(x_k)}$, or in $n$ variables $\mathbf x_{k+1} = \mathbf x_k - H^{-1}\nabla f$. Convergence is **quadratic** near the solution, and a **damping** factor keeps it safe far away.

---

## 1. Why numerical methods are needed

Setting $\nabla f = 0$ often gives equations **with no closed-form solution**. For example:

$$e^x + 2x - 4 = 0$$

No algebraic manipulation isolates $x$ (it mixes an exponential and a polynomial). The same happens with the KKT systems of real problems. **Iterative methods** start from a guess $x_0$ and generate $x_1, x_2, \dots \to x^*$.

---

## 2. Basic ideas

| Term | Meaning |
|---|---|
| **Gradient** $\nabla f$ | The vector of first partials. It points in the direction of steepest increase, and $\nabla f = 0$ at a stationary point |
| **Hessian** $H = \nabla^2 f$ | The matrix of second partials, i.e. the curvature ([Ch. 18](18-nlp-and-unconstrained-extrema.md), [Ch. 21](21-convex-optimization.md)) |
| **Iterative method** | A rule $x_{k+1} = \Phi(x_k)$ applied repeatedly |
| **Convergence** | $x_k \to x^*$. **Quadratic** convergence means $\lvert e_{k+1}\rvert \approx C\lvert e_k\rvert^2$: the number of correct digits roughly **doubles** each step |
| **Stopping criteria** | Stop when **any** of these holds: $\lvert x_{k+1} - x_k\rvert < \varepsilon$ · $\lvert f(x_k)\rvert < \varepsilon$ (root) or $\lVert\nabla f(x_k)\rVert < \varepsilon$ (optimum) · $k \ge$ **max iterations** (a safeguard against divergence) |

---

## 3. Newton–Raphson for a root: $g(x) = 0$ ⭐⭐

**Derivation.** Near $x_k$, $g(x) \approx g(x_k) + g'(x_k)(x - x_k)$. Setting the tangent line to zero gives:

$$\boxed{x_{k+1} = x_k - \frac{g(x_k)}{g'(x_k)}}$$

```
   g(x)
     │      ╱ tangent at x_k
     │    ╱●  (x_k, g(x_k))
     │  ╱ ╱
  ───┼─●─╱──────────── x
     │x_{k+1}  x_k        next guess = where the tangent meets the axis
```

### Working procedure

1. Choose $x_0$ (close to the root if possible, e.g. by sign change: $g(a) g(b) < 0$).
2. Compute $g(x_k)$ and $g'(x_k)$.
3. Update $x_{k+1} = x_k - g(x_k)/g'(x_k)$.
4. Check the stopping criteria, then repeat.

### Example 1: $e^x + 2x - 4 = 0$ ⭐

$g(x) = e^x + 2x - 4$ and $g'(x) = e^x + 2$. Since $g(0) = -3 < 0$ and $g(1) = 0.718 > 0$, there is a root in $(0, 1)$. Take $x_0 = 1$.

| $k$ | $x_k$ | $g(x_k)$ | $g'(x_k)$ | $x_{k+1}$ |
|---|---|---|---|---|
| 0 | 1.000000 | 0.718282 | 4.718282 | 0.847766 |
| 1 | 0.847766 | 0.029959 | 4.334426 | 0.840854 |
| 2 | 0.840854 | 0.0000556 | 4.318347 | 0.840841 |
| 3 | 0.840841 | $1.9\times10^{-10}$ | 4.318317 | 0.840841 |

$$x^* \approx \mathbf{0.840841}$$

Note the **quadratic convergence**: $g$ goes $0.7 \to 0.03 \to 5.6\times10^{-5} \to 1.9\times10^{-10}$.

---

## 4. Newton's method for a stationary point (1 variable) ⭐⭐

To **optimise** $f$, find a root of $f'$, i.e. apply §3 to $g = f'$:

$$\boxed{x_{k+1} = x_k - \frac{f'(x_k)}{f''(x_k)}}$$

Equivalently, minimise the **quadratic model** $f(x_k) + f'(x_k)(x - x_k) + \frac12 f''(x_k)(x - x_k)^2$.

| | Root finding | Stationary point (optimisation) |
|---|---|---|
| Solves | $g(x) = 0$ | $f'(x) = 0$ |
| Update | $x - g/g'$ | $x - f'/f''$ |
| Needs | 1st derivative | **2nd** derivative |
| Afterwards | – | Check $f''(x^*)$: $> 0$ is a min, $< 0$ a max |

> Newton finds **any** stationary point (min, max or inflection). Always classify the result.

### Example 2: $f(x) = x^3 - 6x^2 + 4x + 12$, starting from $x_0 = 3$

$f'(x) = 3x^2 - 12x + 4$ and $f''(x) = 6x - 12$.

| $k$ | $x_k$ | $f'(x_k)$ | $f''(x_k)$ | $x_{k+1}$ |
|---|---|---|---|---|
| 0 | 3.000000 | −5.0000 | 6.0000 | 3.833333 |
| 1 | 3.833333 | 2.0833 | 11.0000 | 3.643939 |
| 2 | 3.643939 | 0.1076 | 9.8636 | 3.633030 |
| 3 | 3.633030 | 0.00036 | 9.7982 | 3.632993 |

$x^* = 3.632993$ (exactly $2 + \frac{2\sqrt6}{3}$), with $f''(x^*) = 9.80 > 0$, so it is a **local minimum**. Starting near $x_0 = 0$ instead would converge to the other stationary point, $x = 2 - \frac{2\sqrt6}{3} \approx 0.367$, a **local max**.

---

## 5. Newton's method in two (or $n$) variables ⭐⭐⭐

Quadratic model: $f(\mathbf x) \approx f(\mathbf x_k) + \nabla f_k^T(\mathbf x - \mathbf x_k) + \frac12 (\mathbf x - \mathbf x_k)^T H_k (\mathbf x - \mathbf x_k)$. Setting its gradient to zero gives:

$$\boxed{\mathbf x_{k+1} = \mathbf x_k - H(\mathbf x_k)^{-1}\, \nabla f(\mathbf x_k)}$$

*(In practice solve $H_k\,\mathbf p_k = -\nabla f_k$ for the **Newton direction** $\mathbf p_k$, then set $\mathbf x_{k+1} = \mathbf x_k + \mathbf p_k$.)*

For a $2\times2$ matrix: $\begin{bmatrix} a & b \\ c & d \end{bmatrix}^{-1} = \dfrac{1}{ad - bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$.

### Example 3: a quadratic function converges in ONE step ⭐

Minimise $f(x_1, x_2) = x_1 - x_2 + 2x_1^2 + 2x_1x_2 + x_2^2$ from $\mathbf x_0 = (0, 0)$.

$$\nabla f = \begin{pmatrix} 1 + 4x_1 + 2x_2 \\ -1 + 2x_1 + 2x_2 \end{pmatrix} \Rightarrow \nabla f(\mathbf x_0) = \begin{pmatrix} 1 \\ -1 \end{pmatrix}, \qquad H = \begin{bmatrix} 4 & 2 \\ 2 & 2 \end{bmatrix}, \quad H^{-1} = \frac14\begin{bmatrix} 2 & -2 \\ -2 & 4 \end{bmatrix} = \begin{bmatrix} \tfrac12 & -\tfrac12 \\ -\tfrac12 & 1 \end{bmatrix}$$

$$\mathbf x_1 = \begin{pmatrix} 0 \\ 0 \end{pmatrix} - \begin{bmatrix} \tfrac12 & -\tfrac12 \\ -\tfrac12 & 1 \end{bmatrix}\begin{pmatrix} 1 \\ -1 \end{pmatrix} = -\begin{pmatrix} 1 \\ -\tfrac32 \end{pmatrix} = \begin{pmatrix} -1 \\ 1.5 \end{pmatrix}$$

**Check:** $\nabla f(\mathbf x_1) = (1 - 4 + 3,\; -1 - 2 + 3) = (0, 0)$ ✔. $H$ is PD (since $D_1 = 4$ and $D_2 = 4$), so this is the **minimum**: $f^* = -1.25$.

> For a quadratic function the model is **exact**, so Newton lands on the optimum in one step from **any** start.

### Example 4: a non-quadratic function, $f = x^4 + xy + (1 + y)^2$, from $(1, 0)$

$\nabla f = (4x^3 + y,\; x + 2(1 + y))$ and $H = \begin{bmatrix} 12x^2 & 1 \\ 1 & 2 \end{bmatrix}$.

**Iteration 1:** $\nabla f(1,0) = (4, 3)$, $H = \begin{bmatrix} 12 & 1 \\ 1 & 2 \end{bmatrix}$ with $\det = 23$, so $H^{-1}\nabla f = \frac{1}{23}(2\cdot4 - 3,\; -4 + 12\cdot3) = \frac{1}{23}(5, 32)$. That gives $\mathbf x_1 = (1 - \frac{5}{23},\; -\frac{32}{23}) = (0.7826, -1.3913)$.

| $k$ | $x$ | $y$ | $\lVert\nabla f\rVert$ | $f$ |
|---|---|---|---|---|
| 0 | 1.0000 | 0.0000 | 5.0 | 2.0000 |
| 1 | 0.7826 | −1.3913 | 0.526 | −0.5606 |
| 2 | 0.7058 | −1.3529 | 0.054 | −0.5822 |
| 3 | 0.6960 | −1.3480 | 0.0008 | −0.582445 |
| 4 | 0.6959 | −1.3479 | $2\times10^{-7}$ | −0.582445 |

The minimum is at $(0.6959, -1.3479)$, with $f^* \approx -0.5824$.

---

## 6. The damped Newton method ⭐⭐

**The problem with pure Newton.** Far from the solution, or where $H$ is not positive definite, the full step can **overshoot** and diverge, or even head uphill.

**Damped Newton:** keep the Newton **direction** but scale the **step**:

$$\boxed{\mathbf x_{k+1} = \mathbf x_k - \alpha_k\, H_k^{-1}\nabla f_k, \qquad 0 < \alpha_k \le 1}$$

$\alpha_k$ is chosen by a **line search**, for example backtracking: start with $\alpha = 1$ and halve it until $f$ decreases enough (Armijo: $f(\mathbf x + \alpha\mathbf p) \le f(\mathbf x) + c\,\alpha\nabla f^T\mathbf p$). Near the solution $\alpha = 1$ is accepted, and fast quadratic convergence returns.

### Example 5: pure Newton diverges, damped Newton converges

Minimise $f(x) = \sqrt{1 + x^2}$ (the minimum is at $x = 0$). Here $f' = \dfrac{x}{\sqrt{1 + x^2}}$ and $f'' = (1 + x^2)^{-3/2}$, so the pure Newton step is $x_{k+1} = x_k - x_k(1 + x_k^2) = -x_k^3$.

| Start $x_0 = 1.5$ | $x_1$ | $x_2$ | $x_3$ |
|---|---|---|---|
| **Pure Newton** | −3.375 | 38.44 | −56 815 ⟶ **diverges** |

| $k$ | $x_k$ | Newton step $p$ | $\alpha$ accepted | $x_{k+1}$ |
|---|---|---|---|---|
| 0 | 1.5 | −4.875 | **0.5** | −0.9375 |
| 1 | −0.9375 | 1.7615 | 1 | 0.8240 |
| 2 | 0.8240 | −1.3834 | 1 | −0.5594 |
| 3 | −0.5594 | 0.7345 | 1 | 0.1751 |
| 4 | 0.1751 | −0.1804 | 1 | −0.0054 |
| 5 | −0.0054 | 0.0054 | 1 | ≈ 0 ✔ |

Damped Newton converges to 0. (Pure Newton converges only if $\lvert x_0\rvert < 1$.)

| Pure Newton | Damped Newton |
|---|---|
| $\alpha = 1$ always | $\alpha_k$ from a line search |
| Quadratic convergence **near** $x^*$ | Global safeguard **plus** quadratic convergence near $x^*$ |
| May diverge or oscillate | Guarantees $f$ decreases each step (if $H$ is PD) |

**Other drawbacks of Newton** (all variants): it needs second derivatives, and it costs $O(n^3)$ per step to solve with $H$. It fails if $H$ is singular. It can converge to a max or saddle (§4). Quasi-Newton methods (BFGS) approximate $H$ to avoid these costs.

---

## 7. Python code for Newton–Raphson

```python
import math
import numpy as np


# ---------- 1. Newton-Raphson for a root: solve g(x) = 0 ----------
def newton_root(g, dg, x0, tol=1e-8, max_iter=50):
    x = x0
    for k in range(max_iter):
        gx, dgx = g(x), dg(x)
        if dgx == 0:
            raise ZeroDivisionError("g'(x) = 0: Newton step undefined")
        x_new = x - gx / dgx
        print(f"k={k}  x={x:.6f}  g(x)={gx:.6e}  x_new={x_new:.6f}")
        if abs(x_new - x) < tol:          # stopping criterion
            return x_new
        x = x_new
    raise RuntimeError("did not converge in max_iter iterations")


# ---------- 2. Newton for a stationary point: f'(x) = 0 ----------
def newton_min_1d(df, d2f, x0, tol=1e-8, max_iter=50):
    return newton_root(df, d2f, x0, tol, max_iter)   # same algorithm on f'


# ---------- 3. Newton / damped Newton in n variables ----------
def newton_nd(f, grad, hess, x0, tol=1e-8, max_iter=50, damped=False):
    x = np.array(x0, dtype=float)
    for k in range(max_iter):
        g = grad(x)
        if np.linalg.norm(g) < tol:       # stopping criterion ||grad|| < eps
            break
        p = -np.linalg.solve(hess(x), g)  # Newton direction  (H p = -g)
        alpha = 1.0
        if damped:                        # backtracking (Armijo) line search
            while f(x + alpha * p) > f(x) + 1e-4 * alpha * g @ p:
                alpha /= 2
        x = x + alpha * p
        print(f"k={k}  x={np.round(x, 6)}  f={f(x):.6f}  alpha={alpha}")
    return x


if __name__ == "__main__":
    print("Root of e^x + 2x - 4 = 0")
    r = newton_root(lambda x: math.exp(x) + 2*x - 4, lambda x: math.exp(x) + 2, x0=1.0)
    print("root =", round(r, 6))

    print("\nMinimise f(x1,x2) = x1 - x2 + 2x1^2 + 2x1x2 + x2^2 from (0,0)")
    f = lambda v: v[0] - v[1] + 2*v[0]**2 + 2*v[0]*v[1] + v[1]**2
    grad = lambda v: np.array([1 + 4*v[0] + 2*v[1], -1 + 2*v[0] + 2*v[1]])
    hess = lambda v: np.array([[4.0, 2.0], [2.0, 2.0]])
    print(newton_nd(f, grad, hess, [0, 0]))
```

**Output** (actual run):

```
Root of e^x + 2x - 4 = 0
k=0  x=1.000000  g(x)=7.182818e-01  x_new=0.847766
k=1  x=0.847766  g(x)=2.995891e-02  x_new=0.840854
k=2  x=0.840854  g(x)=5.563384e-05  x_new=0.840841
k=3  x=0.840841  g(x)=1.923937e-10  x_new=0.840841
root = 0.840841

Minimise f(x1,x2) = x1 - x2 + 2x1^2 + 2x1x2 + x2^2 from (0,0)
k=0  x=[-1.   1.5]  f=-1.250000  alpha=1.0
[-1.   1.5]
```

---

## 8. Common exam questions

1. **Why are numerical methods needed in optimization? Give an example.** $e^x + 2x - 4 = 0$ (§1).
2. **Define convergence, rate of convergence and stopping criteria.** See §2.
3. **Derive the Newton–Raphson formula** (tangent line, §3).
4. **Difference between Newton for roots and for stationary points.** See the table in §4.
5. **Perform 3 iterations of Newton's method to find the root/minimum of …** Use Examples 1–2.
6. **Newton's method for two variables: one iteration from $\mathbf x_0$.** Use Examples 3–4, computing $H^{-1}$ carefully.
7. **What is the damped Newton method and why is it needed?** See §6 and Example 5.
8. **Write a Python program for Newton–Raphson.** See §7.

---

## ⚡ Quick revision

- **Root:** $x_{k+1} = x_k - g/g'$. **Optimum (1-D):** $x_{k+1} = x_k - f'/f''$. **n-D:** $\mathbf x_{k+1} = \mathbf x_k - H^{-1}\nabla f$.
- **Stop** when $\lvert\Delta x\rvert < \varepsilon$, or $\lVert\nabla f\rVert < \varepsilon$, or $k = $ max_iter.
- **Quadratic convergence**: the correct digits double each step (near the root).
- A quadratic $f$ converges in **one** Newton step.
- Newton finds **any** stationary point, so check $f''$ or $H$.
- **Damped:** $\mathbf x_{k+1} = \mathbf x_k - \alpha_k H^{-1}\nabla f$ with $\alpha$ from a backtracking line search, which fixes divergence (as for $\sqrt{1+x^2}$ from 1.5).
- Must-know answers: root of $e^x + 2x - 4$ is **0.840841**. Example 3 gives **$(-1, 1.5)$, $f = -1.25$** in one step.

---

**Previous:** [← 21. Convex Optimization](21-convex-optimization.md) · **Back to:** [Optimization index](../README.md)
