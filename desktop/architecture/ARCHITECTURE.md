# ArchaeoPhD Desktop — Workstation Architecture

> **Stack:** Native Windows C++20 (Win32 API + Microsoft Edge WebView2).  
> **Distribution:** Single self-contained Windows executable (~2.2 MB, statically linked).  
> **Network Footprint:** Pure In-Memory IPC. Zero open HTTP/TCP ports. Zero cloud sockets.

---

## 1. High-Level Architectural Model

ArchaeoPhD Desktop abandons the traditional heavy Electron/Node runtime and multi-tier client-server model in favor of an **air-gapped monolithic workstation** running directly on researcher hardware.

```text
┌────────────────────────────────────────────────────────────────────────┐
│                   ArchaeoPhD.exe (Single-File PE Binary)               │
│                                                                        │
│  ┌───────────────────────────────┐  Direct In-Memory  ┌──────────────┐ │
│  │   Microsoft Edge WebView2     │◄──────────────────►│ Native C++   │ │
│  │   UI Renderer (Chromium)      │  JSON IPC Bridge   │ Core Engine  │ │
│  │                               │  (Zero Sockets)    │              │ │
│  │  - Warm Archaeological Design │                    │ - Storage    │ │
│  │  - Fraunces & Inter Fonts     │                    │ - Extractor  │ │
│  │  - Light/Dark Mode Adapters   │                    │ - Conflicts  │ │
│  └───────────────┬───────────────┘                    └───────┬──────┘ │
│                  │                                            │        │
│                  ▼                                            ▼        │
│         Extracted /dist/                            User Data Root     │
│         Web Assets (HTML/CSS)                       (Local/Ext SSD)    │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Zero-Port In-Memory IPC Bridge

Unlike conventional web-wrapper desktop apps that spin up an internal `localhost:8000` HTTP server (which triggers Windows Firewall prompts and exposes ports to local malware), ArchaeoPhD connects the WebView2 frontend and the C++ engine over **direct in-memory string messaging**:

1. **Frontend to Engine (Request):**
   ```javascript
   window.chrome.webview.postMessage({
     id: "req-101",
     action: "get_contradictions",
     payload: { project_id: "default" }
   });
   ```
2. **C++ Native Message Handler (`src/main.cpp`):**
   - Implements `ICoreWebView2WebMessageReceivedEventHandler`.
   - Reads raw JSON string from `WebMessageReceivedEventArgs`.
   - Dispatches synchronously to the appropriate engine subsystem (`DocumentExtractor`, `ContradictionEngine`, `Storage`, `DataRootManager`).
   - Responds directly via `PostWebMessageAsString(responseJson.c_str())`.
3. **Engine to Frontend (Response):**
   - Native bridge JavaScript wrapper resolves the awaiting Promise.
   - Zero network overhead: Latency is < 0.2 ms per call.

---

## 3. Embedded PE Resource Extraction (`IDR_APP_PAYLOAD`)

ArchaeoPhD compiles as a **single standalone executable** without requiring an installer or loose asset directories:

1. **Compilation Phase (`build.bat`):**
   - The compiled frontend (`dist/`) and `WebView2Loader.dll` are compressed into `payload.zip`.
   - Windows resource compiler (`windres`) embeds `payload.zip` into `src/resource.rc` under resource ID `IDR_APP_PAYLOAD`.
   - MinGW G++ compiles `main.cpp` + `resource.res` with `-static -static-libgcc -static-libstdc++`.
2. **Runtime Boot Phase (`EnsureRuntimeExtracted()`):**
   - On cold boot, the executable inspects `%LOCALAPPDATA%\ArchaeoPhD\app\dist\index.html`.
   - If missing or outdated, it extracts the embedded `IDR_APP_PAYLOAD` in memory to `%LOCALAPPDATA%\ArchaeoPhD\app`.
   - WebView2 initializes directly against this local directory using `file:///` or virtual host mapping.

---

## 4. Subsystem Layout

| Subsystem | Path | Description |
| :--- | :--- | :--- |
| **Shell & Window** | `src/main.cpp` | Win32 message loop, DPI awareness, Unicode titlebar, shortcut installer |
| **Resources** | `src/resource.rc` | Embedded icon (16x16 to 256x256), application manifests, payload |
| **Core Engine** | `engine/core/` | Domain ontology (`models.hpp`) and hardware inspector (`system_inspector.hpp`) |
| **Storage & Root** | `engine/storage/` | Data root manager (`data_root.hpp`) and Zstd storage engine (`storage.hpp`) |
| **Analysis** | `engine/analysis/` | Tarjan cycle detector (`contradictions.hpp`) and thesis auditor (`thesis_audit.hpp`) |
| **Extraction** | `engine/extraction/` | Entity extraction & citation verifier (`document_extractor.hpp`) |
| **Validation** | `engine/validation/` | Ground truth archaeological corpus (`benchmark_seed.hpp`) |
