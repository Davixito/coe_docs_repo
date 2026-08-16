# Dashboard Development Procedure

**Procedure ID:** APC-SOP-304 | **Document Type:** SOP | **Lifecycle Phase:** Phase 3 – Develop (APC-PHASE-003)

> ## ⚠️ DRAFT — NOT YET ISSUED
>
> This document is a **brainstorm working draft**, structured against APC-TMP-001. It is not authoritative and has not been approved. Reference convention: codes shown as `[APC-XXX-000]` with a **NEW** marker are assets that do not yet exist and require a code to be assigned and the asset created — they are not issued. Bracketed values (e.g. `[YYYY-MM-DD]`) require confirmation. All open questions are consolidated in [Section 13, Open APC Decisions](#13-open-apc-decisions).

[← Back to documentation index](../index.md)

---

Procedure governing the development of dashboards and reports on Microsoft Power BI and Microsoft Fabric within the APC Develop phase.

## Document Control

| Field | Value | Field | Value |
| --- | --- | --- | --- |
| Document ID | APC-SOP-304 | Revision | 0 |
| Document Title | Dashboard Development Procedure | Status | **Draft** |
| Document Type | SOP | Issue Date | *[YYYY-MM-DD]* |
| Document Owner | *[Name], BI Analytics Lead* | Next Review | *[YYYY-MM-DD]* |
| Approver | *[Name], Analytics Leadership]* | Review Cycle | Annual |
| Applies To | BI Analytics Team; Practitioners developing APC-governed dashboards | Classification | Internal |

> **Draft note:** APC-SOP-304 is already registered in the Develop Phase procedure index but has never been authored. This draft fills that entry. No dashboard Standard exists at any APC-STD ID; see Section 13 on whether the requirement content in 5.4, 5.6, 5.9 and 5.11 should be extracted into a new Standard. References shown as `[APC-XXX-000]` are assets that do not exist yet — a code must be assigned and the asset created before this document is issued.

## 1. Purpose

The purpose of this procedure is to define how APC-governed dashboards are developed so that reporting assets are built consistently, perform predictably, protect sensitive data, and can be supported by a team other than the one that built them. This procedure establishes the sequence of development activities, the conventions applied at each step, and the conditions under which a dashboard is considered ready to leave the Develop phase.

Dashboards are the most visible output of the analytics function and are frequently the only part of the platform a business stakeholder ever sees. Inconsistent layout, undocumented calculations, unmanaged performance, and report-layer security workarounds erode trust in the underlying data far faster than defects in the data itself. This procedure exists to prevent that erosion by making development decisions explicit and repeatable rather than left to individual preference.

This procedure protects the integrity of the certification path. A dashboard developed outside of it cannot be reliably validated in the Deliver phase, certified under APC-STD-007, or transitioned to operational support with a known cost of ownership.

## 2. Scope

This procedure applies to:

- Dashboards and reports developed on Microsoft Power BI or Microsoft Fabric
- Scorecards and KPI visualizations built on APC-approved semantic models
- Paginated reports where they form part of an APC-governed reporting solution
- Thin reports connected by live connection to a shared semantic model
- Practitioner-developed assets seeking APC certification, promotion, or enterprise support
- Enhancements to existing dashboards that add or materially alter pages, KPIs, or visuals

This procedure applies to activities involving:

- BI Analytics Team (BI)
- Practitioner
- Data Engineering Team (DE)
- APC Representatives
- Business Stakeholder
- Support Owner

**Exclusions**

- Semantic model development, including measures, calculated columns, relationships and RLS role definitions — covered by APC-SOP-303.
- KPI definition and approval — covered by APC-SOP-305 and APC-STD-003.
- Data pipeline and transformation development — covered by APC-SOP-301.
- Validation, UAT execution and business sign-off — covered by APC-SOP-031 and APC-SOP-033.
- Deployment to production and release communication — covered by APC-SOP-041 and APC-SOP-043.
- Self-service exploratory content in personal workspaces that is not seeking certification, promotion, or enterprise support.

> **Draft note:** The last exclusion is the contested one. Confirm whether uncertified personal-workspace content is genuinely out of scope, or whether a lightweight subset of this procedure should apply to it to ease later promotion.

## 3. Roles & Responsibilities

