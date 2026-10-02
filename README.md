# ArcheoPhd-Docs

Official Architecture, Problem Statement, Engineering Roadmap & Security Specifications for **ArchaeoPhD** — The Offline-First AI Research Workstation for Archaeological Academia.

---

## 📚 Documentation Index

1. **[Problem Statement](PROBLEM_STATEMENT.md)**
   - The archaeological "connection crisis"
   - 5 core pain points: broken evidence chains, chronological/interpretive contradictions, lost spatial context, and AI hallucination hazards in academic writing.

2. **[Project Overview & Architecture](PROJECT_OVERVIEW.md)**
   - Domain model & knowledge graph (hypotheses, claims, supporting/refuting evidence, findspots, loci, ceramics, chronology).
   - Core architecture: Native C++ vector engine, SQLite epistemological store, WebView2 workstation frontend, local embedding models.

3. **[Master Engineering Plan & Roadmap](PLAN.md)**
   - System design, implementation phases, offline migration, local vector indexing, native shell, and release distribution.

4. **[Pricing, Offline Leasing & Security Architecture](pricing_security.md)**
   - Subscription model architecture: Ed25519 digitally signed leases, Windows DPAPI encryption (`CryptProtectData`), hardware fingerprint binding, anti-clock-tampering (monotonic counter), and 30-day offline grace period.

---

## 🏛️ About ArchaeoPhD

ArchaeoPhD is a specialized offline research workstation built to address the unique challenges of archaeological scholarship:
- **Evidence-Traceable Knowledge Graph:** Connect theoretical claims directly to excavation trenches, loci, stratigraphy, and museum catalog numbers.
- **Contradiction Analysis:** Detect and track conflicting dating proposals, excavator debates, and stratigraphic disagreements.
- **100% Offline & Zero Cloud Leakage:** Local vector search, zero external telemetry, user-chosen data roots on external SSDs or local drives.
