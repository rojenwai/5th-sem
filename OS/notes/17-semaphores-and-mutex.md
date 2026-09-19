# 17. Semaphores & Mutex

> ⚠️ **Written from standard course knowledge.** No class material was supplied for Operating Systems.
> **Syllabus:** *Semaphore · Types (binary, counting) · Working mechanism · Two operations · Counting semaphore · Binary semaphore · Mutex*

---

## 🎯 In one line

A **semaphore is an integer variable accessed only through two atomic operations — `wait()` and `signal()`** — that blocks a process instead of making it spin, which is why it solves both the mutual-exclusion problem and the lost-wakeup problem.

---

## 1. Definition ⭐⭐⭐

> **A semaphore S is an integer variable that, apart from initialisation, is accessed only through two standard ATOMIC operations: `wait(S)` and `signal(S)`.**

Invented by **Edsger Dijkstra**, which is why the operations also carry Dutch names:

| Operation | Other names | Meaning |
|---|---|---|
| **`wait(S)`** | **`P(S)`** (*proberen* — to test), `down(S)`, acquire | **Decrement**; block if the result would be negative |
| **`signal(S)`** | **`V(S)`** (*verhogen* — to increment), `up(S)`, release | **Increment**; wake a blocked process if any |

> ⭐ **The word "atomic" is doing all the work.** `wait()` and `signal()` must execute **indivisibly** — no two processes may be inside them at the same time. Without atomicity a semaphore is just another broken lock variable.

---

## 2. The two operations ⭐⭐⭐

### 2.1 The simple (busy-waiting) definition

```c
wait(S) {                   signal(S) {
    while (S <= 0)              S++;
        ;   /* spin */      }
    S--;
}
```

This is correct but **spins** — a **spinlock**. Fine for very short critical sections, wasteful otherwise.

### 2.2 The real (blocking / no-busy-waiting) definition ⭐⭐⭐

Each semaphore carries **an integer value and a queue of waiting processes**:

```c
typedef struct {
    int value;                 /* the count                      */
    struct process *list;      /* queue of blocked processes  ⭐ */
} semaphore;
```

```c
wait(semaphore *S) {                    signal(semaphore *S) {
    S->value--;                             S->value++;
    if (S->value < 0) {                     if (S->value <= 0) {
        add this process to S->list;            remove a process P
        block();          /* sleep */               from S->list;
    }                                           wakeup(P);
}                                           }
                                        }
```

| Step in `wait()` | Meaning |
|---|---|
| `S->value--` | Claim a unit of the resource |
| `if (S->value < 0)` | There wasn't one available… |
| `block()` | …so **put myself to sleep** in the semaphore's queue (state → **Waiting**) |

| Step in `signal()` | Meaning |
|---|---|
| `S->value++` | Return a unit |
| `if (S->value <= 0)` | Someone is blocked waiting for it… |
| `wakeup(P)` | …so **move one process** from the queue to **Ready** |

> ⭐⭐⭐ **The interpretation of a NEGATIVE value — a guaranteed exam question:**
> $$\boxed{\text{If } S < 0, \text{ then } |S| \text{ is the number of processes currently BLOCKED on } S}$$
> If $S = -3$, **three processes are waiting** in its queue. If $S \ge 0$, **no process is waiting** and $S$ is the number of units still available.

> ⭐ **Why this version cannot lose a wakeup:** the **count remembers** that a `signal()` happened even if nobody was asleep yet, and the whole operation is atomic. Compare with plain [`sleep()`/`wakeup()`](15-synchronization-mechanisms.md), where the signal simply vanishes.

### How atomicity of `wait`/`signal` is achieved

| System | Method |
|---|---|
| **Uniprocessor** | Briefly **disable interrupts** inside `wait()`/`signal()` — the section is only a few instructions long |
| **Multiprocessor** | A **spinlock** (built on `TestAndSet`/`compare_and_swap`) guards the semaphore's own code |

> ⚠️ **Busy waiting has not disappeared — it has been MOVED.** Instead of spinning for the whole critical section (which may be long), processes spin only for the few instructions of `wait()`/`signal()`. **That is the real achievement.** Write this sentence; it shows you understand the mechanism rather than reciting it.

---

## 3. Types of semaphore ⭐⭐⭐

