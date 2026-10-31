# Phase 1 — Requirements and operational analysis

**Charging Station Management System (CSMS)**  
Management Information Systems · Collaborative undergraduate analysis and design project

[Report index](README.md) · [Next: system modeling](phase-2-system-modeling.md)

## Abstract

This phase defines the operating context and requirements for a system that manages an electric vehicle charging network. The proposed CSMS connects asset records, charging activity, equipment events, maintenance decisions and financial information. The analysis identifies the users of that information, describes five core workflows and establishes functional, quality, data, security and infrastructure requirements. The operational setting gives particular attention to equipment from multiple manufacturers, interrupted communications, local payment arrangements and the information needs of station owners and electricity distribution representatives. The deliverable is a requirements and design specification for the subsequent UML and interface phases.

## 1. Problem definition and system boundary

The project asks how a charging-network operator can manage geographically distributed equipment through a consistent information system. A network contains physical assets, people, operating rules and financial relationships. Its central management view must bring those elements together so that a status change, charging request or maintenance action can be traced to the relevant station and equipment.

The main questions are:

- What equipment and operational records must the system identify?
- Which stakeholders need to view or change those records?
- How should the system coordinate routine operation and exceptional events?
- What information supports maintenance, service-quality assessment and settlement?

The core focus is the operator's management environment. Driver interactions and external services are included where they initiate a session, receive information or exchange operational and financial records. The project develops requirements, models and prototypes across three course phases.

### 1.1. Equipment hierarchy and terminology

| Concept | Meaning in this project | Main information |
| --- | --- | --- |
| Station | A physical charging site | Identity, location, owner, opening hours, electrical capacity and operational status |
| Charger | A charging device assigned to a station | Internal ID, serial number, model, manufacturer, firmware, protocol version and power rating |
| Connector | A vehicle connection point belonging to a charger | Internal ID, type, power rating and current condition |
| Charging session | One vehicle's charging transaction on a connector | Request, confirmed start/end, measurements, events, applied tariff and amount |
| Measurement | A timestamped observation from equipment | Quantity, value, unit, source and measurement context |
| Operational event | A recorded change or exception | Equipment/session reference, type, timestamp, severity and outcome |

The hierarchy is **station → charger → connector**. Connector-level information matters because two connectors on the same charger may have different conditions. Equipment identity persists through maintenance so that session, fault and replacement histories remain traceable.

### 1.2. Operational situations motivating the design

The case considers several situations that management information must make visible: reduced charging power, connector wear, payment or display faults, interrupted communications, repeated errors and disagreement between a reported status and the condition experienced at the site. A communications interruption is recorded separately from a confirmed physical fault. The interface should show the last valid equipment response and the information supporting the displayed condition.

At management level, the design addresses fragmented equipment records, incomplete maintenance histories and the need to relate technical activity to financial reports. A common asset hierarchy and linked event records support investigation across those areas.

## 2. Stakeholders and access boundaries

The business roles can belong to separate organizations even when one organization performs several of them.

| Stakeholder or role | Responsibility and information need |
| --- | --- |
| Charging point operator / charging-network operator (CPO) | Operates the charging network, reviews operational decisions and monitors network performance |
| System administrator | Maintains asset information, registration, system configuration, tariffs and analytical views |
| Operations specialist | Monitors equipment, investigates alerts, coordinates maintenance and follows investigation outcomes |
| Station or site owner | Reviews the status, use and financial performance of owned stations |
| Field technician / maintenance contractor | Receives assigned work, examines equipment and records actions, parts and technical findings |
| Electricity distribution representative | Reviews station-capacity information and receives relevant capacity notifications within an authorized area |
| EV driver | Selects suitable equipment, requests charging, monitors progress and receives session information |
| Electric mobility service provider (eMSP) | Represents a driver-service relationship and exchanges relevant customer/session or settlement information |
| Supervisory or regulatory body | Uses authorized aggregate infrastructure and service reports |
| Payment and notification services | Exchange payment outcomes and deliver messages to the appropriate users |

The seven interface roles developed in phase 3 are the administrator, CPO, operations specialist, technician, owner, electricity distribution representative and driver. External services and supervisory actors remain part of the broader system context.

Access follows responsibility and data scope. An owner sees the owner's stations; a technician sees assigned work; a driver sees personal charging information; a utility representative sees relevant capacity records. Administrative, operational and decision-making permissions are described separately in the detailed workflows.

## 3. Comparable-system study

