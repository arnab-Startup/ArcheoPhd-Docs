# Specification: Phase 3 — Chronological Engine, Spatial Intelligence, Graph Traversal & Dissertation Defense Export

> **Document ID:** `SPEC-PHASE3-MASTER-BUILD-PLAN`  
> **Status:** APPROVED & ACTIVE  
> **Date:** October 7, 2026  
> **Authors:** ArchaeoPhD Core Architecture & Engineering Team  
> **Milestone Horizon:** Phase 3 (Steps 1–5)  
> **Pre-Flight Invariants:**  
> - 100% Native C++ offline execution; zero cloud leakage.  
> - Zero modification to `frontend/` source; IPC contracts strictly adhere to existing React schemas.  
> - Sealed Benchmark Dataset (`tests/step4_eval/step4_sealed_benchmark.json`, SHA-256 `4B9AD58F...`) remains unopened and unexecuted.  

---

## 1. Executive Summary & Architectural Scope

Phase 1 established the lossless ingestion, storage, and vector retrieval foundation.  
Phase 2 delivered the core Knowledge Graph, Harris Matrix DAG, Two-Tier Hybrid Attribution, Contradiction Engine, and Thesis Auditor.

**Phase 3** elevates ArchaeoPhD into a complete analytical research workstation by adding:
1. **Temporal Dimension (Step 1):** Continuous astronomical chronology, multi-site stratigraphic alignment, and IntCal20 C-14 radiocarbon calibration.
2. **Spatial Dimension (Step 2):** GeoJSON site serialization, spherical Haversine distance queries, and trench clustering.
3. **Network Dimension (Step 3):** Full Knowledge Graph traversal, centrality analysis, citation depth tracing, and isolated claim detection.
4. **Academic Synthesis (Step 4):** Automated BibTeX bibliography compilation, portable JSON research archives, and formatted Pre-Submission Dissertation Dossiers.
5. **Hardening & Signoff (Step 5):** Master test battery, release packaging, and live DOM validation.

---

## 2. Component Specifications & Data Architectures

