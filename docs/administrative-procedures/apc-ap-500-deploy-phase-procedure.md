# Deploy Phase Procedure

**Procedure ID:** APC-AP-500 | **Internal reference:** APC-PHASE-005

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of the Deploy phase is to promote approved analytics solutions into the production environment, validate deployment success, communicate solution availability, establish operational ownership, and transition the solution into ongoing support and maintenance.

The Deploy phase ensures that production releases are completed consistently, securely, and in accordance with APC governance and operational requirements.

## 2. Scope

This procedure applies to all APC-governed solutions approved for production deployment, including:

- Data products
- Data pipelines
- Lakehouses
- Warehouses
- Semantic models
- Reports
- Dashboards
- KPI implementations
- Certified analytics assets
- Approved enhancements

This procedure applies to activities involving:

- Data Engineering Team (DE)
- BI Analytics Team (BI)
- Business Stakeholders
- APC Representatives
- Support Owners
- Analytics Leadership

## 3. Roles & Responsibilities

#### Data Engineering Team (DE)

Responsible for:

- Deploying data engineering assets
- Promoting pipelines and data structures
- Validating production data operations
- Resolving deployment issues related to DE-owned assets

#### BI Analytics Team (BI)

Responsible for:

- Deploying semantic models
- Deploying reports and dashboards
- Validating reporting functionality
- Resolving deployment issues related to BI-owned assets

#### Business Stakeholder

Responsible for:

- Confirming deployment objectives have been met
- Participating in production validation when required
- Supporting release communications when applicable

#### APC Representatives

Responsible for:

- Supporting governance-related deployment questions
- Reviewing certification requirements when applicable
- Supporting release governance activities

#### Support Owner

Responsible for:

- Accepting operational ownership
- Supporting production operations after deployment
- Participating in transition activities

#### Analytics Leadership

Responsible for:

- Resolving escalated deployment issues
- Supporting release decisions when required

## 4. Definitions

#### Deployment

The process of promoting approved solution components into a production environment.

#### Production Environment

The approved operational environment used to support business users and enterprise analytics activities.

#### Hypercare

A defined period following deployment during which additional monitoring and support activities are performed to identify and resolve deployment-related issues.

#### Production Validation

Activities performed after deployment to confirm that solution functionality, data processing, reporting outputs, and access controls operate as expected in the production environment.

#### Release Communication

Communication issued to stakeholders regarding availability, changes, enhancements, impacts, or support expectations associated with a deployment.

## 5. Procedure

### 5.1 Review Deployment Authorization

Deployment activities shall begin upon receipt of approved deployment authorization from the Deliver phase.

The review should confirm:

- Business approval
- Test sign-off
- Documentation availability
- Deployment readiness
- Identified support ownership

### 5.2 Deploy Approved Solution Components

Approved solution components shall be deployed to the production environment.

Deployment activities may include:

- Data pipeline promotion
- Lakehouse or warehouse promotion
- Semantic model promotion
- Report and dashboard publication
- Security configuration deployment
- Configuration deployment

### 5.3 Validate Production Deployment

Production deployment shall be validated to ensure successful release.

Validation activities may include:

- Pipeline execution validation
- Refresh validation
- Data validation
- Report validation
- Semantic model validation
- Security validation
- Access validation

### 5.4 Perform Initial Production Monitoring

Following deployment, the solution shall be monitored to identify issues requiring remediation.

Monitoring activities may include:

- Refresh monitoring
- Pipeline monitoring
- Report availability monitoring
- Capacity monitoring
- Performance monitoring

### 5.5 Execute Release Communication

Appropriate stakeholders shall be informed of solution availability.

Communication may include:

- Release notifications
- New functionality notifications
- Known issues
- Support information
- User guidance

### 5.6 Transition to Operational Ownership

Operational ownership shall be formally established.

Transition activities may include:

- Support handoff
- Support documentation review
- Ownership confirmation
- Operational support planning

### 5.7 Conduct Hypercare Activities

Hypercare activities shall be performed for a defined period following deployment.

Activities may include:

- Elevated monitoring
- Issue response
- User support
- Defect resolution
- Adoption support

### 5.8 Close Deployment Activities

Deployment activities are considered complete when:

- Production validation is complete
- Critical issues are resolved
- Ownership is established
- Hypercare activities are complete or transitioned

The solution shall transition to the Operate phase.

## 6. Inputs

The following inputs may initiate the Deploy phase:

- Deployment Authorization
- Business Sign-Off
- Test Sign-Off
- Approved Solution Components
- Technical Documentation
- Business Documentation
- Operational Support Information

## 7. Outputs

The Deploy phase may produce:

- Production Deployment Record
- Production Validation Results
- Release Communications
- Hypercare Tracking
- Deployment Issue Log
- Operational Ownership Confirmation
- Updated Documentation
- Operate Authorization

## 8. Related Procedures

| **Procedure ID** | **Procedure Name** |
| --- | --- |
| APC-SOP-040 | Release Management Procedure |
| APC-SOP-041 | Production Deployment Procedure |
| APC-SOP-042 | Production Validation Procedure |
| APC-SOP-043 | Release Communication Procedure |
| APC-SOP-044 | Hypercare Procedure |
| APC-SOP-045 | Operational Handoff Procedure |

## 9. Related Standards

| **Standard ID** | **Standard Name** |
| --- | --- |
| APC-STD-002 | Documentation Standards |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-007 | Report Certification Standard |
| APC-STD-008 | Security & Access Standard |

## 10. Related Templates

| **Template ID** | **Template Name** |
| --- | --- |
| APC-TMP-020 | Deployment Plan Template |
| APC-TMP-021 | Production Validation Template |
| APC-TMP-022 | Release Communication Template |
| APC-TMP-023 | Hypercare Tracking Template |
| APC-TMP-024 | Production Handoff Template |

## 11. Related Checklists

| **Checklist ID** | **Checklist Name** |
| --- | --- |
| APC-CHK-020 | Deployment Readiness Checklist |
| APC-CHK-021 | Production Validation Checklist |
| APC-CHK-022 | Hypercare Readiness Checklist |
| APC-CHK-023 | Deploy Phase Exit Checklist |

## 12. Open APC Decisions

The following unresolved APC decisions may impact execution of this phase.

#### APC-OD-001: Environment Management Strategy

Standards governing:

- DEV environments
- TEST environments
- PROD environments
- Workspace strategy

have not yet been finalized.

#### APC-OD-002: CI/CD Strategy

The APC has discussed environment promotion and deployment governance; however, a formal CI/CD strategy and deployment governance model have not yet been approved.

#### APC-OD-003: Operational Ownership Model

Final ownership expectations for support, monitoring, and operational responsibilities remain under review.

#### APC-OD-004: Production Monitoring Standards

Monitoring requirements, alerting requirements, and operational reporting standards have not yet been finalized.

#### APC-OD-005: Release Communication Standards

Standardized release communication requirements remain under development.

## Revisions

| **Issue Date** | **Rev** | **Change** | **Written / Revised by** |
| --- | --- | --- | --- |
|  | 0 | Initial Release |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes.  Then highlight all new document changes in yellow for quick reference.  An original issue document will have no highlights.
