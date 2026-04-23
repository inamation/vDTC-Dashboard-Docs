# Platform Architecture

## System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        FIELD (EDGE)                             │
│                                                                 │
│  Android Tablet          Raspberry Pi 5       Jetson Orin NX   │
│  ┌─────────────┐         ┌─────────────┐      ┌─────────────┐  │
│  │ edge911     │         │ Sensor Node │      │ AI Edge Node│  │
│  │ Android App │         │ GPIO sensors│      │ Local LLM   │  │
│  │ WebRTC cam  │         │ BLE wearable│      │ YOLO detect │  │
│  │ MQTT client │         │ MQTT client │      │ MQTT client │  │
│  └──────┬──────┘         └──────┬──────┘      └──────┬──────┘  │
│         │                       │                    │         │
└─────────┼───────────────────────┼────────────────────┼─────────┘
          │     MQTT over WiFi/LTE│                    │
          ▼                       ▼                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                       911HUB SERVER                             │
│                                                                 │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────────┐  │
│  │ MQTT Broker  │    │ FastAPI      │    │ AI Layer         │  │
│  │ (Mosquitto)  │───▶│ Backend      │───▶│ Ollama (local)   │  │
│  │ port 1883    │    │ port 9111    │    │ llama3 / llava   │  │
│  └──────────────┘    └──────┬───────┘    │ Anthropic (opt.) │  │
│                             │            └──────────────────┘  │
│                      ┌──────▼───────┐                          │
│                      │ React SPA    │                          │
│                      │ port 5173    │                          │
│                      └──────────────┘                          │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────┐
│  DISPATCHER BROWSER │
│  Dashboard at       │
│  192.168.1.8:5173   │
└─────────────────────┘
```

---

## Data Flow

### Vitals + EKG
```
Android sensor → MQTT publish edge/{device_id}/vitals/scenario
→ Hub subscribes → LLM analysis (llama3) → MQTT publish 911hub/vitals/response
→ Android receives → displays on VitalsScreen
→ Hub WebSocket → Dashboard updates
```

### Video
```
Android camera → WebRTC offer → Hub /webrtc/offer
→ aiortc answer → ICE negotiation → RTP stream
→ Hub VideoPanel (browser) → YOLO detection overlay
```

### X-Ray
```
Android selects image → HTTP POST /api/xray/upload (base64)
→ Hub saves to /uploads/xrays/ → MQTT publish edge/{id}/xray
→ Hub triggers LLaVA analysis → MQTT publish 911hub/xray/response
→ Dashboard XRayPanel updates
```

### Chat
```
Responder types → MQTT publish edge/{device_id}/chat
→ Hub LLM call (llama3 or Claude) → MQTT publish 911hub/chat
→ Android ChatScreen receives reply
```

---

## MQTT Topic Schema

| Direction | Topic | Payload |
|---|---|---|
| Edge → Hub | `edge/{device_id}/vitals` | `{hr, spo2, bp_sys, bp_dia, temp, rr}` |
| Edge → Hub | `edge/{device_id}/vitals/scenario` | `{stage, ...vitals}` |
| Edge → Hub | `edge/{device_id}/ekg` | `{samples[], lead, sample_rate_hz}` |
| Edge → Hub | `edge/{device_id}/chat` | `{text, timestamp}` |
| Edge → Hub | `edge/{device_id}/xray` | `{xray_id, image_id, study_type}` |
| Hub → Edge | `911hub/vitals/response` | `{stage, text, confidence, latency_ms}` |
| Hub → Edge | `911hub/chat` | `{text}` |
| Hub → Edge | `911hub/xray/response` | `{xray_id, analysis, confidence, model}` |
| Hub → Edge | `911hub/llm/stats` | `{model, latency_ms, tokens_in, tokens_out}` |

---

## Feature Flags

All major capabilities are controlled by runtime feature flags, togglable via the hub dashboard Settings panel or REST API (`/api/settings`):

| Flag | Default | Description |
|---|---|---|
| `vitals_llm` | ON | LLM analysis on vitals data |
| `chat_llm` | ON | LLM replies to responder chat |
| `xray_llm` | ON | Vision AI X-ray analysis |
| `webrtc` | ON | Live WebRTC video |
| `yolo` | ON | YOLO object/weapon detection |
| `warmup` | ON | GPU model pre-load at startup |
| `anthropic_llm` | OFF | Route LLM calls to Anthropic Claude API |
| `ng911_bridge` | OFF | NG911 CAD integration (future) |
| `fhir_export` | OFF | FHIR R4 structured export (future) |

---

## Hardware Reference

| Device | Role | Specs |
|---|---|---|
| RTX 5080 Workstation | Hub server, LLM inference | 16GB VRAM, WSL2/Ubuntu |
| Android Tablet | Field responder device | edge911 app, WebRTC publisher |
| Raspberry Pi 5 | Edge sensor node | GPIO sensors, BLE, MQTT |
| Jetson Orin NX | Edge AI node | Local LLM inference, YOLO |
| TP-Link Kasa × 5 | Security cameras | RTSP streams (BIN, FRONT DOOR, HALLWAY, LIVING ROOM, TRUCK) |
