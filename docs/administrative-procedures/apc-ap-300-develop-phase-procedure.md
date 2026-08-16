# Develop Phase Procedure

**Procedure ID:** APC-AP-300 | **Internal reference:** APC-PHASE-003

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of the Develop phase is to build, configure, document, and test approved analytics solutions in accordance with APC requirements, approved designs, enterprise standards, and governance expectations.

During this phase, Data Engineering and BI Analytics develop the approved solution, prepare supporting documentation, perform validation activities, and prepare the solution for formal testing and business review.

## 2. Scope

This procedure applies to all APC-governed initiatives requiring development activities, including:

- Data products
- Data pipelines
- Lakehouses
- Warehouses
- Data transformations
- Semantic models
- Reports
- Dashboards
- KPI implementations
- Certified analytics assets
- Practitioner asset promotions
- Approved enhancements

This procedure applies to activities involving:

- Data Engineering Team (DE)
- BI Analytics Team (BI)
- Business Stakeholders
- APC Representatives
- Practitioners, when applicable

## 3. Roles & Responsibilities

#### Data Engineering Team (DE)

Responsible for:

- Data ingestion
- Data transformation
- Data engineering development
- Medallion layer implementation
- Data quality validation
- Technical documentation creation
- Environment deployment preparation

#### BI Analytics Team (BI)

Responsible for:

- Semantic model development
- Report development
- Dashboard development
- KPI implementation
- Report validation
- Business-facing documentation creation
- UAT scenario development

#### Business Stakeholder

Responsible for:

- Providing clarification on business requirements
- Providing clarification on KPI logic
- Reviewing development progress when requested
- Assisting with UAT preparation

#### APC Representatives

Responsible for:

- Supporting governance questions
- Reviewing standards exceptions
- Reviewing certification impacts when required

#### Practitioners

Responsible for:

- Supporting development of practitioner-promoted assets when applicable
- Participating in asset migration or certification activities when required

## 4. Definitions

#### Development Environment

The approved environment used to build, configure, and validate analytics solutions prior to formal testing.

#### UAT Scenario

A documented business test scenario used during User Acceptance Testing to validate solution functionality and expected outcomes.

#### Data Validation

Activities performed to verify completeness, accuracy, consistency, and reliability of data being used or delivered by the solution.

#### Semantic Model

A business-friendly representation of data designed to support reporting, KPIs, self-service analytics, and business consumption.

#### Documentation

Business, technical, or operational information required to support development, deployment, support, and maintenance activities.

## 5. Procedure

### 5.1 Review Approved Design Deliverables

Development activities shall begin by reviewing approved outputs from the Design phase.

The review should confirm:

- Business requirements
- Technical specifications
- Data architecture
- Reporting requirements
- Security requirements
- Applicable standards
- Open APC decisions

### 5.2 Develop Data Engineering Components

Required data engineering components shall be developed.

Development activities may include:

- Data ingestion
- Data transformations
- Data movement
- Lakehouse development
- Warehouse development
- Medallion layer implementation
- Data quality controls
- Pipeline development

### 5.3 Develop Semantic Models

Required semantic models shall be developed.

Development activities may include:

- Table creation
- Relationships
- Measures
- Calculated columns
- KPIs
- Perspectives
- Semantic layer optimization

### 5.4 Develop Reports and Dashboards

Required reporting assets shall be developed.

Development activities may include:

- Dashboard development
- Report development
- KPI visualizations
- Navigation structures
- User experience design
- Report performance optimization

### 5.5 Develop Documentation

Required documentation shall be developed and maintained throughout the development phase.

Documentation may include:

- Technical documentation
- Business documentation
- Data source documentation
- Semantic model documentation
- Report documentation
- KPI documentation
- Operational support documentation

### 5.6 Develop UAT Scenarios

User Acceptance Testing scenarios shall be developed to support future validation activities.

Scenarios should align to:

- Business requirements
- KPIs
- Reporting requirements
- Business processes
- Success criteria

### 5.7 Perform Development Testing

