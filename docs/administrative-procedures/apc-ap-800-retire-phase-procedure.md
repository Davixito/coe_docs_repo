# Retire Phase Procedure

**Procedure ID:** APC-AP-800 | **Internal reference:** APC-PHASE-008

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of the Retire phase is to evaluate, approve, archive, decommission, and remove APC-governed analytics assets that are no longer required, no longer supported, duplicated, replaced, or no longer aligned with business needs or APC standards.

The Retire phase ensures assets are removed in a controlled and documented manner while minimizing operational risk, preserving required information, and maintaining governance compliance.

## 2. Scope

This procedure applies to retirement of APC-governed assets, including:

- Reports
- Dashboards
- Semantic Models
- Data Products
- Data Pipelines
- Lakehouses
- Warehouses
- KPI Frameworks
- Certified Analytics Assets
- Practitioner Assets promoted into APC governance

This procedure applies to activities involving:

- Business Stakeholders
- BI Analytics Team (BI)
- Data Engineering Team (DE)
- APC Representatives
- Analytics Leadership
- Compliance Stakeholders, when applicable

## 3. Roles & Responsibilities

#### Business Stakeholder

Responsible for:

- Confirming business need for retirement
- Participating in retirement evaluations
- Approving retirement when required
- Identifying business impacts

#### BI Analytics Team (BI)

Responsible for:

- Evaluating report and semantic model retirement impacts
- Retiring BI-owned assets
- Updating documentation
- Updating certification records

#### Data Engineering Team (DE)

Responsible for:

- Evaluating data asset retirement impacts
- Retiring DE-owned assets
- Managing archival activities when required
- Updating technical documentation

#### APC Representatives

Responsible for:

- Reviewing governance implications
- Reviewing certification impacts
- Validating compliance with APC standards
- Supporting retirement decisions when required

#### Analytics Leadership

Responsible for:

- Resolving retirement conflicts
- Approving retirement of high-impact assets when required
- Supporting prioritization and governance decisions

#### Compliance / Legal Representatives

Responsible for:

- Reviewing retention requirements when applicable
- Reviewing regulatory obligations when applicable

## 4. Definitions

#### Retirement

The formal process of decommissioning and removing an analytics asset from active use.

#### Retirement Candidate

An asset being evaluated for potential removal from production use.

#### Archive

The preservation of information, documentation, data, or solution artifacts following retirement.

#### Dependency

A relationship between assets where one asset relies on another to function correctly.

#### Certified Asset

A report, semantic model, data product, or other APC-governed asset that has met approved certification requirements.

## 5. Procedure

### 5.1 Identify Retirement Candidate

Assets may be identified for retirement based on factors including:

- Low or no usage
- Replacement by another solution
- Duplicate functionality
- Obsolete business processes
- Unsupported architecture
- Governance decisions
- Data quality concerns
- Business request

### 5.2 Evaluate Asset Impact

The retirement candidate shall be assessed to determine potential impact.

The assessment should consider:

- Business users
- Reports
- Dashboards
- Semantic models
- Data products
- Dependent assets
- Operational processes
- Regulatory requirements

### 5.3 Review Usage and Dependency Information

Available usage and dependency information shall be reviewed to determine:

- Current usage levels
- User population
- Business reliance
- Upstream dependencies
- Downstream dependencies

### 5.4 Determine Archival Requirements

Archival requirements shall be reviewed before retirement.

Considerations may include:

- Data retention requirements
- Historical reporting requirements
- Audit requirements
- Documentation retention requirements
- Regulatory requirements

### 5.5 Obtain Retirement Approval

Retirement approval shall be obtained from appropriate stakeholders.

Approval requirements may vary based on:

- Asset type
- Business impact
- Governance classification
- Certification status

### 5.6 Communicate Retirement

Affected stakeholders shall be informed of pending retirement activities.

Communication may include:

- Retirement timelines
- Replacement solutions
- User guidance
- Support contact information