#### BI Analytics Team (BI)

Responsible for:

- Develop dashboards in accordance with this procedure and the standards referenced in Section 10.
- Apply naming, layout, performance and accessibility conventions consistently across all pages.
- Connect reports to the approved semantic model and escalate any need for a report-level model as an exception.
- Execute development testing and record results.
- Perform peer review of dashboards developed by other BI team members.
- Complete report documentation before requesting transition to the Deliver phase.

#### Data Engineering Team (DE)

Responsible for:

- Provide and maintain the semantic model and underlying data assets the dashboard consumes.
- Confirm refresh schedules and data latency so they can be displayed accurately to users.
- Advise on model-side remediation where a performance issue cannot be resolved at the report layer.

#### Business Stakeholder

Responsible for:

- Confirm that KPIs, filters, and page structure reflect the approved requirements.
- Provide timely feedback during development checkpoints.
- Identify the audience groups that determine access and row-level security expectations.

#### APC Representatives

Responsible for:

- Review dashboards seeking certification against APC-STD-007.
- Approve documented exceptions to this procedure, including import-mode and report-level model requests.
- Confirm that naming, workspace placement and sensitivity classification align to APC standards.

#### Practitioner

Responsible for:

- Apply this procedure when developing assets intended for APC certification, promotion, or enterprise support.
- Engage the BI Analytics Team before beginning development of an asset intended for enterprise use.

#### Support Owner

Responsible for:

- Confirm the dashboard is supportable as built and that documentation is sufficient for operational handoff.
- Raise supportability concerns before the Develop phase exit rather than after deployment.

#### Analytics Leadership

Responsible for:

- Approve this procedure and any revision to it.
- Arbitrate where performance, scope or design expectations cannot be reconciled at the team level.

## 4. Definitions

| Term | Definition |
| --- | --- |
| Accessibility Baseline | The minimum set of contrast, alt text, tab order and non-colour-dependent design conditions a dashboard must satisfy before Develop phase exit. |
| Design System | The governed set of tokens, components, patterns and rules from which APC dashboards are assembled. Maintained in Figma and published as a versioned release. See `[APC-XXX-000]` Analytics Design System — **NEW**, to be created. |
| Design Token | A named design value — a colour, spacing step, type size or radius — referenced by name rather than by literal value, so that a change at the token level propagates to every asset that uses it. |
| Mobile-Optimized Layout | A layout authored specifically for the phone canvas. Distinct from a desktop layout that the platform scales down for a phone screen. |
| Page Archetype | A defined page pattern with an expected zone structure, density and visual count. Every page of an APC dashboard conforms to one archetype. |
| Report Theme File | The Power BI theme JSON generated from the design system token set and applied to every APC-governed report. |
| Certified Dashboard | A dashboard that has completed validation and been endorsed under APC-STD-007 Report Certification Standard. Certification is granted to the asset, not to the developer. |
| Dashboard | An APC-governed analytics asset that presents approved KPIs and supporting visuals to a defined audience. Used in this document to include Power BI reports, dashboards and scorecards unless a distinction is stated. |
| Interaction Response Time | Elapsed time between a user action — slicer change, cross-filter, drill — and the completed re-render of all affected visuals on the page. |
| Load Time Budget | The maximum permitted elapsed time from opening a report page to the completed render of all visuals on that page, measured under defined test conditions. |
| Report-Level Measure | A DAX measure defined inside the report file rather than in the semantic model. Not permitted for APC-governed dashboards; measures belong to the model. |
| Thin Report | A report file containing no data model of its own, connected by live connection to a shared semantic model. The default and expected pattern for APC-governed dashboards. |
| Visual Density | The count of rendered visual elements on a single report page, including cards, charts, tables, slicers and shapes that issue a query. |

## 5. Procedure

> **Draft note:** Sub-steps are ordered as a developer would execute them. Steps 5.4, 5.6, 5.9 and 5.11 carry most of the standards-type content; if a separate Dashboard Standard is created they would reduce to references. Consider whether 5.11 Accessibility should merge into 5.6 Design rather than stand alone.

### 5.1 Confirm Development Readiness

Dashboard development shall not begin until approved Design phase outputs and a development-ready semantic model are available.

