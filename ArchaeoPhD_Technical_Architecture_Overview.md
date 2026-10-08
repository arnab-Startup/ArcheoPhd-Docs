# ARCHAEOPHD: TECHNICAL ARCHITECTURE OVERVIEW
**Deterministic-Neural Dual Routing, Stratigraphic Graph Validation, and Air-Gapped Field Deployment**

- **Target Audience:** PhD Supervisor & Doctoral Advisory Committee
- **Scope:** Software Engineering Approach & Algorithmic Architecture
- **Architecture Model:** Hybrid Native C++20 Core + Governed Local Neural Model (Qwen 2.5 7B GGUF)
- **Pagination Constraint:** Strictly 3 Printed A4 Pages (~850 words total)
- **Classification:** Academic Technical Architecture Memorandum (Monochrome / B&W)

---

# PAGE 1 — WHY THIS TECHNICAL APPROACH OVER OTHERS

> **CORE ENGINEERING THESIS:** Archaeological monograph ingestion demands 100% numerical fidelity, mathematical graph cycle detection, and complete data confidentiality under state antiquities permits. Generic cloud LLMs fail on silent numerical drift and regulatory secrecy; pure regex systems fail on irregular 19th-century prose syntax. ArchaeoPhD resolves this through a deterministic C++ fast path backed by a strictly governed, air-gapped local neural arbitrator.

```
+---------------------------------------------------------------------------------------+
| ARCHIVAL INGESTION DUAL-ROUTING PIPELINE                                              |
+---------------------------------------------------------------------------------------+
Raw Scan (PDF / TIFF) ---> OCR & Layout Analysis
  |
  +---> [Class A: Clean Typography]  ---> Native C++ Engine (<1 ms) ---> Deterministic Commit
  |
  +---> [Class B: Degraded Archival] ---> Split-Screen UI          ---> Human Double-Entry
                                                                        (0% Auto-Fill Pre-fill)
```

### 1. Rejection of Generic Cloud AI (GPT-4, Claude, Python Cloud APIs)
* **Probabilistic Hallucination & Numeric Drift:** In archival OCR benchmarks, commercial LLMs silently alter excavation coordinates and depth strata (empirical test transcribed *1966* as *1656*, and *20–40 cm* as *20–10 cm*). In archaeological field data, numerical drift corrupts stratigraphic ordering.
* **Antiquities Permit NDAs & Site Security:** Primary excavation reports frequently contain exact, unexcavated findspot GPS coordinates. Sending raw unredacted data to external cloud APIs violates state antiquities permits and exposes vulnerable sites to illicit looting.
* **Prohibitive Latency:** Full-page cloud LLM inference incurs 15–30 seconds per page with variable network dependency, making batch ingestion of 500-page excavation monographs computationally unviable.

### 2. Rejection of Pure Regex / Pure Rule-Based Parsers
* **Multi-Clausal Syntactic Collapse:** Standard regex parsers fail when a single sentence contains multiple chronological layers (e.g., *"pottery recovered in 1968, though Evans (1921) noted similar forms dating to 1450 BCE"*).
* **Multilingual Archaic Variations:** Rule-based heuristics break across historical German, French, and Victorian English excavation prose where syntactic structures and abbreviations diverge unpredictably.

### 3. The Chosen Architecture: Hybrid C++20 + Governed Local Neural Model
* **Native C++20 Fast Path:** Executes deterministically in sub-millisecond time with zero heap allocation per token, extracting measurements, counts, and stratigraphic relationships via mathematical grammar parsers.
* **Governed Local Neural Model:** An in-process, 4-bit quantized Qwen 2.5 7B GGUF (~4.4 GB) model, invoked solely for semantic ambiguity resolution. It runs fully offline with zero internet access required.
* **Strict Air-Gap Guarantee:** The system opens zero outbound TCP/UDP ports. All UI communication executes through in-memory Win32 WebView2 IPC, ensuring complete compliance with antiquities permit NDAs in remote field excavation camps.

---
*(End of Page 1 — ArchaeoPhD Technical Architecture Overview)*
\pagebreak

---

# PAGE 2 — OUR APPROACH NOW: C++ SPEED VS. LOCAL LLM ARBITRATION

```
[ MULTI-DATE CLAUSAL ARBITRATION FLOW ]
Complex Sentence ---> Native C++ (Strips Lifespans "1820–1903") ---> Local LLM (Resolves Event vs Historiography)
```

### 1. Algorithmic Division of Labor Matrix

Tasks are allocated strictly according to algorithmic guarantees: mathematical and syntactic proofs to native C++, and semantic arbitration to the governed local model.

