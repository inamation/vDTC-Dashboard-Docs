# 911AutoKiosk — Vehicle Platform

## Concept

911AutoKiosk is a ruggedized edge compute platform mounted in emergency vehicles. It provides offline-capable AI, automatic incident documentation, and a live data link to the 911Hub PSAP server — activated automatically when a unit is dispatched.

---

## Hardware Configuration

| Component | Selection | Role |
|---|---|---|
| AI Compute | NVIDIA Jetson Orin NX 16GB | Local LLM inference, YOLO detection |
| Connectivity | LTE modem (AT&T FirstNet SIM) | Primary WAN to 911Hub |
| Display | 10" ruggedized touchscreen | Responder UI |
| Camera | Android device (dual-role) | Video publisher + crew interface |
| GPS | u-blox ZED-F9P | PIDF-LO location for NG911 |
| Sensors | BLE 5.0 hub | Wearable vitals from patient |
| Vehicle | OBD-II / J1939 reader | Speed, door status, crash detection |

---

## Offline Capability

When cellular connectivity is lost, 911AutoKiosk continues operating locally:

- Jetson Orin runs Meditron-7B (Q4 quantized, ~8GB VRAM) for medical AI
- MQTT broker runs locally on Jetson
- All incident data buffered to NVMe SSD
- Sync to 911Hub resumes when connectivity restored

---

## Auto-Activation

On dispatch signal (CAD → unit notification):
1. Jetson powers on compute modules
2. LTE modem establishes FirstNet connection
3. MQTT connects to 911Hub
4. Incident record created
5. Android crew device notified

---

## Status

> **Roadmap** — Hardware components selected. Software architecture defined. Integration with Jetson Orin NX in progress.
