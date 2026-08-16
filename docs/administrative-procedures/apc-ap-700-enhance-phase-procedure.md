# Enhance Phase Procedure

**Procedure ID:** APC-AP-700 | **Internal reference:** APC-PHASE-007

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of the Enhance phase is to evaluate, prioritize, approve, develop, validate, and implement modifications to existing APC-governed analytics assets.

The Enhance phase provides a structured process for managing changes required to improve functionality, address business needs, support changing business processes, improve performance, resolve operational issues, or maintain alignment with APC governance standards.

## 2. Scope

This procedure applies to enhancements involving existing APC-governed assets, including:

- Reports
- Dashboards
- Semantic Models
- Data Products
- Data Pipelines
- Lakehouses
- Warehouses
- KPI Implementations
- Certified Analytics Assets
- Supported Practitioner Assets

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

- Identifying enhancement needs
- Providing business justification
- Clarifying business requirements
- Validating enhancement outcomes
- Participating in prioritization discussions when required

#### BI Analytics Team (BI)

Responsible for:

- Evaluating report, dashboard, semantic model, and KPI impacts
- Estimating effort
- Implementing BI-related enhancements
- Updating documentation as required

#### Data Engineering Team (DE)

Responsible for:

- Evaluating data architecture impacts
- Estimating data engineering effort
- Implementing DE-related enhancements
- Updating documentation as required

#### APC Representatives

Responsible for:

- Evaluating governance impacts
- Reviewing standards impacts
- Reviewing certification implications
- Supporting prioritization decisions

#### Analytics Leadership

Responsible for:

- Resolving prioritization conflicts
- Approving major enhancement efforts when required
- Supporting resource allocation decisions

#### Practitioner

Responsible for:

- Providing input when practitioner-developed assets are impacted
- Participating in validation activities when applicable

## 4. Definitions

#### Enhancement

A modification, improvement, expansion, optimization, or correction made to an existing APC-governed asset.

#### Enhancement Request

A formal request submitted to modify an existing analytics asset.

#### Backlog

A collection of approved or pending enhancement requests awaiting prioritization or execution.

#### Major Enhancement

An enhancement that significantly impacts requirements, architecture, data structures, reporting functionality, security, ownership, or operational support.

#### Minor Enhancement

An enhancement that can be implemented without significant architectural, governance, or operational impact.

## 5. Procedure

### 5.1 Submit Enhancement Request

Enhancement requests shall be submitted through an approved intake mechanism.

Requests may originate from:

- Business stakeholders
- Operational support activities
- Data quality reviews
- Governance reviews
- User feedback
- APC recommendations
- Analytics Leadership

### 5.2 Review Enhancement Request

Enhancement requests shall be reviewed to determine:

- Business need
- Business value
- Impacted assets
- Impacted users
- Potential risks
- Governance implications

### 5.3 Assess Impact

An impact assessment shall be performed to determine:

- Data impacts
- Reporting impacts
- Semantic model impacts
- KPI impacts
- Security impacts
- Operational impacts
- Documentation impacts

### 5.4 Estimate Effort

The enhancement shall be evaluated to determine:

- Complexity
- Resource requirements
- Estimated effort
- Dependencies
- Potential release approach

### 5.5 Prioritize Enhancement

Enhancements shall be prioritized using approved APC prioritization criteria.

Prioritization considerations may include:

- Business value
- Strategic alignment
- Enterprise impact
- Regulatory requirements
- Risk
- Resource availability

Enhancements may be:

- Approved
- Deferred
- Bundled
- Returned for clarification
- Rejected

### 5.6 Determine Required Lifecycle Activities

The enhancement shall be evaluated to determine the level of lifecycle execution required.

Examples may include:

- Direct implementation
- Partial lifecycle execution
- Full lifecycle execution beginning at Discovery / Define

The decision should be based on scope, complexity, risk, and business impact.

### 5.7 Implement Approved Enhancement

Approved enhancements shall be implemented using the applicable APC lifecycle phases.

Activities may include:

- Design updates
- Development activities
- Validation activities
- Deployment activities
- Documentation updates

### 5.8 Validate Enhancement

Enhancements shall be validated to ensure requirements and expected outcomes have been achieved.

Validation activities may include:

- Data validation
- KPI validation
- User acceptance testing
- Security validation
- Business review

### 5.9 Update Documentation

All affected documentation shall be reviewed and updated as required.

Documentation may include:

- Technical documentation
- Business documentation
- KPI documentation
- Metadata records
- Operational documentation

### 5.10 Return Asset to Operate

Once enhancement activities are complete, the asset shall transition back to the Operate phase.

## 6. Inputs

The following inputs may initiate the Enhance phase:

- Enhancement Request
- Operational Support Recommendation
- User Feedback
- Data Quality Issue
- APC Recommendation
- Analytics Leadership Request
- Business Request

## 7. Outputs

The Enhance phase may produce:

- Enhancement Assessment
- Impact Analysis
- Effort Estimate
- Prioritization Decision
- Updated Requirements
- Updated Solution Components
- Validation Results
- Documentation Updates
- Operate Authorization

## 8. Related Procedures

| **Procedure ID** | **Procedure Name** |
| --- | --- |
| APC-SOP-060 | Enhancement Intake Procedure |
| APC-SOP-061 | Impact Assessment Procedure |
| APC-SOP-062 | Enhancement Prioritization Procedure |
| APC-SOP-063 | Enhancement Planning Procedure |
| APC-SOP-064 | Documentation Update Procedure |

## 9. Related Standards

| **Standard ID** | **Standard Name** |
| --- | --- |
| APC-STD-001 | Naming Standards |
| APC-STD-002 | Documentation Standards |
| APC-STD-003 | KPI Governance Standard |
| APC-STD-004 | Data Modeling Standard |
| APC-STD-005 | Medallion Architecture Standard |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-007 | Security & Access Standard |
| APC-STD-008 | Report Certification Standard |

## 10. Related Templates

| **Template ID** | **Template Name** |
| --- | --- |
| APC-TMP-040 | Enhancement Request Form |
| APC-TMP-041 | Enhancement Assessment Template |
| APC-TMP-042 | Impact Analysis Template |
| APC-TMP-043 | Prioritization Worksheet |
| APC-TMP-044 | Documentation Update Log |

## 11. Related Checklists

| **Checklist ID** | **Checklist Name** |
| --- | --- |
| APC-CHK-040 | Enhancement Review Checklist |
| APC-CHK-041 | Impact Assessment Checklist |
| APC-CHK-042 | Validation Checklist |
| APC-CHK-043 | Enhance Phase Exit Checklist |

## 12. Open APC Decisions

The following unresolved APC decisions may impact execution of this phase.

#### APC-OD-001: Enhancement Prioritization Framework

The APC has discussed prioritization, effort thresholds, bundling, and escalation processes but has not finalized a formal enhancement prioritization framework.

#### APC-OD-002: Effort Thresholds

Formal definitions for:

- Standard Work
- Bundled Work
- Demand Initiatives

remain under review.

#### APC-OD-003: Enhancement Approval Authority

Approval requirements for various enhancement types remain under development.

#### APC-OD-004: Backlog Governance

Ownership, review frequency, and management expectations for enhancement backlogs have not yet been finalized.

#### APC-OD-005: Practitioner Enhancement Governance

Standards governing enhancement of practitioner-promoted assets remain under review.

## Revisions

| **Issue Date** | **Rev** | **Change** | **Written / Revised by** |
| --- | --- | --- | --- |
|  | 0 | Initial Release |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes.  Then highlight all new document changes in yellow for quick reference.  An original issue document will have no highlights.
