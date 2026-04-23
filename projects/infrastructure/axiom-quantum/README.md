# Axiom Quantum — Compute Platform

**Quantum computing integration within the Luminary data center campus — targeting drug discovery, cryptography, and optimization at scale.**

Axiom Quantum is the quantum computing arm of the vDTC infrastructure stack, co-located within Luminary Architecture. It combines cryogenic quantum processing units (QPUs), classical HPC co-processors, and quantum-classical hybrid software tooling — targeting applications in pharmaceutical simulation, financial optimization, logistics, and post-quantum cryptography.

---

## Technology Approach

Axiom Quantum operates as a quantum-as-a-service platform rather than building QPUs from scratch. The strategy is integration and orchestration:

| Layer | Provider / Technology | vDTC Role |
|---|---|---|
| QPU hardware | IBM Quantum (127–1,000+ qubit), IonQ (trapped ion) | Co-location partner / access resale |
| Classical HPC co-processor | NVIDIA H100 / GH200 clusters in Luminary | vDTC operates |
| Quantum-classical middleware | Qiskit Runtime, PennyLane, CUDA-Q | vDTC develops integration layer |
| Application layer | Drug discovery (VQE), optimization (QAOA), QKD | vDTC develops and licenses |
| Cryogenic infrastructure | Dilution refrigerators (Bluefors, Oxford) | vDTC hosts in Luminary |

---

## Target Applications

- **Drug discovery:** Variational Quantum Eigensolver (VQE) for molecular simulation — target: protein folding for NeuroSeal peptide candidates, CardioPoint drug interactions
- **Cryptography:** Post-quantum key distribution (QKD), NIST PQC algorithm implementation (CRYSTALS-Kyber, CRYSTALS-Dilithium)
- **Emergency response optimization:** QAOA for multi-incident resource allocation in 911Hub dispatch
- **Portfolio optimization:** Quantum annealing for supply chain and BOM optimization

---

## Status

> **Current:** Concept and partnership evaluation phase. IBM Quantum Network membership under review.
>
> **Next:** Cryogenic infrastructure spec for Luminary Phase 1, IBM Quantum / IonQ access agreement, first application pilot (VQE for NeuroSeal molecular targets).