This step prevents rework caused by building against unapproved requirements or an unstable model. Readiness is evidenced by APC-CHK-010 Development Readiness Checklist.

- Approved Business Requirements Document (APC-TMP-201)
- Approved Technical Specification (APC-TMP-202)
- Approved KPI definitions for every metric to be displayed (APC-TMP-013)
- Semantic model available in the target workspace and passing its own development tests
- Assigned Fabric workspace, capacity and development access provisioned
- Named report owner and named support owner
- Confirmed audience groups and expected row-level security roles

### 5.2 Wireframe the Report

Wireframing shall begin only once the approved Business Requirements Document and Technical Specification are available, and every wireframe element shall trace back to a specific requirement or constraint defined in those documents.

A wireframe invented independently of the approved requirements is just a guess with good production values. Tracing each zone back to a specific requirement is what turns a wireframe into a design, rather than a decoration.

- Wireframing draws directly from the approved Business Requirements Document (APC-TMP-201) and Technical Specification (APC-TMP-202) confirmed at Development Readiness (5.1)
- Each wireframe zone or KPI placement traces to a specific business requirement, KPI definition, or technical constraint — untraceable elements are removed, or the requirement is clarified first
- Wireframes produced for every anticipated page before any visual is built in Power BI
- Wireframes show zone structure only (header, filter, summary, primary analysis, detail, footer) — not colour, iconography, or finished typography
- KPI placement and priority ordering established at wireframe stage, before any DAX is written
- Wireframes retained with the report documentation as a record of design intent and requirement traceability

> **Draft note:** No wireframing tool is currently standardized. Options include Figma (consistent with where the Analytics Design System lives), PowerPoint (lowest barrier to entry for BI developers), or a blank Power BI canvas with placeholder shapes (fastest, but risks becoming the final build instead of a disposable sketch). Confirm whether a formal requirement-to-wireframe traceability matrix is expected, or whether tracing is satisfied informally by the wireframe visibly reflecting the BRD's stated KPIs and structure.

### 5.3 Select Dashboard Type

Once the wireframe reflects the approved requirements, the report shall be classified against one of the approved dashboard types, and each page shall be assigned its corresponding page archetype under 5.6.7.

Classifying type after the wireframe exists, rather than before, lets the actual shape of the requirements decide the type — rather than forcing requirements into a type chosen too early.

- Dashboard type recorded in the report documentation once confirmed
- Each page's declared page archetype (5.6.7) assigned based on the finalized wireframe and confirmed type
- Type selection made once, at the start of Develop, and revisited only through a formal Enhance request
- A report may combine types across pages, but each page still declares a single archetype
- Type determines refresh cadence expectations and interaction depth — not just visual style

| Dashboard type (proposed baseline) | Purpose | Typical audience | Refresh cadence | Interaction depth |
| --- | --- | --- | --- | --- |
| Operational | Monitor near-real-time state; flag exceptions | Frontline / operations teams | Frequent (e.g. intraday) | Low — glance and act |
| Analytical / Exploratory | Investigate a question; support ad hoc analysis | Analysts, subject matter experts | Scheduled (daily/weekly) | High — filter, drill, slice |
| Strategic / Executive | Track KPIs against targets; support decisions | Leadership | Scheduled (weekly/monthly) | Low — summary first, drill on demand |
| Certified Enterprise Report | Single source of truth for a certified metric set | Broad / enterprise-wide | Scheduled, governed | Low–medium — controlled navigation |
| Scorecard | Track a fixed set of KPIs against goals over time | Leadership, accountable teams | Scheduled | Low |

> **Draft note:** This taxonomy is proposed, not yet ratified by APC. Confirm against the current report inventory whether these five types cover what exists, and whether "Embedded / Self-Service" needs to be a sixth category with its own rules.

### 5.4 Establish Report Structure and Naming

All dashboard artifacts shall be named and placed in accordance with APC-STD-001 Naming Standards and APC-STD-006 Fabric Architecture Standard before development content is added.

Naming applied retroactively is rarely applied completely. Establishing structure first also makes peer review and later enhancement substantially cheaper.

