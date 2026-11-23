# 22. Numerical Problem Bank (Fully Solved)

> ✅ **Topics checked against the class notes** (`Rati OS FULL.pdf` pp. 1–64; also `Rati-OS 1.pdf`, `bhaves_os_notes.pdf`). The class covers exactly these topics. Explanations are written from standard OS theory; class-specific examples are collected in [Ch. 22](22-numerical-problem-bank.md).
> **Scope:** every numerical type in the syllabus, solved end to end.

---

## 🎯 How to use this chapter

Cover the solution, work the problem on paper, then compare. **Problems 1–6 all use the same process set**, so you can see the six algorithms side by side on identical data.

---

# PART A — CPU Scheduling

## The common process set

| Process | AT | BT | Priority *(lower = higher)* |
|---|---|---|---|
| **P1** | 0 | 7 | 3 |
| **P2** | 1 | 5 | 1 |
| **P3** | 2 | 3 | 4 |
| **P4** | 3 | 1 | 2 |
| **P5** | 4 | 6 | 5 |

$\sum BT = 22$, so **every correct Gantt chart ends at $t = 22$** (no idle time, no overhead).

---

## Problem 1 — FCFS ⭐⭐⭐

**Order by arrival:** P1, P2, P3, P4, P5.

```
 ┌──────────────┬──────────┬──────┬──┬────────────┐
 │      P1      │    P2    │  P3  │P4│     P5     │
 └──────────────┴──────────┴──────┴──┴────────────┘
 0              7         12     15 16           22
```

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 0 | 7 | 7 | 7 | 0 |
| P2 | 1 | 5 | 12 | 11 | 6 |
| P3 | 2 | 3 | 15 | 13 | 10 |
| P4 | 3 | 1 | 16 | 13 | 12 |
| P5 | 4 | 6 | 22 | 18 | 12 |
| | | | | **62** | **40** |

$$\text{Avg TAT} = \frac{62}{5} = \mathbf{12.4} \qquad \text{Avg WT} = \frac{40}{5} = \mathbf{8.0}$$

> 📌 **The convoy effect is visible:** P4 needs only **1 unit** of CPU but waits **12**.

---

## Problem 2 — SJF (non-preemptive) ⭐⭐⭐

| CPU free at | Arrived & waiting (BT) | Shortest | Runs |
|---|---|---|---|
| 0 | P1 (7) only | P1 | 0 → 7 |
| 7 | P2 (5), P3 (3), P4 (**1**), P5 (6) | **P4** | 7 → 8 |
| 8 | P2 (5), P3 (**3**), P5 (6) | **P3** | 8 → 11 |
| 11 | P2 (**5**), P5 (6) | **P2** | 11 → 16 |
| 16 | P5 | P5 | 16 → 22 |

```
 ┌──────────────┬──┬──────┬──────────┬────────────┐
 │      P1      │P4│  P3  │    P2    │     P5     │
 └──────────────┴──┴──────┴──────────┴────────────┘
 0              7  8     11         16           22
```

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 0 | 7 | 7 | 7 | 0 |
| P2 | 1 | 5 | 16 | 15 | 10 |
| P3 | 2 | 3 | 11 | 9 | 6 |
| P4 | 3 | 1 | 8 | 5 | 4 |
| P5 | 4 | 6 | 22 | 18 | 12 |
| | | | | **54** | **32** |

$$\text{Avg TAT} = \frac{54}{5} = \mathbf{10.8} \qquad \text{Avg WT} = \frac{32}{5} = \mathbf{6.4}$$

---

## Problem 3 — SRTF (preemptive SJF) ⭐⭐⭐

**Check at every arrival: $t = 0, 1, 2, 3, 4$ — and at every completion.**

