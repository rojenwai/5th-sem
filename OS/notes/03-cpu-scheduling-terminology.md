# 3. CPU Scheduling — Parameters & Terminology

> ⚠️ **Written from standard course knowledge.** No class material was supplied for Operating Systems.
> **Syllabus:** *CPU scheduling — important parameters and terminologies*

---

## 🎯 In one line

Every scheduling numerical in the exam reduces to two formulas — $TAT = CT - AT$ and $WT = TAT - BT$ — applied to a Gantt chart.

---

## 1. Why schedule at all?

A process alternates between **CPU bursts** and **I/O bursts**:

```
   CPU burst   I/O burst   CPU burst   I/O burst   CPU burst
  ┌─────────┐ ┌─────────┐ ┌────────┐ ┌─────────┐ ┌────────┐
  │ compute │→│  wait   │→│compute │→│  wait   │→│compute │→ exit
  └─────────┘ └─────────┘ └────────┘ └─────────┘ └────────┘
```

Whenever the running process leaves the CPU, **somebody must choose who goes next**. That choice is **CPU scheduling**, and the chooser is the **short-term scheduler**.

> ⭐ **"Burst time" always means the length of one CPU burst**, never the I/O time, unless the question says otherwise.

---

## 2. The parameters ⭐⭐⭐

| Symbol | Term | Definition |
|---|---|---|
| **AT** | **Arrival Time** | The instant the process enters the **ready queue** |
| **BT** | **Burst Time** (service/execution time) | The CPU time the process **needs** |
| **CT** | **Completion Time** | The instant the process **finishes** |
| **TAT** | **Turnaround Time** | **Total time spent in the system** = from arrival to completion |
| **WT** | **Waiting Time** | Time spent **sitting in the ready queue**, doing nothing |
| **RT** | **Response Time** | From arrival until the process gets the CPU for the **first time** |

### The formulas to memorise ⭐⭐⭐

$$\boxed{TAT = CT - AT} \qquad \boxed{WT = TAT - BT = CT - AT - BT}$$

$$\boxed{RT = \text{(time of first CPU allocation)} - AT}$$

$$\text{Average TAT} = \frac{\sum TAT_i}{n} \qquad \text{Average WT} = \frac{\sum WT_i}{n}$$

> ⭐ **The intuition behind $WT = TAT - BT$:** total time in the system, minus the part you were actually being served, is the part you were waiting.

> ⚠️ **RT ≠ WT.** Response time stops at the **first** CPU allocation; waiting time counts **every** stretch in the ready queue. In a **non-preemptive** algorithm a process runs to completion once started, so $RT = WT$. In a **preemptive** one (RR, SRTF) $RT \le WT$, usually strictly less.

### Three more, for the "criteria" question

| Term | Definition | Want it |
|---|---|---|
| **CPU utilisation** | % of time the CPU is busy doing useful work | **Maximum** (40–90% in real systems) |
| **Throughput** | Number of processes **completed per unit time** | **Maximum** |
| **Fairness** | Every process gets a reasonable share; nobody starves | **Yes** |

> ⭐ **Scheduling criteria (a standard 5-mark question):** *maximise* CPU utilisation and throughput; *minimise* turnaround time, waiting time and response time.

> ⚠️ These goals **conflict**. Maximising throughput favours short jobs (SJF), which starves long ones; minimising response time favours frequent switching (RR), which costs overhead and raises turnaround time. **No algorithm wins on every metric** — say this explicitly in an answer.

---

## 3. Preemptive vs Non-preemptive ⭐⭐⭐

Scheduling decisions occur at four moments:

| # | Situation | Transition |
|---|---|---|
| **1** | Process **blocks** for I/O | Running → Waiting |
| **2** | Process is **preempted** (quantum over, higher priority arrives) | Running → Ready |
| **3** | I/O **completes** for a waiting process | Waiting → Ready |
| **4** | Process **terminates** | Running → Terminated |

> ⭐ **Scheduling at only 1 and 4 is NON-PREEMPTIVE.** (The CPU is given up voluntarily.)
> **Scheduling at 2 and 3 as well is PREEMPTIVE.**

| | **Non-preemptive** | **Preemptive** |
|---|---|---|
| **CPU released** | Only **voluntarily** (block or exit) | Can be **taken away** by the OS |
| **Needs** | Nothing special | A **timer interrupt** |
| **Overhead** | Low | **Higher** (more context switches) |
| **Response time** | Poor | **Good** |
| **Starvation** | Long jobs cause it for short ones | Long jobs may themselves starve |
| **Data consistency** | Safe | Risk of **race conditions** → needs synchronisation |
| **Examples** | FCFS, SJF, non-preemptive Priority | **SRTF, Round Robin, preemptive Priority** |

---

## 4. The Gantt chart ⭐⭐⭐

A **Gantt chart** is a timeline showing which process occupies the CPU during each interval. Every scheduling numerical starts with one.

```
 ┌──────────┬────────┬──────────────┬─────────────┐
 │    P1    │   P2   │      P3      │     P4      │
 └──────────┴────────┴──────────────┴─────────────┘
 0          5        8             16            22
```

**Rules for drawing one:**

