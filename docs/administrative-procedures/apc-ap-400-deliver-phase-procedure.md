# Deliver Phase Procedure

**Procedure ID:** APC-AP-400 | **Internal reference:** APC-PHASE-004

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of the Deliver phase is to validate that the developed solution meets approved business requirements, technical requirements, data quality standards, security requirements, KPI definitions, and APC governance expectations prior to production deployment.

The Deliver phase provides the formal review, testing, validation, and approval activities necessary to ensure the solution is ready for release into production.

## 2. Scope

This procedure applies to all APC-governed initiatives requiring formal validation and approval, including:

- Data products
- Data pipelines
- Semantic models
- Reports
- Dashboards
- KPI implementations
- Certified analytics assets
- Practitioner assets seeking certification or promotion
- Major enhancements

This procedure applies to activities involving:

- Business Stakeholders
- BI Analytics Team (BI)
- Data Engineering Team (DE)
- APC Representatives
- Analytics Leadership
- Practitioners, when applicable

## 3. Roles & Responsibilities

#### Business Stakeholder

Responsible for:

- Participating in User Acceptance Testing (UAT)
- Validating business requirements
- Validating KPI calculations
- Validating business rules
- Approving or rejecting delivered functionality
- Providing final business sign-off

#### BI Analytics Team (BI)

Responsible for:

- Supporting report validation
- Supporting dashboard validation
- Supporting semantic model validation
- Supporting KPI validation
- Resolving identified issues

#### Data Engineering Team (DE)

Responsible for:

- Supporting data validation
- Supporting pipeline validation
- Supporting source-to-target validation
- Resolving data quality issues
- Supporting technical testing activities

#### APC Representatives

Responsible for:

- Reviewing governance compliance as required
- Reviewing certification requirements as required
- Reviewing standards-related concerns

#### Analytics Leadership

Responsible for:

- Resolving escalated testing issues
- Resolving approval conflicts
- Providing release support when required

## 4. Definitions

#### User Acceptance Testing (UAT)

Formal testing performed by business stakeholders to confirm the solution meets business requirements and expected outcomes.

#### Test Sign-Off

Formal approval indicating that testing activities have been completed and deployment may proceed.

#### Data Validation

Verification that data presented by the solution is accurate, complete, and consistent with approved business expectations.

#### KPI Validation

Verification that KPI calculations align with approved business definitions and requirements.

#### Deliverable

Any solution component, artifact, or output requiring review and approval prior to deployment.

## 5. Procedure

### 5.1 Review Development Outputs

The Deliver phase begins with the review of development outputs.

The review should confirm:

- Development activities are complete
- Required documentation is available
- UAT scenarios have been developed
- Validation resources are identified
- Outstanding issues are documented

### 5.2 Perform Data Validation

Data validation activities shall be performed to confirm that delivered data meets approved requirements.

Validation activities may include:

- Source-to-target comparisons
- Data quality reviews
- Reconciliation activities
- KPI data validation
- Exception review

### 5.3 Perform Report and Dashboard Validation

Reports and dashboards shall be reviewed to validate:

- Business requirements
- Visualization accuracy
- KPI presentation
- Filtering functionality
- Navigation functionality
- Expected user experience

### 5.4 Execute User Acceptance Testing (UAT)

User Acceptance Testing shall be performed using approved UAT scenarios.

Testing should validate:

- Business requirements
- Business processes
- Expected outcomes
- KPI calculations
- Reporting functionality

Issues identified during UAT shall be documented and resolved or formally accepted.

### 5.5 Validate KPIs and Business Rules

KPIs and business rules shall be reviewed with appropriate business stakeholders.

Validation activities should confirm:

- KPI calculations
- Business logic
- Data interpretation
- Expected outcomes
- Approved definitions

### 5.6 Validate Security and Access

Security and access controls shall be reviewed to ensure users have appropriate permissions and access.

Validation may include:

- User access validation
- Security role validation
- Sensitive data review
- Compliance review

### 5.7 Resolve Defects and Issues

Issues identified during validation activities shall be:

- Corrected
- Retested
- Deferred with approval
- Accepted with documented justification

All decisions should be documented.

### 5.8 Obtain Business Sign-Off

Business stakeholders shall formally review delivered functionality and provide approval when requirements have been met.

Business approval confirms readiness for production deployment.

### 5.9 Approve for Deployment

The Deliver phase concludes when validation activities have been completed and deployment approval has been obtained.

Approved solutions shall transition to the Deploy phase.

## 6. Inputs

The following inputs may initiate the Deliver phase:

- Completed Development Activities
- Technical Documentation
- Business Documentation
- UAT Scenarios
- Data Validation Results
- Development Issue Log
- Applicable APC Standards

## 7. Outputs

The Deliver phase may produce:

- Data Validation Results
- Dashboard Validation Results
- KPI Validation Results
- UAT Results
- Defect Log
- Issue Resolution Log
- Security Validation Results
- Test Sign-Off
- Business Sign-Off
- Deploy Authorization

## 8. Related Procedures

| **Procedure ID** | **Procedure Name** |
| --- | --- |
| APC-SOP-030 | Data Validation Procedure |
| APC-SOP-031 | Dashboard Validation Procedure |
| APC-SOP-032 | KPI Validation Procedure |
| APC-SOP-033 | UAT Execution Procedure |
| APC-SOP-034 | Defect Management Procedure |
| APC-SOP-035 | Test Sign-Off Procedure |

## 9. Related Standards

| **Standard ID** | **Standard Name** |
| --- | --- |
| APC-STD-002 | Documentation Standards |
| APC-STD-003 | KPI Governance Standard |
| APC-STD-007 | Report Certification Standard |
| APC-STD-008 | Security & Access Standard |

## 10. Related Templates

| **Template ID** | **Template Name** |
| --- | --- |
| APC-TMP-305 | UAT Scenario Template |
| APC-TMP-015 | UAT Results Template |
| APC-TMP-016 | Defect Log Template |
| APC-TMP-017 | KPI Validation Template |
| APC-TMP-018 | Test Sign-Off Form |

## 11. Related Checklists

| **Checklist ID** | **Checklist Name** |
| --- | --- |
| APC-CHK-303 | UAT Readiness Checklist |
| APC-CHK-401 | Data Validation Checklist |
| APC-CHK-402 | Security Validation Checklist |
| APC-CHK-403 | Deliver Phase Exit Checklist |

## 12. Open APC Decisions

The following unresolved APC decisions may impact execution of this phase.

#### APC-OD-001: KPI Governance Framework

Approval, versioning, and management of KPI definitions remain under review.

#### APC-OD-002: Certification Requirements

Final certification criteria for reports, semantic models, and data products have not yet been approved.

#### APC-OD-003: Documentation Standards

Final requirements for report documentation, semantic model documentation, lineage documentation, and metadata management remain under review.

#### APC-OD-004: Security Validation Requirements

Final standards governing security validation and certification activities have not yet been approved.

## Revisions

| **Issue Date** | **Rev** | **Change** | **Written / Revised by** |
| --- | --- | --- | --- |
|  | 0 | Initial Release |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes.  Then highlight all new document changes in yellow for quick reference.  An original issue document will have no highlights.
