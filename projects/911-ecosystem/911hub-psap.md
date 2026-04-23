# 911Hub — PSAP Command Center

## What It Is

911Hub is the server-side platform deployed at a Public Safety Answering Point (PSAP) — the 911 call center. It receives real-time data from field responders, runs AI analysis, and presents a unified incident dashboard to dispatchers and medical directors.

---

## Dashboard Panels

### Live Video
WebRTC stream from the field responder's Android device. Sub-second latency. YOLO object detection overlay identifies persons and weapons in real time with alert sound on weapon detection.

### Vitals Panel
Continuous vital signs display: heart rate, SpO2, blood pressure, temperature, respiratory rate. Color-coded by severity. Includes AI-generated clinical recommendation per stage.

### EKG Waveform
Real-time EKG waveform rendered from 50Hz sample stream. Supports escalation modes: IDLE → MONITORING → ELEVATED → CRITICAL.

### X-Ray Panel
Displays uploaded X-ray images with LLaVA vision AI analysis. Shows anatomical region, abnormalities, fracture detection, and confidence score.

### Chat Panel
Direct LLM-assisted communication channel between dispatcher/hub and field responder. Supports voice input. Separate from vitals analysis — pure Q&A consultation interface.

### Security Cameras
Multi-camera viewer for facility and vehicle cameras. Currently: BIN, FRONT DOOR, HALLWAY, LIVING ROOM, TRUCK (TP-Link Kasa via RTSP).

### LLM Stats
Live performance metrics for each AI inference: model name, latency (ms), tokens/second, confidence score. LIVE/SIMULATED indicator.

### Settings
Runtime feature flag toggles. LLM provider switch (local Ollama ↔ Anthropic Claude). No restart required.

---

## Incident Lifecycle

```
DISPATCH SIGNAL
      ↓
Android app activates → MQTT connects → Hub creates device record
      ↓
Field data streams: vitals → LLM analysis → response to responder
      ↓
Video stream: WebRTC → YOLO → dashboard display
      ↓
X-ray upload → LLaVA analysis → result to responder + dashboard
      ↓
Chat consultation → LLM reply → responder + dispatcher see exchange
      ↓
TRANSPORT / CLOSE → Mission timeline recorded to audit log
```

---

## Deployment

**Current (PoC):**
- RTX 5080 workstation, WSL2/Ubuntu
- Local WiFi, single incident
- Ollama local LLM

**Production target:**
- Cloud VM or on-premise server at PSAP
- Cellular connectivity to field devices (AT&T FirstNet)
- Multi-incident dashboard (10–50 simultaneous)
- PostgreSQL persistent storage
- MQTT over TLS with device certificates
- JWT authentication (dispatcher, medic, admin roles)

---

## Integration Points

| System | Status | Protocol |
|---|---|---|
| Android field device | Live | MQTT + WebRTC |
| Raspberry Pi 5 sensor node | Live | MQTT |
| Jetson Orin NX edge AI | Live | MQTT |
| TP-Link Kasa cameras | Configured (RTSP pending enable) | RTSP |
| NG911 CAD systems | Roadmap | SIP / i3 XML |
| EHR systems | Roadmap | FHIR R4 |
| Motorola PremierOne CAD | Roadmap | REST API |
