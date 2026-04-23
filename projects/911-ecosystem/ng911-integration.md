# NG911 Integration Roadmap

## What is NG911?

Next Generation 911 is the federally mandated transition from the current analog 911 system to an IP-based network — the Emergency Services IP Network (ESInet). NG911 enables data, text, video, and AI to travel alongside every 911 call for the first time.

**Key standards:** NENA i3, NENA STA-010, RFC 6443 (LoST), RFC 5222 (PIDF-LO)

---

## How 911Hub Fits

```
FIELD RESPONDER                    PSAP (911 Call Center)
┌─────────────────┐                ┌─────────────────────────┐
│ Android edge911 │                │       ESInet             │
│ + Orin/Pi nodes │                │  ┌──────────────────┐   │
│                 │                │  │ Emergency Call   │   │
│  MQTT/WebRTC    │──────LTE──────▶│  │ Routing Function │   │
│  (today)        │                │  │ (ECRF)           │   │
│                 │                │  └────────┬─────────┘   │
└─────────────────┘                │           │             │
                                   │  ┌────────▼─────────┐  │
                                   │  │  911Hub Server    │  │
                                   │  │  + CAD System     │  │
                                   │  │  + AI Layer       │  │
                                   │  └──────────────────┘  │
                                   └─────────────────────────┘
```

---

## Integration Components (Roadmap)

### 1. PIDF-LO Location Object
Attach responder GPS location to every MQTT message in PIDF-LO XML format for NG911 routing.

```xml
<presence xmlns="urn:ietf:params:xml:ns:pidf"
          xmlns:gp="urn:ietf:params:xml:ns:pidf:geopriv10">
  <tuple id="edge911-device">
    <status><gp:geopriv>
      <gp:location-info>
        <gs:Point srsName="urn:ogc:def:crs:EPSG::4326">
          <gs:pos>42.2917 -85.5872</gs:pos>
        </gs:Point>
      </gp:location-info>
    </gp:geopriv></status>
  </tuple>
</presence>
```

### 2. Additional Data (AD) XML
Transmit structured patient/incident data to PSAP via NG911 Additional Data mechanism.

```xml
<EmergencyCallData.Comment>
  <Comment>
    HR:88 SpO2:97 BP:120/80 Temp:98.6
    AI Assessment: Patient stable, monitor for deterioration.
    Confidence: 0.80
  </Comment>
</EmergencyCallData.Comment>
```

### 3. CAD Integration
Connect to Computer-Aided Dispatch systems via vendor REST APIs:

| CAD Vendor | Market Share | Integration Method |
|---|---|---|
| Motorola PremierOne | ~35% | REST API + webhooks |
| Tyler Technologies | ~20% | REST API |
| Hexagon (Intergraph) | ~15% | REST API |

### 4. MQTT → SIP Bridge
Route MQTT incident data to PSAP via SIP INFO messages, enabling 911Hub data to appear in the PSAP operator console alongside the voice call.

---

## Feature Flag

NG911 bridge is available as a feature flag (`ng911_bridge`) currently set to **OFF** pending specification completion. Enable when CAD integration credentials are configured:

```bash
curl -X POST http://localhost:9111/api/settings/feature \
  -H "Content-Type: application/json" \
  -d '{"name": "ng911_bridge", "enabled": true}'
```

---

## Standards References

- [NENA STA-010](https://www.nena.org/page/i3_stage) — NG911 Core Services
- [NENA i3 Architecture](https://www.nena.org/page/i3_resources) — ESInet design
- [RFC 5222](https://tools.ietf.org/html/rfc5222) — LoST protocol
- [RFC 4119](https://tools.ietf.org/html/rfc4119) — PIDF-LO
- [NENA Additional Data](https://www.nena.org/page/AdditionalData) — Structured incident data
