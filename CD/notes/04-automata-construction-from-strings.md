# 4. Constructing Automata from Strings & Regular Expressions

> ⚠️ **Written from standard course knowledge.** No class material was supplied for Compiler Design.
> **Syllabus:** *their construction from given string*

---

## 🎯 In one line

To build an automaton that accepts a **given string**, chain one state per character; to build one for a **pattern**, decide what each state must "remember".

---

## 1. Case 1 — accept exactly ONE given string ⭐⭐

**Problem:** construct a DFA that accepts **only** the string $w = a_1a_2\dots a_n$ and nothing else.

### The recipe

- Use $n+1$ states $q_0, q_1, \dots, q_n$ — a straight chain.
- $\delta(q_{i-1}, a_i) = q_i$ for each character.
- $F = \{q_n\}$ — only the last state accepts.
- **Every other transition goes to a dead state $q_d$.**

### Worked example — accept only `abb`

```
     ──►( q0 )──a──►( q1 )──b──►( q2 )──b──►(( q3 ))
           │           │           │            │
           │b          │a          │a           │a,b
           ▼           ▼           ▼            ▼
        ┌──────────────────────────────────────────┐
        │              ( qd )  dead state          │◄─┐
        └───────────────────┬──────────────────────┘  │
                            └──────── a,b ────────────┘
```

**Transition table:**

| State | `a` | `b` |
|---|---|---|
| →$q_0$ | $q_1$ | $q_d$ |
| $q_1$ | $q_d$ | $q_2$ |
| $q_2$ | $q_d$ | $q_3$ |
| *$q_3$ | $q_d$ | $q_d$ |
| $q_d$ | $q_d$ | $q_d$ |

> ⚠️ **The dead state is essential here.** A DFA must have a transition defined for **every** (state, symbol) pair. Without $q_d$ the machine is not a valid DFA. In an **NFA** you may simply omit those transitions.

**As an NFA** it is much cleaner — just the chain, no dead state:

```
     ──►( q0 )──a──►( q1 )──b──►( q2 )──b──►(( q3 ))
```

---

## 2. Case 2 — strings CONTAINING a given substring ⭐⭐

**Problem:** accept all strings over $\{a,b\}$ that **contain `abb`** as a substring.

Same chain, but two changes: $q_0$ **loops** on symbols that don't start the pattern, and the final state is **absorbing** (once found, always accept).

```
        ┌─b─┐                                    ┌─a,b─┐
        │   ▼                                    │     ▼
     ──►( q0 )──a──►( q1 )──b──►( q2 )──b──►(( q3 ))
           ▲           │  │        │
           │           │a─┘        │a
           │           ▼           │
           └───────────────────────┘
```

**Transition table:**

| State | Meaning | `a` | `b` |
|---|---|---|---|
| →$q_0$ | nothing matched | $q_1$ | $q_0$ |
| $q_1$ | matched `a` | $q_1$ | $q_2$ |
| $q_2$ | matched `ab` | $q_1$ | $q_3$ |
| *$q_3$ | **found `abb`** | $q_3$ | $q_3$ |

> ⭐ **The key technique — name your states by what they remember.** Each state means *"the longest prefix of the pattern matched so far"*. Then every transition is forced:
> - From $q_2$ (matched `ab`) on `a`: the `ab` is now useless, but the new `a` is a fresh start → go to $q_1$, **not** $q_0$.
> - From $q_1$ (matched `a`) on `a`: still just one `a` → stay at $q_1$.
>
> Getting these "partial restart" transitions right is where most marks are lost.

---

## 3. Case 3 — strings ENDING with a given string ⭐⭐

**Problem:** accept all strings **ending in `abb`**.

Almost identical to Case 2, except the final state is **not** absorbing — if more input arrives, we must re-track the pattern.

| State | Meaning | `a` | `b` |
|---|---|---|---|
| →$q_0$ | — | $q_1$ | $q_0$ |
| $q_1$ | ends with `a` | $q_1$ | $q_2$ |
| $q_2$ | ends with `ab` | $q_1$ | $q_3$ |
| *$q_3$ | **ends with `abb`** | $q_1$ | $q_0$ |

