# ArchaeoPhD — Project Architecture & Domain Specification

> **An AI-powered research workspace engineered specifically for Archaeology PhD researchers, postdocs, supervisors, and cultural heritage managers.**

---

## 1. Executive Summary & Core Mission

### The Core Problem in Archaeological Academia
Archaeological research differs fundamentally from most academic disciplines. While a typical doctoral thesis in the humanities or sciences revolves around literature or laboratory experiments, archaeological research synthesizes wildly disparate and fragmented data formats:
- **Heterogeneous Sources:** Excavation monographs, gray literature, field journals, radiocarbon lab sheets, museum acquisition registers, and peer-reviewed journal articles.
- **Physical & Spatial Context:** Physical findspots, geographic coordinates, stratigraphic layers (loci), and artifact typologies.
- **Dating Disagreements:** Conflicting proposed chronological ranges across publications without standardized consensus.
- **Fragile Evidence Chains:** A single claim in chapter four often rests on a pottery sherd described in an excavation report read months ago in another country.

Traditional reference managers (Zotero, Mendeley) only store bibliographic metadata. Generalist note-taking tools (Notion, Obsidian) lack archaeological primitives like stratigraphic matrices, coordinate findspot maps, or evidence-verification chains.

### The ArchaeoPhD Solution
ArchaeoPhD provides an **evidence-traceable knowledge graph** that bridges academic publications, primary field data, and dissertation writing into a single unified workspace.

---

## 2. Core Domain Model & Knowledge Graph

At the heart of ArchaeoPhD is an epistemological model connecting research hypotheses to primary physical evidence:

```
                      ┌────────────────────────┐
                      │    Research Project    │
                      └───────────┬────────────┘
                                  │
                      ┌───────────▼────────────┐
                      │   Research Question    │
                      └───────────┬────────────┘
                                  │
                      ┌───────────▼────────────┐
                      │         Claims         │
                      └─────┬────────────┬─────┘
            Supporting      │            │      Refuting / Contradicting
            Evidence        │            │      Evidence
                      ┌─────▼──────┐┌────▼───────┐
                      │  Evidence  ││  Evidence  │
                      └─────┬──────┘└────┬───────┘
                            │            │
       ┌────────────────────┼────────────┼───────────────────┐
       │                    │            │                   │
┌──────▼──────┐      ┌──────▼─────┐┌─────▼──────┐     ┌──────▼──────┐
│ Publications│      │    Sites   ││  Artifacts │     │ Chronology  │
│  & Sources  │      │ & Strata   ││ & Material │     │ (BCE / CE)  │
└─────────────┘      └────────────┘└────────────┘     └─────────────┘
```

### Verification States
To maintain academic rigor, the platform separates automated insights from peer-reviewed evidence:
- **Verified by Researcher:** Explicitly confirmed and documented by the researcher.
- **AI Suggested:** Discovered through text-mining and entity extraction, requiring academic sign-off.
- **Unresolved / Contested:** Actively flagged as having contradictory data in the literature.

---

## 3. Comprehensive Feature Modules

### 3.1. Evidence & Argumentation Engine

| Module | Route | Purpose & Key Features |
|---|---|---|
| **Evidence Graph** | `/evidence-graph` | Interactive visual graph rendering nodes for Questions, Claims, Evidence, Sites, Artifacts, and Publications. Features customizable filtering, search, and node-inspector drawers. |
| **Claims Manager** | `/claims`, `/claims/:id` | Central registry for formal academic propositions. Tracks supporting vs. refuting evidence ratios, resolution status, and confidence levels. |
| **Argument Builder** | `/argument-builder` | Structural tool to assemble individual claims into coherent, defensible dissertation chapters and arguments. |
| **Contradiction Detector** | `/contradiction-detector` | Algorithmic detector highlighting contradictory dating or typological disputes between different published authorities. |
| **Research Gap Explorer** | `/gap-explorer` | Identifies assertions lacking empirical backup, ungrounded dates, or unexcavated contexts needing further investigation. |

---

### 3.2. Archaeological Data Hub

| Module | Route | Purpose & Key Features |
|---|---|---|
| **Library & Source Reader** | `/library`, `/source-reader/:id` | Full repository for PDFs, articles, and field notes. The Source Reader provides side-by-side reading, in-situ note taking, and contextual AI queries. |
| **Sites Database** | `/sites`, `/sites/:id` | Detailed profiles for archaeological sites including regional context, latitude/longitude, excavation history, cultural periods, and excavator affiliations. |
| **Site Comparison** | `/site-comparison` | Side-by-side comparative analysis of multiple sites across material culture, dating ranges, and environmental settings. |
| **Artifacts Catalog** | `/artifacts` | Registry of physical material culture (ceramics, lithics, metals, archaeobotanical finds) linked to specific archaeological strata and inventory numbers. |
| **Chronology Engine** | `/chronology` | Archaeological timeline visualization across BCE and CE. Rather than forcibly merging conflicting dates, it presents competing dating models side by side. |
| **Archaeological Matrix** | `/matrix` | Stratigraphic sequencing based on the **Harris Matrix** principle to track relative chronological superposition of archaeological deposits. |
| **Interactive Research Map**| `/research-map` | Geospatial mapping powered by Leaflet, visualizing archaeological coordinates, regional clusters, and artifact distributions. |