### 5.7 Retire Asset

Approved assets shall be retired using approved retirement procedures.

Activities may include:

- Disabling refreshes
- Removing scheduled processes
- Removing access
- Removing reports
- Removing semantic models
- Removing pipelines
- Removing certifications

### 5.8 Archive Documentation and Records

Required documentation and records shall be archived in accordance with approved standards and retention requirements.

### 5.9 Update Governance Records

Governance-related records shall be updated.

Activities may include:

- Documentation updates
- Metadata updates
- Certification updates
- Asset inventory updates
- Ownership updates

### 5.10 Close Retirement Activities

Retirement activities are complete when:

- Retirement actions have been executed
- Documentation has been updated
- Archive activities are complete
- Required approvals have been recorded

## 6. Inputs

The following inputs may initiate the Retire phase:

- Business Retirement Request
- APC Recommendation
- Analytics Leadership Request
- Usage Analysis
- Asset Review Findings
- Replacement Solution Deployment
- Governance Review Results

## 7. Outputs

The Retire phase may produce:

- Retirement Assessment
- Dependency Analysis
- Usage Analysis
- Retirement Approval
- Retirement Communication
- Archive Records
- Updated Documentation
- Updated Metadata
- Updated Asset Inventory
- Retirement Closure Record

## 8. Related Procedures

| **Procedure ID** | **Procedure Name** |
| --- | --- |
| APC-SOP-070 | Asset Retirement Procedure |
| APC-SOP-071 | Report Retirement Procedure |
| APC-SOP-072 | Semantic Model Retirement Procedure |
| APC-SOP-073 | Data Product Retirement Procedure |
| APC-SOP-074 | Archive Management Procedure |
| APC-SOP-075 | Retirement Communication Procedure |

## 9. Related Standards

| **Standard ID** | **Standard Name** |
| --- | --- |
| APC-STD-002 | Documentation Standards |
| APC-STD-003 | KPI Governance Standard |
| APC-STD-007 | Security & Access Standard |
| APC-STD-008 | Report Certification Standard |

## 10. Related Templates

| **Template ID** | **Template Name** |
| --- | --- |
| APC-TMP-050 | Retirement Request Form |
| APC-TMP-051 | Retirement Assessment Template |
| APC-TMP-052 | Dependency Analysis Template |
| APC-TMP-053 | Retirement Approval Form |
| APC-TMP-054 | Retirement Communication Template |

## 11. Related Checklists

| **Checklist ID** | **Checklist Name** |
| --- | --- |
| APC-CHK-050 | Retirement Evaluation Checklist |
| APC-CHK-051 | Dependency Review Checklist |
| APC-CHK-052 | Archive Readiness Checklist |
| APC-CHK-053 | Retire Phase Exit Checklist |

## 12. Open APC Decisions

The following unresolved APC decisions may impact execution of this phase.

#### APC-OD-001: Retirement Criteria

Formal retirement criteria and usage thresholds have not yet been established.

#### APC-OD-002: Asset Inventory Management

The APC has not finalized how governed assets, certified assets, and practitioner-promoted assets will be tracked and maintained.

#### APC-OD-003: Archive Strategy

The approach for archiving retired assets, documentation, lineage information, and historical records remains under review.

#### APC-OD-004: Documentation & Metadata Governance

Requirements for maintaining metadata, glossary information, KPI definitions, and lineage records following retirement remain under development.

#### APC-OD-005: Certification Removal Process

Formal procedures governing certification removal and retirement approval for certified assets remain under review.

#### APC-OD-006: Retention Requirements

Retention requirements for retired analytics assets, documentation, and associated records have not yet been finalized.

## Revisions

| **Issue Date** | **Rev** | **Change** | **Written / Revised by** |
| --- | --- | --- | --- |
|  | 0 | Initial Release |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes.  Then highlight all new document changes in yellow for quick reference.  An original issue document will have no highlights.
