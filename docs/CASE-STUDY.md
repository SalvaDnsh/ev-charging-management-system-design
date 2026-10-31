# CSMS project overview

## Problem and context

Operating an EV charging network involves connected assets, user requests and maintenance decisions. A station contains chargers, and each charger exposes one or more connectors. Operators need a consistent view of equipment condition, charging activity, energy use and faults across that hierarchy.

This undergraduate Management Information Systems project develops a Charging Station Management System (CSMS) through requirements analysis, UML modeling and interface design.

## Requirements analysis

The first phase examines the operating context, stakeholders and comparable systems. It describes five workflows:

1. Station and charger lifecycle management.
2. Charging-session management.
3. Monitoring, event detection and operational response.
4. Tariffs, billing and settlement.
5. Fault handling.

The requirements distinguish roles such as administrators, network operators, operations specialists, technicians, station owners, electricity distribution representatives and drivers. They cover the information each role needs, the actions it can perform and the events that connect operational processes.

## Analysis and modeling

Three workflows are modeled in detail: asset lifecycle, charging sessions and fault handling. Use case diagrams describe actors and system interactions; activity diagrams describe process decisions; class diagrams describe domain entities and relationships; sequence diagrams describe interactions over time.

The lifecycle model follows station, charger and connector registration, transfer requests and equipment maintenance. The session model follows readiness checks, start confirmation, monitoring, end causes, tariff association and reporting. The fault model follows detection, ticket creation, remote action, field work and technical decisions.

Administrative assignment, physical equipment condition and ticket/session outcomes are treated as distinct parts of operational records. A charging-session request progresses to charging after equipment confirmation. A completed maintenance record captures the resulting asset condition and the outcome of the ticket.

## User experience

The third phase connects personas to 17 user stories and acceptance criteria across the three detailed workflows. Desktop and mobile designs provide role-specific dashboards, asset forms, active-session views, transfer decisions, fault tickets, field assignments and reports.

The design system includes a shared palette, typography, navigation, form controls, status labels and dashboard components. Prototype entry screens route to seven roles. Persian interface labels support the project's operational setting.

## Portfolio contents

The repository includes Persian reports for all three phases, an English project overview, diagram images, editable model files, desktop/mobile prototype links and a story-to-frame mapping. The project demonstrates requirements analysis, domain modeling, workflow design, UX specification and collaborative project organization.

- [Phase 1 reports](fa/phase1/report.md)
- [Phase 2 reports](fa/phase2/report.md)
- [Phase 3 reports](fa/phase3/report.md)
- [UML gallery and model files](UML.md)
- [Interface prototypes](PROTOTYPE.md)
