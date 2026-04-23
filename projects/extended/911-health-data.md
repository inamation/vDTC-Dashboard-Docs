# 911HealthData

**Health Data Standardization Initiative (HDSI) — From IoT to ICU**

NG911 modernizes call routing, multimedia, and precise location, but there is no standard for transmitting wearable and device health data into the 911 ecosystem. The 911 Health Data Standardization Initiative establishes the protocol layer that makes every connected health device a 911-compatible emergency data source.

---

## Core Problem

- Wearables (Apple Watch, Garmin, Dexcom, Owlet) generate clinical-grade data during emergencies
- No interoperability standard exists between consumer health devices and PSAP systems
- First responders arrive blind to vitals data that was captured in real time during the incident

---

## Core Technology

- **HDSI Protocol** — open standard for health device → 911Hub data transmission (built on FHIR R4 + MQTT)
- **Device SDK** — manufacturer integration kit for Apple HealthKit, Google Health Connect, and proprietary APIs
- **911Hub HDSI Gateway** — normalization layer that maps device data to standard Observation resources
- **PSAP display module** — dispatcher receives vitals timeline from moment of incident to call answer

---

## Strategic Value

- Positions vDTC as the standards body for emergency health data interoperability
- Licensing revenue from device manufacturers and PSAP software vendors
- Underpins all wearable integrations across the vDTC portfolio (VitalsOne, CradleAlert, CardioPoint)

---

*Status: Active — protocol design and FHIR R4 mapping in development*
