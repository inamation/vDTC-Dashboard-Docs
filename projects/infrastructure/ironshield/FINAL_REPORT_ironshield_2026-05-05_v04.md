# IronShield NRC Licensing Workflow Finalization — v04 Detailed Specification
_Generated: 2026-05-05 08:00 | Owner: CompliancePhD | Project: IronShield | Priority: High_

# IronShield NRC Licensing Workflow Finalization — v04 Detailed Specification

## Section 1: Endpoint `/license_request` Validation Logic

### Requirement 1: Schema Validation Against NRC ADAMS Protocols
- **Implementing agent or role:** CompliancePhD implements in Python 3.11 using FastAPI
- **Platform / language / runtime:** Python 3.11, FastAPI framework on Ubuntu 22.04
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/compliancephd/license_request_validator.py`
- **Interface / protocol:** JSON over HTTP POST to `/license_request` endpoint

**Validation Logic:**
```python
from pydantic import BaseModel, Field, ValidationError

class LicenseRequest(BaseModel):
    site_class: str = Field(..., description="Site Class definition from NRC ADAMS")
    ss_s1_acceleration: float = Field(..., description="Ss/S1 acceleration values in g")
    component_category: str = Field(..., description="Mapped IronShield component categories")
    distance_qd_feet: int = Field(..., description="Q-D distance in feet")
    hazard_division: str = Field(..., description="Hazard division classification")
    quantity_distance_table: dict = Field(..., description="Quantity-distance table for components")

def validate_license_request(data):
    try:
        LicenseRequest(**data)
        return True
    except ValidationError as e:
        print(f"Validation error: {e}")
        return False

# Example usage
if __name__ == "__main__":
    sample_data = {
        "site_class": "Class 1",
        "ss_s1_acceleration": 0.5,
        "component_category": "Shielding",
        "distance_qd_feet": 200,
        "hazard_division": "High",
        "quantity_distance_table": {"ComponentA": 10, "ComponentB": 20}
    }
    print(validate_license_request(sample_data))
```

## Section 2: Implementing Agent Assignments and Interface Protocols

### Requirement 2: Downstream Steps Implementation
- **Implementing agent or role:** SWPhD implements in Python 3.11 using FastAPI
- **Platform / language / runtime:** Python 3.11, FastAPI framework on Ubuntu 22.04
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/swphd/process_license_request.py`
- **Interface / protocol:** RabbitMQ message broker at `amqp://localhost:5672`

**Agent Handoff Logic:**
```python
import pika

def process_license_request(data):
    # Process the license request data
    processed_data = {
        "status": "processed",
        "data": data
    }
    
    # Send processed data to RabbitMQ queue
    connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
    channel = connection.channel()
    channel.queue_declare(queue='license_processed')
    channel.basic_publish(exchange='',
                          routing_key='license_processed',
                          body=str(processed_data))
    connection.close()

# Example usage
if __name__ == "__main__":
    sample_data = {
        "site_class": "Class 1",
        "ss_s1_acceleration": 0.5,
        "component_category": "Shielding",
        "distance_qd_feet": 200,
        "hazard_division": "High",
        "quantity_distance_table": {"ComponentA": 10, "ComponentB": 20}
    }
    process_license_request(sample_data)
```

## Section 3: Cross-Domain Compliance Matrix

### Requirement 3: Numeric Thresholds and Decision Logic Specificity
- **Implementing agent or role:** CompliancePhD implements in Python 3.11 using FastAPI
- **Platform / language / runtime:** Python 3.11, FastAPI framework on Ubuntu 22.04
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/compliancephd/cross_domain_compliance_matrix.py`
- **Interface / protocol:** JSON over HTTP GET to `/compliance_matrix` endpoint

**Compliance Matrix:**
```python
from pydantic import BaseModel, Field

class ComplianceMatrix(BaseModel):
    site_class: str = Field(..., description="Site Class definition from NRC ADAMS")
    ss_s1_acceleration_threshold: float = Field(..., description="Threshold for Ss/S1 acceleration values in g")
    component_category: str = Field(..., description="Mapped IronShield component categories")
    distance_qd_feet_threshold: int = Field(..., description="Threshold for Q-D distance in feet")
    hazard_division: str = Field(..., description="Hazard division classification")

def check_compliance(data):
    compliance_matrix = ComplianceMatrix(
        site_class="Class 1",
        ss_s1_acceleration_threshold=0.5,
        component_category="Shielding",
        distance_qd_feet_threshold=200,
        hazard_division="High"
    )
    
    if (data['site_class'] == compliance_matrix.site_class and
        data['ss_s1_acceleration'] <= compliance_matrix.ss_s1_acceleration_threshold and
        data['component_category'] == compliance_matrix.component_category and
        data['distance_qd_feet'] <= compliance_matrix.distance_qd_feet_threshold and
        data['hazard_division'] == compliance_matrix.hazard_division):
        return True
    else:
        return False

# Example usage
if __name__ == "__main__":
    sample_data = {
        "site_class": "Class 1",
        "ss_s1_acceleration": 0.5,
        "component_category": "Shielding",
        "distance_qd_feet": 200,
        "hazard_division": "High"
    }
    print(check_compliance(sample_data))
```

## Section 4: Validation or Test Plan Document

### Requirement 4: Acceptance Criteria for `/license_request` Endpoint
- **Implementing agent or role:** CompliancePhD implements in Python 3.11 using FastAPI
- **Platform / language / runtime:** Python 3.11, FastAPI framework on Ubuntu 22.04
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/compliancephd/test_plan.md`
- **Interface / protocol:** JSON over HTTP POST to `/license_request` endpoint

**Test Plan:**
```markdown
# Test Plan for IronShield NRC Licensing Workflow

## Section 1: Acceptance Criteria

### Requirement 1: Schema Validation Against NRC ADAMS Protocols
- **Acceptance Criterion:** The `/license_request` endpoint must validate incoming data against the defined schema.
- **Test Method:** Use `pytest` to simulate valid and invalid requests, checking for successful validation or appropriate error messages.

### Requirement 2: Downstream Steps Implementation
- **Acceptance Criterion:** The processed license request data must be correctly sent to the RabbitMQ queue.
- **Test Method:** Monitor the RabbitMQ queue using a consumer script that checks for the presence of processed data.

### Requirement 3: Numeric Thresholds and Decision Logic Specificity
- **Acceptance Criterion:** The compliance matrix must accurately determine compliance based on predefined thresholds.
- **Test Method:** Use unit tests to verify that different input scenarios result in correct compliance outcomes.

## Section 2: Error Logging Destination

- **Implementing agent or role:** CompliancePhD implements in Python 3.11 using FastAPI
- **Platform / language / runtime:** Python 3.11, FastAPI framework on Ubuntu 22.04
- **Output file or artifact:** `/mnt/d/vDTC/OpenClaw/outputs/compliancephd/error_log.txt`
- **Interface / protocol:** File-based logging

**Error Logging:**
```python
import logging

logging.basicConfig(filename='/mnt/d/vDTC/OpenClaw/outputs/compliancephd/error_log.txt', level=logging.ERROR)

def log_error(message):
    logging.error(message)
```

## Handoff →
Owner: SWPhD, Task: Implement RabbitMQ consumer to process license data, Target file: `/mnt/d/vDTC/OpenClaw/outputs/swphd/rabbitmq_consumer.py`