# System Requirements & Hardware Specifications

> ArchaeoPhD is engineered to run locally on standard academic laptops without requiring institutional supercomputers or cloud GPU subscriptions.

---

## 1. Hardware Matrix

| Component | Minimum Specification (Tight Floor) | Recommended Specification |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 / 11 (64-bit) | Windows 11 (64-bit) |
| **System Memory (RAM)** | **8 GB** *(Functional floor)* | **16 GB or higher** *(Optimal for concurrent RAG + extraction)* |
| **Processor (CPU)** | 4 Cores, 2.0 GHz, **AVX2 support** | 8 Cores (Intel Core i7/i9 or AMD Ryzen 7/9) |
| **Graphics (GPU)** | Not required (CPU-only execution supported) | Dedicated NVIDIA GPU with 6–8 GB VRAM (CUDA/TensorRT) |
| **Free Storage Space** | 10 GB free space on chosen Data Root | Fast internal NVMe SSD or high-speed USB 3.2 External SSD |
| **Display Resolution** | 1280 x 720 | 1920 x 1080 or higher |

---

## 2. Storage Footprint Breakdown

| Subsystem | Footprint | Scaling Behavior |
| :--- | :--- | :--- |
| **Application Binary (`ArchaeoPhD.exe`)** | ~2.2 MB | Fixed (Single standalone PE file) |
| **Embedded Workstation Shell (`dist/`)** | ~15 MB | Fixed (HTML/CSS/JS bundled) |
| **Embedding Model (`nomic-embed-text-v1.5.gguf`)** | ~0.5 GB | Fixed (Loaded into RAM on demand) |
| **Reasoning Model (`llama-3-8b-instruct-q4_k_m.gguf`)**| ~4.9 GB | Fixed (Quantized 4-bit weights) |
| **Corpus Archive (`archives/*.zst`)** | ~1–4 GB | Scales with library (Lossless ~74% compression) |
| **Native Storage & Vector Index (`state.json`, `vectors.bin`)** | ~0.1–0.5 GB | Scales with total chunks (512 bytes/vector) and graph nodes |
| **Total Typical Footprint** | **~7–11 GB** | Fully contained inside user-selected Data Root |

---

## 3. Native Hardware Inspection

On workstation initialization, `NativeSystemInspector::get_hardware_info()` interrogates the host machine:
- **Total Physical RAM (`GlobalMemoryStatusEx`)**: Warns if available RAM is below the 8 GB floor.
- **CPU Cores (`GetSystemInfo`)**: Calculates optimal worker thread allocation for document processing.
- **AVX2 Instruction Set**: Verifies SIMD vector instruction availability for quantized dot products.
