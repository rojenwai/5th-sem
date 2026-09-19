# 4. FCFS Scheduling (Gantt Chart, Overhead, Convoy Effect)

> ⚠️ **Written from standard course knowledge.** No class material was supplied for Operating Systems.
> **Syllabus:** *FCFS · Gantt chart · FCFS with overhead · Disadvantage of FCFS (convoy effect)*

---

## 🎯 In one line

**First Come First Served** runs processes in arrival order — the simplest algorithm, and the worst for average waiting time, because one long job at the front makes everyone behind it wait (**the convoy effect**).

---

## 1. The algorithm

> **Whichever process requests the CPU first gets the CPU first.**

| Property | Value |
|---|---|
| **Type** | **Non-preemptive** |
| **Data structure** | A simple **FIFO queue** |
| **Selection criterion** | Smallest **arrival time** |
| **Tie-break** | Lower process ID |

**How it runs:**
1. Sort the processes by arrival time.
2. Give the CPU to the first one and let it run to completion.
3. Repeat. If no process has arrived, the CPU **idles** until the next arrival.

```mermaid
graph LR
    A["New process"] -->|"enqueue at tail"| Q["READY QUEUE (FIFO)"]
    Q -->|"dequeue from head"| C["CPU — runs to completion"]
    C --> E["Terminated"]
    style A fill:#e8eaf6,stroke:#3f51b5,color:#1a237e
    style E fill:#e0f2f1,stroke:#00897b,color:#004d40
```

---

## 2. Worked Example 1 — basic FCFS ⭐⭐⭐

**The master process set:**

| Process | AT | BT |
|---|---|---|
| P1 | 0 | 5 |
| P2 | 1 | 3 |
| P3 | 2 | 8 |
| P4 | 3 | 6 |

**Step 1 — order by arrival:** P1 (0) → P2 (1) → P3 (2) → P4 (3).

**Step 2 — Gantt chart:**

```
 ┌──────────┬────────┬──────────────┬─────────────┐
 │    P1    │   P2   │      P3      │     P4      │
 └──────────┴────────┴──────────────┴─────────────┘
 0          5        8             16            22
```

**Step 3 — the table:**

| Process | AT | BT | CT | TAT = CT−AT | WT = TAT−BT |
|---|---|---|---|---|---|
| P1 | 0 | 5 | 5 | 5 | 0 |
| P2 | 1 | 3 | 8 | 7 | 4 |
| P3 | 2 | 8 | 16 | 14 | 6 |
| P4 | 3 | 6 | 22 | 19 | 13 |
| | | | | **45** | **23** |

$$\text{Average TAT} = \frac{45}{4} = \mathbf{11.25} \qquad \text{Average WT} = \frac{23}{4} = \mathbf{5.75}$$

**Verify:** chart length $22 = 5+3+8+6$ with no idle time ✓ · all $WT \ge 0$ ✓ · $RT = WT$ (non-preemptive) ✓

---

## 3. Worked Example 2 — FCFS with idle time ⭐⭐

A trap version: what if nothing has arrived yet?

| Process | AT | BT |
|---|---|---|
| P1 | 3 | 4 |
| P2 | 5 | 3 |
| P3 | 12 | 2 |

```
 ┌───────────┬────────┬──────┬────────┬────┐
 │   IDLE    │   P1   │  P2  │  IDLE  │ P3 │
 └───────────┴────────┴──────┴────────┴────┘
 0           3        7      10       12   14
```

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 3 | 4 | 7 | 4 | 0 |
| P2 | 5 | 3 | 10 | 5 | 2 |
| P3 | 12 | 2 | 14 | 2 | 0 |

$$\text{Avg TAT} = \frac{11}{3} = 3.67 \qquad \text{Avg WT} = \frac{2}{3} = 0.67$$

**CPU utilisation** $= \dfrac{\text{busy time}}{\text{total time}} = \dfrac{9}{14} = 64.3\%$

> ⚠️ **Do not compress the idle gaps.** P3 cannot start at 10 — it has not arrived. Forgetting this shifts every later completion time and loses most of the marks.

