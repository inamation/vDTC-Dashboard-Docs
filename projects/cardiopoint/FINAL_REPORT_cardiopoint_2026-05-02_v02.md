# Detailed Technical Specification and BOM Update for CardioPoint
_Generated: 2026-05-02 04:00 | Owner: SWPhD | Project: CardioPoint | Priority: High_

## Section 1: Bill of Materials (BOM)

### Hardware Components

| Component Name | MPN/Part Number | Supplier | Quantity | Cost per Unit ($) |
|----------------|-----------------|----------|----------|-------------------|
| STM32H750VBT6   | STM32H750VBT6    | STMicroelectronics | 1 | 4.90              |
| SIM800L         | SIM800L          | Ai-Thinker/SIMCOM | 1 | 2.50              |
| Power Bank (PB) | PB-3000mAh       | Anker    | 1 | 15.00             |
| MicroSD Card   | SDHC Class 10    | SanDisk  | 1 | 5.00              |
| GPS Module     | GP20U7           | Quectel  | 1 | 8.00              |
| Accelerometer  | ADXL345          | Analog Devices | 1 | 3.50            |
| Gyroscope      | ITG-3200         | InvenSense | 1 | 4.00             |
| Heart Rate Sensor | MAX30102       | Maxim Integrated | 1 | 7.00           |
| Temperature Sensor | TMP102        | Texas Instruments | 1 | 3.00          |

### Notes:
- **Power Bank (PB-3000mAh):** The Anker Power Bank is a consumer-grade product with a capacity of 3000mAh. It provides power to the STM32H750VBT6 and other peripherals.
- **SIM800L:** This module is used for cellular communication. It supports GSM/GPRS/EGPRS and has an Ai-Thinker/SIMCOM chipset.
- **MicroSD Card:** Used for data storage, with a minimum write speed of 10MB/s.
- **GPS Module (GP20U7):** Provides location services for emergency response coordination.

## Section 2: Detailed Technical Specification

### Subsystem Definitions

#### 1. CardioPoint Core
- **Implementing agent:** SWPhD implements in STM32H7 bare-metal C
- **Platform / language / runtime:** STM32H7 bare-metal C
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/cardio_point_core.c`
- **Interface / protocol:** I2C for sensor communication, UART for GPS and SIM800L

#### 2. Anomaly Detection Subsystem
- **Implementing agent:** SWPhD implements in STM32H7 bare-metal C
- **Platform / language / runtime:** STM32H7 bare-metal C
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/anomaly_detection.c`
- **Interface / protocol:** I2C for sensor data input

#### 3. Communication Subsystem
- **Implementing agent:** SWPhD implements in STM32H7 bare-metal C
- **Platform / language / runtime:** STM32H7 bare-metal C
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/communication_subsystem.c`
- **Interface / protocol:** UART for SIM800L, I2C for GPS

#### 4. Data Storage Subsystem
- **Implementing agent:** SWPhD implements in STM32H7 bare-metal C
- **Platform / language / runtime:** STM32H7 bare-metal C
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/data_storage.c`
- **Interface / protocol:** SPI for MicroSD Card

### Numeric Thresholds and Clinical Decision Criteria

#### Anomaly Detection Triggers
- **Heart Rate Variability (HRV) > 50% of Baseline:** HRV threshold is set to 50% above the user's baseline HRV. This value is normalized based on the user's average HRV over a period of one week.
- **R-R Interval < 400 ms:** R-R interval threshold is set to less than 400 milliseconds, indicating ventricular tachycardia or fibrillation.
- **Skin Conductance Level (SCL) > 2.0 μS/cm:** SCL threshold is set to greater than 2.0 microSiemens per centimeter, indicating stress or anxiety.

#### Intervention Timing Windows
- **Immediate Escalation:** If any of the anomaly detection triggers are met, an immediate escalation alert is sent via SMS and GPS location.
- **Handoff Confirmation Timeout:** The system waits for a confirmation from the responder within 30 seconds. If no response is received, the system retries sending the alert.

### Architecture Diagram

![CardioPoint Architecture](/mnt/d/vDTC/OpenClaw/outputs/swphd/cardio_point_architecture.png)

## Section 3: System Overview

The CardioPoint device integrates multiple subsystems to provide real-time monitoring and anomaly detection. The core of the system is the STM32H750VBT6 microcontroller, which manages sensor data acquisition, anomaly detection, communication, and data storage. Each subsystem communicates with the core via defined interfaces (I2C, UART, SPI).

### Data Flow Trace

1. **Sensor Input:**
   - Heart Rate Sensor (MAX30102) → I2C to STM32H750VBT6
   - Accelerometer (ADXL345) → I2C to STM32H750VBT6
   - Gyroscope (ITG-3200) → I2C to STM32H750VBT6
   - Temperature Sensor (TMP102) → I2C to STM32H750VBT6

2. **Anomaly Detection:**
   - Data from sensors is processed in the Anomaly Detection Subsystem.
   - If any anomaly trigger is met, an alert is generated.

3. **Communication:**
   - The Communication Subsystem sends alerts via SMS and GPS location using the SIM800L module.
   - Location data is obtained from the GP20U7 GPS module.

4. **Data Storage:**
   - Raw sensor data and anomaly detection logs are stored on the MicroSD Card for later analysis.

5. **Error Handling:**
   - If any component fails, the system logs the error and retries the operation.
   - If multiple failures occur, the system enters a safe mode and sends an emergency alert.

## Handoff

**Handoff →** Owner: SWPhD, Task: Develop Quantum-Classical Hybrid Firmware Architecture (QCHA), Target file: `/mnt/d/vDTC/OpenClaw/outputs/swphd/qcha_architecture.c`