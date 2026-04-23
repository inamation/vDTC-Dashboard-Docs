# AI & LLM Pipeline

## Overview

911Hub uses a multi-model AI pipeline with local-first inference (privacy, latency, offline capability) and optional cloud API fallback. All AI outputs are framed as **clinical decision support** — informational guidance for trained responders, not autonomous diagnosis.

---

## Model Stack

| Model | Role | Runtime | VRAM |
|---|---|---|---|
| **llama3 8B** | Text: vitals analysis, chat, triage guidance | Ollama (local) | 4.7GB |
| **llava 7B** | Vision: X-ray image analysis | Ollama (local) | 4.7GB |
| **Claude Haiku** (optional) | Text: all text tasks via Anthropic API | Cloud | — |
| **Claude Opus** (optional) | Complex clinical reasoning | Cloud | — |

---

## LLM Provider Toggle

Switch between local and cloud inference at runtime — no restart required:

```
Hub Dashboard → Settings → LLM Provider
  [🖥️ Local (llama3)]   [☁️ Anthropic (claude-haiku)]
```

Or via API:
```bash
curl -X POST http://localhost:9111/api/settings/llm/anthropic
curl -X POST http://localhost:9111/api/settings/llm/local
```

When Anthropic is selected, the hub routes all text LLM calls to the Claude API using `ANTHROPIC_API_KEY`. Vision (X-ray) always uses local llava unless extended.

---

## Vitals Analysis

**Trigger:** Android publishes `edge/{id}/vitals/scenario` with a stage number and full vitals payload.

**Prompt template:**
```
You are an emergency medical decision support system.
Stage {stage}
Vitals: {hr, spo2, bp, temp, rr, ...}
Next action:
```

**Output:** Structured text recommendation — drug dosages, intervention priorities, transport decisions.

**Guard:** `_vitals_llm_in_flight` flag prevents queue flooding. If a previous vitals analysis is still running, incoming vitals for that device are skipped until complete.

**Stats published:** `911hub/llm/stats` — model, latency_ms, tokens_in, tokens_out, tokens/sec, confidence.

---

## X-Ray Vision Analysis

**Trigger:** Android uploads image via HTTP POST `/api/xray/upload`, then publishes MQTT metadata.

**Analysis chain:**
1. **MONAI** (medical AI) — attempted first for fracture/pathology detection
2. **LLaVA** (vision LLM) — fallback or supplement to MONAI
3. **Simulated** — placeholder when both unavailable

**LLaVA prompt:**
```
Analyze this X-ray image as an emergency medical AI assistant:
1. Identify anatomical region
2. Note visible abnormalities, fractures, or trauma
3. Assess bone density and alignment
4. Check for concussion signs (if skull) or internal injuries
5. Evaluate soft tissue for swelling, fluid, foreign objects
6. Provide emergency medical recommendations
7. Rate confidence level (0-100%)
```

**Response time:** ~30-60s on RTX 5080 (llava 7B quantized Q4).

---

## Chat Interface

**Design intent:** Free-form Q&A between field responder and hub AI. Not a vitals feed — pure conversational consultation.

**Trigger:** MQTT `edge/{id}/chat` with `{text}` payload.

**Prompt:**
```
You are the 911 Emergency Medical Informatics Kiosk assistant.
Responder says: {text}
Kiosk reply:
```

**Response routing:** LLM reply published to `911hub/chat` (MQTT → Android) and via WebSocket to dashboard.

---

## GPU Warmup

At hub startup, llama3 and llava are pre-loaded into VRAM:

```python
# Runs 3s after startup to let MQTT settle
for model in ("llama3", "llava"):
    POST /api/generate {model, prompt: ".", keep_alive: "30m"}
```

First response after warmup: ~369ms. Without warmup: ~97s (cold GPU load).

Warmup can be disabled via feature flag `warmup: OFF` (e.g., when using Anthropic API).

---

## Production LLM Roadmap

| Phase | Model | Rationale |
|---|---|---|
| PoC | llama3 8B general | Available, fast, good enough for demo |
| Beta | OpenBioLLM-8B or Meditron-7B | Medical fine-tune, local deployment |
| Production | BioMistral (HIPAA environment) or Claude claude-haiku-4-5 (cloud) | Validated clinical performance |
| Orin NX | Meditron-7B Q4 or MiniCPM-Med | Fits in 16GB, offline capable |

---

## Regulatory Note

> All LLM outputs in 911Hub are labeled **"FOR INFORMATIONAL USE ONLY — NOT A DIAGNOSIS"**. The system is designed as FDA Class II clinical decision support (non-device software function) under the 21st Century Cures Act framework. Human clinician override is always available and documented in the audit log.
