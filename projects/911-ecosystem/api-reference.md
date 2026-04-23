# API Reference

Base URL: `http://{hub-ip}:9111`

---

## State & Status

### GET /api/state
Returns full hub state including devices, vitals, EKG, chat, LLM stats, and system status.

```json
{
  "incident_active": false,
  "devices": { "edge911-device": { "vitals": {...}, "ekg": [...] } },
  "vitals": { "hr": 88, "spo2": 97, "llm_response": "..." },
  "ekg": [...],
  "chat_log": [{ "ts": 1234567890, "dir": "out", "text": "..." }],
  "llm_stats": { "model": "llama3", "latency_ms": 369, "tokens_per_sec": 42.1 },
  "status": { "mqtt": "connected", "webrtc": "streaming" }
}
```

---

## Settings / Feature Flags

### GET /api/settings
Returns all feature flags and LLM provider info.

### POST /api/settings/feature
Toggle a feature flag.
```json
{ "name": "vitals_llm", "enabled": false }
```

### POST /api/settings/llm/{provider}
Switch LLM provider. `provider` = `local` or `anthropic`.

---

## Chat

### POST /api/chat
Send a chat message and get LLM reply (dev/debug).
```json
{ "device_id": "edge911-device", "text": "Patient unresponsive, no pulse" }
```

### DELETE /api/chat/{device_id}
Clear chat history for a device.

---

## X-Ray

### POST /api/xray/upload
Upload X-ray image for AI analysis.
```json
{
  "device_id": "edge911-device",
  "image_base64": "...",
  "timestamp": 1234567890,
  "study_type": "Chest"
}
```
Returns: `{ "success": true, "image_id": "edge911-device_1234567890.jpg", "image_url": "/uploads/xrays/..." }`

### GET /api/xray/{device_id}
Get latest X-ray data and LLM analysis for a device.

---

## Security Cameras

### GET /api/security/cameras
List all configured cameras with status.

### POST /api/security/cameras/{camera_id}/select
Set active camera for viewing.

### POST /api/security/cameras/{camera_id}/configure
Configure camera name and RTSP credentials.
```json
{
  "name": "FRONT DOOR",
  "rtsp_user": "admin",
  "rtsp_pass": "your-password"
}
```

### POST /api/security/cameras/{camera_id}/status
Update camera status: `online`, `offline`, `connecting`, `error`.

---

## Video / WebRTC

### POST /webrtc/offer
Submit WebRTC SDP offer from Android publisher.
```json
{ "sdp": "...", "type": "offer" }
```

### POST /browser/offer  
Submit WebRTC SDP offer from browser viewer.
```json
{ "sdp": "...", "type": "offer" }
```

---

## YOLO Detection

### GET /api/yolo/status
Returns `{ "enabled": true }`.

### POST /api/yolo/toggle
Toggle YOLO detection. Optional `?enabled=true/false`.

---

## WebSocket Endpoints

### WS /ws/device/{device_id}
Device WebSocket for real-time push to Android app.

**Messages from hub:**
```json
{ "type": "chat_llm_response", "payload": { "text": "..." } }
{ "type": "vitals_llm_response", "payload": { "stage": 2, "text": "...", "confidence": 0.80 } }
{ "type": "xray_llm_response", "payload": { "xray_id": "...", "analysis": "..." } }
```

### WS /ws/detections
Real-time YOLO detection stream to browser.
```json
{ "type": "video_detections", "payload": { "detections": [{ "class": "person", "confidence": 0.94, "bbox": [x1,y1,x2,y2] }] } }
```