- Report file named to the approved convention — proposed pattern: [Domain]-[Subject]-[Audience]
- Page names are business-meaningful; default names such as "Page 1" are not permitted
- Bookmarks, buttons, groups and selection-pane items are named descriptively, not left as system defaults
- Report developed in a governed workspace; personal workspaces are not permitted for APC-governed development
- Development, Test and Production workspace separation applied per APC-STD-006
- Report saved in the file format defined in Section 5.5, within the approved source-controlled location where Git integration is in use
- Unused pages, bookmarks, visuals and fields removed before Develop phase exit

> **Draft note:** Confirm the file naming pattern against APC-STD-001 rather than inventing one here. See Section 5.5 for the PBIX vs PBIP file format decision.

### 5.5 Connect to the Approved Semantic Model

Dashboards shall connect by live connection to an APC-approved semantic model and shall not contain a report-level data model.

A report that carries its own model duplicates business logic, defeats lineage, and cannot inherit row-level security. Exceptions exist but must be visible.

- Live connection to the approved semantic model is the required pattern
- Import mode, composite models and DirectQuery to arbitrary sources require a documented exception approved by an APC Representative
- Report-level measures are not permitted; all measures are defined in the semantic model under APC-SOP-303
- Local files, personal spreadsheets and manually maintained lookup tables are not permitted as report data sources
- Any gap in the semantic model is raised to Data Engineering rather than worked around at the report layer
- The model version the report is built against is recorded in the report documentation

Report files shall be saved in the file format that supports the version-control requirement in Section 5.4 — Power BI Desktop file (.pbix) or Power BI Project (.pbip) — applied consistently across all APC-governed development.

Version control is the primary driver of this choice, not a secondary convenience. PBIX bundles the report, data model and cached data into a single opaque binary; a Git diff on a .pbix file shows only that the file changed, not what changed, which defeats code review, blocks meaningful pull requests, and forces merge conflicts to be resolved by discarding one side's changes entirely. PBIP splits the report and semantic model into a folder of human-readable JSON and TMDL files, so a reviewer can see the actual change — a colour token, a measure, a page layout — the same way any other source-controlled artifact is reviewed. Where Git integration is mandated under 5.4, PBIP is the format that makes that mandate meaningful; PBIX under Git integration satisfies the letter of the requirement but not its purpose.

- Proposed baseline — PBIP for all APC-governed development, since it is the format that makes the Section 5.4 version-control requirement effective, where Developer Mode and Git integration are available on the tenant
- PBIX remains the fallback where PBIP is not yet supported, or for personal exploratory work excluded under Section 2
- A report developed in PBIX and later brought under APC governance is converted to PBIP before Develop phase exit, once PBIP is adopted as the standard
- Semantic model TMDL definitions under PBIP are reviewed by a second BI team member before merge, consistent with the peer review requirement in 5.12
- Mixed-format development within a single report is not permitted; a report is developed as PBIX or PBIP for its full lifecycle
- The file format used and its repository location are recorded in the report documentation

| File format (proposed baseline) | Proposed value |
| --- | --- |
| Development format | PBIP (Power BI Project), where tenant support is confirmed |
| Legacy fallback | PBIX, for excluded personal workspaces or where Developer Mode is unavailable |
| Source of truth | Git repository defined in APC-STD-006 |
| Conversion path | Power BI Desktop "Save as .pbip", or pbi-tools where bulk conversion is required |

> **Draft note:** Confirm whether Power BI Desktop Developer Mode and Git integration are available and supported on your tenant and capacity before mandating PBIP. If not yet available, PBIX remains the interim standard and this section should read "should" rather than "shall" until confirmed. See Section 13.

### 5.6 Apply the APC Analytics Design System

Dashboards shall be designed in accordance with the Analytics Design System (`[APC-XXX-000]` — **NEW**, to be created), which is the authoritative source for all visual design decisions. This procedure names the components of the design system and the minimum conditions each must satisfy; it does not restate the specifications themselves.

A design system exists so that visual decisions are made once, centrally, and then reused — rather than re-litigated by each developer on each report. Consistency across the portfolio matters more than the optimisation of any single dashboard. A user who has learned to read one APC dashboard should be able to read the next one without re-orientation.

> **Draft note:** The Analytics Design System and its theme file do not exist and no code has been assigned to either. Both are shown as `[APC-XXX-000]` throughout. A further question is whether they belong in an existing class at all: a living design asset versioned in Figma does not fit the document revision model that SOP, STD, TMP and CHK assume, so a new class may be needed. See Section 13.