> ⭐ **Contains vs Ends with — the one difference:** in "contains", $q_3$ loops to itself on everything (the substring has been found forever). In "ends with", $q_3$ must keep tracking, because more characters can spoil the ending.

**Check `abbab`:** $q_0 \xrightarrow{a} q_1 \xrightarrow{b} q_2 \xrightarrow{b} q_3 \xrightarrow{a} q_1 \xrightarrow{b} q_2 \notin F$ ❌ — correct, `abbab` ends in `ab`, not `abb` ✓

---

## 4. Case 4 — strings STARTING with a given string ⭐

**Problem:** accept all strings **starting with `ab`**.

Chain through the prefix, then accept everything afterwards. Any deviation is fatal.

| State | `a` | `b` |
|---|---|---|
| →$q_0$ | $q_1$ | $q_d$ |
| $q_1$ | $q_d$ | $q_2$ |
| *$q_2$ | $q_2$ | $q_2$ |
| $q_d$ | $q_d$ | $q_d$ |

---

## 5. The four cases side by side ⭐⭐⭐

For the pattern $P$, the difference is entirely in **$q_0$'s loop** and **$q_{final}$'s behaviour**:

| Requirement | $q_0$ loops on non-matching symbols? | Final state absorbing? | Dead state needed? |
|---|---|---|---|
| **Exactly** $P$ | ❌ No | ❌ No (all → dead) | ✅ Yes |
| **Starts with** $P$ | ❌ No | ✅ **Yes** | ✅ Yes |
| **Contains** $P$ | ✅ **Yes** | ✅ **Yes** | ❌ No |
| **Ends with** $P$ | ✅ **Yes** | ❌ **No** (keep tracking) | ❌ No |

> 💡 **Read the question's verb first.** "Exactly", "starts with", "contains", "ends with" each pick a different row of this table. Misreading the verb loses the whole question.

---

## 6. Regular expressions → NFA (Thompson's Construction) ⭐⭐

Given a **regular expression**, build an ε-NFA mechanically. Every sub-expression gets **one start state and one final state**.

### The base cases

```
   ε:        ──►( i )──ε──►(( f ))

   symbol a: ──►( i )──a──►(( f ))
```

### The three operators

**Union $r_1 \mid r_2$** — branch with ε, rejoin with ε:

```
                    ┌──ε──►( N(r₁) )──ε──┐
                    │                    ▼
         ──►( i )───┤                   (( f ))
                    │                    ▲
                    └──ε──►( N(r₂) )──ε──┘
```

**Concatenation $r_1r_2$** — merge $r_1$'s final with $r_2$'s start:

```
         ──►( N(r₁) )────►( N(r₂) )──►(( f ))
```

**Kleene star $r^*$** — a loop back plus a bypass:

```
                        ┌───────ε────────┐
                        │                │
                        ▼                │
         ──►( i )──ε──►( N(r) )──ε──►(( f ))
                │                        ▲
                └──────────ε─────────────┘
                    (bypass for zero occurrences)
```

### Worked example — NFA for `(a|b)*abb` ⭐

This is the classic textbook example.

```
           ┌─────────────ε──────────────┐
           │      ┌──ε──►(2)──a──►(3)──ε┐│
           ▼      │                     ▼▼
   ──►(0)──ε──►(1)┤                     (6)──a──►(7)──b──►(8)──b──►((9))
           │      │                     ▲▲
           │      └──ε──►(4)──b──►(5)──ε┘│
           └─────────────ε───────────────┘
                     (a|b)*                    a b b
```

| Part | States |
|---|---|
| $(a\mid b)^*$ | 0 – 6 |
| `a` | 6 → 7 |
| `b` | 7 → 8 |
| `b` | 8 → 9 |

Then apply the **subset construction** of [Ch. 3](03-nfa-to-dfa-conversion.md) to get the DFA. Its start state is

$$\varepsilon\text{-closure}(0) = \{0, 1, 2, 4, 7\}$$

> 📌 **The complete pipeline for a lexical analyser:**
> $$\text{regular expression} \xrightarrow{\text{Thompson}} \varepsilon\text{-NFA} \xrightarrow{\text{subset construction}} \text{DFA} \xrightarrow{\text{minimise}} \text{scanner}$$
> This is literally what **Lex** does internally ([Ch. 5](05-lexical-analysis-and-lex.md)).