| Time | Event | Remaining (arrived) | Min | Action |
|---|---|---|---|---|
| 0 | P1 arrives | P1 = 7 | P1 | Run P1 |
| 1 | P2 arrives | P1 = **6**, P2 = **5** | P2 | ⚡ preempt → **P2** |
| 2 | P3 arrives | P1 = 6, P2 = **4**, P3 = **3** | P3 | ⚡ preempt → **P3** |
| 3 | P4 arrives | P1 = 6, P2 = 4, P3 = **2**, P4 = **1** | P4 | ⚡ preempt → **P4** |
| 4 | **P4 done**, P5 arrives | P1 = 6, P2 = 4, P3 = **2**, P5 = 6 | P3 | Run **P3** |
| 6 | **P3 done** | P1 = 6, P2 = **4**, P5 = 6 | P2 | Run **P2** |
| 10 | **P2 done** | P1 = **6**, P5 = **6** | tie → **lower AT** → P1 | Run **P1** |
| 16 | **P1 done** | P5 = 6 | P5 | Run **P5** |
| 22 | **P5 done** | — | — | Finished |

```
 ┌──┬──┬──┬──┬──────┬────────────┬──────────────┬────────────┐
 │P1│P2│P3│P4│  P3  │     P2     │      P1      │     P5     │
 └──┴──┴──┴──┴──────┴────────────┴──────────────┴────────────┘
 0  1  2  3  4      6           10             16           22
```

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 0 | 7 | 16 | 16 | 9 |
| P2 | 1 | 5 | 10 | 9 | 4 |
| P3 | 2 | 3 | 6 | 4 | 1 |
| P4 | 3 | 1 | **4** | **1** | **0** |
| P5 | 4 | 6 | 22 | 18 | 12 |
| | | | | **48** | **26** |

$$\text{Avg TAT} = \frac{48}{5} = \mathbf{9.6} \qquad \text{Avg WT} = \frac{26}{5} = \mathbf{5.2}$$

**Audit:** P1 $= 1+6 = 7$ ✓ · P2 $= 1+4 = 5$ ✓ · P3 $= 1+2 = 3$ ✓ · P4 $= 1$ ✓ · P5 $= 6$ ✓

> ⭐ **Best of all six algorithms**, and P4 (the 1-unit job) achieves **WT = 0**.

---

## Problem 4 — Priority, non-preemptive ⭐⭐⭐

| CPU free at | Waiting (priority) | Highest | Runs |
|---|---|---|---|
| 0 | P1 (3) only | P1 | 0 → 7 |
| 7 | P2 (**1**), P3 (4), P4 (2), P5 (5) | **P2** | 7 → 12 |
| 12 | P3 (4), P4 (**2**), P5 (5) | **P4** | 12 → 13 |
| 13 | P3 (**4**), P5 (5) | **P3** | 13 → 16 |
| 16 | P5 | P5 | 16 → 22 |

```
 ┌──────────────┬──────────┬──┬──────┬────────────┐
 │      P1      │    P2    │P4│  P3  │     P5     │
 └──────────────┴──────────┴──┴──────┴────────────┘
 0              7         12 13     16           22
```

| Process | AT | BT | Pri | CT | TAT | WT |
|---|---|---|---|---|---|---|
| P1 | 0 | 7 | 3 | 7 | 7 | 0 |
| P2 | 1 | 5 | 1 | 12 | 11 | 6 |
| P3 | 2 | 3 | 4 | 16 | 14 | 11 |
| P4 | 3 | 1 | 2 | 13 | 10 | 9 |
| P5 | 4 | 6 | 5 | 22 | 18 | 12 |
| | | | | | **60** | **38** |

$$\text{Avg TAT} = \frac{60}{5} = \mathbf{12.0} \qquad \text{Avg WT} = \frac{38}{5} = \mathbf{7.6}$$

---

## Problem 5 — Priority, preemptive ⭐⭐⭐

| Time | Event | Ready (priority) | Highest | Action |
|---|---|---|---|---|
| 0 | P1 arrives | P1 (3) | P1 | Run P1 |
| 1 | **P2 arrives (1)** | P1 (3), P2 (**1**) | P2 | ⚡ **preempt P1** (rem 6) → P2 |
| 2 | P3 arrives (4) | P2 (1) still highest | P2 | Continue |
| 3 | P4 arrives (2) | P2 (1) still highest | P2 | Continue |
| 4 | P5 arrives (5) | P2 (1) still highest | P2 | Continue |
| 6 | **P2 done** | P1 (3, rem 6), P3 (4), P4 (**2**), P5 (5) | **P4** | Run P4 |
| 7 | **P4 done** | P1 (**3**), P3 (4), P5 (5) | **P1** | Run P1 (rem 6) |
| 13 | **P1 done** | P3 (**4**), P5 (5) | **P3** | Run P3 |
| 16 | **P3 done** | P5 | P5 | Run P5 |
| 22 | **P5 done** | — | — | Finished |

