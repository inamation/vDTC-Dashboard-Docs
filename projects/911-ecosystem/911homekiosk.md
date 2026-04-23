# 911HomeKiosk — Consumer Platform

## Concept

911HomeKiosk is a consumer device for at-risk individuals — elderly, chronic condition patients, or anyone who needs a passive safety net. It monitors continuously, escalates automatically, and connects directly to 911Hub when an emergency is detected.

---

## Key Features

- **Fall detection** — IMU + barometric pressure, accelerometer array
- **BLE wearable ingestion** — FDA-cleared pulse ox, blood pressure cuff, EKG patch
- **Panic button** — physical + app-based, tamper-detected
- **Smoke/CO detection** — environmental emergency triggers
- **Automatic 911 escalation** — configurable escalation ladder (caregiver → family → 911)
- **Two-way audio** — speak directly to 911 dispatcher via device
- **HIPAA consent flow** — built-in, user controls data sharing scope

---

## Hardware

| Component | Selection |
|---|---|
| Compute | Raspberry Pi 5 (4GB) |
| Display | 7" touchscreen (optional) |
| Connectivity | WiFi + cellular backup (optional LTE HAT) |
| BLE | Integrated BLE 5.0 |
| Sensors | IMU, barometric, mic array |
| Audio | Speaker + microphone for voice |

---

## Business Model

| Item | Price |
|---|---|
| Hardware (device) | $299 one-time |
| Monitoring subscription | $9.99/month |
| Professional monitoring add-on | $14.99/month |
| Family plan (up to 4 devices) | $24.99/month |

---

## Status

> **Roadmap** — Concept defined. Raspberry Pi 5 validated as compute platform. BLE sensor integration specification in progress.