The design system is maintained in Figma and published as a versioned release. Where the Figma design system and the proposed baseline values in this section differ, the published Figma release takes precedence and this section is to be updated at the next revision.

- `[APC-XXX-000]` Analytics Design System (Figma) — **NEW**, to be created — canonical source for all values below
- `[APC-XXX-000]` Power BI Report Theme File (.json) — **NEW**, to be created — generated from the design system tokens and versioned with them
- The theme file applied to a report shall match the design system release recorded in the report documentation
- Ad hoc colour, font and spacing selection outside the applied theme is not permitted

Full specification of the following areas is maintained in the Analytics Design System `[APC-XXX-000]`, the Power BI Report Theme File (.json), and the Power BI Template (.pbit). This SOP names them as required components of every report; it does not duplicate their content, and a developer executing this procedure should treat those artifacts — not this document — as the source of exact values, components, and specifications.

- Design tokens — naming convention, categories, primitive/semantic architecture
- Canvas, grid and layout — dimensions, columns, gutters, margins, minimum visual sizes
- Spacing and density — spacing scale, padding, zone heights, density modes
- Typography — type scale, type family, licensing
- Colour system — primary, neutral, secondary/status and data visualization palettes
- Iconography, shape and elevation — icon set, sizes, corner radius, elevation treatment
- Dashboard anatomy and page archetypes — zone structure, archetype definitions
- Component library — KPI cards, navigation, filters, tables, buttons, states, and all other components
- Data visualization language — chart selection rules, chart anatomy, number formatting
- Interaction and state — hover, focus, selected, loading and disabled states
- Content, labelling and voice — terminology, capitalisation, tone, empty/error copy
- Accessibility foundations — contrast ratios, WCAG baseline
- Mobile-optimized layout — breakpoints, touch targets, mobile type scale
- Conformance and exceptions — the departure and change-request process

Departures from any of the above are handled through the standard APC exception process; recurring exceptions are raised as change requests against the Analytics Design System `[APC-XXX-000]` rather than repeated per report.

### 5.7 Implement KPIs and Visuals

Every KPI displayed on an APC-governed dashboard shall trace to an approved KPI definition.

This is the step where undocumented business logic most commonly enters the platform, usually as a well-intentioned quick fix.

- KPI names on the dashboard match the approved definition in APC-TMP-013 exactly
- No calculation is introduced at the report layer that does not exist in the approved KPI set
- Conditional formatting thresholds are taken from the KPI definition and are not hard-coded to arbitrary values
- Tooltips expose the KPI definition, owner and refresh cadence where space permits
- Totals, subtotals and aggregation behaviour are verified against the semantic model
- Null, zero and no-data states are handled explicitly rather than left to default rendering
- Filters applied at visual level are documented where they change the meaning of a displayed figure

### 5.8 Implement Navigation and Interactivity

Navigation shall be explicit, consistent and discoverable without training.

Interactivity that is undocumented is indistinguishable from a defect during UAT.

- Persistent navigation control present on every page
- Slicer synchronisation behaviour defined per page and documented
- Default filter state on open is deliberate and documented, including default date range
- Cross-filter and cross-highlight behaviour set intentionally rather than left at default
- Drill-through targets are labelled and reachable; a return path is always provided
- A reset-to-default control is provided where the report carries more than a small number of filters
- Hidden pages used only as drill-through or tooltip targets are named and listed in the documentation
- Mobile-optimized layout implemented in accordance with 5.6.13, or the report explicitly documented as desktop-only

### 5.9 Optimize Performance

Dashboards shall meet the APC performance targets before the Develop phase exit, and results shall be recorded.

Performance measured only after deployment is measured too late. Targets below are proposals for confirmation.

- Proposed target — initial page render at or under 5 seconds
- Proposed target — interaction response at or under 3 seconds
- Proposed target — no more than 12 query-issuing visuals on a single page, with 8 as the design guideline
- Measurement performed with Performance Analyzer under defined test conditions, on the target capacity, against production-scale data
- Bidirectional relationships and unnecessary bidirectional filters avoided
- High-cardinality slicers avoided; Select All disabled where the field is high cardinality
- Auto date/time disabled; date logic sourced from the model date table
- Aggregations, summarised tables or model-side remediation used where report-layer tuning is insufficient
- Measured results recorded in the report documentation, not only reviewed verbally

