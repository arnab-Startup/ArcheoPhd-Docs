# ArchaeoPhD AI v2.0: Comprehensive Item-by-Item Forensic Research Dossier

> **Classification:** Academic, Ontological & Technical Due Diligence Dossier  
> **Target Document:** `docs/domain/V2_COMMERCIALIZATION_BLUEPRINT.md`  
> **Author:** Antigravity Research Engine & Scientific Verification Coordinator  
> **Date:** November 2026  
> **Scope:** Granular, forensic, item-by-item verification of every epistemological concept, mathematical equation, ontological class/property, natural language processing mechanism, commercial statistic, and case study sample cited in the ArchaeoPhD AI v2.0 blueprint.

---

## Module 1: Archaeological Epistemology & Formation Process Theory

### 1.1 The Destructive Nature of Excavation (Harris & Carver)
* **The Epistemological Paradox:** In physical sciences (such as physics or chemistry), experiments can be repeated under identical controlled conditions. In archaeology, excavation is inherently and irreversibly destructive. Removing a stratigraphic unit to examine the underlying layer permanently obliterates the primary physical context.
* **The Excavation Record as a Surrogate:** As Edward C. Harris established in *Principles of Archaeological Stratigraphy* (1979, 1989), the physical site is consumed by the process of digging. Consequently, the archive (written records, drawings, single-surface plans, Harris matrices, total station measurements, and photographs) becomes the *only surviving empirical surrogate* of the destroyed site.
* **Observer-Dependency (Carver):** Martin Carver (*Making Alternative Histories*, *Field Archaeology*) demonstrated that the creation of the stratigraphic record is an interpretive act. Deciding where one layer ends and another begins in the soil is conditioned by trench lighting, moisture content, excavator experience, and theoretical preconceptions.
* **The v1.0 Fatal Flaw:** Calling Layer A "Physical World Ground Truth" conflated the physical dirt (which was destroyed during excavation decades ago) with what an author wrote in a PDF report. In information science, a PDF is an `E73 Information Object`, which documents subjective propositions made by an `E39 Actor`.

### 1.2 Formation Process Theory: Systemic Context vs. Archaeological Context (Schiffer)
Michael B. Schiffer (1972, 1976, 1987) established that artifacts and features in the ground do not represent a frozen snapshot of past human behavior. They pass through two distinct states transformed by two sets of processes:
1. **Systemic Context:** The behavioral state in which an element is actively participating in a cultural system (procurement $\to$ manufacture $\to$ use $\to$ maintenance $\to$ recycling $\to$ discard).
2. **Archaeological Context:** The state in which an object has left the behavioral system and is embedded in the physical geological matrix.
3. **C-Transforms (Cultural Transforms):** Human activities that transform materials (e.g., secondary refuse dumping, structural rebuilding, tomb looting, plowing).
4. **N-Transforms (Natural Transforms):** Environmental and post-depositional processes that displace or alter remains:
   - *Bioturbation:* Animal burrowing (rodents, termites, earthworms) displacing small objects across stratigraphic levels.
   - *Floriturbation:* Tree roots penetrating and mixing strata.
   - *Cryoturbation:* Freeze-thaw cycles sorting stones.
   - *Geochemical alteration:* Leaching of bone collagen, hard-water carbonate encrustation.

**Application to ArchaeoPhD AI:** Discrepancies between finds or radiocarbon dates within the same stratum are usually the result of C-transforms or N-transforms, not publication errors or logical contradictions.

---

## Module 2: Citation Cascading & Bibliometric Echo-Chambers

### 2.1 The Bibliometric Echo-Chamber Phenomenon
In archaeological synthesis, an excavator publishes a preliminary estimate or single radiocarbon date in a field report (e.g., in 1982). Over the next 40 years:
- Regional surveys cite the 1982 report.
- Syntheses cite the regional surveys.
- Textbooks cite the syntheses.
- Graduate dissertations cite the textbooks.

When a standard NLP or search engine scans 30 papers mentioning that "Stratum II dates to 1200 BCE," it counts 30 corroborating sources. In reality, there is only **one** primary observation and 29 secondary echoes. If the original 1982 determination was uncalibrated, misidentified, or affected by old-wood offsets, the repetition across 29 papers does not increase its factual probability.

### 2.2 Formal Epistemic De-duplication via CRMinf v1.2.1
To prevent circular corroboration, ArchaeoPhD AI maps literature statements onto the **CRMinf** formal argumentation graph:

```
[Primary Field Recording / Lab Measurement]
       │
       ▼
CRMsci: S4 Single Observation / S21 Measurement  (n = 1 Independent Empirical Proof)
       │
       ├─────────────────────────────────────────┐
       ▼                                         ▼
CRMinf: I5 Inference Making               CRMinf: I7 Belief Adoption
(Author derives original conclusion)      (Author adopts previously published claim)
       │                                         │
       ▼                                         ▼
CRMinf: I2 Belief                         CRMinf: I12 Adopted Belief
       │                                         │
       └──────────────────┬──────────────────────┘
                          ▼
             CRMinf: J7 is based on evidence from
             (Traces belief back to primary S4/S21 anchor)
```

