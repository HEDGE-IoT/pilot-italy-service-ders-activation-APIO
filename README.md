# SUC-IT-01 – DERs Activation Service

## General Information and Purpose

**Service Name/Title**: DERs Activation Service  
**Description and Purpose**: Dispatches activation commands to Distributed Energy Resources (DERs) through the appropriate channel.  
**Owner/Contact Information**: Mattia Alfieri (Apio) <m.alfieri@apio.cc>  

---

## Functional Requirements

1. **Setpoint Dispatch**: Dispatch setpoints through the correct medium (protocol/external system) in the correct time window.  
2. **User Authentication and Authorization**: Protect resources and functionalities with proper authorization and authentication.  
3. **Audit Logging**: Track configuration modifications.  

---

## Non-Functional Requirements

- **Performance**:  
  - Setpoint forwarding must be quick enough to allow DERs to apply the required setpoint in time.  
- **Reliability and Availability**:  
  - High availability targeted at 99%, with failover mechanisms.  
- **Security**:  
  - **Authentication**: Token-based authentication for both interactive and non-interactive methods.  
  - **Authorization**: The service primarily operates as a scheduled service, with manual intervention allowed for authorized users (e.g., the DSO).  
  - **Encryption**: Data at rest and in motion must be encrypted.  
- **Privacy**: Compliant with data privacy regulations.  

---

## Service Interfaces

Resources follow a REST paradigm. Main endpoints include (a full OpenAPI spec is available with parameters, payloads, and responses):  

| Method | Path                                                               | Description                                        |
|--------|--------------------------------------------------------------------|----------------------------------------------------|
| POST   | `/projects/{projectId}/flexibilityRequests/{uuid}/dispatch`        | Programmatically dispatches a flexibility request  |

---

## Data Model

- Reuses definitions from the **Optimal Setpoint Computation Service**.  

---

## Integration and Dependencies

- **System dependencies**:  
  - **IoT Platform**: Relies on the downlink channel for sending activation commands via MQTT.  
  - **Optimal Setpoint Computation Service**: Provides setpoints to forward to field devices.  
  - **Databases, libraries, frameworks, and other internal tools**.  

- **External dependencies**: TBD  
- **Third-party integrations**: TBD  
- **HEDGE-IoT integration**: Interfaces with edge devices and cloud services.  
- **Integration with the App Store**: API-related integration constraints.  
- **Integration with the Data Space**: TBD  

---

## Security and Privacy

- **Data Sensitivity**: TBD  
- **Access Control**: API and frontend usage requires authentication. Roles and permissions restrict available features.  
- **Audit Logs**: All user actions that modify the system trigger audit log collection.  

---

## Performance Considerations

- **Stress Testing**: Periodically performed.  
- **Response Times**: Continuously monitored (see Deployment section).  

---

## Deployment and Environment

- **Configuration**: Environment-specific settings.  
- **CI/CD**: Continuous Integration and Continuous Deployment pipeline includes:  
  - **Test Stage**:  
    - Audit: Check for known vulnerabilities at application and container level.  
    - Lint: Identify linting errors.  
    - Test: Run automated test suite.  
  - **Build Stage**:  
    - Build container image.  
    - Publish container image to registry.  
- **Monitoring and Logging**:  
  - Prometheus metrics for system vitals (resource consumption, application-specific metrics).  
  - JSON logging.  
  - OpenTelemetry-compatible traces.  

---

## Testing and Validation

- All commits are checked against the automated test suite.  

