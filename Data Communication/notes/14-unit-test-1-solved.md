# 14. Unit Test 1 — Solved

> **Source:** `test 1.jpeg` — *Unit Test, BTech Semester V (CS 3504), Data Communication · 10 marks · 30 minutes*
> **Why this chapter exists:** it shows the **question pattern** the teacher uses. There are short numericals, one answer per blank, and no long theory. Expect the mid-term short-answer section to look like this.

Every question from the test, with a worked answer. Q3–Q6 use **performance formulas** (period, throughput, propagation and transmission time) that the other chapters do not cover. They are collected in [§ Performance formulas](#performance-formulas) at the end.

| Q | Topic | Answer | Chapter |
|---|---|---|---|
| 1 | CRC | `100111001011` | [Ch. 9](09-error-detection.md) |
| 2 | Hamming distance | Detect **3**, correct **1** | [Ch. 10](10-error-correction.md) |
| 3 | Period → frequency | **0.01 kHz** | [Ch. 2](02-signals-and-noise.md) |
| 4 | Shannon capacity | **≈ 2.09 × 10⁶ bits/min** (34,881 bps) ⚠️ | [Ch. 3](03-nyquist-rate-and-shannon-capacity.md) |
| 5 | Throughput | **B. 2 Mbps** | below |
| 6 | Propagation & transmission time | **PT = 0.05 s, TT = 40 s** | below |

---

### Q1. In CRC, if the data unit is `100111001` and the divisor is `1011`, what is the dividend at the receiver?

The divisor has 4 bits → degree 3 → append **3 zeros** at the sender.

**Sender dividend:** `100111001` + `000` = `100111001000`

Divide by `1011` using XOR (mod-2) division:

| Step | Bits under divisor | XOR with | Remainder |
|---|---|---|---|
| 1 | `1001` | `1011` | `010` |
| 2 | `0101` | `0000` | `101` |
| 3 | `1011` | `1011` | `000` |
| 4 | `0000` | `0000` | `000` |
| 5 | `0000` | `0000` | `000` |
| 6 | `0001` | `0000` | `001` |
| 7 | `0010` | `0000` | `010` |
| 8 | `0100` | `0000` | `100` |
| 9 | `1000` | `1011` | **`011`** |

Quotient = `101000001`, **CRC = `011`**.

The sender replaces the three appended zeros with the CRC and transmits the codeword. **The receiver divides the whole received codeword, so that codeword is its dividend:**

$$\boxed{\text{Dividend at receiver} = \texttt{100111001}\,\texttt{011} = \texttt{100111001011}}$$

**Check:** `100111001011 ÷ 1011` leaves remainder `000` → no error ✓

> ⚠️ **Read the question carefully.** "Dividend at the **sender**" is `100111001000`, with zeros appended. "Dividend at the **receiver**" is `100111001011`, with the CRC appended.

---

### Q2. A coding scheme has $d_{min} = 4$. What is its error detection and correction capability?

$$s = d_{min} - 1 = 4 - 1 = \mathbf{3} \qquad t = \left\lfloor \frac{d_{min} - 1}{2} \right\rfloor = \left\lfloor \frac{3}{2} \right\rfloor = \mathbf{1}$$

**Detects up to 3 errors; corrects up to 1 error.**

---

### Q3. The period of a signal is 100 ms. What is its frequency in kilohertz?

$$f = \frac{1}{T} = \frac{1}{100 \times 10^{-3}\ \text{s}} = 10\ \text{Hz} = \mathbf{0.01\ kHz}$$

---

### Q4. A telephone line has a bandwidth of 3000 Hz (300 to 3300 Hz). The SNR is 3162. Calculate the capacity per minute.

The line is **noisy** (an SNR is given), so use **Shannon**:

$$C = B \log_2(1 + \text{SNR}) = 3000 \times \log_2(3163)$$

$$\log_2 3163 = \frac{\log_{10} 3163}{\log_{10} 2} = \frac{3.5001}{0.30103} \approx 11.627$$

$$C \approx 3000 \times 11.627 \approx \mathbf{34{,}881\ bps} \;(\approx 34.88\ \text{kbps})$$

The question asks **per minute**:

$$C_{\text{per minute}} = 34{,}881 \times 60 \approx \mathbf{2{,}092{,}874\ bits/min} \approx 2.09 \times 10^6\ \text{bits/min}$$

> ⚠️ **This question was marked wrong on the sheet.** The usual mistakes:
> 1. Using **3300** instead of the bandwidth. The bandwidth is $3300 - 300 = 3000$ Hz.
> 2. Taking $\log_{10}$ instead of $\log_2$. Convert with $\log_2 x = \log_{10} x \,/\, 0.30103$.
> 3. Forgetting the **× 60**, because the question asks for capacity *per minute*.
> 4. Using Nyquist. Nyquist is for **noiseless** channels only; an SNR means Shannon.
>
> Textbook value (Forouzan): $C \approx 34{,}860$ bps, rounding $\log_2 3163 \approx 11.62$. Either rounding earns the marks if the working is shown.

---

### Q5. A network with bandwidth 10 Mbps passes on average 12,000 frames per minute, each carrying 10,000 bits. What is the throughput?

$$\text{Throughput} = \frac{12{,}000 \times 10{,}000\ \text{bits}}{60\ \text{s}} = \frac{120 \times 10^6}{60} = 2 \times 10^6\ \text{bps}$$

**Answer: B. 2 Mbps**, one-fifth of the 10 Mbps bandwidth.

> 💡 **Bandwidth ≠ throughput.** Bandwidth is what the link *could* carry. Throughput is what it *actually* delivers. The 10 Mbps is only there to tempt you.

---

### Q6. What are the propagation time and transmission time for a 5-Mbyte message if the bandwidth is 1 Mbps? Distance = 12,000 km, speed of light in the medium = 2.4 × 10⁸ m/s.

**Propagation time**, the time for one bit to travel the distance:

$$T_p = \frac{\text{Distance}}{\text{Propagation speed}} = \frac{12{,}000 \times 10^3\ \text{m}}{2.4 \times 10^8\ \text{m/s}} = \mathbf{0.05\ s} = 50\ \text{ms}$$

**Transmission time**, the time to push all the bits onto the link:

$$T_t = \frac{\text{Message size}}{\text{Bandwidth}} = \frac{5 \times 10^6 \times 8\ \text{bits}}{1 \times 10^6\ \text{bps}} = \mathbf{40\ s}$$

> 📌 **Bytes → bits: multiply by 8.** Forgetting this is the most common error. If your teacher uses $1\ \text{MB} = 2^{20}$ bytes, $T_t = 41.94$ s. The textbook (Forouzan) uses $10^6$, giving **40 s**.
>
> 💡 **Which one dominates?** For a large message, **transmission time dominates**: 40 s vs 0.05 s. For a very short message, such as one bit, **propagation time dominates**.

---

## Performance formulas

These are not in the lecture notes, but Q3, Q5 and Q6 depend on them.

| Quantity | Formula | Unit |
|---|---|---|
| **Frequency / period** | $f = \dfrac{1}{T}$, $\quad T = \dfrac{1}{f}$ | Hz ↔ s |
| **Throughput** | $\dfrac{\text{bits actually delivered}}{\text{time}}$ | bps |
| **Propagation time** | $T_p = \dfrac{\text{Distance}}{\text{Propagation speed}}$ | s |
| **Transmission time** | $T_t = \dfrac{\text{Message size (bits)}}{\text{Bandwidth}}$ | s |
| **Latency** | $\text{Propagation} + \text{Transmission} + \text{Queuing} + \text{Processing delay}$ | s |
| **Bandwidth–delay product** | $\text{Bandwidth} \times \text{Delay}$ | bits "in flight" on the link |

**Unit prefixes:** 1 ms = 10⁻³ s · 1 μs = 10⁻⁶ s · 1 kHz = 10³ Hz · 1 MHz = 10⁶ Hz · 1 Mbps = 10⁶ bps · 1 byte = 8 bits

---

## ⚡ Quick revision

- **CRC:** append (divisor length − 1) zeros → XOR-divide → the remainder is the CRC → transmit data + CRC. The **receiver's dividend is data + CRC**, and remainder 0 means no error.
- **$d_{min}$:** detect $d_{min} - 1$, correct $\lfloor (d_{min}-1)/2 \rfloor$. For $d_{min} = 4$: detect 3, correct 1.
- **$f = 1/T$:** watch the units (ms → s, Hz → kHz).
- **Shannon:** $B \log_2(1 + \text{SNR})$, with $B$ = the width of the band, not its upper edge. Read the question for *per minute*.
- **Throughput** is what actually passes, not the bandwidth.
- **$T_p$ = distance / speed; $T_t$ = bits / bandwidth.** Convert MB → bits (× 8).

---

**Previous:** [← 13. Spread Spectrum](13-spread-spectrum.md) · **Back to:** [Data Communication index](../README.md)