The coursework examined ChargeLab, Virta, Driivz and ChargePoint as reference systems for organizing requirements. The study considered operational dashboards, asset management, energy management, pricing, maintenance, financial records and external integration. It served as a design comparison for the academic case.

| Reference system | Themes examined in the coursework | Design lessons used in this project |
| --- | --- | --- |
| ChargeLab | Central management of connected chargers, equipment status, power and pricing | Common asset records and an operator dashboard across equipment brands |
| Virta | Modular charging-business functions, energy, finance and external interfaces | Separable functional modules and integration boundaries |
| Driivz | Network operations, troubleshooting, charging records and settlement | Linked fault tickets, remote-action history and financial traceability |
| ChargePoint | Access policies, pricing, reports, support and driver interactions | Role-specific views, site policies and coordinated operational support |

The local design priorities are payment in Iranian rials, financial reporting suited to local workflows, Persian-calendar presentation, capacity coordination with the electricity distributor, support for mixed equipment and clear behavior during interrupted connectivity. These priorities guide the proposed system's requirements rather than asserting a measured advantage over the reference products.

The broader feature study also considered waiting lists, fleet-specific policies, roaming and advanced energy services. The detailed course models concentrate on asset lifecycle, charging sessions and fault handling.

## 4. Vision, goals and feature priorities

The intended system provides a shared operational record for the charging network. Its goals are to support timely fault response, maintain a usable history of each asset, present charging information clearly and make station-level technical and financial performance understandable to the responsible roles.

Operational goals include improving charging-service reliability, reducing the time between detection and action, tracking equipment downtime, retaining records across communications interruptions and considering station power limits when planning charging capacity. Management goals include transparent revenue reports, analysis of equipment use and maintenance history, and information to support network-development decisions.

The proposed feature groups are:

1. Asset registration, commissioning, configuration, transfer, maintenance and retirement.
2. Equipment and connector status monitoring, including communications condition and last valid response.
3. Charging-session initiation, monitoring, confirmed termination and record keeping.
4. Event detection, prioritization, remote action and field referral.
5. Tariff management, session-cost calculation, billing and stakeholder settlement.
6. Role-based permissions, reports and dashboard views.
7. Communications resilience, external interfaces and a modular basis for future expansion.

Predictive maintenance, advanced roaming, fleet integration and vehicle-to-grid functions are longer-term directions considered in the initial vision. The main analysis and interface deliverables specify the selected operational workflows.

## 5. Core workflows

### 5.1. Station and charger lifecycle

**Trigger:** a station or item of equipment is added, changed, moved, maintained or withdrawn.

The administrator registers a station with its name, owner, address, coordinates, opening hours, electrical capacity, communications information and initial status. Chargers are then associated with that station, and connectors with their charger. Required fields and identifier uniqueness are validated at each stage.

Commissioning confirms that the records are complete, the equipment belongs to the intended site, communications are established and the operational condition permits service. A registration record alone does not establish readiness to charge.

During operation, the system records changes in condition, connection responses, maintenance and configuration. A transfer request identifies the charger, source, proposed destination and reason. The operator reviews the request and destination capacity. Approval records an administrative assignment and planned destination, then leads to field execution and commissioning. The transfer is complete after the field work, communications and equipment readiness are confirmed.

Retirement removes the station and dependent equipment from available service while retaining history. Reports support asset counts, current status, maintenance records and changes over time.

**Outputs:** asset records, status history, transfer decisions, field assignments and retirement records.

### 5.2. Charging-session management

**Trigger:** an authorized driver or operator requests charging on a selected connector.

The user selects station, charger and connector. The system verifies that the station is active, the charger is usable and the connector is ready. It records an initialized session and sends the start command. Equipment acknowledgement confirms the transition to charging and marks the connector in use.

During charging, received measurements support the display of delivered energy, elapsed time, instantaneous power and estimated cost. Session events and operational events are linked to the same equipment and session identifiers. A pause, interruption, fault or communications loss changes the information presented and may initiate an investigation.

On a stop request, the system sends a stop command. A confirmed end requires acknowledgement or reliable end data. The final record contains the start and end times, valid final measurements, end cause, tariff reference and amount. Equipment readiness is determined from its confirmed condition following the session.

**Outputs:** session history, event history, final charging record, receipt/payment information and investigation requests where applicable.

### 5.3. Monitoring, event detection and operational response

**Trigger:** a periodic response check, a received equipment message, a measurement threshold or a reported anomaly.

The monitoring function receives communications responses, equipment-status messages and measurements. It records timestamps, evaluates configured rules and distinguishes loss of communication from a confirmed equipment fault. The dashboard presents network counts, recent events, affected equipment and the last valid response.