| | **Counting semaphore** | **Binary semaphore** |
|---|---|---|
| **Range of values** | **Any non-negative integer** (0, 1, 2, … and negative while processes wait) | **0 or 1 only** |
| **Initialised to** | The **number of available instances** of the resource | **1** (for mutual exclusion) |
| **Used for** | Controlling access to a resource with **$N$ identical instances** | **Mutual exclusion** — one process at a time |
| **Also called** | — | **Mutex lock** (loosely — see §5) |
| **Example** | 5 printers ⇒ `S = 5` | A shared variable ⇒ `S = 1` |

### Counting semaphore — worked example ⭐⭐

**Five printers, `S = 5`:**

| Event | `S` after | Meaning |
|---|---|---|
| Start | **5** | 5 printers free |
| P1 `wait(S)` | 4 | P1 printing; 4 free |
| P2, P3, P4, P5 each `wait(S)` | **0** | All 5 busy, none free |
| P6 `wait(S)` | **−1** | ⚠️ P6 is **blocked**; 1 process waiting |
| P7 `wait(S)` | **−2** | 2 processes waiting |
| P1 `signal(S)` | **−1** | P1 finished; **P6 is woken** and takes the printer |
| P2 `signal(S)` | **0** | P7 is woken |

### The standard numerical ⭐⭐⭐

> **A counting semaphore is initialised to 10. Then 6 `P` operations and 4 `V` operations are performed. What is the final value?**

$$S_{final} = S_{initial} - (\text{number of } P) + (\text{number of } V) = 10 - 6 + 4 = \mathbf{8}$$

> **Variant:** initialised to 7, with 20 `P` and 15 `V`: $7 - 20 + 15 = \mathbf{2}$.
> **Variant:** initialised to 3, with 8 `P` and 2 `V`: $3 - 8 + 2 = \mathbf{-3}$ ⇒ **3 processes are blocked.**

$$\boxed{S_{final} = S_{initial} - n_P + n_V}$$

> ⚠️ **Careful with the question's wording.** This formula assumes the `P`s that would block are counted anyway (the textbook convention). If the question says "*successful* P operations", blocked ones do not decrement further — read it twice.

### Binary semaphore for mutual exclusion ⭐⭐⭐

```c
semaphore mutex = 1;          /* shared, initialised to 1 */

do {
    wait(mutex);              /* ENTRY  */

        /* CRITICAL SECTION */

    signal(mutex);            /* EXIT   */

        /* REMAINDER SECTION */
} while (true);
```

**Trace with two processes:**

| Step | Action | `mutex` | Who is inside |
|---|---|---|---|
| 0 | initial | **1** | — |
| 1 | P1 `wait(mutex)` | **0** | **P1** |
| 2 | P2 `wait(mutex)` → value −1 ⇒ **blocks** | **−1** | P1 (P2 waiting) |
| 3 | P1 `signal(mutex)` → wakes P2 | **0** | **P2** |
| 4 | P2 `signal(mutex)` | **1** | — |

✅ **Mutual exclusion holds at every step.**

---

## 4. The second use: enforcing execution ORDER ⭐⭐

Semaphores are not only for mutual exclusion — they also force one statement to happen **before** another.

**Problem:** P2's statement `S2` must execute **after** P1's statement `S1`.

```c
semaphore sync = 0;          /* ⭐ initialised to ZERO */

/* Process P1 */             /* Process P2 */
    S1;                          wait(sync);      /* blocks until P1 signals */
    signal(sync);                S2;
```

If P2 runs first, `wait(sync)` makes `sync = −1` and P2 **blocks**. When P1 finishes `S1` and signals, `sync` becomes 0 and P2 is woken. **`S1` always precedes `S2`.**

> ⭐ **The rule of thumb:** *initialise to 1 for mutual exclusion; initialise to 0 for ordering/signalling; initialise to N for N resource instances.*

---

## 5. Mutex vs Binary Semaphore ⭐⭐⭐

They look identical (both are 0/1), but they differ in **ownership**.

| | **Mutex (mutual exclusion lock)** | **Binary semaphore** |
|---|---|---|
| **Purpose** | **Locking** — protect a critical section | **Signalling** — coordinate between processes |
| **Ownership** ⭐ | **Owned** — only the thread that **locked** it may unlock it | **Not owned** — **any** process may `signal()` it |
| **Operations** | `lock()` / `unlock()` (acquire/release) | `wait()` / `signal()` |
| **Value** | Locked / unlocked | 0 or 1 |
| **Can it signal an event?** | ❌ No | ✅ **Yes** — the ordering use in §4 |
| **Priority inheritance** | ✅ Usually supported (fixes priority inversion) | ❌ Usually not |
| **Analogy** | A **toilet key** — whoever took it must return it | A **traffic light** — anyone can turn it green |

