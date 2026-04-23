# Design Team Collaboration

vDTC operates as a cross-functional research organization. Engineering, clinical, regulatory, and design disciplines collaborate on every project from concept through first production unit. This page describes how teams are structured, how work flows between them, and how the OpenClaw AI agent network supports the process.

---

## Team Structure

| Role | Discipline | Responsibilities |
|---|---|---|
| **SWPhD** | Software Engineering | Firmware, APIs, embedded systems, AI pipelines |
| **EEPhD** | Electrical Engineering | Schematics, PCB layout, power systems, sensors |
| **PCBPhD** | PCB Design | Layer stackup, controlled impedance, Gerber packages |
| **BiomedPhD** | Biomedical Engineering | Clinical protocols, physiological signal validation |
| **RegulatoryPhD** | Regulatory Affairs | FDA, FCC, NRC, FAA compliance documentation |
| **MicroArchPhD** | Microarchitecture | FPGA, SoC integration, real-time control loops |
| **AiPhD** | AI/ML | Model selection, fine-tuning, inference pipelines |
| **SysPhD** | Systems Engineering | Architecture, ICD, requirements traceability |
| **BizPhD** | Business Development | Market analysis, go-to-market, investor relations |
| **BrandPhD** | Brand & Communications | Documentation, GitBook, design language |

---

## Collaboration Workflow

### 1. Work Order (WO) System
Every deliverable begins as a Work Order in the OpenClaw agent network. WOs define the owner, target file, acceptance criteria, and iteration stage. Agents produce outputs that are reviewed, quality-gated, and promoted through three iteration stages before being considered complete.

### 2. Design Review Cycle
- **Concept (Stage 1):** System-level block diagrams, requirements, market positioning
- **Specification (Stage 2):** Interface control documents, component selection, regulatory requirements
- **Implementation (Stage 3):** Schematics, code, BOM, test procedures, FDA pre-submission

### 3. Cross-Domain Handoffs
When a deliverable from one discipline enables another, a handoff is declared in the WO. Example:
- EEPhD completes schematic → PCBPhD receives layout WO
- SWPhD completes API spec → AiPhD receives LLM integration WO
- BiomedPhD completes clinical protocol → RegulatoryPhD receives FDA submission WO

### 4. AI Agent Network (OpenClaw)
The [OpenClaw](https://github.com/vDTC/OpenClaw) agent network runs a fleet of specialized AI agents that operate as virtual PhD-level collaborators. Each agent:
- Reads active Work Orders from the shared state directory
- Produces implementation-ready outputs (not planning documents)
- Is critiqued by Hermes (AI quality gate) before output is saved
- Contributes insights to the INTEL.md knowledge base

---

## Design Standards

| Domain | Standard |
|---|---|
| Software | IEC 62304 medical device software lifecycle |
| Electrical | IPC-2221B PCB design, IEC 60601-1 medical electrical equipment |
| Clinical | ISO 14971 risk management, IEC 62366 usability |
| Regulatory | FDA 21 CFR Part 820, 510(k) SaMD pathway |
| Communications | NENA i3, FHIR R4, MQTT v5.0 |
| Infrastructure | NERC CIP, NRC 10 CFR Part 52, FAA AC 70/7460-1L |

---

## Shared Resources

| Resource | Location |
|---|---|
| Agent outputs | `/mnt/d/vDTC/OpenClaw/outputs/` |
| Work orders | `/mnt/d/vDTC/OpenClaw/state/WORK_ORDERS_AUTO.md` |
| Intelligence base | `/mnt/d/vDTC/OpenClaw/state/INTEL.md` |
| Project registry | `/mnt/d/vDTC/OpenClaw/state/projects_registry.json` |
| Coordination log | `/mnt/d/vDTC/OpenClaw/state/COORDINATION_LOG.md` |

---

## Communication

- **Daily:** vCEO agent produces a cycle priorities report
- **Weekly:** vChair agent produces a board-level strategic review with agent scorecards
- **Ad hoc:** Blue Sky and Debate agents run hypothesis-driven sessions across the portfolio
- **Insights:** Promoted from INSIGHT_INBOX.md to INTEL.md daily at 06:30 via Hermes review
