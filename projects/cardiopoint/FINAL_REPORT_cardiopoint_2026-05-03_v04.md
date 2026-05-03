# Detailed Technical Specification — CardioPoint — v04 FDA Submission Preparation and Interface Protocols
_Generated: 2026-05-03 16:00 | Owner: SWPhD | Project: CardioPoint | Priority: High_

## Detailed Technical Specification — CardioPoint — v04 FDA Submission Preparation and Interface Protocols

### Section 1: FDA Submission Pathway

#### 1.1 Device Classification
- **Implementing Agent:** RegulatoryPhD
- **Platform / Language / Runtime:** N/A (Regulatory Analysis)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/regulatoryphd/classification_report_2026-05-03.md`
- **Interface / Protocol:** N/A

**Requirement 1.1.1:**
Classify the CardioPoint device as Class I, II, or III based on risk assessment.

**Acceptance Criteria:**
- A detailed classification report with a clear rationale for the assigned class.
- The report must include a risk-based justification for De Novo submission if applicable.

#### 1.2 Risk-Based Justification
- **Implementing Agent:** RegulatoryPhD
- **Platform / Language / Runtime:** N/A (Regulatory Analysis)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/regulatoryphd/risk_assessment_2026-05-03.md`
- **Interface / Protocol:** N/A

**Requirement 1.2.1:**
Provide a detailed risk-based justification for De Novo submission, including a demonstration of novel low-to-moderate risk with no predicate.

**Acceptance Criteria:**
- A comprehensive risk assessment report that demonstrates the device's novelty and low-to-moderate risk.
- The report must include references to relevant standards (e.g., IEC 14971 FMEA).

#### 1.3 Submission Content Requirements
- **Implementing Agent:** RegulatoryPhD
- **Platform / Language / Runtime:** N/A (Regulatory Analysis)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/regulatoryphd/submission_content_2026-05-03.md`
- **Interface / Protocol:** N/A

**Requirement 1.3.1:**
Include specific submission content requirements according to 21 CFR 807.87 for 510(k) or 21 CFR 860.257 for De Novo submissions.

**Acceptance Criteria:**
- A detailed document outlining all required submission content.
- The document must include references to relevant regulations and standards.

#### 1.4 Special Controls
- **Implementing Agent:** RegulatoryPhD
- **Platform / Language / Runtime:** N/A (Regulatory Analysis)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/regulatoryphd/special_controls_2026-05-03.md`
- **Interface / Protocol:** N/A

**Requirement 1.4.1:**
Cite any Special Controls required and provide references to relevant standards (e.g., IEC 14971 FMEA).

**Acceptance Criteria:**
- A list of all special controls required for the device.
- References to relevant standards and guidelines.

#### 1.5 IEC 62304 Software Class
- **Implementing Agent:** RegulatoryPhD
- **Platform / Language / Runtime:** N/A (Regulatory Analysis)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/regulatoryphd/software_class_2026-05-03.md`
- **Interface / Protocol:** N/A

**Requirement 1.5.1:**
Assign the appropriate IEC 62304 software class with a clear linkage to hazard analysis.

**Acceptance Criteria:**
- A document outlining the assigned software class.
- The document must include a detailed hazard analysis and linkage to the software class.

### Section 2: UART Data Transmission Protocols

#### 2.1 Baud Rate and Framing
- **Implementing Agent:** SWPhD
- **Platform / Language / Runtime:** STM32H7 bare-metal C
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/uart_config_2026-05-03.c`
- **Interface / Protocol:** UART

**Requirement 2.1.1:**
Specify the baud rate, framing, error-handling methods, and data throughput requirements (e.g., ECG at 500 Hz × 12 leads × 16-bit = ~96 kbps minimum).

**Acceptance Criteria:**
- Baud rate set to 1 Mbps.
- Framing format: 8N1 (8 data bits, no parity, 1 stop bit).
- Error-handling method: Parity error detection and framing error detection.

#### 2.2 UART Frame Structure
- **Implementing Agent:** SWPhD
- **Platform / Language / Runtime:** STM32H7 bare-metal C
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/uart_frame_2026-05-03.c`
- **Interface / Protocol:** UART

**Requirement 2.2.1:**
Define the CRC polynomial (e.g., CRC-16/CCITT), frame structure byte layout, maximum retry count, timeout numeric values (ms), and DMA channel or IRQ priority assignment on the STM32H7.

**Acceptance Criteria:**
- CRC polynomial: CRC-16/CCITT.
- Frame structure: SOF marker (0x01), payload length field width (1 byte), payload data, CRC (2 bytes), EOF delimiter (0xFF).
- Maximum retry count: 3.
- Timeout numeric value: 50 ms.
- DMA channel assignment: DMA1 Stream 3.
- IRQ priority numeric value: NVIC priority 5.

### Section 3: OpenAPI Schema Path, Authentication Method, and Failure-Mode Behavior

#### 3.1 OpenAPI Schema Path
- **Implementing Agent:** SWPhD
- **Platform / Language / Runtime:** FastAPI (Python 3.11)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/openapi_schema_2026-05-03.json`
- **Interface / Protocol:** REST API

**Requirement 3.1.1:**
Specify the OpenAPI schema path.

**Acceptance Criteria:**
- The OpenAPI schema must be defined in JSON format.
- The schema must include all necessary endpoints and operations.

#### 3.2 Authentication Method
- **Implementing Agent:** SWPhD
- **Platform / Language / Runtime:** FastAPI (Python 3.11)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/auth_config_2026-05-03.py`
- **Interface / Protocol:** REST API

**Requirement 3.2.1:**
Specify the authentication method (e.g., TLS version floor per NIST SP 800-52r2, OAuth2 scope definitions).

**Acceptance Criteria:**
- Authentication method: OAuth2 with JWT using HS256 algorithm.
- Token expiry numeric value: 3600 seconds (1 hour).
- RBAC role definitions must be included.

#### 3.3 Failure-Mode Behavior
- **Implementing Agent:** SWPhD
- **Platform / Language / Runtime:** FastAPI (Python 3.11)
- **Output File or Artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/failure_mode_2026-05-03.py`
- **Interface / Protocol:** REST API

**Requirement 3.3.1:**
Specify the failure-mode behavior for authentication failures, rate limiting, and downstream API unavailability.

**Acceptance Criteria:**
- Authentication failure: Return HTTP 401 Unauthorized with error message.
- Rate limiting threshold: 100 requests per minute.
- Downstream API unavailability: Retry mechanism with exponential backoff up to 5 attempts.

### Handoff →
Owner: RegulatoryPhD, Task: Conduct and assign classification based on the completed risk assessment report, Target file: `/mnt/d/vDTC/OpenClaw/outputs/regulatoryphd/classification_report_2026-05-03.md`