---

## 7. More worked constructions ⭐

### Example 1 — strings over $\{0,1\}$ with an **even number of 0s and even number of 1s**

Four states tracking the parity of each count:

| State | (0s, 1s) parity | `0` | `1` |
|---|---|---|---|
| →*$q_{EE}$ | (even, even) | $q_{OE}$ | $q_{EO}$ |
| $q_{OE}$ | (odd, even) | $q_{EE}$ | $q_{OO}$ |
| $q_{EO}$ | (even, odd) | $q_{OO}$ | $q_{EE}$ |
| $q_{OO}$ | (odd, odd) | $q_{EO}$ | $q_{OE}$ |

$F = \{q_{EE}\}$.

> 💡 **The pattern:** for "even/odd count of $k$ things", you need $2^k$ states — one per combination of parities.

### Example 2 — identifiers (as in a real compiler)

A C identifier is a letter or underscore, followed by any number of letters, digits or underscores:

$$\texttt{letter} = [A\text{-}Za\text{-}z\_] \qquad \texttt{digit} = [0\text{-}9]$$
$$\textbf{identifier} = \texttt{letter}\,(\texttt{letter} \mid \texttt{digit})^*$$

```
                        ┌─ letter, digit ─┐
                        │                 ▼
     ──►( q0 )── letter ──►(( q1 ))───────┘
```

| State | letter | digit | other |
|---|---|---|---|
| →$q_0$ | $q_1$ | dead | dead |
| *$q_1$ | $q_1$ | $q_1$ | dead |

### Example 3 — unsigned numbers

$$\textbf{number} = \texttt{digit}^+ \,(\,.\,\texttt{digit}^+\,)^?\,(\,E\,(+\mid-)^?\,\texttt{digit}^+\,)^?$$

```
              ┌digit┐                 ┌digit┐
              │     ▼                 │     ▼
   ──►(q0)─digit─►((q1))──.──►(q2)─digit─►((q3))
                     │                        │
                     └────────── E ───────────┤
                                              ▼
                                    (q4)─+,−,digit─►…
```

---

## 8. Common exam questions

1. **Construct a DFA/NFA that accepts only the string `abb`.** ⭐⭐
2. **Construct a DFA for all strings containing / ending with / starting with a given substring.** ⭐⭐⭐
3. **Construct a DFA for strings with an even/odd number of a given symbol.** ⭐⭐
4. **Construct an NFA from a given regular expression using Thompson's construction.** ⭐⭐⭐
5. **Draw the transition diagram for identifiers / numbers.** ⭐
6. **Construct an automaton for strings of length exactly / at least / at most $n$.**
7. **Write the regular expression for a given automaton** (the reverse direction).

---

## ⚡ Quick revision

- **Accept exactly one string $w$ of length $n$:** a chain of $n+1$ states; all other transitions → **dead state**.
- ⭐ **Name each state by what it remembers** — *"the longest prefix of the pattern matched so far"*. Every transition then follows mechanically.
- **The four verbs give four different machines:**
  - **Exactly $P$** — no $q_0$ loop, final not absorbing, dead state needed
  - **Starts with $P$** — no $q_0$ loop, final **absorbing**, dead state needed
  - **Contains $P$** — $q_0$ **loops**, final **absorbing**
  - **Ends with $P$** — $q_0$ **loops**, final **keeps tracking** (not absorbing)
- ⚠️ On a partial match failing, restart at the **longest still-valid prefix** (e.g. $q_2 \xrightarrow{a} q_1$), **not** always at $q_0$.
- A **DFA needs a transition for every (state, symbol)** — hence dead states. An **NFA may omit** them.
- **Thompson's construction:** ε for the base cases; **union** = ε-branch and ε-rejoin; **concatenation** = join final to start; **star** = ε loop back + ε bypass.
- **Parity problems:** "even number of $k$ symbol types" → **$2^k$ states**.
- **Full pipeline:** regex → ε-NFA (Thompson) → DFA (subset construction) → minimal DFA → scanner.

---

**Previous:** [← 3. NFA → DFA](03-nfa-to-dfa-conversion.md) · **Next:** [5. Lexical Analysis & Lex →](05-lexical-analysis-and-lex.md)
