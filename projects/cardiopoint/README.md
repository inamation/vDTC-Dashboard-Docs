# CardioPoint

**Continuous cardiac monitoring and AI-assisted ECG analysis for clinical and field deployment.**

CardioPoint is a medical-grade cardiac monitoring platform designed for both hospital and pre-hospital environments. It combines multi-lead ECG acquisition, real-time arrhythmia detection, and AI clinical decision support into a single integrated system.

---

## Core Capabilities

- **12-lead ECG acquisition** — hospital-grade signal quality via dry-electrode array
- **Real-time arrhythmia detection** — AI classification (AF, VF, VT, STEMI, NSTEMI) with <2s latency
- **Continuous monitoring** — 72-hour ambulatory recording with cellular uplink
- **Clinical AI** — LLM-assisted differential diagnosis and risk stratification
- **FHIR R4 integration** — native EHR interoperability for hospital deployment
- **Edge inference** — on-device AI on Jetson Orin NX for zero-cloud dependency

---

## Deployment Environments

| Environment | Hardware | Connectivity |
|---|---|---|
| PSAP / Hospital | Fixed station, large display | Ethernet / Wi-Fi |
| Ambulance | Ruggedized tablet + auto mount | FirstNet LTE |
| Home Monitoring | Android device + BLE patch | Wi-Fi / LTE |
| Field (Mass Casualty) | Jetson Orin NX portable unit | Satellite uplink |

---

## Status

> **Current:** Signal acquisition validated on prototype hardware. AI model trained on PhysioNet MIT-BIH dataset.
>
> **Next:** ISO 14971 risk management file, IEC 60601-1 electrical safety testing, FDA 510(k) pre-submission meeting.

---

*vDTC Research Corporation — research@dtc-intl.com*