```
 ┌──┬──────────┬──┬────────────┬──────┬────────────┐
 │P1│    P2    │P4│     P1     │  P3  │     P5     │
 └──┴──────────┴──┴────────────┴──────┴────────────┘
 0  1          6  7           13     16           22
```

| Process | AT | BT | Pri | CT | TAT | WT |
|---|---|---|---|---|---|---|
| P1 | 0 | 7 | 3 | 13 | 13 | 6 |
| P2 | 1 | 5 | **1** | **6** | **5** | **0** |
| P3 | 2 | 3 | 4 | 16 | 14 | 11 |
| P4 | 3 | 1 | 2 | 7 | 4 | 3 |
| P5 | 4 | 6 | 5 | 22 | 18 | 12 |
| | | | | | **54** | **32** |

$$\text{Avg TAT} = \frac{54}{5} = \mathbf{10.8} \qquad \text{Avg WT} = \frac{32}{5} = \mathbf{6.4}$$

**Audit:** P1 $= 1 + 6 = 7$ ✓ · total $= 22$ ✓ · **P2, the highest-priority process, got WT = 0** ✓

---

## Problem 6 — Round Robin, q = 3 ⭐⭐⭐

**Convention:** a process arriving at the same instant as a preemption is **queued first**.

| Time | Running | Ran | Remaining | Arrivals | Ready queue after |
|---|---|---|---|---|---|
| 0–3 | **P1** | 3 | P1 = 4 | P2@1, P3@2, P4@3 | [P2, P3, P4, **P1**] |
| 3–6 | **P2** | 3 | P2 = 2 | P5@4 | [P3, P4, P1, P5, **P2**] |
| 6–9 | **P3** | 3 | **0 → done** | — | [P4, P1, P5, P2] |
| 9–10 | **P4** | 1 | **0 → done** | — | [P1, P5, P2] |
| 10–13 | **P1** | 3 | P1 = 1 | — | [P5, P2, **P1**] |
| 13–16 | **P5** | 3 | P5 = 3 | — | [P2, P1, **P5**] |
| 16–18 | **P2** | 2 | **0 → done** | — | [P1, P5] |
| 18–19 | **P1** | 1 | **0 → done** | — | [P5] |
| 19–22 | **P5** | 3 | **0 → done** | — | [ ] |

```
 ┌──────┬──────┬──────┬──┬──────┬──────┬────┬──┬──────┐
 │  P1  │  P2  │  P3  │P4│  P1  │  P5  │ P2 │P1│  P5  │
 └──────┴──────┴──────┴──┴──────┴──────┴────┴──┴──────┘
 0      3      6      9 10     13     16   18 19     22
```

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 7 | 19 | 19 | 12 | **0** |
| P2 | 1 | 5 | 18 | 17 | 12 | **2** |
| P3 | 2 | 3 | 9 | 7 | 4 | **4** |
| P4 | 3 | 1 | 10 | 7 | 6 | **6** |
| P5 | 4 | 6 | 22 | 18 | 12 | **9** |
| | | | | **68** | **46** | |

$$\text{Avg TAT} = \frac{68}{5} = \mathbf{13.6} \qquad \text{Avg WT} = \frac{46}{5} = \mathbf{9.2}$$

**Audit:** P1 $= 3+3+1 = 7$ ✓ · P2 $= 3+2 = 5$ ✓ · P5 $= 3+3 = 6$ ✓ · total $= 22$ ✓
**Context switches:** 9 dispatches − 1 = **8**.

---

## ⭐ Problem 7 — Compare all six

