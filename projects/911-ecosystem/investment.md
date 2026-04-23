# Investor Summary

## The Problem

Emergency responders operate blind. A paramedic on scene with a critical patient has no real-time AI support, no live data link to the hospital or 911 center, and no way to share what they're seeing. The 911 dispatcher has voice only. Decisions are made on incomplete information under extreme time pressure.

The US processes **240 million 911 calls per year** across ~6,000 PSAPs and ~15,000 EMS agencies. The technology infrastructure at most of these centers hasn't meaningfully advanced in 20 years.

---

## The Opportunity

Next Generation 911 (NG911) is a federally mandated transition from analog to IP-based emergency communications — a $15B+ infrastructure upgrade already underway. NG911 enables data, video, and AI to travel alongside every 911 call for the first time.

911Hub is purpose-built to be the AI data layer of NG911.

---

## Product Portfolio

### 911Hub — PSAP Platform
**Market:** ~6,000 PSAPs in the US, 240M 911 calls/year
**Model:** SaaS subscription per PSAP — $2,400–$8,400/year
**Value:** AI triage support, live vitals, video, X-ray at the dispatcher console

### 911AutoKiosk — Vehicle Platform  
**Market:** ~15,000 EMS agencies, ~60,000 ambulances
**Model:** Per-vehicle license + hardware — $1,200/vehicle/year + $800 hardware
**Value:** Offline-capable AI on Jetson Orin, automatic incident documentation, live hub link

### 911HomeKiosk — Consumer Platform
**Market:** 34M Americans over 65, 15M with chronic conditions requiring monitoring
**Model:** Hardware + subscription — $299 device + $9.99/month
**Value:** Fall detection, BLE wearable integration, automatic 911 escalation

---

## Differentiation

| Capability | 911Hub | CAD Vendors | Patient Monitors |
|---|---|---|---|
| AI triage at dispatch | ✓ | ✗ | ✗ |
| Live field video | ✓ | Limited | ✗ |
| X-ray AI analysis | ✓ | ✗ | ✗ |
| Open MQTT architecture | ✓ | ✗ | ✗ |
| NG911 i3 native | ✓ (roadmap) | Partial | ✗ |
| Local + cloud LLM | ✓ | ✗ | ✗ |
| Hardware agnostic | ✓ | ✗ | ✗ |

---

## Traction

- Working proof-of-concept: live vitals, EKG, video, X-ray AI, chat LLM
- Hardware validated: Android, Raspberry Pi 5, Jetson Orin NX
- AI pipeline: llama3 + llava via Ollama; Anthropic Claude API integrated
- Architecture designed for FDA SaMD Class II pathway
- NG911 integration specification in development (NENA i3 / ESRP)

---

## Strategic Partners (Target)

| Partner | Rationale |
|---|---|
| **Motorola Solutions** | Dominant CAD vendor (PremierOne) — integration partner |
| **AT&T FirstNet** | First responder LTE network — connectivity partner |
| **Stryker** | Power-PRO ambulance cot — hardware integration |
| **Physio-Control (Stryker)** | LIFEPAK 15/35 monitor — vitals data bridge |
| **Anthropic** | Claude API — AI partner / co-sell |

---

## Regulatory Path

- **FDA Class II SaMD** — clinical decision support, non-device software function
- **Predicate:** Existing cleared EMS clinical decision support tools
- **IEC 62304** software lifecycle documentation in progress
- **HIPAA** — audit log, encryption, BAA with cloud provider
- **Timeline:** Pre-submission meeting → 510(k) → clearance: 18–24 months

---

## Team

**vDTC Research Corporation** — Design Team Collaboration Non-Profit Research Corporation, Michigan

AI-native R&D organization with expertise in embedded systems, emergency medicine, regulatory compliance, and real-time communications infrastructure.

---

*For partnership inquiries: research@dtc-intl.com*
*Technical documentation: research.dtc-intl.com*
