# 29. Disk Structure & Disk Scheduling

> ✅ **From the class notes** (`Rati OS FULL.pdf`, pp. 95–99). All six head-movement totals were recomputed and match the notes.
> **Syllabus:** *After-mid: hard disk structure (platter, track, sector), seek time, rotational latency, disk scheduling (FCFS, SSTF, SCAN, LOOK, C-SCAN, C-LOOK)*

---

## 🎯 In one line

A disk read is slow mainly because the **read/write head must move to the right track** (seek time). **Disk scheduling** orders the pending requests to **minimise total head movement**.

---

## 1. Hard disk structure (p. 95) ⭐⭐

- A hard disk is a **collection of multiple platters**, and **data is stored on both sides** of each platter.
- **Track:** a **concentric circular path** on the surface of a platter.
- **Sector:** a **segment of a track**. The **standard sector size is 512 B**. Sectors are loosely packed in outer tracks and tightly packed in inner ones, but **every sector stores the same amount of data**, and the same applies to every track.
- **Cylinder:** the same track on all platters.
- **Read/write head:** one per surface. To read or write data, the R/W head moves to the desired sector.

```
         ┌─────── track (concentric circle)
     ╭───┼────╮
   ╭─┼─╮ │    │      ◄── platter (both surfaces used)
   │ ● │ │    │
   ╰───╯ │    │      ◄── sector = arc segment of a track
     ╰───┴────╯
          ▲
      R/W head on an arm
```

### Access-time components ⭐⭐⭐

| Term | Definition |
|---|---|
| **Seek time** | Time to move the head from its current **track** to the **desired track** |
| **Rotational latency** (rotational delay) | Time for the **desired sector** to rotate under the R/W head |
| **Transfer time** | Time to actually read or write the data |
| **RPM** | Rotations per minute. **60 RPM = 1 rotation per second** |

$$\text{Access time} = \text{seek time} + \text{rotational latency} + \text{transfer time}$$
$$\text{One rotation} = \frac{60}{\text{RPM}} \text{ s} \qquad \text{Average rotational latency} = \frac{1}{2}\times\frac{60}{\text{RPM}} \text{ s}$$

*Example:* at 7200 RPM one rotation takes 60/7200 s = 8.33 ms, so the average latency is **4.17 ms**.

**Disk scheduling** aims to **minimise the seek time**, i.e. the total head movement.

---

## 2. The class problem (p. 96)

> A disk has **200 tracks (0–199)**. The request queue is **82, 170, 43, 140, 24, 16, 190**. The head is currently at **50**. Calculate the total track movement by the R/W head. If moving between adjacent tracks takes **1 ns**, what is the total time?

Sorted: 16, 24, 43, | **50** |, 82, 140, 170, 190.

---

## 3. FCFS: First Come First Served (p. 96)

Requests are **processed in the order they arrive** in the queue.

$$50 \to 82 \to 170 \to 43 \to 140 \to 24 \to 16 \to 190$$
$$(82-50) + (170-82) + (170-43) + (140-43) + (140-24) + (24-16) + (190-16)$$
$$= 32 + 88 + 127 + 97 + 116 + 8 + 174 = \boxed{642} \quad\Rightarrow\quad \text{time} = 642 \text{ ns}$$

*(The notes group this as 120 + 127 + 97 + 124 + 174 = 642.)* Fair but wild zig-zags.

---

## 4. SSTF: Shortest Seek Time First (p. 97)

**Select the request closest to the current position.**

$$50 \to 43 \to 24 \to 16 \to 82 \to 140 \to 170 \to 190$$
$$= (50 - 16) + (190 - 16) = 34 + 174 = \boxed{208} \quad (208 \text{ ns})$$

Much better, but requests far from the head can **starve** if near requests keep arriving.

---

## 5. SCAN: the elevator algorithm (p. 97)

The **disk arm moves in one direction serving all pending requests along the way**. When it reaches the **last track** in that direction, it **reverses** and continues serving. *(The direction of initial movement is given as a hint: here, towards **higher** numbers.)*

