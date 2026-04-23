# Purple Patch — Active Bandage Platform

**Intelligent wound management with embedded biosensors, drug delivery, and AI healing optimization.**

Purple Patch is a next-generation wound care platform that replaces passive dressings with active, sensor-equipped bandages. Embedded electrodes monitor wound bioelectrical activity, temperature, pH, and exudate composition in real time. An on-patch microcontroller triggers targeted antimicrobial or growth-factor delivery based on wound state — and transmits healing data to clinical teams via BLE.

---

## Clinical Problem

- Chronic wounds affect 6.5 million Americans, costing $25B/year in treatment
- Diabetic foot ulcers (DFU) are the leading cause of non-traumatic lower limb amputation
- Standard-of-care dressings are passive — clinicians have no real-time wound data between visits
- Infection detection currently requires culture results: 48–72 hour lag that allows wound deterioration

---

## Core Technology

- **Biosensor array** — interdigitated electrodes measuring impedance, pH, temperature, exudate lactate
- **Microcontroller** — STM32L4 ultra-low-power; 7-day battery life on CR2032
- **Drug reservoir** — iontophoresis-controlled release of antimicrobial or PDGF-BB (platelet-derived growth factor)
- **BLE 5.2 uplink** — data to companion app (Android/iOS) and FHIR R4 EHR
- **AI healing model** — wound healing trajectory prediction based on sensor time series

---

## Status

> **Current:** Biosensor prototype on flexible PCB. In-vitro validation of impedance-based infection detection.
>
> **Next:** ISO 10993 biocompatibility testing, IACUC animal study protocol, FDA 510(k) strategy.