| Algorithm | Avg TAT | Avg WT | Switches | Verdict |
|---|---|---|---|---|
| FCFS | 12.4 | 8.0 | **4** | Simplest, worst convoy |
| SJF | 10.8 | 6.4 | 4 | Good, needs burst times |
| **SRTF** | **9.6** ⭐ | **5.2** ⭐ | 7 | **Optimal average WT** |
| Priority (non-preemptive) | 12.0 | 7.6 | 4 | Serves importance |
| Priority (preemptive) | 10.8 | 6.4 | 5 | **P2 gets WT = 0** |
| Round Robin (q = 3) | 13.6 | 9.2 | **8** | **Best response time, fairest** |

> ⭐ **Model concluding sentence:** *"SRTF gives the minimum average waiting time (5.2), Round Robin the best response time and fairness at the cost of the highest average waiting time (9.2), and FCFS the least overhead. No algorithm is best on every criterion."*

---

## Problem 8 — Round Robin **with context-switch overhead** ⭐⭐⭐

> **P1 = 5, P2 = 4, P3 = 3, all arriving at $t = 0$. $q = 2$, context-switch time $\delta = 1$. Find avg TAT, avg WT and CPU efficiency.**

**Slice sequence:** P1(2), P2(2), P3(2), P1(2), P2(2 ✓), P3(1 ✓), P1(1 ✓) — **7 dispatches ⇒ 6 context switches.**

```
 ┌────┬──┬────┬──┬────┬──┬────┬──┬────┬──┬──┬──┬──┐
 │ P1 │CS│ P2 │CS│ P3 │CS│ P1 │CS│ P2 │CS│P3│CS│P1│
 └────┴──┴────┴──┴────┴──┴────┴──┴────┴──┴──┴──┴──┘
 0    2  3    5  6    8  9   11 12   14 15 16 17 18
```

| Process | BT | CT | TAT | WT |
|---|---|---|---|---|
| P1 | 5 | 18 | 18 | 13 |
| P2 | 4 | 14 | 14 | 10 |
| P3 | 3 | 16 | 16 | 13 |
| | | | **48** | **36** |

$$\text{Avg TAT} = \frac{48}{3} = \mathbf{16.0} \qquad \text{Avg WT} = \frac{36}{3} = \mathbf{12.0}$$

$$\text{Total time} = \sum BT + (\text{switches})\delta = 12 + 6 = 18$$
$$\boxed{\text{CPU efficiency} = \frac{12}{18} = \mathbf{66.7\%}}$$

> ⚠️ **One third of the CPU was spent switching.** With $\delta = 0$ the same schedule would finish at $t = 12$.

---

## Problem 9 — Burst-time prediction (exponential averaging) ⭐⭐⭐

> **$\tau_1 = 8$, $\alpha = 0.4$. Actual bursts: 10, 6, 8, 12. Predict $\tau_2 \ldots \tau_5$.**

$$\tau_{n+1} = \alpha t_n + (1-\alpha)\tau_n = 0.4\,t_n + 0.6\,\tau_n$$

$$\tau_2 = 0.4(10) + 0.6(8) = 4 + 4.8 = \mathbf{8.8}$$
$$\tau_3 = 0.4(6) + 0.6(8.8) = 2.4 + 5.28 = \mathbf{7.68}$$
$$\tau_4 = 0.4(8) + 0.6(7.68) = 3.2 + 4.608 = \mathbf{7.808}$$
$$\tau_5 = 0.4(12) + 0.6(7.808) = 4.8 + 4.685 = \mathbf{9.485}$$

| $n$ | Actual $t_n$ | Predicted $\tau_n$ |
|---|---|---|
| 1 | 10 | 8 *(given)* |
| 2 | 6 | 8.8 |
| 3 | 8 | 7.68 |
| 4 | 12 | 7.808 |
| 5 | — | **9.485** |

**Follow-ups:** with $\alpha = 1$ every prediction equals the previous actual burst (10, 6, 8, 12); with $\alpha = 0$ every prediction stays at **8**.

---

# PART B — Process Creation

## Problem 10 — Counting processes ⭐⭐⭐

> **(a)** How many processes does this create, and how many times is `Hi` printed?