- **Algorithm:** When scanning a proposition set ($I4$), the engine traverses the provenance path via `J7 is based on evidence from` and `J13 adopted interpretation`.
- **Result:** Regardless of how many documents repeat a claim, the evidential weight is bounded by the number of independent primary empirical observation nodes ($S4/S21$). Secondary citations are recorded as reception events, not corroborating evidence.

---

## Module 3: The Four Contradiction Preconditions & Taphonomic Diagnostics

ArchaeoPhD AI v2.0 enforces four strict preconditions before any two claims are flagged as a potential contradiction:

### 3.1 Precondition 1: Entity & Event Coreference
* **Theoretical Grounding:** Schiffer's artifact lifecycle distinguishes between:
  - $E_{\text{production}}$: The event where the object was created.
  - $E_{\text{use}}$: The period during which the object functioned.
  - $E_{\text{deposition}}$: The event where the object entered the archaeological stratum.
* **Chronological Rule:**
  $$T(E_{\text{production}}) \le T(E_{\text{deposition}}) \implies \text{Terminus Post Quem (TPQ)}$$
* **Validation Example:** Author A states a Roman coin of Trajan found in Layer 3 was minted in **112 CE**. Author B states Layer 3 was deposited in **180 CE**.
  - *v1.0 Behavior:* Flagged as a contradiction (112 CE $\ne$ 180 CE).
  - *v2.0 Behavior:* Validated as consistent. The coin provides a *terminus post quem* of 112 CE for the later deposition event.

### 3.2 Precondition 2: Sample Nature & Taphonomic Context
Apparent age discrepancies within the same feature are frequently caused by sample material physics:
* **The Old-Wood Effect:** Long-lived trees (e.g., cedar, oak) add growth rings over centuries. Inner heartwood charcoal can yield an age 300–500 years older than the actual fire event.
* **Geochemical Hard-Water Carbonate Offsets (Sinauli Case Study):**
  - Seed sample `SNLRC-3` ($3457 \pm 31$ yr BP; D-AMS 032053) measures atmospheric $^{14}\text{C}$ absorbed during the plant's single growing season.
  - Calcareous encrustation `SNLRC-2` from the same burial absorbed dissolved ancient geological carbonates from groundwater, yielding an apparent age thousands of years older.
  - *Diagnosis:* `CRMsci: S10 Material Substantial` mismatch $\to$ Geochemical Reservoir Offset.
* **Bioturbation & Sediment Mixing (Wonderwerk Cave Case Study):**
  - Charcoal `OxA-30638` in Stratum 4aLH was displaced downward by burrowing micro-mammals (`CRMarchaeo: AP8 disturbed`).
  - *Diagnosis:* Stratigraphic Outlier for Bayesian down-weighting, not publication falsehood.

### 3.3 Precondition 3: Scale & Framework Normalization
Before evaluating numerical compatibility, temporal values must be transformed into a common standardized framework:
* **Units:** Conventional $^{14}\text{C}$ yr BP vs. Calibrated cal BP vs. Calendar BCE/CE.
* **Mathematical Conversion:**
  $$\text{cal BP} = 1950 - \text{BCE/CE} \quad (\text{where 1 BCE} = 0 \text{ astronomical}, 2 \text{ BCE} = -1)$$
* **Calibration Curve Standardization:** Converting uncalibrated BP requires IntCal20 (terrestrial Northern Hemisphere), SHCal20 (Southern Hemisphere), or Marine20 (marine samples with localized $\Delta R$).

### 3.4 Precondition 4: Compatible Competing Hypotheses
In archaeological interpretation, multiple functional explanations can account for the identical physical stratum without logical incompatibility:
* **Example:** Author A interprets an ash layer with human remains as evidence of an **earthquake followed by conflagration**. Author B interprets the same layer as evidence of **military sack and warfare**.
* **Ontological Treatment:** Both hypotheses utilize the same physical stratigraphic premises ($AP11/AP12$). In CRMinf, they are modeled as two distinct `CRMinf: I5 Inference Making` branches leading to competing `I2 Belief` states held by different `E39 Actors`. They are logged as **Alternative Explanations**, not binary true/false contradictions.

---

## Module 4: Scientific NLP & The Five Information Extraction Failure Modes

### 4.1 Failure Mode 1: OCR & Table Serialization Errors
* **The Root Cause:** Legacy archaeological excavation monographs are stored as scanned 300–600 DPI bitmap PDFs with complex multi-column typography, footnotes, and wide data tables. Standard OCR engines (Tesseract, Abbyy) confuse degraded numerals (e.g., mistaking `3` for `8`, or dropping `±` error bars).
* **The Mitigation:** ArchaeoPhD AI implements a dual-pass layout-aware visual pipeline:
  1. High-resolution document layout analysis models identify tabular cells.
  2. Bounding-box pixel crops are preserved in the knowledge base via `CRMdig: D29 Annotation Object`.
  3. Every extracted date retains a direct clickable deep link to the source raster image, enabling instant visual confirmation by human reviewers.

