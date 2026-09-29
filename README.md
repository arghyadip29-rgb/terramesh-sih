# TerraMesh — AI-Enabled Mine Subsidence Monitoring & Early Warning System

## 1. Project Title

**TerraMesh: Low-Cost Intelligent Surface Mesh for Real-Time Mine Subsidence Monitoring, Risk Assessment and Early Warning**

**Physical sensing unit:** TerraPeg
**SIH Problem Statement:** SIH26025

---

## 2. One-Line Solution Statement

**TerraMesh is a distributed network of low-cost TerraPeg sensing nodes that combines multi-sensor ground-movement verification, Edge AI, LoRa mesh communication, adaptive monitoring and node-health intelligence to provide continuous subsidence-risk assessment and early warning.**

---

## 3. Problem

Underground coal extraction can alter the stability and movement of overlying strata, eventually producing surface deformation and subsidence.

Conventional monitoring approaches may involve periodic surveys, expensive geotechnical instrumentation or wide-area satellite observations. These approaches provide valuable information, but a mine also needs **localized, continuous and operationally actionable monitoring** around vulnerable areas.

The challenge is therefore not simply to collect sensor data, but to determine:

* Is the observed change a genuine ground movement?
* Is it persistent or only a transient disturbance?
* Are nearby sensing points showing a similar pattern?
* Is the sensing node itself healthy?
* Should monitoring intensity increase?
* Does the observed pattern require an operational warning?

TerraMesh is designed around these questions.

---

# 4. Practical Gap

TerraMesh targets the combination of:

**Low-cost sensing + dense deployment + multi-sensor verification + Edge AI + resilient communication + adaptive monitoring + node-health awareness + GIS visualization.**

The goal is not to replace established techniques such as geotechnical surveys or InSAR, but to provide a **continuous local sensing and early-warning layer** that can complement them.

---

# 5. TerraMesh Solution

TerraMesh uses multiple **TerraPeg** nodes distributed over mine panels.

Each node collects ground-movement information and communicates through a **multi-hop LoRa mesh**.

The overall system is:

**TerraPeg**
→ **ESP32 Edge AI**
→ **LoRa Mesh**
→ **ESP32 Edge Gateway**
→ **Local Processing / Storage**
→ **Cloud / Database**
→ **Ground Movement Fingerprint**
→ **AI/ML Risk Assessment**
→ **GIS Dashboard / Alerts**

Two additional intelligent loops operate alongside this pipeline:

**Node Health**
→ **Node-Health Intelligence**
→ **Maintenance Priority Map**

and:

**Risk Assessment**
→ **Adaptive Monitoring**
→ **High-Risk TerraPeg**
→ **Higher Sampling / Transmission**

---

# 6. How TerraMesh Works

### Step 1 — Sense

TerraPeg collects:

* Tilt
* Displacement
* Vibration
* Optional crack/strain information
* Optional environmental information
* Optional position

### Step 2 — Verify

The system does not rely solely on one sensor threshold.

It considers:

**Tilt + Displacement + Vibration + Time + Neighbouring Nodes**

to determine whether an event deserves further attention.

### Step 3 — Fingerprint

The sensor streams are converted into a **Ground Movement Fingerprint** — a spatiotemporal signature describing how an event develops across sensors and neighbouring nodes.

### Step 4 — Assess

AI/ML analyses the event pattern for:

* anomaly detection
* event classification
* severity
* progression
* subsidence-risk assessment

### Step 5 — Adapt

If risk increases, the relevant TerraPegs increase their sampling/transmission frequency.

### Step 6 — Monitor Network Health

Battery, packet loss, sensor consistency and last-seen information are independently evaluated.

### Step 7 — Visualize & Alert

The operator receives:

* deformation maps
* risk zones
* trends
* event fingerprints
* node-health information
* maintenance priorities
* alerts

---

# 7. TerraPeg

**TerraPeg** is the low-cost distributed sensing unit of TerraMesh.

It is designed around:

* ESP32 microcontroller
* SX1278 LoRa
* MPU6050
* Hall-effect displacement sensing with mechanical tether
* vibration sensing / piezo
* optional crack/strain sensor
* optional environmental sensor
* optional GPS
* battery-powered enclosure

The physical design allows multiple sensing points to be distributed over a mine panel rather than concentrating monitoring at a single location.

---

# 8. Multi-Sensor Event Verification

A major design principle is:

> **Do not interpret an isolated sensor reading in isolation when additional evidence is available.**

For example:

**Vibration spike only**

* no displacement
* no sustained tilt
* isolated node

→ lower-confidence transient event.

Whereas:

**Increasing tilt**

* increasing displacement
* supporting vibration
* persistence over time
* neighbouring-node correlation

→ higher-confidence deformation pattern.

Vibration is therefore not simply treated as noise. It remains a potentially important ground-motion signal whose interpretation is strengthened by other measurements.

---

# 9. Ground Movement Fingerprint

The **Ground Movement Fingerprint** represents the combined signature of an event.

### Concept

**Multiple sensor streams + Time + Neighbouring Nodes**

↓

**Event Fingerprint**

↓

**Event Classification**

↓

**Risk Assessment**

It captures not just *what* a sensor measured, but **how multiple measurements change over time and space**.

This provides a richer input to the AI/risk layer than a single threshold-based alarm.

The fingerprint itself does not automatically prove subsidence; it provides structured evidence for event classification and risk assessment.

---

# 10. Edge AI / TinyML

TerraMesh places lightweight intelligence close to the sensors using:

* **ESP32**
* **TensorFlow Lite Micro**
* **Edge Impulse**
* **1D-CNN / TinyML**

Edge processing can support:

* local anomaly/event detection
* sensor-pattern analysis
* faster response
* reduced communication load
* local verification during intermittent connectivity

The final model performance would need to be established through experimental validation.

---

# 11. LoRa Mesh & Offline Operation

TerraPegs communicate using a multi-hop architecture:

**TerraPeg → TerraPeg → TerraPeg → ESP32 Gateway**

The network is designed for:

* low-power communication
* distributed coverage
* multi-hop connectivity
* local buffering
* offline operation
* synchronization when connectivity returns

The system does not depend entirely on continuous cloud connectivity.

The prototype architecture uses an **ESP32 Edge Gateway**, with no Raspberry Pi requirement.

---

# 12. Dynamic Monitoring Density

This feature turns TerraMesh from a fixed-rate monitoring system into a **risk-adaptive monitoring system**.

### Normal

**Low sampling / transmission**

### Risk Increasing

**Higher sampling / transmission**

### High Risk

**High-frequency monitoring**

Instead of making every TerraPeg continuously operate at maximum intensity, TerraMesh is designed to allocate more sensing and communication resources where the risk is changing.

This can potentially improve temporal resolution around emerging events while reducing unnecessary energy and communication overhead.

---

# 13. Node-Health Intelligence

TerraMesh monitors the health of the monitoring infrastructure itself.

Parameters include:

* Battery
* Packet loss
* Sensor consistency
* Last-seen time
* Communication quality

This creates a second information layer:

### Ground Risk

**What is happening to the ground?**

### Node Health

**Can I trust this TerraPeg's measurements?**

This distinction is important because:

**Ground Risk ≠ Node Failure**

A node showing abnormal data while simultaneously exhibiting poor battery or sensor health should be investigated differently from a healthy node showing persistent deformation.

---

# 14. Maintenance Priority Map

Node-Health Intelligence feeds a:

**Maintenance Priority Map**

It combines available information about:

* battery condition
* sensor consistency
* communication quality
* packet loss
* node availability

The dashboard can therefore help mine staff identify **which TerraPeg requires maintenance first**.

This is maintenance prioritization rather than an unsupported claim of predictive equipment failure.

---

# 15. AI Risk Assessment

The AI/risk layer considers:

* sensor observations
* temporal trends
* neighbouring-node relationships
* Ground Movement Fingerprints
* node-health context

Potential outputs include:

* event classification
* anomaly detection
* severity assessment
* progression analysis
* subsidence risk zones
* alerts

The system is designed to **support operational decision-making**, rather than claiming that AI can deterministically predict a mine collapse.

---

# 16. GIS Dashboard & Alerts

The TerraMesh dashboard provides a spatial and temporal view of the monitoring network.

It can display:

* real-time TerraPeg status
* deformation maps
* subsidence-risk zones
* historical trends
* Ground Movement Fingerprints
* node health
* Maintenance Priority Map
* alerts

This converts raw sensor measurements into information that mine operators, planners and regulators can interpret more easily.

---

# 17. Complete End-to-End Workflow

### Primary monitoring path

**TerraPeg Sensors**
↓
**ESP32 + TinyML**
↓
**LoRa Mesh**
↓
**ESP32 Edge Gateway**
↓
**Data Aggregation / Local Storage**
↓
**Ground Movement Fingerprint**
↓
**AI/ML Event Classification + Risk Assessment**
↓
**GIS / Risk / Progression**
↓
**Dashboard / Maps / Alerts**

### Node-health path

**Node Health**
↓
**Node-Health Intelligence**
↓
**Maintenance Priority Map**
↓
**Dashboard**

### Adaptive feedback path

**Risk Assessment**
↓
**Adaptive Monitoring Control**
↓
**LoRa Mesh**
↓
**High-Risk TerraPeg**
↓
**Higher Sampling / Transmission**

This creates a **closed-loop intelligent monitoring architecture**, rather than a simple sensor-to-cloud pipeline.

---

# 18. Technical Architecture

### Sensing Layer

TerraPeg + ESP32 + ground sensors

### Edge Intelligence Layer

TinyML + multi-sensor verification

### Communication Layer

SX1278 LoRa mesh + ESP32 gateway

### Edge Data Layer

Filtering + time synchronization + local buffering

### Intelligence Layer

Ground Movement Fingerprint + AI/ML + risk assessment

### Node Health Layer

Battery + packet loss + sensor consistency + last seen

### Application Layer

GIS + dashboard + risk zones + alerts + maintenance priorities

---

# 19. Technology Stack

### Hardware

**ESP32 · SX1278 LoRa · MPU6050 · SS49E Hall Sensor · Mechanical Tether · Piezo · 18650 Battery + TP4056**

### Edge AI / ML

**TensorFlow Lite Micro · Edge Impulse · 1D-CNN · TinyML**

### Network

**LoRa Mesh · ESP32 Edge Gateway · MQTT · Local Buffering / Offline Support**

### Backend

**Python · FastAPI · SQLite · PostgreSQL**

### Frontend / GIS

**React.js · Leaflet.js · GIS deformation maps · Risk visualization**

---

# 20. Innovation / Differentiation

TerraMesh does not claim that **AI, IoT or LoRa individually** are novel.

The differentiation is in their **integrated closed-loop interaction**:

1. Low-cost TerraPeg sensing
2. Multi-sensor event verification
3. Ground Movement Fingerprint
4. Edge AI / TinyML
5. LoRa mesh
6. Dynamic Monitoring Density
7. Node-Health Intelligence
8. Maintenance Priority Map
9. GIS risk visualization
10. Offline/local buffering
11. Risk-adaptive monitoring

The system therefore attempts to make the monitoring network aware of both **ground behavior and its own operational condition**.

---

# 21. Demo Scenario

### 01 — Normal State

Multiple TerraPegs report stable tilt, displacement and vibration.

### 02 — Isolated Disturbance

One TerraPeg detects a vibration spike.

There is no supporting tilt or displacement.

→ Lower-confidence transient event.

### 03 — Emerging Deformation

A TerraPeg begins showing increasing tilt and displacement.

Supporting vibration is also detected.

### 04 — Spatial Confirmation

Neighbouring TerraPegs begin showing correlated movement.

### 05 — Ground Movement Fingerprint

The system combines:

**Sensor streams + Time + Neighbouring Nodes**

to construct the event fingerprint.

