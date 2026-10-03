# Air-Gapped Privacy & Security Policy

> **The ArchaeoPhD Promise:** 100% Local. Zero Network Telemetry. Zero Cloud Inference. Nothing a researcher uploads is ever transmitted to an external server.

---

## 1. Why Archaeology Demands Strict Air-Gapped Privacy

Generalist AI tools (OpenAI ChatGPT, Anthropic Claude, Google Gemini) require transmitting research prompts and uploaded documents across the public internet to third-party data centers. In archaeological doctoral research, this introduces fatal risks:

1. **Unpublished Excavation Discoveries**:
   - A doctoral thesis often rests on 3–5 years of proprietary field data prior to peer-reviewed publication.
   - Cloud leakage risks premature disclosure, academic scooping, or copyright violations with excavation directors.
2. **Looting & Cultural Heritage Site Protection**:
   - Primary excavation reports frequently contain GPS coordinates, trench elevations, and descriptions of unexcavated gold, bronze, or intact ceramic hoards.
   - Uploading raw coordinates to third-party cloud servers risks exposing vulnerable cultural heritage sites to illegal antiquities trafficking and looting.
3. **Supervisor & Institutional NDAs**:
   - Many foreign archaeological expeditions operate under bilateral government antiquities permits that legally prohibit exporting or transmitting raw research data to foreign cloud servers.

---

## 2. Technical Enforcements of the Air-Gap Guarantee

ArchaeoPhD guarantees privacy through **hard technical constraints**, not soft legal promises:

| Architectural Layer | Technical Enforcement |
| :--- | :--- |
| **No Inbound/Outbound Sockets** | The application does not listen on any TCP/UDP ports. All communication between the UI and C++ engine occurs in-memory via WebView2 IPC. |
| **Local-Only LLM Inference** | All text summarization, entity extraction, and contradiction checks are computed by a quantized 7–8B model running locally on the device CPU/GPU. |
| **Local Vector Search** | Document chunk embeddings are generated and searched on-device. No vector database cloud sync occurs. |
| **Cloud-Sync File Watcher** | Active path scanning detects and warns if a user accidentally places their Data Root inside OneDrive, iCloud, or Dropbox. |
| **Zero Background Analytics** | No telemetry trackers, no crash reporters (e.g. Sentry), and no usage beacons are included in the build. |