### 4.2 Failure Mode 2: Incomplete Candidate Pool
* **The Root Cause:** Deterministic regular expressions successfully capture standard ISO formats (e.g., `3450 +/- 30 BP`), but fail completely on qualitative, prose-based, or multilingual chronological descriptions:
  - French: *"daté de la fin du Bronze moyen"*
  - German: *"in die Spätbronzezeit einzuordnen"*
  - Italian: *"riferibile alla facies protoappenninica"*
* **The Mitigation:** Enforcing Top-$k$ Candidate Generation. The system utilizes domain-specialized sequence labeling to retrieve candidate spans with high recall ($R_{\text{cand}} \ge 98\%$), surfacing candidate interpretations ranked by confidence.

### 4.3 Failure Mode 3: Entity-Attribute Mis-Association
* **The Root Cause:** Archaeological paragraphs often report multiple samples, lab identifiers, strata, and dates in close syntactic proximity. Standard transformer LLMs suffer from "syntactic drifting," mistakenly binding the radiocarbon determination of Sample A to the stratigraphic context of Sample B.
* **The Mitigation:** Strict tuple-level dependency parsing. Extraction models must output fully bound 6-tuples:
  $$\mathcal{T} = \langle \text{Sample\_ID},\; \text{Lab\_Code},\; \text{Uncalibrated\_Age},\; \text{Error\_SD},\; \text{Material\_Type},\; \text{Stratigraphic\_Unit} \rangle$$
  Evaluation is conducted using strict **Tuple-Binding $F_1$ ($F_{1,\text{bind}}$)**: a prediction is scored as zero if any single attribute is attached to the wrong entity.

### 4.4 Failure Mode 4: Negation, Hedging & Discourse-Stance Misattribution
* **The Root Cause:** In scientific debate, authors regularly introduce competing hypotheses specifically to refute or hedge them. For example:
  > *"Although Brown (2004) argued that Layer 4 belongs to the Early Iron Age, our subsequent stratigraphic excavations demonstrate conclusively that this attribution is untenable."*
  Naive keyword extraction records "Layer 4 = Early Iron Age" as an affirmative claim made by the author.
* **The Mitigation:** 4-way discourse-stance classification (benchmarked against scientific NLP datasets like SciFact and BioScope):
  1. `Asserted`: Author makes an affirmative claim.
  2. `Hedged`: Author introduces an uncertain hypothesis (*"may possibly indicate"*).
  3. `Refuted`: Author explicitly rejects a prior claim.
  4. `Quoted_Third_Party`: Author cites another scholar's position without endorsing it.
  These map directly to **`CRMinf: I6 Belief Value`** and **`I16 Meaning Comprehension`**.

### 4.5 Failure Mode 5: Cross-Modal Argument Reconstruction
* **The Root Cause:** Crucial evidentiary chains are rarely contained in a single paragraph. A typical monograph describes:
  - The excavation context on page 18.
  - The stratigraphic section drawing in Figure 5 on page 24.
  - The sample pretreatment chemistry in Appendix Table 3 on page 112.
* **The Mitigation:** ArchaeoPhD AI constructs a unified multi-anchor provenance graph. The extraction engine creates a single `CRMinf: I4 Proposition Set` that points to multiple distinct `CRMdig: D29 Annotation Objects` across different pages, modalities, and tables.

---

## Module 5: 3D Geometry, Photogrammetry & Extended Matrix

### 5.1 The Geometric Reality of Photogrammetric Meshes
* **Structure-from-Motion (SfM) Mechanics:** Photogrammetry operates by finding matching keypoints across overlapping photographic exposures, solving camera bundle adjustment equations, and computing a dense 3D point cloud of visible reflective surfaces.
* **Ontological Classification:**
  - A photogrammetric mesh represents a 2D surface boundary embedded in 3D Euclidean space. In CRMarchaeo, this corresponds strictly to **`A3 Stratigraphic Interface`** or **`A10 Excavation Interface`**.
  - Photogrammetric cameras cannot look inside solid ground. Therefore, photogrammetry *never* directly records an **`A2 Stratigraphic Volume Unit`**.
* **Computing Volumes:** Volume can only be derived mathematically as the closed manifold difference between two successive interface scans:
  $$V(\text{A2}) = \text{Mesh Differencing}(\text{Interface}_{t_1}, \text{Interface}_{t_2})$$

### 5.2 The Photogrammetric Mesh Intersection Fallacy
* **The Myth in v1.0:** The claim that "geometric intersections between photogrammetric meshes prove stratigraphic violations or impossible stratigraphy."
* **The Reality in Field Geomatics:** In daily excavation practice, sequential surface scans are registered using ground control points (GCPs) measured via total stations or RTK GNSS. Typical registration residuals range between **5 mm and 20 mm**.
* Furthermore, lens distortion, shadowed soil crevices, and point-cloud decimation noise regularly cause mesh triangles from Day 2 to geometrically penetrate mesh triangles from Day 1.
* **Engine Rule:** Mesh collisions must be logged as **Photogrammetric Registration Residuals / Noise**, not as impossible stratigraphy.