### 06 — Risk Assessment

The AI/risk engine identifies a persistent deformation pattern and raises the risk state.

### 07 — Adaptive Monitoring

Monitoring intensity increases around the affected TerraPegs.

### 08 — Node Health Check

A separate TerraPeg produces abnormal data but also shows poor battery/communication health.

Node-Health Intelligence flags it for maintenance rather than automatically treating the reading as geological deformation.

### 09 — Operator View

The dashboard shows:

**Risk Zone + Event Fingerprint + Node Health + Maintenance Priority + Trend + Alert**

This demonstrates the complete closed loop.

---

# 22. Challenges & Mitigation

| Challenge                     | TerraMesh Approach                                              |
| ----------------------------- | --------------------------------------------------------------- |
| Sensor noise                  | Multi-sensor + temporal/spatial verification                    |
| Animal/mechanical disturbance | Event fingerprinting + cross-sensor verification                |
| Rain/topsoil effects          | Anchored sensing + consistency checks                           |
| Machinery vibration           | Interpret vibration alongside tilt/displacement and persistence |
| Connectivity loss             | LoRa mesh + local buffering                                     |
| Node failure                  | Node-Health Intelligence                                        |
| Battery limitations           | Dynamic Monitoring Density                                      |
| Sensor drift                  | Sensor-consistency monitoring + maintenance prioritization      |

These mechanisms are intended to **reduce** uncertainty and false interpretation; they do not eliminate these challenges completely.

---

# 23. Feasibility

TerraMesh is suitable for incremental prototyping by a small engineering team because it relies primarily on commercially available components and established software frameworks.

The prototype can demonstrate:

* multiple TerraPegs
* sensor acquisition
* ESP32 processing
* LoRa communication
* event detection
* Ground Movement Fingerprinting
* adaptive sampling
* node-health monitoring
* GIS visualization
* risk alerts

A prototype demonstration should not be presented as equivalent to a certified field-deployment safety system. Long-term field calibration, environmental testing and operational validation would remain necessary.

---

# 24. Impact

### Social

Supports earlier identification of abnormal ground movement and more informed mine-safety decisions.

### Economic

Low-cost distributed sensing, adaptive monitoring and maintenance prioritization can potentially reduce unnecessary monitoring and servicing effort.

### Technological

Combines:

**Edge AI + LoRa Mesh + Multi-Sensor Verification + GIS + Adaptive Monitoring + Node-Health Intelligence**

within one architecture.

### Operational

Transforms raw sensor readings into:

* event fingerprints
* risk zones
* trends
* alerts
* monitoring priorities
* maintenance priorities.

---

# 25. Scalability

The architecture is designed to scale from:

**a small prototype**

→ **mine panel**

→ **larger monitoring areas**

→ **multiple mine sites / coalfields**

Scaling can be achieved by increasing TerraPeg density while retaining the same basic sensing, mesh, gateway, analytics and dashboard architecture.

---

# 26. Future Scope

Potential extensions include:

* **Satellite/InSAR data fusion** for wider-area validation
* **Solar-powered TerraPeg deployments** for longer-duration operation
* larger field datasets for improved AI models
* mobile/offline field applications
* integration with mine planning and safety systems
* infrastructure exposure mapping
* advanced deformation forecasting
* spatial risk propagation
* multi-coalfield deployment.

These are future extensions rather than claims about the current prototype.

---

# 27. Why TerraMesh Matters

TerraMesh is designed not merely to **sense the ground**, but to make the monitoring system aware of:

**the ground**
+
**the event pattern**
+
**changing risk**
+
**its own health**
+
**where monitoring effort is most needed**

Its central intelligence loop is:

**GROUND → INTELLIGENCE → RISK → ADAPTIVE MONITORING → GROUND**

while the infrastructure-health loop is:

**NODE HEALTH → MAINTENANCE PRIORITY**

The resulting concept is a **low-cost, distributed and adaptive monitoring network** that converts heterogeneous ground measurements into interpretable event signatures, risk information and operational priorities.