---

### 3.3. Grounded AI Research Assistant

The AI capabilities in ArchaeoPhD are strictly engineered to prevent academic hallucination:
- **Grounded Q&A (`/ai-research`):** Queries operate over the researcher's authenticated project library.
- **Structured Output Separation:** Every answer is explicitly segmented into four distinct fields:
  1. **Direct Answer:** Synthesized conceptual response.
  2. **Grounded Evidence:** Verbatim quotations and factual extracts.
  3. **Traceable Sources:** Exact page and publication references.
  4. **Uncertainty & Gaps:** Explicit declaration of missing information or conflicting interpretations.
- **In-App Research Assistant:** Floating AI drawer accessible across all screens for rapid note synthesis and entity lookups.

---

### 3.4. Dissertation Synthesis & Export

| Module | Route | Purpose & Key Features |
|---|---|---|
| **Thesis Outline & Drafter** | `/thesis` | Chapter-by-chapter dissertation workspace connecting written narrative directly to backing evidence nodes. |
| **Literature Graph** | `/literature-graph` | Network diagram visualizing bibliographic relationships, shared author clusters, and citation patterns. |
| **Research Analytics** | `/analytics`, `/activity` | Statistical metrics tracking evidence coverage, verification percentage, source distribution, and research activity logs. |
| **Export Center** | `/export-center` | Academic export engine capable of generating formatted bibliographies, evidence tables, and chapter drafts in PDF, Markdown, and structured formats. |

---

## 4. Technical Architecture

### 4.1. Technology Stack

```
Frontend (React 18 + Vite 6)
  ├── State Management: React Context (Auth, Project) + TanStack React Query
  ├── Styling: TailwindCSS + Lucide Icons + Radix UI Primitives
  ├── Visualizations: Recharts + SVG Graph Engine + Leaflet Maps
  ├── Rich Text & Export: React-Quill, React-Markdown, jsPDF, html2canvas
  └── Routing: React Router DOM v6 with code splitting (React.lazy)
```

### 4.2. Containerization & Deployment

The application includes enterprise-grade containerization with Docker and Docker Compose:
- **Multi-Stage Production Dockerfile (`frontend/Dockerfile`):**
  - **Stage 1 (Builder):** `node:20-alpine` installs dependencies and builds minified assets via `vite build`.
  - **Stage 2 (Server):** `nginx:alpine` serves static assets with gzip compression, asset caching headers, and SPA routing fallback (`try_files $uri $uri/ /index.html;`).
- **Development Container (`frontend/Dockerfile.dev`):** Runs Vite dev server with volume mounts for live hot module replacement inside containerized environments.
- **Docker Compose Orchestration (`docker-compose.yml`):**
  - Production service on port `3000`.
  - Development service with hot-reload on port `5173`.

---

## 5. Directory Structure

```
ArcheoPhd/
├── frontend/                        # Complete React Single-Page Application
│   ├── src/
│   │   ├── api/                     # API clients and data layer
│   │   ├── components/
│   │   │   ├── app/                 # Shell, layout, navigation, sidebar, topbar
│   │   │   ├── landing/             # Marketing and presentation components
│   │   │   └── ui/                  # Accessible UI component system (Radix + Tailwind)
│   │   ├── hooks/                   # Custom React hooks
│   │   ├── lib/                     # Utilities, contexts (AuthContext, ProjectContext), query client
│   │   ├── pages/                   # 30+ Research, data, analysis, and auth pages
│   │   ├── utils/                   # Helper functions, formatting, calculations
│   │   ├── App.jsx                  # Main application routing and lazy-loaded page map
│   │   ├── index.css                # Global theme variables, typography, and design tokens
│   │   └── main.jsx                 # Application entry point
│   ├── public/                      # Static assets, manifests, icons
│   ├── Dockerfile                   # Multi-stage production Nginx container
│   ├── Dockerfile.dev               # Live development container
│   ├── nginx.conf                   # Nginx reverse proxy & SPA routing configuration
│   ├── package.json                 # Frontend dependencies and scripts (start, dev, build)
│   ├── vite.config.js               # Vite build config with path aliases
│   ├── tailwind.config.js           # Heritage and academic design theme
│   └── components.json              # UI component registry
├── docker-compose.yml               # Production and development Docker services
├── package.json                     # Root-level command delegation to frontend/
├── README.md                        # Quickstart instructions
├── PROJECT_OVERVIEW.md              # Complete architecture and domain specification (this document)
└── AGENTS.md                        # Developer and agent guidance
```

---

## 6. Developer Workflow

### Direct Local Execution
```bash
# Install dependencies
npm run install:frontend

# Start development server on http://localhost:5173
npm start
# or: npm run dev

# Run production build (outputs to frontend/dist)
npm run build

# Preview production build locally
npm run preview
```

### Docker Execution
```bash
# Run production container on http://localhost:3000
docker compose up --build

# Run development container with live reload on http://localhost:5173
docker compose --profile dev up --build frontend-dev
```