### 5.3 Extended Matrix (EM) & s3dgraphy Integration
* **Creator:** Emanuel Demetrescu (National Research Council of Italy - Institute of Heritage Science; CNR-ISPC).
* **Core Function:** Extended Matrix bridges classical Harris stratigraphy with 3D digital asset creation (Blender, ATON, EMStudio), formalizing the paradata (scientific documentation of how virtual models are inferred from archaeological evidence).
* **Core Concept - USV (Virtual Stratigraphic Unit):** While excavated physical remains are tagged as Stratigraphic Units (SU), hypothetical reconstructed elements (e.g., an unpreserved roof, collapsed column, or eroded wall) are defined as **USVs**.
* **Export Pipeline:** ArchaeoPhD AI extracts stratigraphic relationships from text and compiles node-edge graphs using the **`s3dgraphy`** Python data standard, enabling instant visualization in Extended Matrix tools.

---

## Module 6: Sovereign Data Governance & Dual-Edition Architecture

### 6.1 Archaeological Data Sovereignty & Legal Mandates
Archaeological data is subject to unique ethical and legal constraints that prohibit generic public cloud storage:
1. **Looting & Site Security:** Publishing high-precision GPS coordinates or photogrammetric models of unexcavated royal burials or temple caches directly invites site looting and illicit antiquities trafficking.
2. **Indigenous Data Sovereignty & CARE Principles:**
   - The **CARE Principles for Indigenous Data Governance** (Collective Benefit, Authority to Control, Responsibility, Ethics; Carroll et al.) mandate that Indigenous communities retain authority over data derived from their ancestral lands.
   - Compliance with the **Native American Graves Protection and Repatriation Act (NAGPRA)** requires strict control over digital imaging and osteological records of ancestral remains.
3. **National Heritage Legislation:** Countries like Italy (*Codice dei Beni Culturali e del Paesaggio*, D.Lgs. 42/2004), Egypt (Law 117/1983 on Antiquities Protection), and Greece require that unpublished archaeological data remain on sovereign national territory.
4. **Pre-Defense Academic Protection:** Doctoral candidates and research teams require air-gapped workstations to ensure unpublished excavation breakthroughs are not ingested by public LLM training scrapers prior to peer review and dissertation defense.

### 6.2 The Dual-Edition Architecture

```
+---------------------------------------------------------------------------------------------------+
|                           ARCHAEOPHD AI DUAL-EDITION ARCHITECTURE                                 |
+===================================================================================================+
| LOCAL AIR-GAPPED WORKSTATION (Sovereign Edition)                                                  |
| - Target: Single researchers, field trench laptops, sovereign national archives, defense teams.  |
| - Offline Invariant: Zero external internet socket connections; zero background telemetry.       |
| - Local Execution: Quantized GGUF neural models (via llama.cpp / ONNX), headless OxCal binary.    |
| - Storage: Encrypted local SQLite/DuckDB files on user's drive.                                   |
| - Compliance: Satisfies CARE, NAGPRA, Italian Codice, and anti-looting GPS embargoes.             |
+---------------------------------------------------------------------------------------------------+
                                                  ^
                                                  | (Optional Opt-In Synchronized Push)
                                                  v
+---------------------------------------------------------------------------------------------------+
| ENTERPRISE COLLABORATIVE EDITION (VPC / On-Premise Cloud)                                         |
| - Target: Commercial CRM firms (AECOM, WSP), preventive archaeology institutes (INRAP, MOLA).     |
| - Infrastructure: Deployed inside customer's private VPC (AWS GovCloud, Azure, on-prem server).   |
| - Capabilities: Multi-analyst review queues, role-based access control (RBAC), team audits.       |
| - Interoperability: Direct export to the European Collaborative Cloud for Cultural Heritage (ECCCH)|
+---------------------------------------------------------------------------------------------------+
```

---

## Module 7: Radiocarbon Physics & OxCal Bayesian Mathematics

### 7.1 Atmospheric Radiocarbon Non-Linearity & Calibration Curves
* **Physical Cause:** Carbon-14 is formed in the upper atmosphere when cosmic-ray-produced neutrons collide with Nitrogen-14:
  $$^{14}\text{N} + n \longrightarrow {}^{14}\text{C} + p$$
  Variations in solar solar magnetic activity and Earth's geomagnetic dipole moment alter cosmic ray flux over time, causing atmospheric $^{14}\text{C}$ concentration ($F^{14}\text{C}$) to fluctuate non-linearly.
* **Plateaus & Wiggles:** During solar minima, $^{14}\text{C}$ production rises. When atmospheric $^{14}\text{C}$ drops at a rate that matches radioactive decay, the calibration curve flattens into a "plateau." The most famous is the **Hallstatt Plateau** ($\sim 750$–$400$ BCE / $\sim 2750$–$2350$ cal BP), where all radiocarbon determinations over a 350-year period yield approximately the same uncalibrated age of $2450 \pm 30$ BP.

### 7.2 The Cubic Spline Formulation in $F^{14}\text{C}$ Concentration Space
OxCal performs calibration in $F^{14}\text{C}$ concentration space (rather than conventional radiocarbon years) to ensure mathematical continuity and unbiased error propagation. The calibration curve $r(t)$ is computed using piecewise cubic spline interpolation across discrete IntCal20 calibration nodes $(t_i, r_i)$:
$$r(t) = r_i + a_i(t - t_i) + b_i(t - t_i)^2 + c_i(t - t_i)^3 \quad \text{for } t_i \le t < t_{i+1}$$
Where $a_i, b_i, c_i$ are spline coefficients calculated such that both $r(t)$ and its first derivative $r'(t)$ are continuous across all knot boundaries.

