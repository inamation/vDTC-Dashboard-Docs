# Pi 5 Edge Development

**Raspberry Pi 5 Edge Compute and Services Platform**

The Pi 5 Edge Development platform defines the hardware and software stack for vDTC's Raspberry Pi 5-based edge deployments — including WavePod audio processing, 911AutoKiosk compute, and field sensor aggregation nodes. Pi 5 + Coral TPU is the primary edge AI inference platform across the vDTC portfolio.

---

## Core Stack

- **Hardware** — Raspberry Pi 5 (8GB); Coral USB TPU or M.2 TPU; NVMe SSD via HAT+; PoE+ power
- **OS** — Raspberry Pi OS Lite (64-bit); hardened; read-only root filesystem; tmpfs overlays
- **Inference runtime** — TFLite runtime with Coral EdgeTPU delegate; ONNX Runtime for non-TPU models
- **Service framework** — systemd services; watchdog-supervised; auto-restart on failure
- **911Hub client** — MQTT Paho; FHIR R4 resource construction; offline queue with SQLite
- **Remote management** — Tailscale mesh VPN; Ansible playbooks for fleet update

---

## Active Deployments

- WavePod — Whisper inference + beamforming on Pi 5 + Coral TPU
- 911AutoKiosk — kiosk compute node
- CardioPoint Field — ECG edge inference
- Sensor aggregation nodes in JOBSITE911 and 911SchoolBUS

---

*Status: Active — platform standardization and deployment tooling*