```c
int main(void) {
    fork();
    fork();
    printf("Hi\n");
    return 0;
}
```

$2^2 = \mathbf{4}$ processes (**3 children**); `Hi` is printed **4 times**.

> **(b)**

```c
for (int i = 0; i < 4; i++)
    fork();
```

$2^4 = \mathbf{16}$ processes, **15 children**.

> **(c)**

```c
if (fork() == 0)
    fork();
```

| Process | `fork()` returns | Forks again? |
|---|---|---|
| Parent | > 0 | ❌ |
| Child | **0** | ✅ creates one grandchild |

**Total = 3 processes.**

> **(d)**

```c
fork();
if (fork() == 0)
    printf("X\n");
```

First `fork()` ⇒ 2 processes. Each executes the second `fork()` ⇒ **4 processes**. Of those, the **two that are children of the second fork** print. **"X" is printed 2 times.**

> **(e)** What is printed?

```c
pid_t p = fork();
if (p == 0) printf("Child\n");
else        printf("Parent\n");
```

**One "Child" and one "Parent"** — in an **unpredictable order** (that is the point of the question).

---

# PART C — Semaphores

## Problem 11 — Semaphore arithmetic ⭐⭐⭐

$$S_{final} = S_{initial} - n_P + n_V$$

| # | Given | Working | Answer |
|---|---|---|---|
| (a) | $S = 10$, 6 `P`, 4 `V` | $10 - 6 + 4$ | **8** |
| (b) | $S = 7$, 20 `P`, 15 `V` | $7 - 20 + 15$ | **2** |
| (c) | $S = 3$, 8 `P`, 2 `V` | $3 - 8 + 2$ | **−3** ⇒ **3 processes blocked** |
| (d) | $S = 0$, 5 `V`, 5 `P` | $0 + 5 - 5$ | **0**, nobody blocked |

> ⭐ **If the final value is negative, its magnitude is the number of blocked processes.** If it is $\ge 0$, it is the number of free resource instances and **nobody is waiting**.

## Problem 12 — Producer–Consumer semaphore trace ⭐⭐⭐

> **Buffer size $n = 2$. Trace `mutex`, `empty`, `full` for: Producer inserts, Producer inserts, Producer tries to insert, Consumer removes.**

Initial: `mutex = 1`, `empty = 2`, `full = 0`.

| Step | Action | mutex | empty | full | Comment |
|---|---|---|---|---|---|
| 0 | initial | 1 | 2 | 0 | buffer empty |
| 1 | P: `wait(empty)` | 1 | **1** | 0 | |
| 2 | P: `wait(mutex)` | **0** | 1 | 0 | inside CS |
| 3 | P: insert, `signal(mutex)` | **1** | 1 | 0 | |
| 4 | P: `signal(full)` | 1 | 1 | **1** | 1 item in buffer |
| 5 | P: `wait(empty)` | 1 | **0** | 1 | |
| 6 | P: `wait(mutex)`, insert, `signal(mutex)` | 1 | 0 | 1 | |
| 7 | P: `signal(full)` | 1 | 0 | **2** | **buffer FULL** |
| 8 | P: `wait(empty)` | 1 | **−1** | 2 | ⚠️ **Producer BLOCKS** |
| 9 | C: `wait(full)` | 1 | −1 | **1** | |
| 10 | C: `wait(mutex)`, remove, `signal(mutex)` | 1 | −1 | 1 | |
| 11 | C: `signal(empty)` | 1 | **0** | 1 | ✅ **Producer WOKEN** |

---

# PART D — Deadlock

## Problem 13 — Banker's algorithm, safety ⭐⭐⭐

> **Resources: A = 10, B = 5, C = 7. Find Need, Available, and determine whether the state is safe.**

| Process | Allocation<br/>A B C | Max<br/>A B C |
|---|---|---|
| P0 | 1 1 2 | 4 3 3 |
| P1 | 2 1 2 | 3 2 2 |
| P2 | 4 0 1 | 9 0 2 |
| P3 | 0 2 0 | 7 5 3 |