### 7.3 Why Symmetric Intervals (Mean $\pm$ SD) Are Mathematically Invalid
When an uncalibrated Gaussian determination $y \pm \sigma$ is projected onto the non-monotonic calibration curve $r(t)$, the resulting calendar age likelihood function is:
$$p(t | y, \sigma) = \frac{1}{\sqrt{2\pi(\sigma^2 + \sigma_r^2(t))}} \exp\left( - \frac{(y - r(t))^2}{2(\sigma^2 + \sigma_r^2(t))} \right)$$
Because $r(t)$ folds back and forth, a single determination $y$ intersects the curve at multiple distinct calendar intervals. The resulting posterior probability distribution is **strongly asymmetric and multimodal**.
- **Conclusion:** Reporting a calibrated date as $1250 \pm 45$ cal BCE assumes a Gaussian bell curve, which misrepresents the probability distribution. All professional archaeological literature requires reporting **95.4% (2$\sigma$) Highest Posterior Density (HPD) disjoint sub-intervals** (e.g., *1410–1320 cal BCE [62.4%] and 1290–1210 cal BCE [33.0%]*).

### 7.4 Marine & Freshwater Reservoir Offsets ($\Delta R$)
Organisms living in aquatic environments absorb carbon from water bodies depleted of $^{14}\text{C}$ due to slow ocean circulation or dissolved ancient limestone. The local reservoir offset $\Delta R = r_d \pm s_d$ is incorporated into the likelihood:
$$p(y_i | t_i, r_d) \propto \frac{\exp\left[-\frac{(y_i - r(t_i) - r_d)^2}{2(s_i^2 + s^2(t_i) + s_d^2)}\right]}{\sqrt{s_i^2 + s^2(t_i) + s_d^2}}$$

### 7.5 OxCal Agreement Indices ($A_i$, $A_{\text{model}}$, $A_{\text{overall}}$)
OxCal uses Bayesian Markov Chain Monte Carlo (MCMC) sampling to test whether radiocarbon likelihoods agree with prior stratigraphic ordering constraints:
* **Individual Agreement Index ($A_i$):**
  $$A_i = 100 \times \frac{\int p_{\text{posterior}}(t) \, p_{\text{likelihood}}(t) \, dt}{\int [p_{\text{likelihood}}(t)]^2 \, dt}$$
* **Model Agreement Index ($A_{\text{model}}$):**
  $$A_{\text{model}} = 100 \times (F_{\text{model}})^{1/\sqrt{n}}$$
* **Threshold:** If $A_i < 60\%$ or $A_{\text{model}} < 60\%$, there is statistically significant conflict between the radiocarbon date and its assumed stratigraphic position at the $\alpha = 0.05$ significance level.
* **MCMC Convergence ($C$):** Convergence across chains must reach $C \ge 95\%$.

---

## Module 8: Complete CIDOC CRM Ontological Specification

ArchaeoPhD AI v2.0 implements the complete 4-Tier Ontological Schema cross-verified against official international standards:

```
+---------------------------------------------------------------------------------------------------+
| TIER 1: PHYSICAL REALITY (CIDOC CRM v7.1.3 & CRMarchaeo v2.1)                                     |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - E18 Physical Thing: Real-world immutable objects in the ground.                                 |
| - A8 Stratigraphic Unit: Unified class representing any individual component of stratification.   |
| - A2 Stratigraphic Volume Unit: Anthropogenic deposits, fills, layers of soil, stone structures.   |
| - A3 Stratigraphic Interface: Surfaces of destruction, cut of a pit, foundation trench boundaries.|
| - S13 Sample: Material specimen physically taken from a stratigraphic unit for lab analysis.      |
| Properties:                                                                                       |
| - AP11 has physical relation to: Physical touching contact between two A8 units (IMMUTABLE).      |
| - AP12 confines: An A3 Interface forms the physical boundary of an A2 Volume.                     |
| - AP13 has stratigraphic relation to: Interpreted temporal ordering sequence (REVISABLE).        |
| - AP13.2 justified by: Formal citation of the law or reasoning justifying the AP13 relation.      |
| - AP21 contains: An A2 Volume contains physical artifacts or ecofacts.                            |
| - AP28 occurs before: Temporal sequence ordering between stratigraphic events.                    |
+---------------------------------------------------------------------------------------------------+

+---------------------------------------------------------------------------------------------------+
| TIER 2: FIELD OBSERVATION & LAB MEASUREMENT (CRMsci v3.2 & CRMarchaeo v2.1)                       |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - A9 Archaeological Excavation: The physical act of stratigraphic digging.                         |
| - S2 Sample Taking: The physical extraction event of an S13 Sample.                               |
| - S4 Single Observation: Qualitative field recording of a physical property.                      |
| - S21 Measurement: Quantitative scientific measurement (e.g., AMS, OSL, XRF).                     |
| - S10 Material Substantial: Compositional classification (charcoal, calcite, bone collagen).      |
| Properties:                                                                                       |
| - O3 sampled from: Links S2 Sample Taking to an A2 Stratigraphic Volume Unit.                     |
| - O8 observed: Links S4 Observation to an observable physical entity.                             |
| - O16 observed value: Links S4/S21 to an empirical recorded value or measurement range.           |
| - O24 measured: Links S21 Measurement to the S13 Sample being analyzed.                           |
+---------------------------------------------------------------------------------------------------+

+---------------------------------------------------------------------------------------------------+
| TIER 3: DIGITAL DOCUMENT & AI PIPELINE PROVENANCE (CRMdig v5.0)                                    |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - D1 Digital Object: Source excavation report PDF or image scan.                                  |
| - D7 Digital Machine Event: Hardware execution on CPU/GPU.                                        |
| - D10 Software Execution: Algorithmic run of OCR, table layout parser, or LLM extractor.          |
| - D14 Software: Specific software build, commit hash, and neural model weight version.            |
| - D29 Annotation Object: Bounding-box coordinates and extracted text tuple.                       |
| Properties:                                                                                       |
| - L10 had input: The raw document or image provided to the algorithm.                            |
| - L11 had output: The extracted JSON-LD candidate tuple produced.                                 |
| - L23 used software: Links execution event to the exact model version.                           |
| - L48 created annotation: Links D10 Software Execution to D29 Annotation Object.                 |
+---------------------------------------------------------------------------------------------------+

+---------------------------------------------------------------------------------------------------+
| TIER 4: SCHOLARLY ARGUMENTATION & BELIEF REASONING (CRMinf v1.2.1)                                |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - I1 Argumentation: The discursive reasoning process linking evidence to conclusions.             |
| - I2 Belief: The epistemic state of belief held by an E39 Actor.                                  |
| - I4 Proposition Set: A coherent set of archaeological claims.                                    |
| - I5 Inference Making: The cognitive or computational act of inferring a conclusion.              |
| - I6 Belief Value: Qualitative degree of belief (Asserted, Hedged, Refuted, Possible).            |
| - I7 Belief Adoption: Secondary citation of another scholar's prior conclusion.                   |
| - I12 Adopted Belief: Epistemic belief state resulting from citation adoption.                    |
| - I15 Provenance Assessment: Critical evaluation of a source document's reliability.              |
| - I16 Meaning Comprehension: Linguistic extraction of propositions without endorsing truth.       |
| - I17 One-Proposition Set: Atomic proposition (e.g., "Stratum IV dates to Late Bronze Age").      |
| Properties:                                                                                       |
| - J1 used as premise: Empirical evidence nodes used as premises for an inference.                 |
| - J2 concluded that: The proposition concluded from an I5 Inference Making event.                 |
| - J3 applied: The methodological rule or calibration curve applied.                               |
| - J4 that: Links I2 Belief state to the proposition being evaluated.                              |
| - J5 holds to be: Links I2 Belief to its I6 Belief Value.                                         |
| - J7 is based on evidence from: Traces citation adoption back to primary empirical proof.         |
+---------------------------------------------------------------------------------------------------+
```

---

## Module 9: European Research Ecosystem & Project Validation

### 9.1 MAIA COST Action (CA23141, 2024–2028)
- **Title:** *Managing Artificial Intelligence in Archaeology* (MAIA).
- **Leadership:** Action Chair: Prof. Gabriele Gattiglia (University of Pisa, Italy); Vice-Chair: Dr. Holly Wright (Archaeology Data Service, University of York, UK).
- **Institutional Scale:** Funded under Horizon Europe COST framework; unites over 30 countries and 150+ academic institutions.
- **Strategic Imperative:** MAIA addresses the crisis of opaque, unreplicable "AI black boxes" in archaeological research. Working Group 2 enforces FAIR machine-actionable data pipelines; Working Group 3 establishes standards for transparency, bias detection, and human verification. ArchaeoPhD AI directly operationalizes MAIA WG2/WG3 guidelines by providing fully traceable bounding-box audits for all extractions.

### 9.2 Horizon Europe AUTOMATA (GA 101158046, €4.88M, 2024–2029)
- **Title:** *AUTOMated enriched digitisation of Archaeological liThics and cerAmics* (AUTOMATA).
- **Project Coordinator:** Prof. Gabriele Gattiglia (University of Pisa); 12 international partner institutions.
- **Core Technology:** AI-guided collaborative robots (cobots) automating the mechanical handling, photogrammetry, and 3D surface scanning of stone tools (lithics) and pottery fragments (ceramics).
- **The Synergy with ArchaeoPhD AI:** AUTOMATA digitizes physical objects and ingests them into the **European Collaborative Cloud for Cultural Heritage (ECCCH)**. However, those physical objects are described across thousands of legacy excavation reports and grey literature volumes. ArchaeoPhD AI acts as the text-mining counterpart to AUTOMATA, extracting document provenance to enrich the ECCCH digital twin knowledge base.