Events are classified by type and severity. An authorized user can inspect the asset and session history, issue an appropriate remote action and review the result. A case requiring further work becomes a traceable ticket or field assignment in the fault-handling workflow.

The monitoring workflow covers initial observation and response; fault handling carries a case through investigation, field work and a documented outcome. Their shared identifiers preserve continuity between detection and resolution.

**Outputs:** events, alerts, status updates, remote-action records and referrals.

### 5.4. Tariffs, billing and settlement

**Trigger:** a tariff is defined or a charging session produces billable activity.

The initial requirements consider energy-based prices, time-based prices, fixed session charges and idle-time charges. Applicability may depend on site, equipment, user group, time period or contract. Tariffs have identities and validity periods so that the applicable rule can be traced.

The detailed session design associates each session with the tariff valid at its start. The model supports energy and time rates; the prototype tariff form focuses on an energy rate in Iranian rials per kilowatt-hour. Estimated cost during charging is based on received data. A final amount is recorded after the session end and relevant measurements are confirmed.

The charging record connects the equipment, session, energy, duration, tariff, amount, currency and payment status. Periodic statements can aggregate driver activity and station-owner revenue. Settlement requirements include reconciling charging records with payment records, applying stakeholder shares and retaining references for follow-up.

**Outputs:** tariff records, charging detail records, receipts, payment outcomes and stakeholder reports.

### 5.5. Fault handling

**Trigger:** an automatic alert, a manual report, a driver complaint or a field observation requires structured investigation.

The system records the affected asset, source, fault type, occurrence time, severity and description. The operations specialist checks completeness, requests missing details where needed and assigns the case a priority. Equipment and related session histories support diagnosis.

An authorized remote action may resolve the issue. Its request, result and subsequent equipment condition are recorded. If physical work is required, the case is assigned to a technician with the location, equipment details, fault description, priority and relevant history.

The technician records progress, actions, parts and findings. Outcomes can include repair, a need for parts, replacement, further investigation or an issue not reproduced. Replacement and other management decisions are retained with the ticket. Returning equipment to service requires confirmation of its condition; a report submission or ticket closure has its own separate meaning.

The initial priority scheme distinguishes critical safety issues, high-priority service interruption, medium-priority degradation and low-priority issues for planned inspection. Response periods are proposed operating targets for the case and would be set through service policy.

**Outputs:** tickets, remote-action records, field maintenance reports, decisions, equipment-condition updates and fault history.

## 6. Functional requirements

| ID | Required capability | Main workflow connection |
| --- | --- | --- |
| FR-01 | Create, validate and maintain station, charger and connector records | Lifecycle |
| FR-02 | Preserve equipment status, configuration, transfer and maintenance history | Lifecycle and fault handling |
| FR-03 | Initiate, monitor and confirm the end of charging sessions | Sessions |
| FR-04 | Receive and link measurements, status messages and operational events | Sessions and monitoring |
| FR-05 | Detect conditions requiring attention and create trackable alerts or tickets | Monitoring and fault handling |
| FR-06 | Record remote commands, results and field-work referrals | Fault handling |
| FR-07 | Define tariffs, associate the applicable tariff with a session and record amounts | Tariffs and sessions |
| FR-08 | Provide financial and operational reports within each role's data scope | All workflows |
| FR-09 | Recover locally retained equipment/session data after communications return | Communications resilience |
| FR-10 | Authenticate users and equipment and enforce role-based permissions | All workflows |
| FR-11 | Notify users and external stakeholders about relevant decisions and events | Lifecycle, sessions and fault handling |
| FR-12 | Support equipment integration through an explicit communications interface | Equipment connectivity |

These report identifiers organize the English specification. The [traceability table](../../traceability.csv) connects the selected workflows to detailed user stories and prototype frames.

## 7. Quality requirements

The proposed system requires responsive operational views, continuous service, recoverable records, controlled access and maintainable components. Quality requirements address performance, availability, security, usability, interoperability, observability and testability.

Specific course design targets include a maximum three-second confirmation for valid asset registration, a maximum three-second display of a recorded connection-status change, an owner dashboard load below three seconds and a capacity notification within one minute of the relevant event. The registration correction flow uses a five-minute editing window. These are **design acceptance targets**, not measured performance results.

Infrastructure planning also considers daily database backups retained for at least 30 days, a documented recovery procedure and network sizing based on message traffic and equipment count. The initial planning discussion considers response times below four seconds, an ideal below two seconds and a 97% availability planning figure; these describe early software-planning assumptions rather than equipment-uptime guarantees or a compliance claim. The story-specific targets in phase 3 identify the interaction being evaluated.

