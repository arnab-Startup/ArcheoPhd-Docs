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
Unified Store (LanceDB Chunks + Graph Tables)
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
