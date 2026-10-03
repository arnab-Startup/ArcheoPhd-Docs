# User-Chosen Data Root Architecture

> **Guiding Principle:** Researchers own their data. Heavy model weights (5+ GB) and sensitive excavation archives must live wherever the researcher chooses (fast internal NVMe or encrypted external SSD), never trapped in a hidden OS folder.

---

## 1. The Two-Tier Pointer Architecture

To maintain full user freedom while keeping OS integration simple, ArchaeoPhD uses a **two-tier pointer system**:

```text
[OS-Standard Fixed Location]
Windows: %LOCALAPPDATA%\ArchaeoPhD\settings.json
macOS:   ~/Library/Application Support/ArchaeoPhD/settings.json
Linux:   ~/.local/share/ArchaeoPhD/settings.json
  │
  └───► Contains ONLY: { "data_root": "E:\\My-Archaeology-SSD" }
                                │
                                ▼
[User-Chosen Data Root — Any Drive, Any Folder]
E:\My-Archaeology-SSD/
  ├── models/
  │     ├── embedding/nomic-embed-text-v1.5.gguf
  │     └── llm/llama-3-8b-instruct-q4_k_m.gguf
  ├── config.json
  ├── logs/
  └── libraries/
        └── <Library Name>/
              ├── library.lancedb/        ← chunks + vectors + knowledge graph
              ├── compression-dict.zstd   ← pre-trained shared dictionary
              ├── archives/               ← <doc_id>.zst lossless archives
              │     └── index.db          ← doc_id to file mapping
              └── library-manifest.json
```

---

## 2. Cloud Leakage Detection & Protection

### The Threat
Academic and archaeological research often contains **unpublished excavation coordinates, pre-monograph C-14 dates, or sensitive cultural heritage findspots**. If an app forces storage into `Documents/` or `Desktop/`, Windows silently uploads these files to **OneDrive**, iCloud, Dropbox, or Google Drive.

### The Defense
When a user configures or relocates their Data Root, `DataRootManager::DetectCloudSyncService()` inspects the selected path against environment variables and virtual volume headers:

1. **OneDrive**: Checks `%OneDrive%`, `%OneDriveConsumer%`, `%OneDriveCommercial%`.
2. **Dropbox**: Checks for `\Dropbox` directory boundaries.
3. **iCloud Drive**: Checks for `\iCloudDrive` or Apple cloud containers.
4. **Google Drive**: Inspects drive letters and calls `GetVolumeInformationW` for the virtual Google Drive volume label.

If a cloud-synced folder is chosen, an explicit warning modal appears:
> **⚠️ Cloud Storage Detected (OneDrive)**  
> Storing multi-gigabyte models and raw research data inside a cloud-synced folder will consume your cloud quota and risk syncing unpublished archaeological findings. A dedicated local drive or external SSD is strongly recommended.

---

## 3. Disconnected External Storage Protection

### The Problem
Archaeology PhDs frequently use external ruggedized SSDs (e.g., Samsung T7) in the field. When unplugging the drive, standard applications either crash or silently write data to a fallback `C:\Users\...` folder, fragmenting the database across drives.

### The Defense
ArchaeoPhD **never writes to a fallback drive**:
1. Before every disk operation, `DataRootManager::IsPathMissing()` queries `GetFileAttributesW()` and `GetDriveTypeW()`.
2. If the external drive letter is disconnected (e.g. `E:\` is missing):
   - All write and indexing operations are paused.
   - The UI displays the modal: **"⚠️ Storage Disconnected: Research Data Root Unavailable"**.
   - The user is prompted to plug the SSD back in and click **"🔄 Retry Connection"**, or relocate the library.
   - Once reconnected, the C++ engine immediately resumes without data loss or fragmentation.
