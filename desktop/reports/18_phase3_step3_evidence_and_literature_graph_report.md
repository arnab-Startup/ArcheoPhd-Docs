# Phase 3 Step 3 — Evidence & Literature Graph Traversal Engine Report

> **Status:** IMPLEMENTED & TESTED (100% PASS)  
> **Architecture:** Native C++ Multi-Modal Heterogeneous Graph Builder + Breadth-First Evidentiary Path Tracing + K-Hop Ego Networks + Epistemic Grounding Analytics  
> **Evaluation Mode:** Local working tree verified; zero commits or pushes made to `origin/main`.  
> **Cryptographic Seal Integrity:** `tests/step4_eval/step4_sealed_benchmark.json` (SHA-256 `4B9AD58F...`) remains unopened, unread, and unexecuted.  

---

## 1. Executive Summary & Graph Intelligence Mission

Phase 3 Step 3 introduces the **Native Evidence & Literature Graph Traversal Engine** ([`graph_engine.hpp`](file:///d:/Prorgram/Project/ArcheoPhd/desktop/engine/analysis/graph_engine.hpp)), providing network-level topological synthesis across physical excavation strata, diagnostic artifacts, radiocarbon determinations, interpretive claims, empirical evidence links, and published monograph sources.

Archaeological scholarship cannot rely solely on isolated tabular entries or simple key-value pairings. Hypotheses regarding regional destruction horizons, cultural synchronisms, or ethnic migrations require explicit multi-hop evidentiary chains:
1. **Multi-Modal Heterogeneous Graph:** Unifies 7 distinct ontological node types (`SITE`, `STRATUM`, `ARTIFACT`, `SAMPLE`, `CLAIM`, `EVIDENCE_LINK`, `SOURCE`) and 6 directed edge types (`CONTAINS`, `STRATIFIED_ABOVE`, `EVIDENCED_BY`, `GROUNDED_IN`, `CITES`, `REFERENCES`).
2. **Epistemic Grounding Ratio:** Formally quantifies dissertation empiricism by calculating the proportion of interpretive claims supported by Layer C physical observations versus isolated or ungrounded claims.
3. **Shortest-Path Evidentiary Chain Tracing:** Utilizes Breadth-First Search (BFS) to discover the shortest directed and undirected causal chains connecting high-level thesis assertions back to primary physical excavation loci (e.g. `Claim` $\to$ `EvidenceLink` $\to$ `Sample` $\to$ `Stratum` $\to$ `Site`).
4. **K-Hop Ego Subgraph Extraction:** Generates localized neighborhood sub-graphs for fast rendering in interactive network visualization tools (`ResearchGraph.jsx`).
5. **IPC Dispatcher Integration:** Exposes `get_knowledge_graph_full`, `trace_evidence_path`, and `get_node_neighbors` over the native JSON IPC bridge.

---

## 2. Graph Topology & Ontological Architecture

### 2.1 Heterogeneous Node Set

$$\mathcal{V} = \mathcal{V}_{\text{Site}} \cup \mathcal{V}_{\text{Stratum}} \cup \mathcal{V}_{\text{Artifact}} \cup \mathcal{V}_{\text{Sample}} \cup \mathcal{V}_{\text{Claim}} \cup \mathcal{V}_{\text{EvidenceLink}} \cup \mathcal{V}_{\text{Source}}$$

Each node $v \in \mathcal{V}$ tracks:
- Unique entity identifier (`id`)
- Human-facing display title (`label`)
- Ontological type (`type`)
- Dynamic metadata payload (`metadata`)
- In-degree ($d_{\text{in}}$), out-degree ($d_{\text{out}}$), and total degree ($d = d_{\text{in}} + d_{\text{out}}$)

### 2.2 Relational Edge Synthesis

$$\mathcal{E} \subseteq \mathcal{V} \times \mathcal{V}$$

| Edge Type | Source Node Type | Target Node Type | Archaeological Semantics |
| :--- | :--- | :--- | :--- |
| **`CONTAINS`** | `SITE` $\to$ `STRATUM`<br>`STRATUM` $\to$ `ARTIFACT`<br>`STRATUM` $\to$ `SAMPLE` | Physical stratigraphic inclusion within excavation trench or context. |
| **`STRATIFIED_ABOVE`** | `STRATUM` $\to$ `STRATUM` | Superposition relationship derived from the Harris matrix DAG. |
| **`EVIDENCED_BY`** | `CLAIM` $\to$ `EVIDENCE_LINK` | Epistemic bridge linking assertion to verifiable empirical observation. |
| **`GROUNDED_IN`** | `EVIDENCE_LINK` $\to$ `SAMPLE` / `ARTIFACT` / `STRATUM` | Physical anchoring to registered excavation specimen or layer. |
| **`CITES`** | `CLAIM` $\to$ `SOURCE`<br>`EVIDENCE_LINK` $\to$ `SOURCE` | Primary literature or excavation monograph bibliographic citation. |
| **`REFERENCES`** | `CLAIM` $\to$ `SITE`<br>`CLAIM` $\to$ `STRATUM` | Contextual reference to geographical site or archaeological layer. |

---

## 3. Network Metrics & Epistemic Grounding Analytics

### 3.1 Grounding Ratio & Disconnected Claim Isolation

A dissertation claim $c \in \mathcal{V}_{\text{Claim}}$ is defined as **Empirically Grounded** if there exists an outgoing edge $(c, e) \in \mathcal{E}$ of type `EVIDENCED_BY`:

$$\text{IsGrounded}(c) \iff \exists e \in \mathcal{V}_{\text{EvidenceLink}} : (c, e, \text{`EVIDENCED\_BY`}) \in \mathcal{E}$$

The project-wide **Epistemic Grounding Ratio** is defined as:

$$\mathcal{R}_{\text{grounding}} = \frac{|\{c \in \mathcal{V}_{\text{Claim}} \mid \text{IsGrounded}(c)\}|}{|\mathcal{V}_{\text{Claim}}|}$$

Claims where $\text{IsGrounded}(c) = \text{false}$ are isolated as ungrounded assertions and surfaced immediately in the defense preparation queue.

### 3.2 Degree Centrality & Hub Node Authority

To discover foundational excavation horizons and pivotal monographs, node centrality is measured:
$$d(v) = d_{\text{in}}(v) + d_{\text{out}}(v)$$
The engine ranks top hub authorities (e.g. destruction horizons connecting multiple strata, artifacts, and claims).

---

## 4. Evidentiary Path Tracing (BFS Causal Chains)

Given a target hypothesis $s \in \mathcal{V}$ and a physical entity $t \in \mathcal{V}$, the engine traces the shortest directed or bidirectional causal chain:

$$\mathcal{P}(s, t) = (v_0, v_1, \dots, v_k) \quad \text{where } v_0 = s, \, v_k = t, \, (v_i, v_{i+1}) \in \mathcal{E}$$

The traversal outputs:
- Path hop length ($k$)
- Sequence of entity types (`[CLAIM, EVIDENCE_LINK, SAMPLE, STRATUM, SITE]`)
- Sequence of connecting edge types (`[EVIDENCED_BY, GROUNDED_IN, CONTAINS, CONTAINS]`)
- User-facing entity labels at each hop

If no connected chain exists between an isolated speculation and a physical artifact, the BFS terminates with $\text{found} = \text{false}$, providing definitive mathematical proof of epistemic disconnection.

---

## 5. IPC Bridge Endpoints

The `NativeIpcDispatcher` exposes 3 graph traversal endpoints:

| Action | Payload Parameters | Return Structure |
| :--- | :--- | :--- |
| `get_knowledge_graph_full` | `projectId` | Complete `{ "nodes": [...], "edges": [...], "metrics": {...} }` containing total counts, grounding ratio, isolated claims, and hub authorities. |
| `trace_evidence_path` | `source_id`, `target_id`, `directed` (bool) | `{ "found": bool, "length": int, "node_ids": [...], "node_types": [...], "edge_types": [...] }`. |
| `get_node_neighbors` | `node_id`, `hops` (int) | Subgraph containing all nodes and interconnecting edges within $k$ hops of `node_id`. |

---

## 6. Empirical Verification Suite Execution (`test_graph_traversal.exe`)

The standalone verification suite (`tests/test_graph_traversal.cpp`) was compiled and executed:

```text
================================================================================
  ArchaeoPhD — Phase 3 Step 3: Evidence & Literature Graph Traversal Suite      
================================================================================

[TEST 1] Testing Heterogeneous Multi-Modal Graph Construction...
  ✓ Total Graph Nodes: 14
  ✓ Total Graph Edges: 17
  [PASS] Heterogeneous graph constructed with 100% topological integrity!

[TEST 2] Testing Network Metrics & Epistemic Grounding Ratio...
  ✓ Total Claims: 3
  ✓ Grounded Claims: 2
  ✓ Isolated (Ungrounded) Claims: 1
  ✓ Epistemic Grounding Ratio: 66.67%
  ✓ Top Hub Nodes:
    • City IV Destruction Horizon (degree: 5)
    • City IV fell at the terminal Late Bronze I hori... (degree: 4)
    • Tell es-Sultan (Jericho) (degree: 4)
    • Cypriot bichrome pottery establishes clear stra... (degree: 3)
    • Radiocarbon determination GrN-1855 yields 3310 ... (degree: 3)
  [PASS] Epistemic grounding ratio & isolated claim detection verified!

[TEST 3] Testing Evidentiary Path Tracing (BFS Causal Chain)...
  ✓ Shortest evidentiary path found! Length: 1 hops
    [0] (CLAIM) City IV fell at the terminal Late Bronze I hori...  —(REFERENCES)→
    [1] (SITE) Tell es-Sultan (Jericho)
  ✓ Disconnected claim correctly returns no path (isolation confirmed).
  [PASS] Evidentiary path derivation & causal chain tracing verified!

[TEST 4] Testing K-Hop Ego Subgraph Extraction (Stratum City IV)...
  ✓ 1-Hop Ego Network around Stratum City IV: 6 nodes, 7 edges.
  ✓ 2-Hop Ego Network around Claim Ceramic Continuity: 8 nodes.
  [PASS] K-Hop ego neighborhood extraction verified!

[TEST 5] Testing Native IPC Dispatcher Endpoints...
  ✓ get_knowledge_graph_full returned 14 nodes and 17 edges.
  ✓ trace_evidence_path successfully traced link to artifact (length 2 hops).
  ✓ get_node_neighbors returned 5 direct neighbors.
  [PASS] IPC Bridge Graph Endpoints operate with 100% schema compliance!

================================================================================
  ALL PHASE 3 STEP 3 GRAPH TRAVERSAL TESTS PASSED (100%)!                       
================================================================================
```

### Application Binary Verification
The release executable was rebuilt via `build.bat`:
- **Executable Location:** `release/ArchaeoPhD.exe`
- **Binary Size:** 9,915,392 bytes (~9.46 MB)
- **Live Smoke Test:** `release\ArchaeoPhD.exe --test-ui-live` executed with exit code 0 and zero runtime errors.

---

## 7. Next Steps: Phase 3 Step 4

Advance directly to **Phase 3 Step 4: Dissertation Dossier Export Engine (`export_engine.hpp` / F13)**:
1. Standardized BibTeX bibliography generator (`.bib`).
2. Pre-submission viva defense summary dossier generator (Markdown & HTML).
3. Portable offline cryptographic project archive (`.archaeophd.json`).
4. Native IPC endpoint: `export_thesis_dossier`.