**Step 1 — Available:**
$$\text{Allocated} = (1{+}2{+}4{+}0,\ 1{+}1{+}0{+}2,\ 2{+}2{+}1{+}0) = (7, 4, 5)$$
$$\textbf{Available} = (10,5,7) - (7,4,5) = \mathbf{(3, 1, 2)}$$

**Step 2 — Need = Max − Allocation:**

| Process | Need A B C |
|---|---|
| P0 | **3 2 1** |
| P1 | **1 1 0** |
| P2 | **5 0 1** |
| P3 | **7 3 3** |

**Step 3 — safety algorithm, Work = (3, 1, 2):**

| Iter | Try | Need | Work | OK? | New Work |
|---|---|---|---|---|---|
| 1 | P0 | 3 2 1 | 3 1 2 | ❌ (B: 2 > 1) | — |
| 1 | **P1** | 1 1 0 | 3 1 2 | ✅ | $(3,1,2)+(2,1,2) = (5,2,4)$ |
| 2 | **P2** | 5 0 1 | 5 2 4 | ✅ | $(5,2,4)+(4,0,1) = (9,2,5)$ |
| 3 | P3 | 7 3 3 | 9 2 5 | ❌ (B: 3 > 2) | — |
| 3 | **P0** | 3 2 1 | 9 2 5 | ✅ | $(9,2,5)+(1,1,2) = (10,3,7)$ |
| 4 | **P3** | 7 3 3 | 10 3 7 | ✅ | $(10,3,7)+(0,2,0) = (10,5,7)$ ✓ |

### ✅ **SAFE**, safe sequence $\boxed{\langle P_1, P_2, P_0, P_3 \rangle}$

## Problem 14 — Banker's, three requests ⭐⭐⭐

**(a) $P_0$ requests $(1, 0, 1)$**

| Check | Result |
|---|---|
| $(1,0,1) \le Need_0 = (3,2,1)$ | ✅ |
| $(1,0,1) \le Available = (3,1,2)$ | ✅ |

**Pretend:** Available = $(2,1,1)$, $Allocation_0 = (2,1,3)$, $Need_0 = (2,2,0)$.

| Try | Need | Work | OK? | New Work |
|---|---|---|---|---|
| P0 | 2 2 0 | 2 1 1 | ❌ | — |
| **P1** | 1 1 0 | 2 1 1 | ✅ | $(2,1,1)+(2,1,2) = (4,2,3)$ |
| P2 | 5 0 1 | 4 2 3 | ❌ | — |
| **P0** | 2 2 0 | 4 2 3 | ✅ | $(4,2,3)+(2,1,3) = (6,3,6)$ |
| **P2** | 5 0 1 | 6 3 6 | ✅ | $(6,3,6)+(4,0,1) = (10,3,7)$ |
| **P3** | 7 3 3 | 10 3 7 | ✅ | $(10,5,7)$ ✓ |

### ✅ **SAFE** ⇒ **GRANT**, safe sequence $\langle P_1, P_0, P_2, P_3 \rangle$

**(b) $P_2$ requests $(3, 0, 1)$**

$(3,0,1) \le Need_2 = (5,0,1)$ ✅ and $(3,0,1) \le Available = (3,1,2)$ ✅

**Pretend:** Available = $(0,1,1)$, $Allocation_2 = (7,0,2)$, $Need_2 = (2,0,0)$.

| Try | Need | $\le (0,1,1)$? |
|---|---|---|
| P0 | 3 2 1 | ❌ |
| P1 | 1 1 0 | ❌ (A: 1 > 0) |
| P2 | 2 0 0 | ❌ |
| P3 | 7 3 3 | ❌ |

### ❌ **UNSAFE** ⇒ **DENY — $P_2$ must wait**

**(c) $P_3$ requests $(0, 2, 0)$**

$(0,2,0) \le Need_3 = (7,3,3)$ ✅, but $(0,2,0) \le Available = (3,1,2)$? **B: $2 > 1$** ❌

### ⏸ **$P_3$ must WAIT — the resources are not currently available** (no safety check is even needed)