> ⭐ **The one-line distinction to write:** *"A mutex has ownership — only the locking thread can unlock it — whereas a binary semaphore has no owner and can be signalled by any process. Hence a mutex is a locking mechanism and a semaphore is a signalling mechanism."*

---

## 6. Advantages, disadvantages and pitfalls ⭐⭐⭐

| Advantages | Disadvantages |
|---|---|
| **No busy waiting** — blocked processes use no CPU | ⚠️ **Deadlock** is easy to create by wrong ordering |
| **No lost wakeups** — the count remembers signals | ⚠️ **Starvation** if the waiting queue is LIFO |
| Works for **N instances**, not just one | ⚠️ **Programmer error is fatal and silent** |
| Machine-independent (unlike TSL) | ⚠️ **Priority inversion** is still possible |
| Simple and flexible | Hard to debug; no compiler help |

### ⚠️ The three classic programming errors ⭐⭐⭐

| Error | Code | Result |
|---|---|---|
| **1. Swapped operations** | `signal(mutex); CS; wait(mutex);` | ❌ **Mutual exclusion violated** — several processes enter at once |
| **2. Both `wait`s** | `wait(mutex); CS; wait(mutex);` | ❌ **Deadlock** — the process blocks on its own lock |
| **3. Omitted `signal`** | `wait(mutex); CS;` *(no signal)* | ❌ **Deadlock** — every other process waits forever |

### Deadlock with two semaphores ⭐⭐⭐

```c
    /* P0 */                        /* P1 */
    wait(S);                        wait(Q);       ⚠️ opposite order
    wait(Q);                        wait(S);
       ...                             ...
    signal(S);                      signal(Q);
    signal(Q);                      signal(S);
```

If P0 completes `wait(S)` and P1 completes `wait(Q)`, then **P0 waits for Q (held by P1) and P1 waits for S (held by P0) — deadlock.**

> ⭐ **The fix is an ordering discipline:** *every process must acquire semaphores in the same global order.* This is exactly the **circular-wait prevention** technique of [chapter 19](19-deadlock-and-necessary-conditions.md).

---

## 7. Common exam questions

1. **Define a semaphore. Explain `wait()` and `signal()` with their implementation.** ⭐⭐⭐
2. **Differentiate binary and counting semaphores.** ⭐⭐⭐
3. **Differentiate mutex and binary semaphore.** ⭐⭐⭐
4. **What does a negative semaphore value mean?** ⭐⭐⭐
5. **A semaphore initialised to X undergoes m P and n V operations — find the final value.** ⭐⭐⭐
6. **How does a semaphore avoid busy waiting? Does it eliminate it completely?** ⭐⭐⭐
7. **Show how semaphores can enforce that S1 executes before S2.** ⭐⭐
8. **What problems can arise from incorrect use of semaphores?** ⭐⭐⭐
9. **Why must `wait()` and `signal()` be atomic?** ⭐⭐

---

## ⚡ Quick revision

- **Semaphore = an integer accessed only by two ATOMIC operations**: **`wait()` = `P` = `down`** and **`signal()` = `V` = `up`**. Invented by **Dijkstra**.
- **Blocking version:** `wait`: `value--`, if `< 0` **block**. `signal`: `value++`, if `<= 0` **wake one**.
- ⭐ **$S < 0$ ⇒ $|S|$ processes are blocked.** $S \ge 0$ ⇒ $S$ units are free, nobody waiting.
- **Counting semaphore** = any value, for **N instances**. **Binary semaphore** = 0/1, for **mutual exclusion**.
- **Initialise: 1 = mutual exclusion · 0 = ordering/signalling · N = N resources.**
- **Numerical:** $S_{final} = S_{initial} - n_P + n_V$.
- **Mutex vs binary semaphore = OWNERSHIP.** Only the locker unlocks a mutex; anyone can signal a semaphore. **Mutex = locking, semaphore = signalling.**
- **Busy waiting is not eliminated, only shortened** — processes spin for the few instructions of `wait`/`signal`, not for the whole critical section.
- **Semaphores never lose a wakeup** because the count remembers the signal.
- ⚠️ **Errors:** swapped `signal`/`wait` ⇒ no mutual exclusion · two `wait`s or a missing `signal` ⇒ **deadlock** · reversed acquisition order between two semaphores ⇒ **deadlock**. Fix: **acquire in a global order**.

---

**Previous:** [← 16. Producer–Consumer Problem](16-producer-consumer-problem.md) · **Next:** [18. Producer–Consumer Using Semaphores →](18-producer-consumer-using-semaphores.md)