| Subsystem / Task | Engine Deployed | Algorithmic Implementation & Rationale | Empirical Benchmark |
| :--- | :--- | :--- | :--- |
| **Physical Measurements & Units** | Native C++20 Engine | Deterministic grammar enforcing regular units (`m`, `cm`, `mm`, `BP`, `%`). Enforces 0% numeric loss invariant. | **< 1.0 ms / page** |
| **Artifact Count Binding** | Native C++20 Engine | Rejects bare numbers unless syntactically bound to verified head nouns (e.g., *"14 rim sherds"*). | **< 0.2 ms** |
| **Author Lifespan Masking** | Native C++20 Engine | Strips biographical date ranges (e.g., *Petrie (1853–1942)*) to prevent citation dates displacing archaeological strata. | **< 0.1 ms** |
| **Stratigraphic Harris DAG** | Native C++20 Engine | Tarjan's Strongly Connected Components (SCC) O(V+E) detects impossible physical cycles; Kahn's topological sort (Steno's Law). | **< 5.0 ms (1k nodes)** |
| **Radiocarbon Splines** | Native C++20 Engine | Continuous piecewise cubic splines on IntCal20 atmospheric calibration curves (1σ / 2σ probability envelopes). | **< 0.1 ms** |
| **Hybrid Retrieval** | Native C++20 Engine | 128-dim Matryoshka dense vectors fused with in-process Okapi BM25 (k=60) to prevent geographic keyword drift. | **22.5 ms query latency** |
| **Clausal Semantic Disambiguation** | Local Qwen 2.5 7B | Disambiguates competing historical vs. event dates in complex multi-clausal sentences across archival excavation prose. | **~3.8 s / invocation** |
| **Historiographical Conflicts** | Local Qwen 2.5 7B | Identifies methodological disputes and chronology conflicts across secondary publications via local KV-cached inference. | **~4.2 s (cached)** |

### 2. Governed Neural Arbitration (Zero-Hallucination Guardrails)
* **Grammar-Constrained Selection-Only Mode:** Unlike consumer chat interfaces, ArchaeoPhD never permits the neural model to generate free-form text. The model receives the verbatim text snippet alongside the pre-extracted C++ candidate list. It is constrained via grammar sampling to output *only* the index integer of the verified candidate or `REJECT`. It cannot invent non-existent dates or citations.
* **The Class B Safe Invariant:** *"A blank field is infinitely safer than a plausible wrong one."* On degraded 19th-century letterpress scans, automated pre-fill is locked out; the researcher transcribes via split-screen verification.

---
*(End of Page 2 — ArchaeoPhD Technical Architecture Overview)*
\pagebreak

---

# PAGE 3 — CRITICAL TRADE-OFFS & FUTURE EXPERIMENTAL HORIZONS

```
[ FUTURE EXPERIMENTAL HORIZONS ]
Doctoral Research ---> 1. Local Vision-Language Models (VLMs) on High-Res Plates (Qwen2-VL GGUF)
Roadmap           ---> 2. 3D SfM Photogrammetric Voxel Intersections in the Harris Matrix DAG
                  ---> 3. Native C++ Bayesian Sequential Calibration Engine (OxCal-in-C++)
```

### 1. Critical Failure Modes & Engineering Mitigations
* **Where C++ Deterministic Rules Fail:** Syntactic parsers cannot resolve unaligned multi-column OCR tables or damaged physical plates where typography is fragmented.  
  *Mitigation:* Flagged deterministically as `UNANCHORED_OR_DEGRADED` and routed to the human verification queue.
* **Where the Local Neural Model Fails:** 3–5 second execution latency and 4.4 GB RAM footprint. If unconstrained, it risks plausible confabulations.  
  *Mitigation:* Strict quarantine to multi-candidate arbitration; constrained index decoding prevents free-form generation.
* **Where Dense Semantic Vector Retrieval Fails:** High-dimensional embeddings cluster documents using similar theoretical terminology even if their stratigraphy or geographic regions conflict.  
  *Mitigation:* Dual-stage lexical BM25 filtering enforces exact trench identifiers, locus numbers, and site names.

### 2. Hardware Footprint Verification
* **Standalone Executable:** Single self-contained Win32 C++ binary: **9.49 MB** (`release/ArchaeoPhD.exe`).
* **Neural Model Weights:** `Qwen2.5-7B-Instruct-Q4_K_M.gguf` + `nomic-embed-text` = **4.45 GB** total.
* **Memory & Networking:** **~65 MB idle RAM**; opens **0 network sockets**; operates entirely air-gapped.

### 3. Planned Technical Experiments (Doctoral Research Roadmap)
1. **Experiment 1: Local Vision-Language Models (VLMs) on High-Resolution Letterpress Crops.**  
   *Approach:* Test quantized local VLMs (Qwen2-VL 2B/7B GGUF) directly on segmented typographic plates from 19th-century monographs (e.g., Petrie, Evans). By processing high-resolution bounding crops rather than full pages, we eliminate token collapse and preserve sub-millimeter plate coordinates without cloud data leakage.
2. **Experiment 2: 3D Volumetric Voxel Intersections in the Harris Matrix DAG.**  
   *Approach:* Bridge trench Structure-from-Motion (SfM) 3D photogrammetric meshes directly into the C++ Tarjan DAG solver. Instead of relying on manual 2D context sheets, the engine will compute 3D volumetric intersections between stratigraphic units to mathematically detect physical overlap violations.
3. **Experiment 3: Native C++ Bayesian Sequential Calibration Engine (OxCal-in-C++).**  
   *Approach:* Embed an in-process Markov Chain Monte Carlo (MCMC) Bayesian sampler directly into the native C++ binary. This fuses prior stratigraphic DAG topological constraints with posterior IntCal20 continuous radiocarbon probability envelopes on-device, replacing external commercial legacy software.

---

### Conclusion for the Doctoral Advisory Committee
ArchaeoPhD pairs deterministic C++ engines for sub-millisecond mathematical precision and zero numerical drift with a governed, offline neural model for semantic nuance. The resulting architecture delivers a fully air-gapped, verifiable computational platform engineered for doctoral-level research.

---
*(End of Page 3 — ArchaeoPhD Technical Architecture Overview)*