> **Draft note:** The three proposed thresholds are the single most important thing to confirm in this document. They should be set from observed performance on your capacity, not adopted from a vendor guideline. Define "production-scale data" and the reference capacity explicitly, or the targets are not reproducible.

### 5.10 Apply Security, Sensitivity and Access Controls

Access to dashboard content shall be governed by row-level security in the semantic model and by workspace and app roles in accordance with APC-STD-008 Security & Access Standard.

Security implemented at the report layer is cosmetic. It survives neither export nor a determined user.

- Row-level security is inherited from the semantic model; no security is implemented at the report layer
- RLS tested from the perspective of every defined role before Develop phase exit
- Sensitivity label applied in accordance with APC-STD-008
- Distribution via app audiences rather than direct item sharing
- External and guest sharing is not permitted without documented approval
- No personally identifiable or restricted data exposed in page titles, tooltips or visual headers
- Export and download permissions set deliberately and recorded in documentation

### 5.11 Meet the Accessibility Baseline

Dashboards should meet the APC accessibility baseline before Develop phase exit.

Accessibility is materially cheaper to build in than to retrofit, and the retrofit usually forces a redesign.

- Text and background contrast ratio at or above 4.5:1
- Alt text provided for every non-decorative visual
- Tab order set deliberately on every page rather than left at the default insertion order
- Colour-vision-safe palette used; colour is never the sole carrier of meaning
- Status and variance communicated by icon, label or position in addition to colour
- Minimum readable font size applied consistently across visuals

> **Draft note:** Accessibility is now addressed in two places by design: 5.6.12 builds it into the design system tokens and components, and this step verifies it on the finished report. Confirm the external baseline being adopted — 5.6.12 proposes WCAG 2.1 AA — and confirm whether this step is a "shall" or a "should".

### 5.12 Conduct Development Testing and Peer Review

Dashboards shall be unit tested by the developer and peer reviewed by a second BI team member before transition to the Deliver phase.

Peer review at this point catches convention and supportability issues while they are still cheap to fix.

- Displayed figures reconciled against the semantic model and, where required, against source
- Every filter and slicer combination that changes displayed meaning exercised
- Edge cases tested: no data returned, single-value selection, maximum date range, new or missing dimension members
- RLS tested for each role, including a role with the narrowest permitted scope
- Rendering verified on the browsers and devices the audience actually uses
- Peer review recorded, including reviewer name and date
- Defects logged in the defect log (APC-TMP-016) and critical defects closed before phase exit

### 5.13 Produce Report Documentation

Report documentation shall be completed in accordance with APC-SOP-306 and APC-TMP-011 before the Develop phase exit.

Documentation is a deliverable of this phase, not a follow-up task. An undocumented dashboard cannot be transitioned to support.

- Purpose, audience and intended decisions the dashboard supports
- Page inventory, including hidden and drill-through pages
- KPI inventory with links to approved definitions
- Source semantic model, model version and lineage
- Refresh schedule and expected data latency
- Row-level security roles and the audience each maps to
- Recorded performance test results and the conditions under which they were measured
- Known limitations, deliberate exclusions and approved exceptions
- Named report owner and named support owner

### 5.14 Transition to the Deliver Phase

Development is complete when the exit criteria in Section 8 are satisfied and the dashboard has been promoted to the test workspace for validation.

This sub-step closes the Develop phase for the dashboard asset and hands control to the Deliver phase.

- Dashboard deployed to the test workspace in accordance with APC-STD-006
- UAT scenarios prepared under APC-SOP-307 and available in APC-TMP-014
- Documentation Completeness Checklist (APC-CHK-011) satisfied
- UAT Readiness Checklist (APC-CHK-012) satisfied
- Develop Phase Exit Checklist (APC-CHK-013) signed by the approval authority
- Handoff to dashboard validation under APC-SOP-031

## 6. Inputs