$$50 \to 82 \to 140 \to 170 \to 190 \to \mathbf{199} \to 43 \to 24 \to 16$$
$$= (199 - 50) + (199 - 16) = 149 + 183 = \boxed{332}$$

---

## 6. LOOK (p. 98)

Similar to SCAN, but it **turns back at the last request** instead of going to the end of the disk.

$$50 \to 82 \to 140 \to 170 \to \mathbf{190} \to 43 \to 24 \to 16$$
$$= (190 - 50) + (190 - 16) = 140 + 174 = \boxed{314}$$

---

## 7. C-SCAN: Circular SCAN (p. 98)

The disk arm moves in **one direction only**, serving all requests along the way. When it reaches the end, it **quickly returns to the beginning without servicing any request** and starts the same process again.

$$50 \to 82 \to 140 \to 170 \to 190 \to \mathbf{199} \Rightarrow \mathbf{0} \to 16 \to 24 \to 43$$
$$= (199 - 50) + (199 - 0) + 43 = 149 + 199 + 43 = \boxed{391}$$

*(The class counts the 199 → 0 return. Some books exclude it, which would give 192, so state your assumption.)*

---

## 8. C-LOOK (p. 99)

Instead of going to the end, it **returns from the last request to the first request** (on the other side).

$$50 \to 82 \to 140 \to 170 \to \mathbf{190} \Rightarrow \mathbf{16} \to 24 \to 43$$
$$= (190 - 50) + (190 - 16) + (43 - 16) = 140 + 174 + 27 = \boxed{341}$$

---

## 9. Summary ⭐⭐⭐

| Algorithm | Order served (head at 50, moving up) | Total movement | Time (1 ns/track) |
|---|---|---|---|
| FCFS | 82, 170, 43, 140, 24, 16, 190 | **642** | 642 ns |
| SSTF | 43, 24, 16, 82, 140, 170, 190 | **208** | 208 ns |
| SCAN | 82, 140, 170, 190, (199), 43, 24, 16 | **332** | 332 ns |
| LOOK | 82, 140, 170, 190, 43, 24, 16 | **314** | 314 ns |
| C-SCAN | 82, 140, 170, 190, (199 → 0), 16, 24, 43 | **391** | 391 ns |
| C-LOOK | 82, 140, 170, 190, (→ 16), 24, 43 | **341** | 341 ns |

| Algorithm | Advantage | Disadvantage |
|---|---|---|
| FCFS | Simple, fair, no starvation | Large total seek |
| SSTF | Low seek time | **Starvation** of far requests |
| SCAN | No starvation, good throughput | Goes to the disk end needlessly. Uneven wait for edge tracks |
| LOOK | Like SCAN without the useless trip to the end | Slightly more logic |
| C-SCAN | **Uniform waiting time** | Long return trip |
| C-LOOK | Uniform waiting time and a shorter return | – |

---

## 10. Common exam questions

1. **Explain the structure of a hard disk: platter, track, sector, cylinder.** See §1.
2. **Define seek time and rotational latency.** See §1.
3. **For the given request queue and head position, compute the total head movement with FCFS / SSTF / SCAN / LOOK / C-SCAN / C-LOOK.** See §3–§9. *This is a guaranteed numerical.*
4. **Which algorithm can cause starvation? Which gives uniform waiting time?** SSTF and C-SCAN/C-LOOK respectively (§9).
5. **Difference between SCAN and LOOK / C-SCAN and C-LOOK.** See §5–§8.

---

## ⚡ Quick revision

- Disk = platters → tracks (circles) → sectors (512 B). Access = **seek + rotational latency + transfer**.
- Avg latency = ½ × 60/RPM.
- **FCFS** in arrival order · **SSTF** nearest first · **SCAN** to the end then back · **LOOK** to the last request then back · **C-SCAN** to the end, jump to 0, continue up · **C-LOOK** to the last request, jump to the lowest request, continue up.
- Class answers (head 50, up): **642 · 208 · 332 · 314 · 391 · 341**.

---

**Previous:** [← 28. Effective Access Time & TLB](28-effective-access-time-tlb.md) · **Next:** [30. End-Sem Numerical Problem Bank →](30-end-sem-numerical-problem-bank.md)
