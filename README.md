# ArchaeoPhD Technical Documentation Suite

> **Official Architecture, Domain Specifications, Engineering Plans & Native Workstation Systems**  
> *ArchaeoPhD — The Private, Fully Offline AI Research Workstation for Archaeological Academia.*

---

## 🧭 Documentation Directory

All documentation is organized hierarchically into dedicated domain and workstation modules:

```text
docs/
├── desktop/                 # Native C++ Desktop Workstation (Win32 + WebView2)
│   ├── architecture/        # Workstation specs, data root management, hardware matrix
│   ├── engine/              # Native C++ engines (Extraction, Contradictions, Storage, Vector)
│   ├── plans/               # MVP meeting plan & master engineering roadmaps
│   └── security/            # Airgap privacy guarantees & DPAPI offline licensing
└── domain/                  # Archaeological Knowledge Graph & Epistemology
    ├── PROBLEM_STATEMENT.md # "Connection crisis", dating clashes & LLM hallucination risk
    ├── PROJECT_OVERVIEW.md  # 3-layer grounding ontology (Finds -> Claims -> Evidence)
    └── README.md            # Domain index & epistemological guide
```

---

## 📂 Detailed Module Index

### 💻 1. [Desktop Workstation](desktop/) (`docs/desktop/`)
The native, air-gapped C++ research workstation:
* **[`architecture/`](desktop/architecture/)**:
  - [`ARCHITECTURE.md`](desktop/architecture/ARCHITECTURE.md): Native Win32 + WebView2 integration, zero open HTTP ports, direct in-process IPC (`chrome.webview.postMessage`), embedded payload extraction, native Windows message loop.
  - [`DATA_ROOT.md`](desktop/architecture/DATA_ROOT.md): User-chosen storage path, external SSD disconnect resilience, zero-cloud-leakage guardrails (OneDrive/iCloud/Dropbox blocklist).
  - [`SYSTEM_REQUIREMENTS.md`](desktop/architecture/SYSTEM_REQUIREMENTS.md): Hardware specs, AVX2 SIMD requirements, RAM footprints (16 GB recommended, 8 GB floor).
* **[`engine/`](desktop/engine/)**:
  - [`EXTRACTION.md`](desktop/engine/EXTRACTION.md): `DocumentExtractor`, PDF layout parsing, structured schema prompting, 100% verbatim grounding.
  - [`CONTRADICTIONS.md`](desktop/engine/CONTRADICTIONS.md): 4-tier contradiction engine, Tarjan's SCC for Harris Matrix stratigraphy cycles.
  - [`STORAGE_COMPRESSION.md`](desktop/engine/STORAGE_COMPRESSION.md): `NativeStorage` Zstandard with pre-trained shared dictionary, byte-for-byte SHA-256 verification.
  - [`VECTOR_SEARCH.md`](desktop/engine/VECTOR_SEARCH.md): 128-dim Matryoshka vector index (`nomic-embed-text-v1.5`), in-memory cosine similarity.
* **[`plans/`](desktop/plans/)**:
  - [`MVP_PLAN.md`](desktop/plans/MVP_PLAN.md): Focused meeting showcase MVP plan and Phase 0 extraction validation gates.
  - [`MASTER_PLAN.md`](desktop/plans/MASTER_PLAN.md): 15-feature long-term engineering and optimization roadmap.
* **[`security/`](desktop/security/)**:
  - [`AIRGAP_PRIVACY.md`](desktop/security/AIRGAP_PRIVACY.md): 100% offline guarantee protecting confidential excavation findspots.
  - [`PRICING_SECURITY.md`](desktop/security/PRICING_SECURITY.md): Ed25519 digital signatures, Windows DPAPI hardware encryption, anti-rollback monotonic clock.

---

### 🏛️ 2. [Domain & Epistemology](domain/) (`docs/domain/`)
Archaeological foundations and dissertation integrity:
* **[`PROBLEM_STATEMENT.md`](domain/PROBLEM_STATEMENT.md)**: The "connection crisis", 150-year chronological contradictions, lost spatial context, and PhD hallucination perils.
* **[`PROJECT_OVERVIEW.md`](domain/PROJECT_OVERVIEW.md)**: 3-layer ground-truth ontology linking physical finds, interpretive claims, and citations.
* **[`README.md`](domain/README.md)**: Overview of archaeological epistemological grounding and domain entity graph.
