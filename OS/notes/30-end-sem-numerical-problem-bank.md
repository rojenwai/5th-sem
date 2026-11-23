# 30. End-Sem Numerical Problem Bank (After-Mid) ⭐

> ✅ **Part A** collects every after-mid numerical from the class notes (`Rati OS FULL.pdf`, pp. 65–99). **Part B** adds fresh practice problems of the same types. **Every answer in this chapter was computed by simulation or formula check.**

---

## 🎯 How to use this chapter

Cover the answer column and redo each problem. The full working is in the chapter linked in each row. Part B problems have **no worked solutions**, only the final answers, so you can check yourself.

---

## Part A: class problems (answers to memorise)

### Memory, linking, contiguous allocation ([Ch. 23](23-memory-management-linker-loader.md), [Ch. 24](24-contiguous-allocation-and-fit-algorithms.md))

| # | Problem | Answer |
|---|---|---|
| A1 | Which system software must always reside in main memory? | **Loader** |
| A2 | Blocks 200, 400, 300, 600; processes 300, 200, 200, 500 | FF ✅ all · NF ❌ P4 · BF ✅ all · WF ❌ P4 |
| A3 | Holes 150K, 350K; requests 300K, 25K, 125K, 50K | **FF but not BF** |
| A4 | BF with fixed partitions 4K/8K/20K/2K and 7 jobs | 20K job runs 11–**19** |
| A5 | Holes 20, 4, 25, 18, 7, 9, 15, 12; BF for 16, 9. Holes < 8 KB? | **3** (4, 2, 7) |
| A6 | Holes 21, 5, 25, 20, 7, 19, 15, 14; BF 16, 9, 3 then WF 10, 5 | Final holes **16, 5, 15, 20, 7, 15, 5** |
| A7 | Base = 1000, limit = 200. Logical 150? Logical 250? | **1150** · **trap** |

### Paging ([Ch. 25](25-paging-and-address-translation.md), [Ch. 26](26-page-table-entry-and-multilevel-paging.md))

| # | Problem | Answer |
|---|---|---|
| A8 | 16 B process, 4 B pages, 64 B memory | LA **4** bits, PA **6** bits, **4** pages, **16** frames |
| A9 | PAS = 128 KB, word = 4 B. PA bits? | **15** |
| A10 | LAS = 256 MB, word = 4 B. LA bits? | **26** |
| A11 | p. 80 table: 5 rows (LAS, PAS, page size → all columns) | See Ch. 25 §4 (**rows 3–5 corrected**) |
| A12 | 12-bit VA, 256 B pages, free frames D, E, F: translate 9EF, 111, 700, 0FF | **0EF, 211, D00, EFF** |
| A13 | LA 22 bits, 4 KB pages, 4 B PTE: PT size? | $2^{10} \times 4 = $ **4 KB** (1 level) |
| A14 | 56-bit VA, 8 KB pages, 4 B PTE: levels? max frames? | **4 levels** · $2^{43} + 2^{32} + 2^{21} + 2^{10} + 1$ |
| A15 | 4 KB pages, 4 B PTE, 3 levels, outer table 256 B: LA bits? | **38** (6 + 10 + 10 + 12) |

### Page replacement ([Ch. 27](27-virtual-memory-and-page-replacement.md)). String: 0 1 2 3 0 1 4 0 1 2 3 4

| # | Algorithm | 3 frames | 4 frames |
|---|---|---|---|
| A16 | Optimal | **7** (7/12) | **6** (1/2) |
| A17 | LRU | **10** (5/6) | **8** (2/3) |
| A18 | FIFO | **9** (75 %) | **10** (5/6), **Belady's anomaly** |

### Effective access time ([Ch. 28](28-effective-access-time-tlb.md))

| # | Problem | Answer |
|---|---|---|
| A19 | $t = 20$, $h = 0.9$, $f = 0.05$, $m = 400$, $T = 6000$, $d = 0.15$ | $s = 6900$ → **494.5 ns** |
| A20 | $m = 150$, $t = 10$, $T = 5000$, $h = 0.95$, $f = 0.1$, $d = 0.2$ | $s = 6000$ → **197.5 ns** |
| A21 | $t = 20$, $m = 100$: (80 %, 1), (80 %, 2), (80 %, 3), (90 %, 1), (60 %, 1), (50 %, 1) | **140, 160, 180, 130, 160, 170 ns** |
| A22 | Same, 1 level, EAT = 130. Find $h$. | $220 - 100h = 130$ → **h = 0.9** |