> ⭐ **Three different outcomes, three different reasons** — granted, unsafe, unavailable. Exam questions often ask all three in one part.

## Problem 15 — Deadlock detection ⭐⭐⭐

> **Resources: A = 7, B = 2, C = 6. Available = (0, 0, 0). Is the system deadlocked?**

| Process | Allocation | Request |
|---|---|---|
| P0 | 0 1 0 | 0 0 0 |
| P1 | 2 0 0 | 2 0 2 |
| P2 | 3 0 3 | 0 0 0 |
| P3 | 2 1 1 | 1 0 0 |
| P4 | 0 0 2 | 0 0 2 |

| Iter | Process | Request | Work | OK? | New Work |
|---|---|---|---|---|---|
| 1 | **P0** | 0 0 0 | 0 0 0 | ✅ | $(0,1,0)$ |
| 2 | **P2** | 0 0 0 | 0 1 0 | ✅ | $(3,1,3)$ |
| 3 | **P3** | 1 0 0 | 3 1 3 | ✅ | $(5,2,4)$ |
| 4 | **P1** | 2 0 2 | 5 2 4 | ✅ | $(7,2,4)$ |
| 5 | **P4** | 0 0 2 | 7 2 4 | ✅ | $(7,2,6)$ |

### ✅ **NOT deadlocked**, sequence $\langle P_0, P_2, P_3, P_1, P_4 \rangle$

**Now change $P_2$'s request to $(0, 0, 1)$:**

| Iter | Process | Request | Work | OK? |
|---|---|---|---|---|
| 1 | **P0** | 0 0 0 | (0,0,0) | ✅ → Work = (0,1,0) |
| 2 | P1 | 2 0 2 | (0,1,0) | ❌ |
| 2 | P2 | 0 0 1 | (0,1,0) | ❌ |
| 2 | P3 | 1 0 0 | (0,1,0) | ❌ |
| 2 | P4 | 0 0 2 | (0,1,0) | ❌ |

### ❌ **DEADLOCKED** — deadlocked set $\boxed{\{P_1, P_2, P_3, P_4\}}$

## Problem 16 — Resource Allocation Graph ⭐⭐

> **Is this system deadlocked? $R_1$ has 1 instance, $R_2$ has 1 instance.**
> Edges: $R_1 \rightarrow P_1$, $P_1 \rightarrow R_2$, $R_2 \rightarrow P_2$, $P_2 \rightarrow R_1$.

**Cycle:** $P_1 \rightarrow R_2 \rightarrow P_2 \rightarrow R_1 \rightarrow P_1$ — a cycle exists, and **every resource has a single instance**.

### ❌ **DEADLOCK** (single instances ⇒ cycle is sufficient)

> **Variation:** if $R_2$ had **two** instances and the second were held by a $P_3$ that is **not waiting for anything**, then $P_3$ would finish, release its instance of $R_2$ to $P_1$, and the chain would unwind — **no deadlock despite the cycle.**

---

## Problem 17 — Class examples from `Rati OS FULL.pdf` (re-computed) ⭐⭐⭐

