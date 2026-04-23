# Regulatory & Compliance

## FDA Classification

911Hub's AI analysis outputs constitute **Software as a Medical Device (SaMD)** under FDA's Digital Health framework.

**Target classification:** Class II — Moderate Risk  
**Regulatory pathway:** 510(k) Premarket Notification  
**Predicate strategy:** Existing cleared EMS clinical decision support software

### Why Class II (Not Class III)

911Hub is designed as **clinical decision support** — it provides information to trained clinicians who make the final decision. Under the 21st Century Cures Act, software that:
- Displays clinical data without interpreting or analyzing it → not a device
- Provides general wellness functions → not a device  
- Supports administrative functions → not a device
- **Supports or supplements clinical decision-making** → may be SaMD Class II

All 911Hub LLM outputs carry the disclaimer: *"FOR INFORMATIONAL USE ONLY — NOT A DIAGNOSIS. Final decisions rest with the licensed medical professional on scene."*

---

## IEC 62304 — Software Lifecycle

IEC 62304 defines software development lifecycle requirements for medical device software.

**Safety class:** Class B (non-serious injury possible if software fails)

**Required documentation:**
- [ ] Software Development Plan
- [ ] Software Requirements Specification
- [ ] Software Architecture Document (this GitBook serves as a starting point)
- [ ] Software Detailed Design Document
- [ ] Unit test records
- [ ] Integration test records
- [ ] System test records
- [ ] Software Release Record

**Current status:** Architecture documented. Codebase under active development. Formal lifecycle documentation to begin at pre-submission stage.

---

## ISO 14971 — Risk Management

Risk management file tracks failure modes, probability, severity, and mitigations.

**Top risk items:**

| Failure Mode | Severity | Probability | Mitigation |
|---|---|---|---|
| LLM hallucination on vitals | High | Medium | Human override always available; "informational" framing |
| Network loss during incident | High | Medium | Local caching on edge device; MQTT QoS 1 |
| GPU overload → LLM timeout | Medium | Medium | `_vitals_llm_in_flight` guard; Anthropic API fallback |
| Sensor malfunction → wrong vitals | High | Low | Data validation; out-of-range alerting |
| Unauthorized access to PHI | High | Low | JWT auth (roadmap); mTLS MQTT (roadmap) |
| Video lag → stale situational awareness | Medium | Medium | WebRTC auto-reconnect; latency monitoring |

---

## HIPAA Technical Safeguards

**Required for production deployment:**

| Safeguard | Status | Implementation |
|---|---|---|
| Encryption in transit | Roadmap | TLS 1.3 for all API/MQTT/WebRTC |
| Encryption at rest | Roadmap | PostgreSQL transparent encryption |
| Access controls | Roadmap | JWT RBAC (dispatcher, medic, admin) |
| Audit logs | Partial | LLM call logs; mission timeline recorder |
| PHI minimization | Partial | Device IDs used instead of patient names |
| Business Associate Agreement | Roadmap | Required with cloud provider (AWS/Azure) |

---

## NG911 / FCC Compliance

911Hub is designed for integration with NG911 infrastructure governed by:
- **NENA STA-010** — NG911 Core Services specification
- **NENA i3** — IP-based emergency services architecture
- **FCC Report and Order** — NG911 transition mandate

See [NG911 Integration Roadmap](ng911-integration.md) for technical integration specification.

---

## Timeline to 510(k) Clearance

| Milestone | Target |
|---|---|
| Architecture documentation complete | Q2 2026 |
| Risk management file (ISO 14971) | Q3 2026 |
| IEC 62304 documentation | Q3 2026 |
| Pre-submission meeting with FDA | Q4 2026 |
| 510(k) submission | Q1 2027 |
| Expected clearance | Q3-Q4 2027 |