---

## 4. FCFS with Overhead (context-switch time) ⭐⭐⭐

Real switching is not free. If the question gives a **context switch time $\delta$** (also written as *s* or *overhead*), insert a $\delta$-wide block **between consecutive process blocks**.

**Process set with $\delta = 1$ ms:**

| Process | AT | BT |
|---|---|---|
| P1 | 0 | 4 |
| P2 | 1 | 3 |
| P3 | 2 | 5 |

### Without overhead (for comparison)

```
 ┌────────┬──────┬──────────┐
 │   P1   │  P2  │    P3    │
 └────────┴──────┴──────────┘
 0        4      7         12
```

| Process | CT | TAT | WT |
|---|---|---|---|
| P1 | 4 | 4 | 0 |
| P2 | 7 | 6 | 3 |
| P3 | 12 | 10 | 5 |

$$\text{Avg TAT} = \frac{20}{3} = 6.67 \qquad \text{Avg WT} = \frac{8}{3} = 2.67$$

### With overhead $\delta = 1$ ⭐

```
 ┌────────┬────┬──────┬────┬──────────┐
 │   P1   │ CS │  P2  │ CS │    P3    │
 └────────┴────┴──────┴────┴──────────┘
 0        4    5      8    9         14
```

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 0 | 4 | 4 | 4 | 0 |
| P2 | 1 | 3 | 8 | 7 | **4** |
| P3 | 2 | 5 | 14 | 12 | **7** |
| | | | | **23** | **11** |

$$\text{Avg TAT} = \frac{23}{3} = \mathbf{7.67} \qquad \text{Avg WT} = \frac{11}{3} = \mathbf{3.67}$$

### What the overhead cost us

| Metric | Without $\delta$ | With $\delta = 1$ | Change |
|---|---|---|---|
| Total time | 12 | **14** | +2 |
| Avg TAT | 6.67 | **7.67** | +1 |
| Avg WT | 2.67 | **3.67** | +1 |
| **CPU efficiency** | 100% | $\frac{12}{14} = \mathbf{85.7\%}$ | −14.3% |

**The formulas for overhead questions:** ⭐

$$\text{Number of context switches in FCFS} = n - 1 \quad (\text{for } n \text{ processes})$$
$$\text{Total overhead} = (n-1)\times\delta \qquad \text{Total time} = \sum BT + (n-1)\delta + \text{idle}$$
$$\boxed{\text{CPU efficiency} = \frac{\text{useful work}}{\text{useful work} + \text{overhead}} = \frac{\sum BT}{\sum BT + (n-1)\delta}}$$

> ⚠️ **Number of switches is a favourite trick.** FCFS needs only $n-1$ switches because each process runs **once**, to completion. **Round Robin** needs far more — once per quantum expiry — which is exactly why RR suffers most from overhead.

> 💡 Some textbooks also charge $\delta$ *before* the first process and *after* the last. Say which convention you use; the marking scheme accepts either if stated.

---

## 5. The Convoy Effect — FCFS's big disadvantage ⭐⭐⭐

> **Convoy effect:** when one **long (CPU-bound) process** holds the CPU, all the **short processes behind it are stuck waiting**, so average waiting time explodes — like a line of cars crawling behind one slow truck.

### The demonstration

Three processes, **all arriving at $t = 0$**:

| Process | BT |
|---|---|
| P1 | **100** |
| P2 | 1 |
| P3 | 1 |

**Case A — FCFS order P1, P2, P3 (the long job first):**

```
 ┌───────────────────────────────────────┬───┬───┐
 │                 P1                    │P2 │P3 │
 └───────────────────────────────────────┴───┴───┘
 0                                      100 101 102
```

| Process | CT | TAT | WT |
|---|---|---|---|
| P1 | 100 | 100 | 0 |
| P2 | 101 | 101 | **100** |
| P3 | 102 | 102 | **101** |

