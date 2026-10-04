# Document Extraction Engine (`DocumentExtractor`)

> **Subsystem Location:** [`desktop/engine/extraction/document_extractor.hpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/engine/extraction/document_extractor.hpp)  
> **Core Responsibility:** Ingest archaeological literature, extract structured domain entities, and enforce 100% verbatim citation grounding.

---

## 1. Extraction Pipeline Architecture

The ingestion pipeline converts unstructured, multi-column archaeological reports into structured knowledge graph nodes:

```text
Upload PDF (Read In Place)
       │
       ▼
Layout & Section Parser (Docling / Native Layout Analysis)
  - Identifies double-column academic formatting
  - Preserves locus registers and stratigraphic tables
  - Extracts page references and section hierarchies
       │
       ▼
Section Chunking & Matryoshka Vectorization
  - Chunks text by archaeological section boundaries (e.g. "Trench B", "Locus 402")
  - Generates 128-dim embeddings via nomic-embed-text-v1.5
       │
       ▼
Structured Extraction Pass (Local 7–8B Model)
  - Enforces strict JSON Schema prompting
  - Extracts: Sites, Strata, Loci, Artifacts, Date Claims, Interpretations
       │
       ▼
Anti-Hallucination Citation Grounding Verifier
  - Every extracted claim must match an exact verbatim substring in the source
  - If a quote cannot be found in the raw chunk, the claim is rejected
       │
       ▼
Unified Native Storage (Relational JSON + Binary Vector Store)
```

---

## 2. Structured Extraction Schema

The local 7–8B reasoning model operates under a fixed archaeological schema:

```json
{
  "doc_id": "string",
  "page_ref": "integer",
  "entities": {
    "sites": ["string"],
    "strata": ["string"],
    "loci": ["string"],
    "artifacts": ["string"],
    "chronological_claims": [
      {
        "dating_phrase": "string (e.g. 'c. 1400 BCE')",
        "start_bce": "integer",
        "end_bce": "integer",
        "basis": "string (e.g. 'scarabs', 'radiocarbon', 'Cypriot ceramics')",
        "exact_quote": "string"
      }
    ]
  },
  "interpretive_claims": [
    {
      "claim_text": "string",
      "confidence": "Verified | Contested | Speculative",
      "exact_quote": "string"
    }
  ]
}
```

---

## 3. Anti-Hallucination Citation Grounding

Generalist LLMs frequently hallucinate page numbers, invent fictional excavation trenches, or confuse BCE with CE. ArchaeoPhD solves this by requiring **verbatim citation grounding**:
1. When the 7–8B model produces an extraction, `DocumentExtractor::ExtractFromText()` extracts the accompanying `exact_quote`.
2. The engine executes a substring search (`raw_text.find(quote)`) against the source chunk.
3. If the quote does not exist verbatim, the extraction is flagged as `hallucinated_claims > 0` and discarded.
4. **Target Tolerance:** Exactly **0.0% hallucinations permitted**.

---

## 4. Ingestion Manager & Adversarial Gating (`IngestionManager`)

> **Subsystem Location:** [`desktop/engine/extraction/ingestion_manager.hpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/engine/extraction/ingestion_manager.hpp)  
> **Test Harness:** [`desktop/tests/test_ingestion_gating_adversarial.cpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/tests/test_ingestion_gating_adversarial.cpp)

Following Phase 0 empirical benchmarks, ArchaeoPhD enforces strict physical print classification and dual-plane data separation:

### 4.1 Default-Safe Ingestion & Zero-Heuristic Classification
- **Default-Safe to Class B:** Every newly ingested document defaults strictly to `CLASS_B` (Porous/Letterpress).
- **Physical Print Confirmation:** Upgrading to `CLASS_A` requires explicit confirmation of physical print attributes (opaque paper, high-contrast black-on-white text, and zero reverse-side ink bleed-through). Calendar year heuristics (e.g. `>1980`) are explicitly forbidden. Any malformed input string fail-safes to `CLASS_B`.

### 4.2 Two Distinct Data Planes: Search vs. Truth
To resolve the question of document discoverability before manual transcription:
1. **Unstructured Passage Retrieval Index (Search Plane):** On ingestion, rough OCR text is chunked and embedded into `VectorIndex` with `transcription_status = "UNVERIFIED_ROUGH_SCAN"`. Researchers can immediately search and find relevant passages across their entire library.
2. **Structured Knowledge Graph (Truth Plane):** Zero automated machine extractions are written to the Knowledge Graph for Class B documents. The truth plane is strictly reserved for verified consensus facts (Class A) or human double-entry (Class B).

### 4.3 Standing Design Principles Enforced in Code
1. **"A Blank Field is Safer Than a Plausible-Looking Wrong One":** `SaveManualTranscription` strictly commits human-entered fields. The desktop UI presents clean blank forms next to high-resolution document scans, avoiding cognitive confirmation bias on plausible machine hallucinations.
2. **Prominent Optical Crops in Verification Queue:** For Class A dual-engine candidate disagreements, the UI mandates prominent visual display of the source image crop before presenting candidate buttons or manual overrides.
3. **Mid-Session Reflag Purge:** If a researcher downgrades a document from Class A to Class B mid-session, all staged unconfirmed facts are purged immediately, and pending verification items are marked `REJECTED_DUE_TO_RECLASSIFICATION`.