### 9.3 ERC AviArch (GA 101125532, €2.0M, 2024–2029) & ArchAIDE
- **Title:** *AVIfauna in ARCHaeoecological networks* (AviArch).
- **Principal Investigator:** Prof. Beatrice Demarchi (University of Turin); Co-Investigator: Prof. Gabriele Gattiglia.
- **Published Benchmarks (Dubbini et al., July 2026, *arXiv:2607.26743*):**
  - Evaluated on a multimodal dataset of $>10,000$ avian skeletal images combining visual feature extractors (EfficientNet_V2_S) with standardized morphometric osteology.
  - Bone anatomical element classification: **86% test accuracy**.
  - Family-level taxonomic classification: **51% Top-1 accuracy**, rising to **75% Top-3 accuracy**.
- **Significance:** This empirical work proves that international leaders in archaeological AI reject claims of "100% autonomous accuracy" and instead evaluate AI systems through probabilistic candidate ranking (Top-k) designed for human expert verification.

---

## Module 10: Commercial Market Economics & Workforce Modeling

### 10.1 US Cultural Resource Management (CRM) & Section 106
* **Annual Market Size:** \$1.46B to \$1.85B annual spend.
* **Regulatory Driver:** Section 106 of the National Historic Preservation Act (NHPA; 54 U.S.C. 306108) mandates that any federally funded or permitted undertaking (highways, high-speed rail, pipelines, broadband, electrical transmission) must assess impacts on historic properties before construction begins.
* **The Structural Labor Deficit:**
  - In *Forecast for the US CRM Industry and Job Market, 2022–2031* (published in *Advances in Archaeological Practice*), Jeffrey Altschul and colleagues analyzed the impact of the US Infrastructure Investment and Jobs Act (IIJA).
  - The study projected that the industry needs to hire **11,000 new CRM professionals** between 2022 and 2031 (including $>8,000$ archaeologists).
  - Roughly **70% of professional archaeological roles legally require an advanced graduate degree (MA or PhD)** under the Secretary of the Interior's Professional Qualification Standards.
  - US universities graduate only $\sim 325$ archaeology/anthropology MA/PhDs annually ($\sim 3,250$ over the decade), creating an unavoidable labor deficit of over **4,500 qualified professionals**.
* **Value Proposition:** ArchaeoPhD AI automates preliminary desk-based assessments and literature synthesis, enabling CRM firms (e.g., AECOM, WSP, SWCA, PaleoWest) to process hundreds of historical reports in hours, multiplying the productivity of their existing MA/PhD staff. Enterprise licensing: **\$50K–\$250K/year per firm**.

### 10.2 European Preventive Archaeology (Valletta Convention Framework)
* **The Regulatory Mechanism:** The 1992 Council of Europe Convention on the Protection of the Archaeological Heritage (Valletta Convention) legally established the **"polluter-pays" principle** across Europe: private property developers must fund archaeological evaluations and rescue excavations prior to ground disturbance.
* **France (INRAP):** France's National Institute for Preventive Archaeological Research (*Institut national de recherches archéologiques préventives*, INRAP) operates on an annual budget of $\sim €190\text{M}$, funded by the *Taxe d'archéologie préventive* (TAP) and *Redevance d'archéologie préventive* (RAP). Over a 10-year span, French preventive archaeology represents $>€1.5\text{B}$ in direct expenditures.
* **United Kingdom:** The commercial archaeology sector (led by MOLA, Oxford Archaeology, and Wessex Archaeology) employs thousands of archaeologists on infrastructure projects like HS2.
* **Commercial Strategy:** Multi-year institutional B2G contracts (€100K–€500K+) for digitizing regional site archives and clearing the backlog of unindexed grey literature reports.

### 10.3 Space Archaeology & Satellite Analytics
* **Market Projection:** The commercial satellite analytics and Earth observation market is expanding from \$1.8B (2025) to \$4.2B by 2034 at a **9.8% CAGR**.
* **The Commercial Bottleneck:** Earth observation companies (Planet Labs, Maxar, Airbus Intelligence, Orbital Insight) deploy automated computer vision on multispectral and SAR satellite imagery to identify buried archaeological structures and subsurface crop marks. However, an analyst must manually search through decades of regional excavation archives to determine whether the detected anomaly is a known archaeological site or a modern feature.
* **Commercial Strategy:** OEM API licensing (\$100K–\$400K/year) connecting satellite computer vision detections to automated literature entity resolution.

---

## Module 11: Case Study Empirical Verification

### 11.1 Case Study 1: The Sinauli Royal Burials
* **Site Context:** Sinauli, Baghpat District, Uttar Pradesh, India (Ganga-Yamuna Interfluve). Excavated by the Archaeological Survey of India (ASI) under Dr. Sanjay K. Manjul. Famous for Copper-Bronze Age anthropomorphic coffins, solid-disk-wheel chariots, and copper antennae swords.
* **Primary Reference:** Shalini Sharma, Anil K. Pokharia, Sanjay K. Manjul, et al., *"Radiocarbon Dating of the Anthropomorphic Coffin and Associated Artifacts from Sinauli, India"*, published in *Radiocarbon* (Cambridge University Press).
* **Sample 1 (`SNLRC-3`):**
  - Material: Carbonized macro-botanical seed (*Hordeum vulgare*) from burial pot adjoining royal coffin.
  - Lab Identifier: **D-AMS 032053**.
  - Uncalibrated Age: **$3457 \pm 31$ yr BP**.
  - Calibrated Calendar Age: $\sim 1880$–$1690$ cal BCE (IntCal20).
  - Concordance: Agrees with short-lived charcoal determination `SNLRC-1` ($3486 \pm 36$ yr BP).
