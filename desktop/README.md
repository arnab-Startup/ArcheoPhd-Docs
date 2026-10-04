# ArchaeoPhD Desktop Workstation Documentation

> **Native C++ Standalone Research Environment**  
> Direct Win32 + WebView2 integration, zero open network sockets, local C++ vector and contradiction engines.

---

## 📂 Subdirectories & Modules

The desktop documentation is structured into the following deep modules:

### 🏛️ 1. [`architecture/`](architecture/)
Architecture specifications, user-controlled data root storage, and hardware requirements:
* **[`ARCHITECTURE.md`](architecture/ARCHITECTURE.md)**: Standalone Win32 + WebView2 architecture, direct in-process IPC (`chrome.webview.postMessage`), embedded payload extraction, native Windows message pump.
* **[`DATA_ROOT.md`](architecture/DATA_ROOT.md)**: User-chosen storage path, external SSD disconnect resilience, zero-cloud-leakage guardrails (OneDrive/iCloud/Dropbox blocklist).
* **[`SYSTEM_REQUIREMENTS.md`](architecture/SYSTEM_REQUIREMENTS.md)**: Hardware matrix, AVX2 SIMD prerequisites, RAM footprints (16 GB recommended, 8 GB floor).

### ⚙️ 2. [`engine/`](engine/)
Native C++ core computational engines:
* **[`CONTRADICTIONS.md`](engine/CONTRADICTIONS.md)**: 4-tier contradiction detection engine, Tarjan's Strongly Connected Components (SCC) for stratigraphic Harris Matrix cycles, review guardrails.
* **[`EXTRACTION.md`](engine/EXTRACTION.md)**: `DocumentExtractor` layout parsing, double-column PDF extraction, schema prompting, 100% verbatim citation grounding.
* **[`STORAGE_COMPRESSION.md`](engine/STORAGE_COMPRESSION.md)**: `NativeStorage` Zstandard compression with shared pre-trained archaeological dictionary, independent `.zst` archives, SHA-256 byte-for-byte fidelity.
* **[`VECTOR_SEARCH.md`](engine/VECTOR_SEARCH.md)**: `VectorIndex` 128-dimensional Matryoshka embeddings (`nomic-embed-text-v1.5`), atomic binary vector store (`vectors.bin`), and AVX2-accelerated in-memory cosine similarity.

### 📋 3. [`plans/`](plans/)
Roadmaps and milestone specifications:
* **[`MVP_PLAN.md`](plans/MVP_PLAN.md)**: Meeting showcase MVP specification, Phase 0 document extraction validation gates, thesis audit checklist.
* **[`MASTER_PLAN.md`](plans/MASTER_PLAN.md)**: Full 15-feature engineering roadmap, long-term scaling, and academic workflow milestones.

### 🔒 4. [`security/`](security/)
Air-gapped privacy and commercial licensing:
* **[`AIRGAP_PRIVACY.md`](security/AIRGAP_PRIVACY.md)**: 100% offline guarantee, zero network sockets, zero telemetry, protecting unpublished excavation sites and vulnerable heritage coordinates.
* **[`PRICING_SECURITY.md`](security/PRICING_SECURITY.md)**: Ed25519 digital licensing, Windows DPAPI hardware encryption (`CryptProtectData`), monotonic anti-clock-rollback, and 30-day offline grace period.

### 📊 5. [`report/`](report/)
Phase 0 empirical benchmarks, technical evaluation reports, and architectural decisions:
* **[`01_ocr_engine_and_preprocessing_benchmark.md`](report/01_ocr_engine_and_preprocessing_benchmark.md)**: 50-page, 166-fact blind ground-truth benchmark; Otsu/Sauvola binarization degradation finding; Class A (88.46%) vs Class B (53.23%–62.90%); 0% false consensus across 47 real errors.
* **[`02_dual_engine_routing_and_verification.md`](report/02_dual_engine_routing_and_verification.md)**: Native C++ Dual-Engine Router (`dual_engine_router.hpp`); deterministic 4-state machine; reproduction audit confirming 119 auto-accepted, 9 verification queue, 20 rejected, 18 hard-gated Class B.
* **[`03_vlm_degraded_scan_feasibility_investigation.md`](report/03_vlm_degraded_scan_feasibility_investigation.md)**: Local VLM feasibility on 1970s porous letterpress; visual patch downsampling resolution collapse; 4/7 silent corruptions; standing principle ("A blank field is safer than a plausible-looking wrong one; assistive pre-fill rejected"); Tier 3 triggered (Class B permanently manual).
* **[`README.md`](report/README.md)**: Master report index and summary of Phase 0 architectural principles.
