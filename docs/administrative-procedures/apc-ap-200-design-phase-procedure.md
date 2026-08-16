# Design Phase Procedure

**Procedure ID:** APC-AP-200 | **Internal reference:** APC-PHASE-002

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of the Design phase is to translate approved business requirements into a documented solution design that defines the business, technical, governance, architecture, data, reporting, security, and operational requirements necessary to support development activities.

The Design phase establishes a common blueprint for the solution and ensures alignment with APC governance requirements, enterprise architecture standards, and approved business objectives before development begins.

## 2. Scope

This procedure applies to all APC-governed initiatives requiring formal solution design, including:

- New reports and dashboards
- New semantic models
- New KPI implementations
- New data products
- Data integration initiatives
- Enterprise reporting initiatives
- Practitioner asset promotion requests
- Major enhancements requiring redesign

This procedure applies to activities involving:

- Business Stakeholders
- BI Analytics Team (BI)
- Data Engineering Team (DE)
- Analytics Leadership
- Practitioners, when applicable

## 3. Roles & Responsibilities

#### Business Stakeholder

Responsible for:

- Validating business requirements
- Defining business rules
- Defining KPI business logic
- Reviewing proposed solution designs
- Identifying business validation resources

#### BI Analytics Team (BI)

Responsible for:

- Designing reporting solutions
- Designing semantic models
- Defining KPI implementation requirements
- Identifying reporting dependencies
- Defining business-facing analytics requirements

#### Data Engineering Team (DE)

Responsible for:

- Designing data architecture
- Defining source system integration requirements
- Defining transformation requirements
- Defining data movement requirements
- Identifying medallion layer requirements

#### Analytics Leadership

Responsible for:

- Resolving escalated design concerns
- Providing strategic direction when required
- Supporting prioritization and resource decisions

#### Practitioner

Responsible for:

- Providing design input when practitioner-developed assets are involved
- Participating in design discussions when required

## 4. Definitions

#### Business Requirements Document (BRD)

A document defining business objectives, requirements, stakeholders, assumptions, constraints, and success criteria.

#### Technical Specification

A document defining the technical approach, architecture, integration requirements, data requirements, and implementation considerations.

#### Data Model

The structure used to organize data for reporting, analytics, and business consumption.

#### Semantic Model

A business-friendly representation of data designed to support reporting, KPI calculations, self-service analytics, and enterprise reporting.

#### KPI

A Key Performance Indicator used to measure business performance or operational effectiveness.

#### Solution Design

The documented business and technical blueprint used to guide development activities.

## 5. Procedure

### 5.1 Review Discovery / Define Outputs

The Design phase begins by reviewing approved outputs from the Discovery / Define phase.

The review should confirm:

- Approved scope
- Business objectives
- Stakeholders
- Requirements
- Prioritization
- Governance considerations
- Open decisions impacting solution design

### 5.2 Develop Business Requirements

Business requirements shall be refined and documented to provide sufficient detail for solution design.

Requirements should address:

- Business objectives
- Expected outcomes
- Business processes
- Reporting requirements
- KPI requirements
- Validation requirements
- Success criteria

### 5.3 Develop Technical Design

A technical approach shall be documented that defines the proposed solution architecture.

The design should identify:

- Source systems
- Data requirements
- Integration requirements
- Data storage requirements
- Security considerations
- Operational considerations

### 5.4 Define Data Architecture

The proposed data architecture shall be documented.

Considerations may include:

- Data sources
- Data movement
- Transformation requirements
- Medallion layer placement
- Data ownership
- Data quality considerations
- Data retention requirements

### 5.5 Define Reporting & Semantic Model Requirements

Reporting and analytics requirements shall be documented.

Considerations may include:

- Semantic model requirements
- KPI requirements
- Dashboard requirements
- Reporting requirements
- Self-service analytics requirements
- Performance considerations

### 5.6 Review Standards Alignment

The proposed solution shall be evaluated against applicable APC standards.

Areas for consideration may include:

- Naming standards
- Data modeling standards
- Architecture standards
- Documentation standards
- Security standards
- Certification requirements

Any required exceptions should be documented and tracked.

### 5.7 Approve for Development

The Design phase concludes when sufficient information exists to support development activities.

The solution should have:

- Approved business requirements
- Approved technical approach
- Defined architecture
- Defined data requirements
- Defined reporting requirements
- Identified standards impacts
- Identified open decisions

Approved initiatives shall transition to the Develop phase.

## 6. Inputs

The following inputs may initiate the Design phase:

- Approved Discovery / Define Outputs
- Business Requirements
- Project Charter
- Prioritization Decision
- Governance Assessment
- Open APC Decisions
- Architecture Considerations

## 7. Outputs

The Design phase may produce:

- Business Requirements Document (BRD)
- Technical Specification
- Solution Architecture
- Data Architecture
- Data Model Design
- Semantic Model Design
- Security Requirements
- Development Requirements
- Architecture Decision Log Entries
- Development Authorization

## 8. Related Procedures

| **Procedure ID** | **Procedure Name** |
| --- | --- |
| APC-SOP-201 | Business Requirements Development Procedure |
| APC-SOP-202 | Technical Specification Procedure |
| APC-SOP-203 | Architecture Design Procedure |
| APC-SOP-204 | Data Modeling Procedure |
| APC-SOP-205 | Semantic Model Design Procedure |

## 9. Related Standards

| **Standard ID** | **Standard Name** |
| --- | --- |
| APC-STD-001 | Naming Standards |
| APC-STD-002 | Documentation Standards |
| APC-STD-003 | KPI Governance Standard |
| APC-STD-004 | Data Modeling Standard |
| APC-STD-005 | Medallion Architecture Standard |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-007 | Report Certification Standards |
| APC-STD-008 | Security & Access Standard |

## 10. Related Templates

| **Template ID** | **Template Name** |
| --- | --- |
| APC-TMP-103 | Project Charter |
| APC-TMP-201 | Business Requirements Document (BRD) |
| APC-TMP-202 | Technical Specification |
| APC-TMP-203 | Architecture Design Template |

## 11. Related Checklists

| **Checklist ID** | **Checklist Name** |
| --- | --- |
| APC-CHK-201 | Design Readiness Checklist |
| APC-CHK-202 | Requirements Validation Checklist |
| APC-CHK-203 | Architecture Validation Checklist |
| APC-CHK-204 | Design Phase Exit Checklist |

## 12. Open APC Decisions

The following unresolved APC decisions may impact execution of this phase.

#### APC-OD-002: Enterprise Naming Standards

Naming standards for:

- Workspaces
- Lakehouses
- Warehouses
- Tables
- Columns
- Semantic Models
- Reports
- DAX Measures

remain under development.

#### APC-OD-003: Documentation & Metadata Strategy

The governance approach for:

- KPI Definitions
- Business Glossary
- Report Documentation
- Semantic Model Documentation
- Lineage Documentation

remains under review.

#### APC-OD-004: Fabric Architecture Standards

Standards governing:

- Lakehouse vs Warehouse
- Shortcut vs Data Replication
- Direct Lake vs Import vs DirectQuery
- Workspace Architecture

remain under review.

#### APC-OD-005: Data Modeling Standards

The APC has discussed establishing a preferred modeling approach, including use of star schemas, but final standards have not yet been approved.

## Revisions

| **Issue Date** | **Rev** | **Change** | **Written / Revised by** |
| --- | --- | --- | --- |
|  | 0 | Initial Release |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes.  Then highlight all new document changes in yellow for quick reference.  An original issue document will have no highlights.