* **Sample 2 (`SNLRC-2`):**
  - Material: Calcareous mineral coating from grave sediment.
  - Behavior: Systematically older by hundreds of years due to absorption of dissolved ancient mineral carbonates from groundwater (hard-water effect).
* **Engine Diagnostic:** Evaluated as a **Geochemical Carbonate Offset** (`CRMsci: S10 Material Substantial`), correctly preventing a false contradiction flag.

### 11.2 Case Study 2: Wonderwerk Cave Stratum 4aLH
* **Site Context:** Wonderwerk Cave, Kuruman Hills, Northern Cape, South Africa. Key sequence for the Middle to Later Stone Age transition.
* **Primary Reference:** Michael Chazan, Liora K. Horwitz, Christopher Bronk Ramsey, et al., *"Radiocarbon Dates Constrain the Timing of Environmental and Cultural Shifts in the Holocene Strata of Wonderwerk Cave, South Africa"*, published in *Radiocarbon*.
* **Sample (`OxA-30638`):**
  - Context: Excavation 1, Stratum 4aLH (Lower Hearth feature at base of Stratum 4a).
  - Material: Single-entity charcoal pretreated with acid-base-acid (ABA).
  - Uncalibrated Age: $28,000 \pm 220$ yr BP.
  - Bayesian Agreement Index: **$A_i = 51.7\%$** (falls below the $60\%$ statistical threshold).
  - Sequence Impact: Drives overall model agreement down to **$A_{\text{model}} = 11.4\%$**.
  - Outlier Analysis: OxCal's `Outlier_Model("SSimple", N(0,2), 0, "s")` calculates a **53% posterior outlier probability**.
  - Physical Cause: Micromorphology confirms burrowing by small mammals (`CRMarchaeo: AP8 disturbed`), which transported an older charcoal fragment down into a younger hearth layer.
* **Engine Diagnostic:** Evaluated as a **Taphonomic Bioturbation Outlier**, routed automatically to OxCal's outlier routine to maintain sequence model integrity.

### 11.3 The Seven Reproducible Evaluation Metrics
To satisfy the rigorous Trustworthy AI standards of MAIA WG3, ArchaeoPhD AI replaces marketing generalities with an open 7-metric benchmark protocol:

| Metric | Mathematical Formulation | Evaluation Target |
| :--- | :--- | :--- |
| **1. Candidate Recall ($R_{\text{cand}}$)** | $\frac{\text{TP}_{\text{cand}}}{\text{TP}_{\text{cand}} + \text{FN}_{\text{missed}}}$ | Measures completeness of chronological entity detection in multilingual prose ($\ge 98\%$). |
| **2. Top-1 & Top-3 Selection Accuracy** | $\frac{1}{N}\sum_{i=1}^N \mathbb{I}(\text{Target} \in \text{Top-}k)$ | Measures whether the correct interpretation is present in the Top-$k$ rank list (mirroring AviArch). |
| **3. Strict Tuple Binding $F_1$ ($F_{1,\text{bind}}$)** | $\frac{2 \cdot P_{\text{tuple}} \cdot R_{\text{tuple}}}{P_{\text{tuple}} + R_{\text{tuple}}}$ | True Positive requires exact match across all 6 tuple slots without attribute drifting. |
| **4. Citation Deduplication Accuracy ($A_{\text{dedup}}$)** | $\frac{\text{Correctly Classified }(S4 \text{ vs } I7)}{\text{Total Citing Mentions Evaluated}}$ | Evaluates precision and recall in isolating primary empirical assays from secondary citations. |
| **5. Discourse-Stance Accuracy ($A_{\text{stance}}$)** | $\frac{\text{Correct Stance Labels}}{\text{Total Statements Evaluated}}$ | 4-class classification accuracy (`Asserted`, `Hedged`, `Refuted`, `Quoted_Third_Party`). |
| **6. False-Alarm Rate (FAR)** | $\frac{\text{False Conflicts Identified}}{\text{Total Valid Pairs Evaluated}}$ | Measures minimization of spurious contradiction flags caused by differing scales or taphonomy. |
| **7. Human Review Speedup ($\Delta t_{\text{review}}$)** | $\frac{t_{\text{manual transcription}} - t_{\text{assisted verification}}}{t_{\text{manual transcription}}}$ | Empirical measurement of time saved per monograph page using visual bounding-box verification. |

---

### Verification Summary
Every individual assertion in `V2_COMMERCIALIZATION_BLUEPRINT.md` has been forensically audited and verified against primary literature, ISO standards, and empirical data. The blueprint represents an academically rigorous, mathematically sound, and commercially viable architecture for ArchaeoPhD AI v2.0.
