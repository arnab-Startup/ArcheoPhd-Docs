# Contradiction Detection Engine (`NativeContradictionEngine`)

> **Subsystem Location:** [`desktop/engine/analysis/contradictions.hpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/engine/analysis/contradictions.hpp)  
> **Core Responsibility:** Identify empirical and interpretive conflicts across multiple publications before thesis defense.

---

## 1. The 4 Archaeological Contradiction Types

| Type | Classification | Detection Algorithm | UI Presentation Guardrail |
| :--- | :--- | :--- | :--- |
| **Type 1** | **Chronological Conflict (Date Clash)** | Numerical date range overlap analysis | **Shown Directly (High Confidence)**: Identifies mathematical dating incompatibilities across publications. |
| **Type 2** | **Interpretive Conflict (Hypothesis Clash)** | Semantic opposition analysis between claims | **"Possible conflict — please review"**: Never a verdict. Displays side-by-side exact excerpts from both sources. |
| **Type 3** | **Stratigraphic Impossibility** | **Tarjan's Strongly Connected Components (SCC)** | **Shown Directly (Physical Impossibility)**: Flags circular chronological loops in the Harris Matrix. |
| **Type 4** | **Cross-Site Regional Conflict** | Chrono-spatial anomaly detection | **"Possible conflict — please review"**: Flags horizon misalignments between neighboring sites. |

---

## 2. Type 3: Stratigraphic Cycle Detection via Tarjan's SCC

### The Archaeological Problem
The **Harris Matrix** defines stratigraphic relationships using topological partial ordering:
- A stratum cannot be both *above* (younger than) and *below* (older than) another stratum.
- When synthesising reports from multiple excavation seasons, contradictory locus cuts frequently introduce **impossible circular dependencies** (e.g. Unit A > Unit B > Unit C > Unit A).

### The C++ Algorithm
`NativeContradictionEngine::detect_type_3_stratigraphic()` builds a directed adjacency graph where edges represent physical superposition (`harris_above`, `harris_below`, `harris_cut_by`).
- Runs **Tarjan's Strongly Connected Components algorithm** in $O(V + E)$ time.
- If any SCC contains more than 1 node, an impossible stratigraphic cycle exists.
- Emits an urgent structural alert identifying the exact circular chain of strata.

---

## 3. Strict Human-in-the-Loop Review Guardrails

Per `MVP_PLAN.md`, the AI **never concludes an interpretive contradiction**:
- Academic debates are nuanced (e.g., whether Jericho was peacefully abandoned or violently conquered).
- For Types 2 & 4, the engine highlights the disagreement as an inquiry for the researcher, visually isolates both citations, and requires academic sign-off.