Interfaces should make required fields, validation messages, status, pending decisions and record history easy to understand. Sensitive changes and access to financial information require an auditable record. Modular design should support changes in communications adapters and functional modules without obscuring the shared domain definitions.

## 8. Data requirements

| Data group | Required content | Use |
| --- | --- | --- |
| Asset master data | IDs, serial/model/manufacturer, station location, owner/operator, power rating, connector details and meter reference | Registration, capacity planning and maintenance preparation |
| Measurements | Source, measurement time, quantity, numeric value, unit and context | Session monitoring, energy accounting and investigation |
| Session records | Session/equipment/user references, start/end confirmation, energy, duration, end cause, tariff and amount | History, receipts, analysis and settlement |
| Events and faults | Type/code, occurrence time, severity, asset/session references, status and source | Alerting, diagnosis and service-quality analysis |
| Maintenance and decisions | Assignee, actions, parts, times, findings, approval and outcome | Follow-up, replacement decisions and lifecycle history |
| Financial records | Tariff validity, applied rates, currency, amount, payment reference and stakeholder allocation | Billing and reconciliation |

Measurements retain units: energy in kilowatt-hours (kWh), power in kilowatts (kW), current in amperes (A), voltage in volts (V), and elapsed session time in minutes where displayed. Measurement time and message-receipt time serve different purposes, especially after an interruption.

Relational storage is proposed for structured transactional records, and time-series storage for high-volume equipment measurements. The asset and session identifiers connect the two forms of information.

## 9. Communications, security and infrastructure planning

### Equipment and external interfaces

The course design selects an OCPP 1.6-oriented integration baseline for its assumed equipment environment and considers an adapter boundary for additional protocol versions. Open Charge Point Protocol (OCPP) is the charger-to-management communication interface in the project. Protocol fields should be mapped into the project's station–charger–connector domain model explicitly.

The technical study considers secure WebSocket communications, web APIs for driver/payment integrations and lightweight messaging for equipment-scale event exchange. These are proposed integration choices. Hardware support and version-specific behavior belong in the implementation specification.

### Interrupted communications and power

The proposed resilience approach retains timestamped measurements locally at equipment and forwards them after reconnection. Reconnection attempts use a backoff strategy. The management view shows the last valid response while a device is unreachable; returning communications and a verified operational condition establish service readiness.

For electricity interruptions or capacity restrictions, the requirements consider an external schedule/notification interface and planned power adjustments. Station capacity and charger ratings provide the information needed to coordinate those actions.

### Security and access

Communications protection, registered-equipment identity and authorized-user authentication are required. A driver credential must be checked before an authorized session begins. Permissions restrict operational actions, financial views and assigned maintenance work to the relevant roles and equipment scope.

Security records include authentication activity, sensitive configuration changes and access to protected financial information. Driver identity and charging history require privacy controls. Software updates, backup handling and recovery procedures form part of the operational security plan.

### Scaling and maintainability

The technical proposal separates equipment communications, asset records, sessions, faults, billing and reporting into modules. The initial study considers independently deployable services for growth from thousands toward larger networks. The course deliverables specify the domain and interactions that such an implementation would need to preserve.

## 10. Handoff to the next phases

Phase 1 establishes the equipment hierarchy, role boundaries and five-workflow context. Phase 2 develops use case, activity, class and sequence models for lifecycle, sessions and faults. Phase 3 turns those three workflows into personas, user stories, acceptance criteria and interfaces for seven roles.

The connection between the phases is traceable: requirements identify what information and decisions are needed; models describe entities and interactions; UX specifications describe how users carry out and recognize those actions.

## Sources and supporting material

This English report brings together the phase 1 problem analysis, comparable-system study, stakeholder analysis, workflows, requirements and technical-planning sections. The [Persian phase 1 collection](../fa/phase1/report.md) contains the original detailed references and supplementary discussion.

Background references used in the coursework include Open Charge Alliance's OCPP specifications, EVRoaming Foundation's OCPI specification, ISO/IEC 25010:2011 for software-quality terminology, ISO 55000:2014 for asset-management terminology, and the role-based access-control literature. The comparable-system study used material from ChargeLab, Virta, Driivz and ChargePoint. These references provide background to the academic design; the requirements above describe the project's proposed behavior.

[Next: Phase 2 — System analysis and UML modeling](phase-2-system-modeling.md)