- Approved Business Requirements Document (APC-TMP-201)
- Approved Technical Specification (APC-TMP-202)
- Approved Architecture Design (APC-TMP-203)
- Approved KPI Definitions (APC-TMP-013)
- Development-ready semantic model in the target workspace
- Semantic Model Documentation (APC-TMP-012)
- Assigned Fabric workspace, capacity and provisioned development access
- `[APC-XXX-000]` Analytics Design System — current published Figma release — **NEW**, to be created
- `[APC-XXX-000]` Power BI Report Theme File generated from the current design system release — **NEW**, to be created
- Declared target form factor — desktop, mobile, or both — from the Technical Specification
- Completed Development Readiness Checklist (APC-CHK-010)
- Confirmed audience groups and row-level security expectations

## 7. Outputs

- Developed dashboard deployed to the test workspace
- Report Documentation (APC-TMP-011)
- Recorded performance test results — free-form, captured within the report documentation
- Peer review record — free-form
- Development defect log (APC-TMP-016)
- UAT scenarios ready for execution (APC-TMP-014)
- Documented exceptions approved by an APC Representative — free-form
- Signed Develop Phase Exit Checklist (APC-CHK-013)

> **Draft note:** Three outputs are currently free-form. Decide whether performance results, the peer review record and exception approvals warrant their own templates, or whether they remain sections inside APC-TMP-011.

## 8. Entry & Exit Criteria

| | Criteria |
| --- | --- |
| Entry Criteria | Design phase outputs approved. KPI definitions approved. Semantic model available and passing its own development tests. Workspace, capacity and access provisioned. Report owner and support owner named. APC-CHK-010 complete. |
| Exit Criteria | All approved requirements and KPIs implemented and traceable to an approved definition. Naming and workspace placement conform to APC-STD-001 and APC-STD-006. Design system conformance confirmed at peer review, with the Analytics Design System `[APC-XXX-000]` release version recorded and any departures approved as exceptions. Mobile-optimized layout delivered where the declared form factor requires it, or desktop-only status documented. Performance targets met and results recorded. RLS tested for every defined role. Accessibility baseline met. Sensitivity label applied. Peer review complete with no open critical defects. Report documentation complete per APC-TMP-011. Dashboard deployed to the test workspace. APC-CHK-013 signed. |
| Approval Authority | BI Analytics Lead, with APC Representative concurrence for assets on the certification track. |

> **Draft note:** Every exit criterion above should be answerable yes or no by a reviewer without interpretation. "Accessibility baseline met" currently fails that test until Section 5.11 names a concrete baseline.

## 9. Related Procedures

| Procedure ID | Procedure Name |
| --- | --- |
| APC-SOP-303 | Semantic Model Development Procedure |
| APC-SOP-305 | KPI Development Procedure |
| APC-SOP-306 | Documentation Procedure |
| APC-SOP-307 | UAT Scenario Development Procedure |
| APC-SOP-031 | Dashboard Validation Procedure |
| APC-SOP-035 | Test Sign-Off Procedure |
| APC-SOP-041 | Production Deployment Procedure |

*All seven are existing register entries, reused as-is. Note that, like APC-SOP-304 itself, these are registered codes; whether each has been authored as a document has not been confirmed.*

## 10. Related Standards

| Standard ID | Standard Name |
| --- | --- |
| APC-STD-001 | Naming Standards |
| APC-STD-002 | Documentation Standards |
| APC-STD-003 | KPI Governance Standard |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-007 | Report Certification Standard |
| APC-STD-008 | Security & Access Standard |
| `[APC-XXX-000]` | Analytics Design System (Figma) — **NEW**, to be created; code to be assigned |
| `[APC-XXX-000]` | Power BI Report Theme File — **NEW**, to be created; code to be assigned |

*APC-STD-001 through APC-STD-008 are existing register entries, reused as-is. The two `[APC-XXX-000]` entries do not exist and must be created, with codes assigned. Note also that the register is inconsistent on three titles: APC-STD-007 appears as "Report Certification Standards" in the Design phase document and "Report Certification Standard" elsewhere; APC-STD-003 and APC-STD-004 vary between singular and plural in the same way. The singular form is used here pending confirmation.*

## 11. Related Templates

| Template ID | Template Name |
| --- | --- |
| APC-TMP-011 | Report Documentation Template |
| APC-TMP-012 | Semantic Model Documentation Template |
| APC-TMP-013 | KPI Definition Template |
| APC-TMP-014 | UAT Scenario Template |
| APC-TMP-016 | Defect Log Template |
| APC-TMP-202 | Technical Specification |