$$\text{Avg WT} = \frac{0+100+101}{3} = \mathbf{67.0} \qquad \text{Avg TAT} = \frac{303}{3} = \mathbf{101.0}$$

**Case B — the short jobs first (P2, P3, P1):**

```
 ┌───┬───┬───────────────────────────────────────┐
 │P2 │P3 │                 P1                    │
 └───┴───┴───────────────────────────────────────┘
 0   1   2                                      102
```

| Process | CT | TAT | WT |
|---|---|---|---|
| P2 | 1 | 1 | 0 |
| P3 | 2 | 2 | 1 |
| P1 | 102 | 102 | 2 |

$$\text{Avg WT} = \frac{0+1+2}{3} = \mathbf{1.0} \qquad \text{Avg TAT} = \frac{105}{3} = \mathbf{35.0}$$

> ⭐ **Same processes, same total work — average waiting time fell from 67 to 1.** That factor-of-67 gap *is* the convoy effect, and it is the motivation for the next chapter, **SJF**.

### The I/O version of the convoy effect ⭐

The effect is worse than the numbers suggest. In a real system:

1. One CPU-bound process holds the CPU for a long time.
2. All the I/O-bound processes finish their I/O and pile into the **ready queue**.
3. **The I/O devices sit idle** while they wait.
4. When the big process finally releases the CPU, the short ones rush through, do a tiny burst each, and all block on I/O again — leaving the **CPU** idle.

**Result: both the CPU and the devices are under-utilised.** This is the point worth writing for full marks.

---

## 6. Advantages and disadvantages ⭐⭐

| Advantages | Disadvantages |
|---|---|
| **Simplest** to understand and implement (a FIFO queue) | **High average waiting time** |
| **No starvation** — every process eventually reaches the front | **Convoy effect** |
| **Fair** in the arrival-order sense | **Non-preemptive** ⇒ bad for interactive/time-sharing systems |
| Low scheduling overhead — only $n-1$ switches | Poor **response time** for late arrivals |
| | Does not favour short or high-priority jobs |

> ⭐ **"Is FCFS free from starvation?"** → **Yes.** Waiting time is bounded because the queue always moves forward. But *no starvation* does **not** mean *low waiting time* — the convoy effect proves that.

---

## 7. Common exam questions

1. **Explain FCFS scheduling. Draw the Gantt chart and compute average TAT and WT for the given processes.** ⭐⭐⭐
2. **What is the convoy effect? Illustrate with an example.** ⭐⭐⭐
3. **Solve the given process set with FCFS including a context switch overhead of δ, and find CPU efficiency.** ⭐⭐⭐
4. **State the advantages and disadvantages of FCFS.** ⭐⭐
5. **Is FCFS preemptive or non-preemptive? Does it cause starvation?** ⭐⭐
6. **How many context switches does FCFS require for n processes?** → $n-1$. ⭐
7. **Why is FCFS unsuitable for a time-sharing system?** ⭐⭐

---

## ⚡ Quick revision

- **FCFS = non-preemptive, FIFO, selected by smallest arrival time.**
- Draw the chart in **arrival order**; show **idle gaps** when nothing has arrived.
- $TAT = CT - AT$, $WT = TAT - BT$; $RT = WT$ because it is non-preemptive.
- **With overhead:** insert a $\delta$ block between processes; $n-1$ switches; total $= \sum BT + (n-1)\delta$; efficiency $= \frac{\sum BT}{\sum BT + (n-1)\delta}$.
- **Convoy effect:** one long job at the head makes all short jobs wait ⇒ huge average WT; devices idle too.
- The 100/1/1 example: avg WT **67 → 1** just by reordering.
- **Advantages:** simple, fair, **no starvation**, least overhead.
- **Disadvantages:** high average WT, convoy effect, non-preemptive, poor response time.
- ⚠️ No starvation ≠ good waiting time.

---

**Previous:** [← 3. CPU Scheduling Terminology](03-cpu-scheduling-terminology.md) · **Next:** [5. SJF Scheduling →](05-sjf-scheduling.md)