Development testing shall be performed to validate that solution components function as expected prior to formal testing activities.

Testing may include:

- Unit testing
- Data validation
- KPI validation
- Report validation
- Security validation
- Performance validation

Issues identified shall be resolved or documented prior to transition to the Deliver phase.

### 5.8 Maintain Development Documentation

Development activities shall maintain appropriate records of:

- Assumptions
- Issues
- Risks
- Exceptions
- Decisions
- Standards deviations

### 5.9 Prepare for Delivery

The Develop phase concludes when development activities are complete and the solution is ready for formal validation and business review.

The solution shall be transitioned to the Deliver phase.

## 6. Inputs

The following inputs may initiate the Develop phase:

- Approved Business Requirements
- Approved Technical Specification
- Approved Architecture Design
- Approved Data Model Design
- Security Requirements
- Applicable APC Standards
- Approved Development Authorization

## 7. Outputs

The Develop phase may produce:

- Data Pipelines
- Lakehouses
- Warehouses
- Data Transformations
- Semantic Models
- Reports
- Dashboards
- KPI Implementations
- Technical Documentation
- Business Documentation
- UAT Scenarios
- Unit Test Results
- Data Validation Results
- Development Issue Log
- Deliver Authorization

## 8. Related Procedures

| **Procedure ID** | **Procedure Name** |
| --- | --- |
| APC-SOP-301 | Data Pipeline Development Procedure |
| APC-SOP-302 | Data Validation Procedure |
| APC-SOP-303 | Semantic Model Development Procedure |
| APC-SOP-304 | Dashboard Development Procedure |
| APC-SOP-305 | KPI Development Procedure |
| APC-SOP-306 | Documentation Procedure |
| APC-SOP-307 | UAT Scenario Development Procedure |

## 9. Related Standards

| **Standard ID** | **Standard Name** |
| --- | --- |
| APC-STD-001 | Naming Standards |
| APC-STD-002 | Documentation Standards |
| APC-STD-003 | KPI Governance Standard |
| APC-STD-004 | Data Modeling Standard |
| APC-STD-005 | Medallion Architecture Standard |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-007 | Report Certification Standard |
| APC-STD-008 | Security & Access Standard |

## 10. Related Templates

| **Template ID** | **Template Name** |
| --- | --- |
| APC-TMP-010 | Technical Documentation Template |
| APC-TMP-011 | Report Documentation Template |
| APC-TMP-012 | Semantic Model Documentation Template |
| APC-TMP-013 | KPI Definition Template |
| APC-TMP-014 | UAT Scenario Template |

## 11. Related Checklists

| **Checklist ID** | **Checklist Name** |
| --- | --- |
| APC-CHK-010 | Development Readiness Checklist |
| APC-CHK-011 | Documentation Completeness Checklist |
| APC-CHK-012 | UAT Readiness Checklist |
| APC-CHK-013 | Develop Phase Exit Checklist |

## 12. Open APC Decisions

The following unresolved APC decisions may impact execution of this phase.

#### APC-OD-002: Enterprise Naming Standards

Standards for:

- Workspaces
- Tables
- Columns
- Semantic Models
- Reports
- DAX Measures
- Data Products

remain under development.

#### APC-OD-003: Documentation & Metadata Strategy

The governance approach for:

- KPI Definitions
- Business Glossary
- Lineage
- Report Documentation
- Semantic Model Documentation

remains under review.

#### APC-OD-004: Fabric Architecture Standards

Standards governing:

- Lakehouse vs Warehouse
- Direct Lake vs Import vs DirectQuery
- Shortcuts vs Data Replication
- Workspace Architecture

remain under review.

#### APC-OD-005: Data Modeling Standards

The APC has discussed utilizing Star Schema as the preferred modeling approach but final standards have not yet been approved.

## Revisions

| **Issue Date** | **Rev** | **Change** | **Written / Revised by** |
| --- | --- | --- | --- |
|  | 0 | Initial Release |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes.  Then highlight all new document changes in yellow for quick reference.  An original issue document will have no highlights.
