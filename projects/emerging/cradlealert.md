# CradleAlert

**Preparation That Begins at Birth. Protection That Never Stops.**

CradleAlert is an AI-powered infant monitoring and emergency alert system that bridges home health monitoring with 911 emergency response. The system combines a smart bassinet sensor array, wearable infant biometric patch, and AI risk assessment — automatically escalating to 911 with vitals data when intervention thresholds are crossed.

---

## Clinical Problem

- **SIDS (Sudden Infant Death Syndrome):** 3,400 infant deaths/year in the US; peak risk: 1–4 months
- **ALTE (Apparent Life-Threatening Events):** 6–9 per 1,000 live births
- Current monitors: Owlet and similar consumer devices detect SpO2 and HR but do not integrate with 911 or EMS systems
- **Gap:** No FDA-cleared device automatically transmits infant vitals to a PSAP at the moment of emergency

---

## Core Technology

- **Biometric patch** — BLE 5.2 infant-safe wearable: SpO2, heart rate, respiratory rate, temperature, movement
- **Smart bassinet mat** — pressure array for body position monitoring and apnea detection
- **AI risk engine** — time-series anomaly detection for cardiorespiratory patterns; SIDS risk scoring
- **911Hub integration** — automatic MQTT alert to 911Hub with vitals + location when threshold crossed
- **Parent app** — Android/iOS real-time dashboard; configurable alert thresholds; pediatrician sharing via FHIR R4

---

## Investment Summary

**Market:** 3.7M births/year in the US; ~80% of parents use some form of infant monitor
**TAM:** 2.9M monitor-buying parents/year × $299 device + $9.99/month = **$867M/year device + $348M/year subscription**
**Funding ask (Pre-Seed):** $1.4M — biocompatibility testing, IACUC infant sensor validation, FDA 510(k) strategy

---

*Status: Concept → hardware prototype Q3 2026*
