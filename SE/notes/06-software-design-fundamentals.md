# 6. Software Design Fundamentals

> **Lecture:** L6 (28-08-2026) · **Source:** `Lecture 6 Software Design-Prahlad-NIT-CS3501.md`

---

## 🎯 In one line

$$\textbf{Good design} = \textbf{HIGH cohesion} + \textbf{LOW coupling}$$

---

## 1. What is Software Design?

> The **Design Phase transforms the SRS document** into a form **easily implementable in some programming language**.

```
   ┌──────────┐      ┌──────────────────┐      ┌──────────────────┐
   │   SRS    │─────►│ Design Activities│─────►│ Design Documents │
   │ Document │      └──────────────────┘      └──────────────────┘
   └──────────┘
```

### Design phase activities

| Activity | Output |
|---|---|
| **High-level design** | Decomposes the system into **modules**, and shows the **control relationships** among them — usually as a **structure chart** |
| **Detailed design** | Designs the **data structures and algorithms** for each module — the **detailed design document** |

---

## 2. Goodness of a Design ⭐

A design is good if it is:

| Criterion | Meaning |
|---|---|
| **Correct** | Implements all functionalities of the system |
| **Understandable** | Another engineer can read and follow it |
| **Efficient** | Uses resources sensibly |
| **Easily maintainable** | Changes can be made without breaking other parts |

> ⭐ **The lecture's central claim:** understandability and maintainability come from **modularity**, and modularity is measured by **cohesion and coupling**.

**A good design should therefore have:**
- **High cohesion**
- **Low coupling**

---

## 3. Functional Independence ⭐⭐

A module is **functionally independent** if it can be used (and understood) **without much reference to other modules**.

### Why it matters

- **Functional independence reduces error propagation** — a defect in one module is less likely to spread to others.
- Independent modules can be **developed, tested and maintained separately**.
- Independent modules are **reusable**.

> 📌 This is the design-phase application of the **decomposition principle** from [Ch. 1](01-introduction-to-software-engineering.md) — recall that decomposition only helps if the parts are genuinely **independent**.

### How is it measured?

> There is **no direct measure** of functional independence. Instead, **two indirect metrics** are used:
>
> $$\textbf{Functional independence} \ \longleftarrow \ \textbf{Cohesion} \ + \ \textbf{Coupling}$$

---

## 4. Cohesion and Coupling — the definitions ⭐⭐

| Term | Definition |
|---|---|
| **Cohesion** | A measure of the **degree to which the elements of a module are functionally related** — how tightly the parts *inside* one module belong together. |
| **Coupling** | Between two modules, a measure of the **degree of interdependence or interaction between the two modules**. |

```
     HIGH COHESION (good)              LOW COUPLING (good)

   ┌─────────────────┐              ┌────────┐      ┌────────┐
   │  ●───●───●───●  │              │ Module │─────►│ Module │
   │  │   │   │   │  │              │   A    │  1   │   B    │
   │  ●───●───●───●  │              └────────┘ link └────────┘
   │ all elements    │                 few, simple connections
   │ work on ONE     │
   │ task            │              ┌────────┐╔════►┌────────┐
   └─────────────────┘              │ Module │╠════►│ Module │
                                    │   A    │╠════►│   B    │
   ← inside a module →              └────────┘╚════►└────────┘
                                       HIGH COUPLING (bad)
                                    ← between modules →
```

> ⭐ **A module having high cohesion and low coupling is said to be functionally independent of other modules.**

---

## 5. Classification of Cohesiveness ⭐⭐⭐

> Classification is often **subjective**, yet it gives us some idea about the cohesiveness of a module. By examining the **type of cohesion** exhibited by a module, we can roughly tell whether it displays **high or low cohesion**.

```
        ▲  1. FUNCTIONAL        ← BEST
        │  2. Sequential
  Degree│  3. Communicational
   of   │  4. Procedural
 cohesion  5. Temporal
        │  6. Logical
        │  7. COINCIDENTAL      ← WORST
        ▼
   The degree of cohesiveness INCREASES from Coincidental to Functional
```

