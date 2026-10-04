# Vector Search & Semantic Indexing (`VectorIndex`)

> **Subsystem Location:** [`desktop/engine/analysis/vector_index.hpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/engine/analysis/vector_index.hpp)  
> **Core Responsibility:** Generate and search semantic text embeddings for localized archaeological retrieval.

---

## 1. 128-Dimensional Matryoshka Vectorization

Standard sentence embeddings (e.g. 768 or 1536 dimensions) consume excessive RAM and disk space on laptop hardware. ArchaeoPhD uses **`nomic-embed-text-v1.5`** with **Matryoshka representation learning**:

1. **Truncation:** The native 768-dim vector is truncated to the first **128 dimensions**.
2. **L2 Renormalization:**
   $$\vec{v}_{norm} = \frac{\vec{v}_{128}}{\|\vec{v}_{128}\|_2}$$
3. **RAM Footprint:** A 128-dim Float32 vector requires only **512 bytes per chunk** (or 128 bytes with Int8 quantization), allowing over 100,000 document sections to fit into standard memory.

---

## 2. In-Memory Cosine Similarity Engine

`VectorIndex` evaluates nearest neighbors using normalized cosine distance:

$$\text{similarity}(\vec{A}, \vec{B}) = \vec{A} \cdot \vec{B} = \sum_{i=1}^{128} A_i B_i$$

- With SIMD AVX2 acceleration, computing cosine similarity across 50,000 document vectors takes **< 1.5 milliseconds** on modern laptop CPUs.

---

## 3. Atomic Disk Persistence (`vectors.bin`)

To ensure that pre-computed vectors survive application restarts, power loss, and crashes without requiring expensive re-embedding:

1. **Binary Layout:** Contiguous binary serialization (`data/vectors.bin`) with `APV1` magic header, record count, and structured entries (`chunk_id`, `doc_id`, `page_ref`, and Float32[128] vector).
2. **Durability Guarantee:** Written to `vectors.bin.tmp`, flushed to physical media via Win32 `FlushFileBuffers`, and atomically promoted via `MoveFileExA` with `MOVEFILE_WRITE_THROUGH`.
3. **Instant Startup:** Loaded during `NativeStorage::load_state()`, restoring the entire vector library in < 5 milliseconds.

