# Android Edge Development

**Edge-Optimized Android Device and Interface Development**

The Android Edge Development platform builds the software and interface layer for vDTC's edge-deployed Android devices — including the 911AutoKiosk, 911InformaticsKioskAuto, BioCode Red companion app, and VitalsOne mobile relay. Focused on optimized performance, offline-first operation, and 911Hub integration.

---

## Core Scope

- **AOSP custom build** — stripped Android base for resource-constrained edge devices; <2GB RAM target
- **Offline-first architecture** — local SQLite + Room; sync to 911Hub when connectivity restores
- **911Hub SDK** — reusable MQTT client + FHIR R4 serialization library for all vDTC Android apps
- **Device management** — MDM integration (Fleet/Esper) for remote update, policy, and monitoring
- **Performance optimization** — Vulkan GPU compute for on-device AI inference; ARM NN delegate for TFLite

---

## Active Projects Using This Platform

- 911AutoKiosk Android interface
- BioCode Red companion app
- VitalsOne mobile relay app
- 911InformaticsKioskAuto dashboard

---

*Status: Active development*
