# Detailed Technical Specification and Implementation Strategy — IronShield-SMR
_Generated: 2026-05-01 12:00 | Owner: EEPhD | Project: IronShield-SMR | Priority: High_

## Section 1: Detailed Technical Specification

### 1.1 Bill of Materials (BOM)

| Component Type | Manufacturer Part Number (MPN) | Voltage / Current / Tolerance | Subsystem Assignment |
|----------------|------------------------------|-------------------------------|----------------------|
| MCU            | STM32H750VBT6                 | 3.3V / 1A                     | CardioPoint          |
| ADC            | ADS1298                       | ±2.5V / 1MSPS                  | CardioPoint          |
| Memory         | W25Q128FV                     | 3.3V                          | CardioPoint          |
| PMIC           | MAX77650                      | 3.3V                          | CardioPoint          |
| AFE            | AD7689                       | ±2.5V / 1MSPS                  | CardioPoint          |

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/bom_cardiopoint_v01.csv`  
**Interface / Protocol:** None (internal component list)

### 1.2 Interface Control Document (ICD)

#### 1.2.1 I2C Bus
- **Bus Speed:** Fast Mode Plus (3.4 MHz)
- **CPOL/CPHA Modes:** CPOL = 0, CPHA = 1
- **Register Map:**
  - Address 0x00: Control Register
  - Address 0x01: Status Register
  - Address 0x02: Data Register

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/icd_i2c_cardiopoint_v01.csv`  
**Interface / Protocol:** I2C over 3.4 MHz

#### 1.2.2 SPI Bus
- **Bus Speed:** 8 MHz
- **CPOL/CPHA Modes:** CPOL = 0, CPHA = 0
- **Register Map:**
  - Address 0x00: Control Register
  - Address 0x01: Status Register
  - Address 0x02: Data Register

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/icd_spi_cardiopoint_v01.csv`  
**Interface / Protocol:** SPI over 8 MHz

#### 1.2.3 UART Bus
- **Baud Rate:** 115200 bps
- **Packet Framing:** Start bit, 8 data bits, no parity, 1 stop bit
- **CRC Polynomial:** CRC-16-CCITT (0x1021)
- **Retry Logic:** Maximum 3 retries with exponential backoff

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/icd_uart_cardiopoint_v01.csv`  
**Interface / Protocol:** UART over 115200 bps

### 1.3 Hardware Component Specifications

#### 1.3.1 MCU (STM32H750VBT6)
- **Clock Speed:** 480 MHz
- **Flash Memory:** ≥1 MB
- **RAM:** 512 KB
- **Power Consumption:** ≤20 mW

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/hardware_mcu_cardiopoint_v01.md`  
**Interface / Protocol:** None (internal component specification)

#### 1.3.2 ADC (ADS1298)
- **Sampling Rate:** 1 MSPS
- **Input Voltage Range:** ±2.5V
- **Resolution:** 24-bit

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/hardware_adc_cardiopoint_v01.md`  
**Interface / Protocol:** I2C over 3.4 MHz

#### 1.3.3 Memory (W25Q128FV)
- **Capacity:** 128 MB
- **Voltage Range:** 2.7V to 3.6V
- **Power Consumption:** ≤5 mW

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/hardware_memory_cardiopoint_v01.md`  
**Interface / Protocol:** SPI over 8 MHz

#### 1.3.4 PMIC (MAX77650)
- **Voltage Regulation:** 3.3V
- **Current Limit:** 1A
- **Power Consumption:** ≤20 mW

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/hardware_pmic_cardiopoint_v01.md`  
**Interface / Protocol:** I2C over 3.4 MHz

#### 1.3.5 AFE (AD7689)
- **Sampling Rate:** 1 MSPS
- **Input Voltage Range:** ±2.5V
- **Resolution:** 24-bit

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/hardware_afe_cardiopoint_v01.md`  
**Interface / Protocol:** I2C over 3.4 MHz

### 1.4 Implementation Strategies for Software Systems

#### 1.4.1 Real-Time Anomaly Detection Algorithms
- **Algorithm:** Pan-Tompkins QRS detection algorithm
- **Sampling Rate:** 1 MSPS
- **Detection Latency:** ≤50 ms
- **False Positive Rate:** ≤1%

**Implementing Agent:** SWPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/anomaly_detection_cardiopoint_v01.c`  
**Interface / Protocol:** I2C over 3.4 MHz

#### 1.4.2 Biosignal Acquisition
- **Sampling Rate:** 1 MSPS
- **Data Format:** Raw ADC values
- **Data Storage:** Internal flash memory
- **Power Consumption:** ≤20 mW

**Implementing Agent:** SWPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/biosignal_acquisition_cardiopoint_v01.c`  
**Interface / Protocol:** SPI over 8 MHz

#### 1.4.3 Communication Stack
- **Wireless Protocol:** Bluetooth Low Energy (BLE)
- **Encryption Standard:** AES-256
- **Cloud Endpoint:** AWS IoT Core
- **Latency Budget:** ≤100 ms

**Implementing Agent:** SWPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/communication_stack_cardiopoint_v01.c`  
**Interface / Protocol:** BLE over AES-256 to AWS IoT Core

#### 1.4.4 Memory Map Layout
- **Flash Memory:** ≥1 MB
- **RAM:** 512 KB
- **Partitioning:**
  - Code: 70%
  - Data: 30%

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/memory_map_cardiopoint_v01.md`  
**Interface / Protocol:** None (internal memory layout)

#### 1.4.5 Power Budget Reconciliation
- **Total System Power Consumption:** ≤65 mW
- **Component Maximums:**
  - PMIC: ≤20 mW
  - ADC: ≤20 mW
  - Memory: ≤5 mW
  - AFE/MCU: ≤20 mW

**Implementing Agent:** EEPhD  
**Platform / Language / Runtime:** STM32H7 bare-metal C  
**Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/eephd/power_budget_cardiopoint_v01.md`  
**Interface / Protocol:** None (internal power budget)

---

## Handoff → Owner: SWPhD, Task: Implement real-time anomaly detection algorithms, Target file: `/mnt/d/vDTC/OpenClaw/outputs/swphd/anomaly_detection_cardiopoint_v01.c`