| # | Type | Definition (from the lecture) | Example |
|---|---|---|---|
| **7** | **Coincidental** ❌ worst | The module performs a set of tasks **which relate to each other very loosely, if at all**. The module contains a **random collection of functions** — put in the module **out of pure coincidence, without any thought or design**. | A "miscellaneous utilities" module |
| **6** | **Logical** | All elements of the module perform **similar operations** — e.g. error handling, data input, data output. | A set of **print functions** to generate an output report, arranged into a single module |
| **5** | **Temporal** | The module contains tasks related by the fact that **all tasks must be executed in the same time span**. | The set of functions responsible for **initialization, start-up, shut-down** of some process |
| **4** | **Procedural** | The set of functions of the module are **all part of a procedure (algorithm)** — a certain sequence of steps carried out in a certain order for achieving an objective. | The **algorithm for decoding a message** |
| **3** | **Communicational** | All functions of the module **reference or update the same data structure**. | A set of functions defined on an **array or a stack** |
| **2** | **Sequential** | Elements of a module form **different parts of a sequence** — the **output from one element is the input to the next** — to achieve a single function. | **sort → search → display** |
| **1** | **Functional** ✅ best | Different elements of a module **cooperate to achieve a single function**. **When a module displays functional cohesion we can describe the function using a single sentence.** | Managing an **employee's payroll** |

### How to determine cohesiveness — the sentence test ⭐⭐

This is a distinctive and very examinable technique:

> **Write down a sentence to describe the function of the module.**
>
> - If the sentence is **compound** → it has **sequential or communicational** cohesion.
> - If it has words like **"first, next, after, then"** → it has **sequential or temporal** cohesion.
> - If it has words like **"initialize"** → it probably has **temporal** cohesion.
> - If you can describe it in **one simple sentence** → **functional** cohesion ✅

---

## 6. Classification of Coupling ⭐⭐⭐

> Coupling indicates **how closely two modules interact or how interdependent they are**. The degree of coupling between two modules depends on their **interface complexity**.
>
> There are **no ways to precisely determine** coupling between two modules; classification of different types of coupling helps us **approximately estimate** the degree.

> **Five types of coupling exist between any two modules.**

```
        ▲  5. CONTENT           ← WORST
        │  4. Common
  Degree│  3. Control
   of   │  2. Stamp
 coupling  1. DATA              ← BEST
        ▼
   The degree of coupling INCREASES from Data coupling to Content coupling
```

| # | Type | Definition (from the lecture) | Example |
|---|---|---|---|
| **1** | **Data** ✅ best | Two modules are data coupled if they communicate via a parameter that is an **elementary data item** — e.g. an integer, a float, a character. The data item should be **problem related** and **not used for control purposes**. | `sqrt(x)` — passes a single float |
| **2** | **Stamp** | Two modules are stamp coupled if they communicate via a **composite data item** — such as a **record in Pascal** or a **structure in C**. | Passing a whole `struct Employee` when only the salary is needed |
| **3** | **Control** | **Data from one module is used to direct the order of instruction execution in another.** | A **flag set in one module and tested in another** |
| **4** | **Common** | Two modules are common coupled if they **share some global data**. | Both modules read/write a global variable |
| **5** | **Content** ❌ worst | Content coupling exists between two modules if they **share code** — e.g. **branching from one module into another module**. | A `goto` from inside module A into the middle of module B |

> ⚠️ **Why content coupling is worst:** if one module can jump into the middle of another, changing either module can break the other in ways no interface documents. The modules are no longer separable at all.

---

## 7. The two scales side by side ⭐⭐

| | **Cohesion** | **Coupling** |
|---|---|---|
| Measures | **Within** one module | **Between** two modules |
| Concerns | How related the elements are | How interdependent the modules are |
| We want | **HIGH** ⬆️ | **LOW** ⬇️ |
| Best | **Functional** | **Data** |
| Worst | **Coincidental** | **Content** |
| Number of levels | **7** | **5** |

> 💡 **Memory hooks:**
> - **Cohesion (7, worst→best):** **Co**incidental, **L**ogical, **T**emporal, **P**rocedural, **C**ommunicational, **S**equential, **F**unctional — *"**C**an **L**ittle **T**ots **P**lay **C**arefully **S**itting **F**irmly"*
> - **Coupling (5, best→worst):** **D**ata, **S**tamp, **C**ontrol, **C**ommon, **C**ontent — *"**D**on't **S**tart **C**oupling **C**ode **C**arelessly"*

---

## 8. Control Hierarchy and Layered Design ⭐

### Neat Hierarchy

> **Control hierarchy represents the organization of modules.** Control hierarchy is also called **program structure**.
>
> The most common notation is a **tree-like diagram called a structure chart**.

### Layered Design

> Layered design essentially means:
> - **Low fan-out**
> - **Control abstraction**

### Characteristics of module hierarchy ⭐

