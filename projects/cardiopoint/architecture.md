# CardioPoint — Architecture

## System Architecture

```
BLE/Electrode Patch
      │
      ▼
Android Edge Device (Kotlin)
  - ECG signal acquisition (250 Hz, 12-lead equivalent)
  - BLE GATT profile (Heart Rate + Custom ECG Service)
  - Local AI inference: TensorFlow Lite arrhythmia model
      │  MQTT over TLS 1.3
      ▼
CardioPoint Hub Backend (FastAPI / Python 3.11)
  - Signal buffering and time-series store (TimescaleDB)
  - Arrhythmia event broker (Kafka topic: cardio.events)
  - FHIR R4 Observation resources (HL7 FHIR server: HAPI)
  - Anthropic Claude API — clinical narrative generation
      │  WebRTC / FHIR
      ▼
Clinical Display (React 18 / TypeScript)
  - Live waveform rendering (60fps canvas)
  - Alert panel with AI-generated differential
  - EHR export (FHIR R4 Bundle)
```

## Key Interfaces

| Interface | Protocol | Standard |
|---|---|---|
| Electrode → Device | BLE 5.2, GATT | IEEE 11073-10406 |
| Device → Hub | MQTT v5.0 over TLS 1.3 | HL7 FHIR R4 |
| Hub → EHR | REST/JSON | HL7 FHIR R4 (STU3 fallback) |
| Display → Hub | WebSocket | RFC 6455 |

## AI Inference Stack

| Layer | Model | Runtime | Latency Target |
|---|---|---|---|
| Edge arrhythmia | Custom CNN (TFLite) | Android NPU | <200ms |
| Hub classification | Larger transformer | Ollama (local) | <2s |
| Clinical narrative | Claude claude-sonnet-4-6 | Anthropic API | <4s |
