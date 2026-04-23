# 911 Ecosystem

**Real-time AI-powered emergency response infrastructure for the Next Generation 911 ecosystem.**

The 911 Ecosystem is vDTC's flagship portfolio — three interconnected products that bridge field responders, 911 call centers (PSAPs), and AI-powered medical decision support.

---

## Three Products, One Platform

| Product | Deployment | Primary User |
|---|---|---|
| **911Hub** | PSAP / 911 Call Center | Dispatcher, Medical Director |
| **911AutoKiosk** | Emergency Vehicle | Paramedic, EMT |
| **911HomeKiosk** | Residence / Consumer | Individual, Caregiver |

---

## Core Capabilities

- **Live vitals streaming** — heart rate, SpO2, BP, temperature, respiratory rate via MQTT
- **EKG waveform** — real-time 12-lead equivalent display with AI rhythm analysis
- **WebRTC video** — sub-second latency live video from field device to hub
- **X-ray AI analysis** — LLaVA vision model analysis of uploaded X-ray images
- **AI chat** — free-form LLM consultation between responder and dispatch hub
- **YOLO detection** — weapon and person detection on live video feed
- **Multi-device** — simultaneous tracking of multiple field units per incident

---

## Technology Stack

```
Edge Device          Hub Backend           AI Layer
──────────────       ──────────────        ──────────────
Android (Kotlin)     FastAPI (Python)      Ollama (local)
Raspberry Pi 5   →   MQTT (Paho)       →   llama3 (text)
Jetson Orin NX       WebRTC (aiortc)       llava (vision)
                     PostgreSQL            Anthropic Claude (optional)
```

---

## Status

> **Current:** Proof-of-concept operational on local WiFi — Android tablet, Raspberry Pi 5, Jetson Orin NX, 911Hub server (RTX 5080 workstation).
>
> **Next:** Cellular connectivity, FHIR R4 data layer, NG911 CAD integration, FDA SaMD pre-submission.

---

*vDTC Research Corporation — research@dtc-intl.com*