| Characteristic | Meaning |
|---|---|
| **Depth** | The **number of levels of control** in the hierarchy |
| **Width** | The overall **span of control** — number of modules at the same level |
| **Fan-out** | The **number of modules directly controlled by** a given module |
| **Fan-in** | The **number of modules that directly control** a given module |

```
                    ┌─────────┐
                    │  Main   │           Depth = 3 levels
                    └────┬────┘
            ┌────────────┼────────────┐
            ▼            ▼            ▼
        ┌───────┐   ┌───────┐   ┌───────┐   ← fan-out of Main = 3
        │   A   │   │   B   │   │   C   │      Width at this level = 3
        └───┬───┘   └───┬───┘   └───┬───┘
            │           │           │
            └───────────┼───────────┘
                        ▼
                   ┌─────────┐
                   │    D    │   ← fan-in of D = 3 (reused module)
                   └─────────┘
```

> ⭐ **Design guidance:** aim for **low fan-out** (a module controlling too many others is doing too much) and **high fan-in** (a module used by many others is well-factored and reusable).

---

## 9. Function-oriented vs Object-oriented design ⭐

| | **Function-Oriented Design** | **Object-Oriented Design** |
|---|---|---|
| Basic unit | **Functions / modules** | **Objects / classes** |
| Decomposition based on | The **functions** the system performs | The **real-world entities** in the problem |
| Data | Often **shared** between functions | **Encapsulated** inside objects |
| Approach | **Top-down** — start with the main function, refine it | **Bottom-up** tendency — identify objects, then their interactions |
| Design notation | **DFDs, structure charts** ([Ch. 7](07-function-oriented-design.md)) | Class diagrams, use-case diagrams |
| Reusability | Lower | **Higher** (inheritance) |
| Suitable for | Systems with clear, stable functionality | Large, evolving systems |

> 📌 **The design model is obtained from the analysis model through transformations over a series of steps**, in which decisions regarding implementation are **consciously made**.

---

## 10. Common exam questions

1. **What is software design? What does the design phase transform?** ⭐ → SRS → implementable form; high-level and detailed design.
2. **What are the characteristics of a good design?** ⭐
3. **What is functional independence? Why is it important?** ⭐⭐ → **reduces error propagation**, aids testing/maintenance/reuse; measured **indirectly** by cohesion and coupling.
4. **Define cohesion and coupling.** ⭐⭐
5. **Explain the classification of cohesion with examples.** ⭐⭐⭐ *(all 7, in order, with the example for each)*
6. **Explain the classification of coupling with examples.** ⭐⭐⭐ *(all 5, in order)*
7. **How do you determine the cohesiveness of a module?** ⭐⭐ → **the sentence test**.
8. **Why should a design have high cohesion and low coupling?** ⭐⭐
9. **Define depth, width, fan-in and fan-out.** ⭐
10. **What is layered design?** → low fan-out + control abstraction.
11. **Differentiate function-oriented and object-oriented design.** ⭐

---

## ⚡ Quick revision

- **Design phase transforms the SRS** into a form easily implementable in a programming language.
- **Two activities:** **high-level design** (modules + control relationships → structure chart) and **detailed design** (data structures + algorithms).
- **Good design = correct, understandable, efficient, easily maintainable.**
- **Functional independence** = a module usable without much reference to others. **Reduces error propagation.** No direct measure — use **cohesion and coupling**.
- **Cohesion** = how functionally related the elements **inside** a module are. Want **HIGH**.
- **Coupling** = degree of **interdependence between two** modules; depends on **interface complexity**. Want **LOW**.
- **Cohesion, 7 levels, worst → best:** Coincidental · Logical · Temporal · Procedural · Communicational · Sequential · **Functional**.
  - Functional ⇒ you can **describe the module in a single sentence**.
- **Coupling, 5 levels, best → worst:** **Data** · Stamp · Control · Common · **Content**.
  - Data = elementary item · Stamp = composite (record/struct) · Control = **flag** directing execution · Common = **global data** · Content = **shared code / branching into another module**.
- **Sentence test:** compound sentence → sequential/communicational · "first, next, after, then" → sequential/temporal · "initialize" → temporal.
- **Control hierarchy = program structure**, drawn as a **structure chart**.
- **Layered design = low fan-out + control abstraction.**
- **Depth** = levels of control · **Width** = span of control · **Fan-out** = modules controlled by it · **Fan-in** = modules controlling it.
- ⭐ **Aim for low fan-out and high fan-in.**

---

**Previous:** [← 5. Formal Specification](05-formal-specification-of-systems.md) · **Next:** [7. Function-Oriented Design →](07-function-oriented-design.md)
