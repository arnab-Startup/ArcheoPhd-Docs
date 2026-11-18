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
* **[`UPDATE_AND_DATA_PERSISTENCE.md`](architecture/UPDATE_AND_DATA_PERSISTENCE.md)**: Zero-data-loss in-place auto-update, 4-Zone storage decoupling, atomic Win32 rename-replace swap, schema migrations, and automated cache/bundle garbage collection.

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

### 📊 5. [`reports/`](reports/)
Engineering benchmarks, empirical evaluation reports, and architectural decisions (Reports 01–12):
* **[`01_ocr_engine_and_preprocessing_benchmark.md`](reports/01_ocr_engine_and_preprocessing_benchmark.md)**: 50-page, 166-fact blind ground-truth benchmark; Otsu/Sauvola binarization degradation finding; Class A (88.46%) vs Class B (53.23%–62.90%); false consensus was unmeasured in Phase 0 (0.0% optical false consensus verified under span anchoring, but auto-accept is paused due to unit loss and neighbor numbers).
* **[`02_dual_engine_routing_and_verification.md`](reports/02_dual_engine_routing_and_verification.md)**: Native C++ Dual-Engine Router (`dual_engine_router.hpp`); deterministic 4-state machine; Class A auto-accept is paused in production with all candidate facts routed to verification queue pending Step 4 attribution.
* **[`03_vlm_degraded_scan_feasibility_investigation.md`](reports/03_vlm_degraded_scan_feasibility_investigation.md)**: Local VLM feasibility on 1970s porous letterpress; visual patch downsampling resolution collapse; 4/7 silent corruptions; standing principle ("A blank field is safer than a plausible-looking wrong one; assistive pre-fill rejected"); Tier 3 triggered (Class B permanently manual).
* **[`12_phase2_step3_entity_extraction_benchmark_report.md`](reports/12_phase2_step3_entity_extraction_benchmark_report.md)**: Span-anchored forensic audit of candidate-picker errors (22/80) vs optical misreads (0/80).
* **[`README.md`](reports/README.md)**: Master report index and summary of Phase 0 through Phase 2 engineering reports.

### 📐 6. [`specs/`](specs/)
Pre-registered engineering specifications and evaluation protocols:
* **[`01_phase2_step3_quantitative_entity_extraction_spec.md`](specs/01_phase2_step3_quantitative_entity_extraction_spec.md)**: Mention-level quantitative extraction grammar, astronomical date normalization, OCR anomaly flagging.
* **[`02_real_ocr_plausibility_evaluation_protocol.md`](specs/02_real_ocr_plausibility_evaluation_protocol.md)**: Real-OCR evaluation methodology and 166-fact plausibility benchmark protocol.
* **[`03_anchored_scorer_rules.md`](specs/03_anchored_scorer_rules.md)**: Deterministic span-anchored scoring rules, error classification taxonomy (Unit Lost, Partial, Displaced, Absent, Optical Misread).
* **[`04_phase2_step4_candidate_generator_and_attribution_spec.md`](specs/04_phase2_step4_candidate_generator_and_attribution_spec.md)**: Candidate generation data contract, semantic slot attribution, rejection rules, and 60-case sealed fail-only gate.

### 7. [`issue_reports/`](issue_reports/)
Comprehensive technical audits, architectural investigations, and domain-epistemological evaluations (Reports 01–17):
* **[`README.md`](issue_reports/README.md)**: Master directory index and archaeological epistemology principles.
* **Architecture & System Resilience**: Workspace separation ([Report 01](issue_reports/01_architecture_flow_and_workspace_separation.md)), data scoping ([Report 02](issue_reports/02_data_scoping_and_cross_project_contamination.md)), SPA routing ([Report 03](issue_reports/03_project_navigation_and_spa_routing_deadlock.md)), database runtime mutations ([Report 04](issue_reports/04_runtime_database_interface_and_bulk_operations.md)), legacy head cleanup ([Report 05](issue_reports/05_destructive_legacy_cleanup_in_index_head.md)), offline model concurrency ([Report 07](issue_reports/07_offline_model_inference_and_ipc_concurrency.md)), and WebView2 subroute reload ([Report 13](issue_reports/13_webview2_spa_subroute_reload_failure_and_white_screen.md)).
* **Visualization & Archaeological Epistemology**: Paradigm visualization gaps ([Report 06](issue_reports/06_domain_specific_archaeological_visualization_gap.md)), topological Harris Matrix ([Report 08](issue_reports/08_stratigraphic_harris_matrix_topological_engine.md)), Bayesian C-14 calibration ([Report 09](issue_reports/09_bayesian_radiocarbon_calibration_probability_splines.md)), Fordian seriation ([Report 10](issue_reports/10_fordian_seriation_and_ceramic_frequency_curves.md)), GIS catchment analysis ([Report 11](issue_reports/11_landscape_archaeology_palaeochannel_and_catchment_gis.md)), taphonomic weighting ([Report 12](issue_reports/12_epistemic_weighting_and_contextual_taphonomy_in_evidence_graph.md)), workbench integration ([Report 14](issue_reports/14_visualization_center_static_teaser_deadlock_and_fragmentation.md)), force-directed graphs ([Report 15](issue_reports/15_evidence_graph_rigid_columnar_svg_vs_dynamic_force_canvas.md)), TPQ/TAQ horizons ([Report 16](issue_reports/16_chronology_tpq_taq_horizon_bounds_and_stratigraphic_phasing.md)), and matrix semantic divergence ([Report 17](issue_reports/17_archaeological_matrix_tabular_misnomer_and_semantic_divergence.md)).