| Rule | Detail |
|---|---|
| 1 | The chart starts at the **earliest arrival time** (usually 0) |
| 2 | Each block is labelled with the process and bounded by **start** and **end** instants |
| 3 | **Idle CPU** must be shown as a gap/blank block — do not silently skip time |
| 4 | Total length = $\sum BT$ **+ idle time + context-switch overhead** (if the question gives one) |
| 5 | **CT of a process = the right-hand edge of its LAST block** |

> ⚠️ **The single most common Gantt mistake:** if no process has arrived yet, the CPU is **idle** — the chart must show that gap. E.g. if the first arrival is at $t=2$, the chart starts with an idle block $0\text{–}2$.

---

## 5. Worked example — reading a Gantt chart ⭐⭐

**The master process set** used throughout these notes:

| Process | AT | BT |
|---|---|---|
| P1 | 0 | 5 |
| P2 | 1 | 3 |
| P3 | 2 | 8 |
| P4 | 3 | 6 |

Suppose the scheduler produced this chart (this is FCFS):

```
 ┌──────────┬────────┬──────────────┬─────────────┐
 │    P1    │   P2   │      P3      │     P4      │
 └──────────┴────────┴──────────────┴─────────────┘
 0          5        8             16            22
```

**Step 1 — read CT off the chart's right edges:**

$$CT_{P1}=5,\quad CT_{P2}=8,\quad CT_{P3}=16,\quad CT_{P4}=22$$

**Step 2 — $TAT = CT - AT$:**

$$TAT_{P1}=5-0=5,\quad TAT_{P2}=8-1=7,\quad TAT_{P3}=16-2=14,\quad TAT_{P4}=22-3=19$$

**Step 3 — $WT = TAT - BT$:**

$$WT_{P1}=5-5=0,\quad WT_{P2}=7-3=4,\quad WT_{P3}=14-8=6,\quad WT_{P4}=19-6=13$$

**Step 4 — the answer table (always present it like this):**

| Process | AT | BT | CT | TAT = CT−AT | WT = TAT−BT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 5 | 5 | 5 | 0 | 0 |
| P2 | 1 | 3 | 8 | 7 | 4 | 4 |
| P3 | 2 | 8 | 16 | 14 | 6 | 6 |
| P4 | 3 | 6 | 22 | 19 | 13 | 13 |
| | | | | **Σ = 45** | **Σ = 23** | |

$$\text{Average TAT} = \frac{45}{4} = \mathbf{11.25}\ \text{ms} \qquad \text{Average WT} = \frac{23}{4} = \mathbf{5.75}\ \text{ms}$$

**Sanity checks that catch most errors:** ✅

- Chart length $22$ = $\sum BT = 5+3+8+6 = 22$, and there is no idle time ✓
- Every $WT \ge 0$ — a negative waiting time means the chart is wrong ✓
- $RT = WT$ for all four, which is correct because FCFS is **non-preemptive** ✓

---

## 6. Tie-breaking conventions ⭐

Exam answers differ only because conventions differ. **State the one you use** at the top of your answer.

| Tie | Convention used in these notes |
|---|---|
| Two processes have the **same burst time** (SJF/SRTF) | The one with the **smaller arrival time** wins; if still tied, the **smaller process ID** |
| A running process's remaining time **equals** a new arrival's burst (SRTF) | **Do not preempt** — switching costs overhead for no gain |
| Same priority | **FCFS** among them |
| A process arrives at the **exact instant** another is preempted (RR) | The **new arrival is queued first**, then the preempted process |

---

## 7. Common exam questions

1. **Define arrival time, burst time, completion time, turnaround time, waiting time and response time.** ⭐⭐⭐
2. **Write the formulas for TAT and WT.** ⭐⭐⭐
3. **Differentiate preemptive and non-preemptive scheduling.** ⭐⭐⭐
4. **List the CPU scheduling criteria. Which are maximised and which minimised?** ⭐⭐
5. **Differentiate waiting time and response time.** ⭐⭐
6. **What is a Gantt chart? Draw one for the given set of processes.** ⭐⭐⭐
7. **What is the difference between CPU-bound and I/O-bound processes?** ⭐

---

## ⚡ Quick revision

- $\ \boxed{TAT = CT - AT}\ $ and $\ \boxed{WT = TAT - BT}\ $ — everything else follows.
- **RT** = first CPU allocation − AT. **Non-preemptive ⇒ RT = WT.**
- **Maximise:** CPU utilisation, throughput. **Minimise:** TAT, WT, RT.
- **Non-preemptive** = scheduling only on **block** or **exit**; **preemptive** adds **timeout** and **I/O completion**.
- Preemptive: better response, more overhead, needs a timer, risks race conditions.
- **Gantt chart:** show **idle gaps**; CT = right edge of the process's **last** block.
- Chart length = $\sum BT$ + idle + overhead. Use it as a check.
- Every $WT \ge 0$ — a negative value means you misread the chart.
- **State your tie-breaking convention** before you start.

---

**Previous:** [← 2. Process & Process States](02-process-and-process-states.md) · **Next:** [4. FCFS Scheduling →](04-fcfs-scheduling.md)