```
┌────────────────────────────────────────────────────────────────────────────┐
│                        ArchaeoPhD Desktop Workstation                      │
│                                                                            │
│    ┌──────────────────────────────────────────────────────────────────┐    │
│    │                        PHASE 3 ENGINES                           │    │
│    │                                                                  │    │
│    │  [Step 1] Chronology Engine (`engine/analysis/chronology.hpp`)   │    │
│    │   - Astronomical Year Mapping: $[-10000, 2026]$ Continuous Line  │    │
│    │   - IntCal20 C-14 Calibration Curve (2-Sigma Probability Envelope)│    │
│    │   - Multi-Site Contemporaneous Stratigraphic Alignment           │    │
│    │                                                                  │    │
│    │  [Step 2] Spatial Intelligence Layer (`analysis/spatial.hpp`)    │    │
│    │   - GeoJSON FeatureCollection Serialization (WGS84 / Elevation)  │    │
│    │   - Haversine Geodesic Radius Queries ("Within R km")            │    │
│    │   - Locus & Trench Agglomerative Spatial Clustering              │    │
│    │                                                                  │    │
│    │  [Step 3] Graph Traversal Engine (`analysis/graph_engine.hpp`)   │    │
│    │   - Unified Multi-Entity Network: Sites ↔ Strata ↔ Claims ↔ Docs │    │
│    │   - Centrality Scoring, Isolated Claim Discovery & Cycle Auditing│    │
│    │   - Directed Path Tracing & Citation Chain Depth                 │    │
│    │                                                                  │    │
│    │  [Step 4] Dissertation Dossier Export (`analysis/export.hpp`)    │    │
│    │   - Standard BibTeX (`.bib`) Generation with Exact Page Citations│    │
│    │   - Formatted Pre-Submission Markdown/HTML Viva Defense Dossier  │    │
│    │   - Portable Zero-Loss JSON Archive (`.archaeophd.json`)         │    │
│    │                                                                  │    │
│    │  [Step 5] Master Verification Audit & Workstation Hardening      │    │
│    │   - Comprehensive F1–F15 Test Battery (100% Automated Pass)      │    │
│    │   - Standalone Release Rebuild (`release/ArchaeoPhD.exe`)        │    │
│    └──────────────────────────────────────────────────────────────────┘    │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 3. Step 1: Chronology Engine & Radiocarbon Calibration (`chronology.hpp`)

### 3.1 Problem Formulation
Archaeological dates appear in divergent formats: BCE, CE, BC, AD, uncalibrated radiocarbon years BP ($^{14}\text{C}\text{ BP}$), and stratigraphic cultural horizons (e.g. `EB III`, `MB IIB`, `LB I`). A researcher cannot synchronize regional sites without converting these expressions into an unambiguous mathematical timeline.

### 3.2 Astronomical Timeline Normalization
The engine normalizes all calendar dates to a continuous real-number astronomical timeline:
- $1\text{ BCE} = 0.0$
- $2\text{ BCE} = -1.0$
- $n\text{ BCE} = -(n - 1)$
- $n\text{ CE} = n$

```cpp
struct ChronoRange {
    double start_year;       // Astronomical year (negative = BCE)
    double end_year;
    bool is_approximate;     // e.g. "ca.", "circa", "approx."
    std::string period_label;
    std::string original_text;
};
```

### 3.3 IntCal20 Radiocarbon Calibration Algorithm
Uncalibrated radiocarbon determinations ($^{14}\text{C}\text{ BP} \pm \sigma$) cannot be directly subtracted from 1950 due to historical fluctuations in atmospheric $^{14}\text{C}/\text{C}$ ratios.
The engine includes a native embedded spline of the **IntCal20 Northern Hemisphere atmospheric calibration curve**:
- Input: Uncalibrated age $T_{\text{BP}}$ and uncertainty $\sigma_{\text{BP}}$ (e.g. $3450 \pm 40\text{ BP}$).
- Output: Calibrated calendar range $[T_{\min}, T_{\max}]$ in cal BCE/CE at $95.4\%$ ($2\sigma$) confidence.
- Advisory Flag: Automatically attaches `UNCALIBRATED_RADIOCARBON_BP` if raw BP is cited in a thesis claim without calibration.

### 3.4 Multi-Site Regional Synchronization
Given two sites $S_1$ and $S_2$, the engine calculates the temporal intersection:
$$\text{Overlap}(S_1, S_2) = [\max(S_1.\text{start}, S_2.\text{start}), \min(S_1.\text{end}, S_2.\text{end})]$$
If $\text{Overlap} > 0$, the sites are synchronized as contemporaneous, and their stratigraphic material cultures (e.g. ceramic horizons) are cross-referenced for chronological spread.

---

## 4. Step 2: Spatial Intelligence Layer (`spatial.hpp`)

### 4.1 Geographic Coordinate Modeling
Archaeological sites are represented with WGS84 geographic coordinates and vertical topographic elevations:

```cpp
struct GeoCoordinate {
    double latitude;
    double longitude;
    double elevation_meters;
    bool has_coordinates;
};
```

### 4.2 Haversine Geodesic Distance Formula
Calculates great-circle distance $d$ between two points $(\phi_1, \lambda_1)$ and $(\phi_2, \lambda_2)$ on Earth (mean radius $R = 6371.0\text{ km}$):
$$a = \sin^2\left(\frac{\Delta \phi}{2}\right) + \cos(\phi_1)\cos(\phi_2)\sin^2\left(\frac{\Delta \lambda}{2}\right)$$
$$c = 2 \cdot \text{atan2}\left(\sqrt{a}, \sqrt{1-a}\right)$$
$$d = R \cdot c$$

### 4.3 Radius Queries & Spatial Clustering
- `get_sites_within_radius(center_lat, center_lon, radius_km)`: Filters regional sites within a specified territory (e.g., "Find all Middle Bronze sites within 40 km of Jerusalem").
- Spatial clustering groups nearby excavation trenches and artifact distributions for rendering in `ResearchMap.jsx`.
- **IPC Endpoint:** `get_geographic_sites` returning a valid GeoJSON `FeatureCollection`.

---

## 5. Step 3: Evidence & Literature Graph Traversal Engine (`graph_engine.hpp`)

### 5.1 Graph Topology
The Knowledge Graph store is mapped into a directed heterogeneous graph:
- **Node Types:** `SITE`, `STRATUM`, `ARTIFACT`, `CLAIM`, `EVIDENCE_LINK`, `SOURCE`.
- **Edge Types:**
  - `CONTAINS` (Site $\to$ Stratum, Stratum $\to$ Artifact)
  - `STRATIFIED_ABOVE` (Stratum $\to$ Stratum, Harris relationship)
  - `EVIDENCED_BY` (Claim $\to$ EvidenceLink)
  - `GROUNDED_IN` (EvidenceLink $\to$ Artifact / Stratum / Site)
  - `CITES` (Claim $\to$ Source)
  - `CONTRADICTS` (Claim $\to$ Claim, Contradiction Engine link)

### 5.2 Network Analytics & Epistemic Audit
1. **Centrality Scoring:** Computes node degree and in-degree to identify foundational archaeological authorities and pivotal strata.
2. **Disconnected Claim Detection:** Isolates claims with in-degree 0 from Layer C (claims with zero empirical evidence links).
3. **Directed Path Tracing:** Identifies the shortest chain of evidence connecting a thesis assertion back to a physical excavation artifact.
4. **IPC Endpoint:** `get_graph_data` returning `{ "nodes": [...], "edges": [...], "metrics": {...} }`.

---

## 6. Step 4: Dissertation Dossier Export Engine (`export.hpp`)

### 6.1 BibTeX Exporter (`.bib`)
Generates standardized BibTeX bibliography entries for all sources in `project_id`:
```bibtex
@book{kenyon1978jericho,
  author = {Kenyon, Kathleen M.},
  title = {The Architecture and Stratigraphy of the Tell},
  year = {1978},
  publisher = {British School of Archaeology in Jerusalem},
  address = {London},
  pages = {42--58}
}
```

### 6.2 Pre-Submission Viva Defense Dossier (Markdown / HTML)
Produces an audit report ready for supervisor review:
- Chapter-by-chapter readiness summary and defense scores.
- Catalog of all Layer A physical entities and Layer B verified claims.
- High-risk viva examination questions generated from detected contradictions.
- List of ungrounded OCR anomalies requiring plate verification.
- Search-augmented literature citations for unsupported assertions.

### 6.3 Portable Offline JSON Archive (`.archaeophd.json`)
A complete cryptographic JSON dump of the local relational state, vector metadata, and Harris matrices for off-machine preservation and multi-workstation replication.
- **IPC Endpoint:** `export_thesis_dossier`.

---

## 7. Step 5: Master Verification Audit & Workstation Hardening

### 7.1 Regression Protocol
1. Compile and execute `tests/test_chronology.cpp`.
2. Compile and execute `tests/test_spatial_engine.cpp`.
3. Compile and execute `tests/test_graph_engine.cpp`.
4. Compile and execute `tests/test_export_engine.cpp`.
5. Execute the full Master Test Battery across all 15 native features (F1–F15).
6. Rebuild production binary via `build.bat` (`release/ArchaeoPhD.exe`).
7. Run `release/ArchaeoPhD.exe --test-ui-live` to confirm zero regressions across all live WebView2 DOM gates.

---

## 8. Milestone Sequence & Execution Roadmap

| Step | Milestone Target | Output Headers & Artifacts | Primary Verification Suite |
| :---: | :--- | :--- | :--- |
| **Step 1** | **Chronology Engine & C-14 Calibration** | `engine/analysis/chronology.hpp` | `tests/test_chronology.cpp` |
| **Step 2** | **Spatial Intelligence Layer** | `engine/analysis/spatial.hpp` | `tests/test_spatial_engine.cpp` |
| **Step 3** | **Evidence Graph Traversal Engine** | `engine/analysis/graph_engine.hpp` | `tests/test_graph_engine.cpp` |
| **Step 4** | **Dissertation Dossier Export** | `engine/analysis/export.hpp` | `tests/test_export_engine.cpp` |
| **Step 5** | **Hardening & Final Verification** | `release/ArchaeoPhD.exe` | Master Test Suite + Live UI |

---

## 9. Approval & Pre-Flight State

This specification is approved. Phase 3 implementation shall proceed sequentially starting with **Step 1: Chronology Engine & Radiocarbon Calibration (`chronology.hpp`)**.