### Disk scheduling ([Ch. 29](29-disk-structure-and-scheduling.md)). 0–199, head 50, queue 82 170 43 140 24 16 190

| # | Algorithm | Movement |
|---|---|---|
| A23 | FCFS | **642** |
| A24 | SSTF | **208** |
| A25 | SCAN (up) | **332** |
| A26 | LOOK (up) | **314** |
| A27 | C-SCAN (up) | **391** |
| A28 | C-LOOK (up) | **341** |

### Deadlock resources ([Ch. 19 §6½](19-deadlock-and-necessary-conditions.md))

| # | Problem | Answer |
|---|---|---|
| A29 | 3 processes each need 2 units. Minimum to avoid deadlock? | **4** |
| A30 | Needs 7, 4, 9, 2, 5. Max with deadlock possible? Min for none? | **22** · **23** |

---

## Part B: fresh practice (answers only)

| # | Problem | Answer |
|---|---|---|
| B1 | CPU utilisation with 3 processes in memory, each waiting on I/O 60 % of the time | $1 - 0.6^3 = $ **78.4 %** |
| B2 | Free blocks 100, 500, 200, 300, 600 (KB); requests 212, 417, 112, 426 | **First fit:** 212 → 500, 417 → 600, 112 → 288 left of the 500, 426 ❌ waits · **Best fit:** 212 → 300, 417 → 500, 112 → 200, 426 → 600 ✅ · **Worst fit:** 212 → 600, 417 → 500, 112 → 388 left of the 600, 426 ❌ |
| B3 | 32-bit LA, 30-bit PA, 4 KB pages: pages, frames, PTE, PT size | $2^{20}$ pages · $2^{18}$ frames · **18-bit** PTE · $2^{20} \times 18$ bits = **2.25 MB** |
| B4 | 32-bit LA, 4 KB pages, 4 B PTE: how many levels? | $2^{10}$ entries per page, so $\lceil 20/10 \rceil = $ **2 levels** (10 + 10 + 12) |
| B5 | String 7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1, 3 frames | **FIFO 15 · LRU 12 · OPT 9** |
| B6 | Same string, 4 frames | **FIFO 10 · LRU 8 · OPT 8** |
| B7 | String 1 2 3 4 1 2 5 1 2 3 4 5: FIFO with 3 and 4 frames | **9 → 10** (Belady). LRU: **10 → 8** (no anomaly) |
| B8 | $t = 10$, $m = 80$, $h = 0.75$, **2-level** paging, no faults | $0.75(90) + 0.25(10 + 240) = $ **130 ns** |
| B9 | Disk 0–199, head **53**, queue 98, 183, 37, 122, 14, 124, 65, 67 | **FCFS 640 · SSTF 236 · SCAN↑ 331 (SCAN↓ 236) · LOOK↑ 299 · C-SCAN↑ 382 · C-LOOK↑ 322** |
| B10 | 4 processes each need 3 units of R. Minimum R to avoid deadlock? | $4(3-1) + 1 = $ **9** |

---

## ⚡ Formula sheet (after-mid)

$$\text{CPU utilisation} = 1 - p^n \qquad \text{physical} = \text{base} + \text{logical} \;(\text{if logical} < \text{limit})$$

$$m = \log_2\frac{\text{PAS}}{\text{word}} \quad l = \log_2\frac{\text{LAS}}{\text{word}} \quad p = \log_2(\text{page size}) \quad \#\text{pages} = 2^{l-p} \quad \#\text{frames} = 2^{m-p}$$

$$\text{PTE} = m - p \text{ bits} \qquad \text{PT size} = 2^{l-p}\times\text{PTE} \qquad \#\text{levels} = \left\lceil\frac{l - p}{\log_2(\text{page size}/\text{PTE size})}\right\rceil$$

$$\text{EAT}_{\text{no TLB}} = (k+1)m \qquad \text{EAT}_{\text{TLB}} = h(t+m) + (1-h)(t+(k+1)m)$$

$$\text{EAT}_{\text{faults}} = (1-f)m_a + fs \qquad s = (1+d)T$$

$$\text{Min resources for no deadlock} = \sum(x_i - 1) + 1 \qquad \text{Avg rotational latency} = \tfrac12 \cdot \tfrac{60}{\text{RPM}}$$

---

**Previous:** [← 29. Disk Structure & Disk Scheduling](29-disk-structure-and-scheduling.md) · **Back to:** [OS index](../README.md)