| Page | Problem | Answer |
|---|---|---|
| p. 14 | **FCFS with overhead** δ = 1 (6 processes, ΣBT = 17, 6 switches) | CPU inefficiency = 6/23, **efficiency = 17/23 ≈ 73.9 %** |
| p. 17 | **Exponential average**, α = 0.5, τ₁ = 10, actual t = 4, 8, 6, 7 | τ₂ = 7, τ₃ = 7.5, τ₄ = 6.75, **τ₅ = 6.875** |
| p. 18 | **SRTF**, 6 processes (AT 0–5; BT 7, 5, 3, 1, 2, 1) | Σ WT = 24, **avg WT = 4** |
| p. 19 | 3 processes at t = 0 with total times 10, 20, 30; each 20 % I/O, 70 % CPU, 10 % I/O (FCFS) | CT 10, 25, 47; **avg WT ≈ 13.3**; CPU busy 42/47 = **89.36 %**, idle 10.64 % |
| p. 20 | **Preemptive priority** (higher number = higher priority) | avg WT 80/7 ≈ 11.43, avg RT 20/7 (see [Ch. 8](08-priority-scheduling.md)) |
| p. 21 | Priority with I/O (lower number = higher priority) | **avg WT = 18/3 = 6**, avg RT = 0, idle time 4 |
| p. 22 | **Round Robin**, q = 2 (AT 0, 1, 2, 3, 4, 6; BT 4, 5, 2, 1, 6, 3) | CT 8, 18, 6, 9, 21, 19 · **avg WT 44/6 = 7.33**, **avg RT 20/6 = 3.33** |
| p. 23 | Round Robin, q = 3 (AT 5, 4, 3, 1, 2, 6; BT 5, 6, 7, 9, 2, 3; CPU idle 0–1) | CT 32, 27, 33, 30, 6, 21 · **avg WT 96/6 = 16** · **avg RT 32/6 ≈ 5.33** ⚠️ |
| p. 24 | RR with context switch $s$: every process must get the CPU at least once every $t$ seconds | $n s + (n-1) q \le t \Rightarrow q \le \dfrac{t - ns}{n-1}$ |
| p. 24 | FCFS, A–D at t = 0 with BT $t, t+1, t+2, t+3$ | **avg WT = $\tfrac32 t + 1$**, avg TAT = $\tfrac52 t + \tfrac52$ |
| p. 25–26 | FCFS: a 5-cycle process every multiple of 10, a 7-cycle process every multiple of 11, from cycle 10; P wins ties; first 14 processes | **avg WT = 91/14 = 6.5**, **avg TAT = 175/14 = 12.5** |
| p. 52 | Counting semaphore = 10, then 6 P() and 4 V() | $10 - 6 + 4 =$ **8** |
| pp. 57–58 | Minimum resources to avoid deadlock | 3 × 2 → **4** · (7, 4, 9, 2, 5) → **22 / 23** (see [Ch. 19 §6½](19-deadlock-and-necessary-conditions.md)) |

> ✅ **Round Robin convention confirmed by the class example (p. 22):** a process that **arrives** at the same instant another is preempted joins the queue **before** the preempted one. Only that ordering reproduces the class answers (WT 44, RT 20). The opposite order gives WT 42, RT 24.
>
> ⚠️ p. 26 writes the average WT as "7.5". The table's own column total is 91, and 91/14 = **6.5**.
> ⚠️ p. 23 writes "avg response time = 22/6". The RT column in the same table (10, 5, 3, 0, 2, 12) sums to **32**, so the average is 32/6 ≈ **5.33**.

---

## ⚡ The formula sheet

$$TAT = CT - AT \qquad WT = TAT - BT \qquad RT = (\text{first CPU allocation}) - AT$$
$$\text{Total time} = \sum BT + (\text{switches})\times\delta + \text{idle} \qquad \text{CPU efficiency} = \frac{\sum BT}{\text{Total time}}$$
$$\text{FCFS/SJF switches} = n - 1 \qquad \text{RR switches} = (\text{dispatches}) - 1 \qquad \text{RR efficiency per slice} = \frac{q}{q+\delta}$$
$$\tau_{n+1} = \alpha t_n + (1-\alpha)\tau_n \qquad \text{(simple average: } \tau_{n+1} = \tfrac1n\textstyle\sum t_i)$$
$$n \text{ forks} \Rightarrow 2^n \text{ processes},\ 2^n - 1 \text{ children}$$
$$S_{final} = S_{initial} - n_P + n_V \qquad S < 0 \Rightarrow |S| \text{ processes blocked}$$
$$\texttt{mutex}=1,\ \texttt{empty}=n,\ \texttt{full}=0 \qquad \texttt{empty} + \texttt{full} = n$$
$$\textbf{Need} = \textbf{Max} - \textbf{Allocation} \qquad \text{Available}_j = \text{Total}_j - \sum_i \text{Allocation}[i][j]$$

---

**Previous:** [← 21. RAG, Detection & Recovery](21-rag-detection-and-recovery.md) · **Next (after-mid):** [23. Memory Management, Linker & Loader →](23-memory-management-linker-loader.md) · **Back to:** [OS index](../README.md)
