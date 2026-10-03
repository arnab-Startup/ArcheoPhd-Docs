# Storage & Lossless Compression Engine

> **Subsystem Location:** [`desktop/engine/storage/storage.hpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/engine/storage/storage.hpp)  
> **Core Responsibility:** Independent per-file archiving, trained dictionary compression, and byte-for-byte original document retrieval.

---

## 1. The Storage Architecture: Zstandard + Shared Trained Dictionary

ArchaeoPhD uses **per-file Zstandard compression with a pre-trained shared dictionary**:

```text
Upload PDF (Read In Place)
       │
       ▼
Zstandard Compress (Shared Dictionary: compression-dict.zstd)
       │
       ├─► Store as independent archive: archives/<doc_id>.zst
       │
       └─► Record in index.db: { doc_id: "...", filename: "<doc_id>.zst", sha256: "..." }
```

### Why a Shared Trained Dictionary?
Archaeological PDFs share immense cross-document structural redundancy:
- Identical PDF font tables, PostScript headers, and XML metadata.
- Repeated journal boilerplate (e.g. *Journal of Archaeological Science*, *Antiquity*, *American Journal of Archaeology*).
- Pre-training a small (4–8 KB) dictionary on representative archaeological papers allows Zstandard to compress these common patterns across documents without grouping the files into a single monolithic archive.

### Benchmark Validation
Tested across real and unseen holdout excavation reports:
- **No-Dictionary Plain Zip / Zstd:** ~73–76% reduction on born-digital text.
- **Zstandard WITH Trained Shared Dictionary:** **36.3% smaller than no-dictionary compression** on completely unseen holdout documents.

---

## 2. The Download-Original Contract (Byte-for-Byte SHA-256 Match)

A researcher must always be able to retrieve the exact original file they uploaded:
1. User clicks **"Download Original PDF"**.
2. Engine queries `index.db` for the `doc_id`.
3. Decompresses `archives/<doc_id>.zst` using `compression-dict.zstd`.
4. Verifies the SHA-256 checksum against `index.db`.
5. Hands the exact, uncorrupted PDF back to the researcher.