*All six are existing register entries, reused as-is.*

## 12. Related Checklists

| Checklist ID | Checklist Name |
| --- | --- |
| APC-CHK-010 | Development Readiness Checklist |
| APC-CHK-011 | Documentation Completeness Checklist |
| APC-CHK-012 | UAT Readiness Checklist |
| APC-CHK-013 | Develop Phase Exit Checklist |

*All four are existing register entries, reused as-is.*

## 13. Open APC Decisions

| Decision ID | Decision | Impact on This Document | Owner | Target Date |
| --- | --- | --- | --- | --- |
| `[APC-OD-###]` | Dashboard performance thresholds | Section 5.9 cannot be finalised. The 5s / 3s / 12-visual figures are proposals and must be set from observed performance on the target capacity. | BI Analytics Lead | *[YYYY-MM]* |
| `[APC-OD-###]` | Accessibility baseline | Section 5.11 references a baseline that does not exist at any APC-STD ID. Adopt WCAG 2.1 AA by reference, or commission a new standard. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Standard vs. procedure split | Determines whether the requirement content in 5.4, 5.6, 5.9 and 5.11 stays in this SOP or is extracted into a new Dashboard Development Standard `[APC-XXX-000 — NEW]` that this SOP then references. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Import-mode exception path | Section 5.5 names an exception route but no approval mechanism or record exists for it. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Design system asset class and code | Two new assets are referenced as `[APC-XXX-000]` and need codes assigned. The prior question is which class they belong to: a living Figma asset does not fit the document revision model that SOP, STD, TMP and CHK assume, so a new class may be required. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Design system ownership and licensing | The Analytics Design System `[APC-XXX-000]` requires a named owner, a Figma seat model, and confirmed licensing for the type family and icon set across desktop, web and mobile rendering. | Analytics Leadership | *[YYYY-MM]* |
| `[APC-OD-###]` | Design system delivery to developers | A Figma library alone is not consumable by a Power BI developer. Determines whether the system ships as a template .pbix, a theme JSON, or both, and how releases are distributed. | BI Analytics Lead | *[YYYY-MM]* |
| `[APC-OD-###]` | Baseline values in 5.6 | Every proposed value in 5.6 — canvas, grid, spacing, type scale, colour roles — is a starting proposal. Confirm or replace from brand guidelines and observed audience screen resolutions. | BI Analytics Lead | *[YYYY-MM]* |
| `[APC-OD-###]` | Status colour convention | Section 5.6.5 proposes red/green for unfavourable/favourable. Confirm whether to move to a blue/orange convention that does not depend on colour vision. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Mobile layout mandate | Section 5.6.13 permits desktop-only by documentation. Confirm whether a mobile-optimized layout is mandatory for all certified reports, mandatory for defined audiences such as field and executive users, or opt-in. | Analytics Leadership | *[YYYY-MM]* |
| `[APC-OD-###]` | Definitions page mandate | Section 5.6.7 proposes a Definitions / Help page archetype as mandatory for certified reports. This is a policy decision and would become an exit criterion. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Approved custom visuals list | Section 5.6.9 restricts custom and third-party visuals to an approved list. No such list currently exists. | Data Engineering Team | *[YYYY-MM]* |
| `[APC-OD-###]` | Scope of practitioner-developed content | Section 2 excludes uncertified personal-workspace content. Confirm whether a lightweight subset of this procedure should apply to ease later promotion. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Source control and PBIP mandate | Section 5.5 proposes PBIP as the standard development format with PBIX as fallback. Confirm tenant availability of Developer Mode and Git integration, and whether PBIP is mandated or encouraged. | Data Engineering Team | *[YYYY-MM]* |

## Revision History

| Issue Date | Rev | Change Description | Written / Revised By | Approved By |
| --- | --- | --- | --- | --- |
| *[YYYY-MM-DD]* | 0 | Initial brainstorm draft. Structure per APC-TMP-001. Not issued. | *[Name]* | *[Pending]* |

Remove the yellow highlight from previous versions of the document when making changes. Then highlight all new document changes in yellow for quick reference. An original issue document will have no highlights.
