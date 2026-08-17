# Production Deployment Procedure

**Procedure ID:** APC-SOP-041 | **Document Type:** Standard Operating Procedure (SOP) | **Process Owner:** BI Analytics Team (BI) & Data Engineering Team (DE) — joint | **Lifecycle Phase:** Phase 5 – Deploy (APC-PHASE-005) | **Status:** Draft — Initial Release, pending APC ratification

> **Editorial note:** This procedure was authored from the BI Center of Excellence's "CI/CD in Microsoft Fabric" working session (August 2026) and from Microsoft Learn — *Manage the Fabric deployment lifecycle*. It documents the four CI/CD deployment patterns available in Microsoft Fabric and the team's current thinking on when to use each one. The Deploy Phase Procedure (APC-AP-500, Section 12) lists **APC-OD-002: CI/CD Strategy** as an open APC decision — "a formal CI/CD strategy and deployment governance model have not yet been approved." This SOP represents the COE BI team's working recommendation and should be treated as the working draft that resolves that open decision, not as ratified governance, until the APC formally approves it.

[← Back to documentation index](../index.md)

---

## 1. Purpose

The purpose of this procedure is to define a repeatable, governed approach for deploying Microsoft Fabric items — data pipelines, lakehouses, warehouses, semantic models, reports, and dashboards — from development through Test into Production using Continuous Integration and Continuous Deployment (CI/CD).

CI/CD in Fabric is really two distinct problems that are often conflated:

- **Continuous Integration ("how do changes come together?")** — the process of bringing changes from different developers into one shared place, typically a Git repository, and integrating them with each other. In Fabric, Git integration (feature branches, workspaces) is the CI story.
- **Continuous Deployment ("how do changes ship safely?")** — taking the integrated changes through Dev → Test → Prod so teams can trust that what worked in one stage keeps working in the next. In Fabric, deployment pipelines and the Fabric CI/CD APIs/library are the CD story.

A complete deployment process needs both. This procedure covers the selection of an appropriate deployment pattern and the mechanics of executing a deployment once a pattern is selected. It complements, and does not replace, APC-SOP-040 (Release Management), APC-SOP-042 (Production Validation), and APC-SOP-045 (Operational Handoff).

### 1.1 Why Fabric CI/CD Is Not Just Software CI/CD

Data platforms move more than code, and that is what makes deployment harder than a typical application release:

- **Metadata, not just code** — a Lakehouse or Warehouse has no single project file describing its structure the way a SQL database project does; schema is often implicit inside the item definition itself.
- **Data has to move too** — beyond deploying code, reference and lookup tables frequently need to be re-pushed into every environment, not just the objects that hold them.
- **IDs bind items together** — connections, lakehouse references, and workspace IDs are baked into item definitions and must be re-bound or parameterized for every stage.

| What Has to Move, Stage to Stage | Traditional Software | Fabric Data Platform |
| --- | --- | --- |
| Code | Yes | Yes |
| Schema / metadata | Usually a project file | Often implicit in items |
| Reference data | Rarely | Frequently |
| Item / connection IDs | Not applicable | Must be re-bound |

## 2. Scope

This procedure applies to promotion of all APC-governed Fabric items into Production, including:

- Data pipelines, notebooks, and Spark job definitions
- Lakehouses and Warehouses (schema and, where applicable, reference data)
- Semantic models
- Reports and dashboards
- Fabric environments, connections, and other supporting items

This procedure applies to activities involving:

- BI Analytics Team (BI) — semantic models, reports, dashboards
- Data Engineering Team (DE) — pipelines, lakehouses, warehouses
- APC Representatives
- Analytics Leadership
- Support Owners

This procedure does not cover the business/test sign-off decision to authorize a release (APC-SOP-035, Test Sign-Off Procedure), post-deployment production validation (APC-SOP-042), release communication (APC-SOP-043), or hypercare (APC-SOP-044) — each of those is governed separately.

## 3. Roles & Responsibilities

#### BI Analytics Team (BI)

Responsible for:

- Deploying semantic models, reports, and dashboards through the selected CI/CD pattern
- Maintaining Git branch hygiene and pull requests for BI-owned items
- Re-validating RLS/OLS and connections after promotion

#### Data Engineering Team (DE)

Responsible for:

- Deploying pipelines, lakehouses, warehouses, and supporting data engineering items
- Managing reference/lookup data movement between environments
- Managing parameterization of connections and workspace IDs across stages

#### APC Representatives

Responsible for:

- Reviewing deployment pattern selection for consistency with APC guidance
- Reviewing exceptions where a team proposes a pattern outside its normal profile

#### Analytics Leadership

Responsible for:

- Approving adoption of code-first patterns (Items APIs, ISV Multi-Tenant) for teams without established Git/DevOps skills
- Resolving escalated deployment issues or pattern disputes

#### Support Owner

Responsible for:

- Confirming operational readiness before Production deployment
- Accepting the deployed asset into operational support per APC-SOP-045

## 4. Definitions

| Term | Definition |
| --- | --- |
| CI/CD | Continuous Integration / Continuous Deployment — combining developer changes and reliably promoting the integrated result through Dev, Test, and Prod. |
| Git Integration | Fabric's mechanism for connecting a workspace to a Git repository branch, enabling version control and definition-based deployment. |
| Definition-Based Deployment | Deployment driven by an item's underlying definition files (as stored in Git), rather than by copying a live workspace item directly. |
| Fabric Items APIs | The Fabric REST APIs (including the Bulk Import Item Definitions API) used to create, update, and deploy item definitions programmatically. |
| fabric-cicd | A Python library that wraps the Fabric Items APIs in configurable, YAML-driven deployment scripts. |
| Fabric Deployment Pipelines | Fabric's native, low-code feature for promoting items directly between linked Dev, Test, and Prod workspaces. |
| Build Environment | An intermediate environment used in code-first deployment to run tests and transform/parameterize item definitions before they are deployed to a target stage. |
| Gitflow | A branching strategy using a dedicated, persistent branch per environment/stage (e.g., dev, test, main). |
| Trunk-Based Development | A branching strategy using a single shared branch (e.g., main), with short-lived feature branches merged frequently. |
| Service Principal | A non-human Microsoft Entra identity used to run automated deployments, so releases are not tied to any one person's account or credentials. |
| Item/Connection ID Binding | The process of re-mapping or parameterizing connection strings, lakehouse references, and workspace IDs so an item works correctly in the target stage's environment. |
| ISV Multi-Tenant Pattern | A deployment pattern for Independent Software Vendors that fans a single, centrally developed solution out to many isolated per-customer Production workspaces. |
| Reference/Lookup Data | Small, relatively static tables (e.g., mapping or configuration tables) that must be re-populated in each environment rather than only having their structure deployed. |

## 5. Procedure

### 5.1 Confirm Deployment Authorization

1. Confirm that Deploy authorization has been received from the Deliver phase, per APC-AP-400: business sign-off, test sign-off, and approved solution components are available.
2. Confirm a named Support Owner has been identified to accept the asset into operations, consistent with APC-SOP-045.

### 5.2 Select the CI/CD Deployment Pattern

1. Select a deployment pattern for the asset using the decision guidance in Section 6. Consider the team's Git/DevOps maturity, environment complexity, the number of downstream workspaces, and whether item definitions require stage-specific transformation.
2. As a starting point:
   - Teams new to Git/DevOps, or working primarily with Power BI semantic models and reports, should default to **Pattern 3 — Fabric Deployment Pipelines**.
   - Teams with established Git/DevOps skills and a need for custom, stage-specific item transformations should use **Pattern 1 — Git Integration** or **Pattern 2 — Fabric Items APIs**.
   - Solutions distributed to many isolated customer workspaces (ISV/SaaS models) should use **Pattern 4 — ISV Multi-Tenant CI/CD**.
3. Document the selected pattern and rationale. Most real deployments end up hybrid — for example, Git integration for source control combined with deployment pipelines for promotion — so document each mechanism in use, not just one.
4. Escalate any proposed departure from a team's normal pattern to an APC Representative for review.

> **Team practice note:** "If you have strong technical capabilities, look at the Fabric CI/CD library. If you're lacking those skills, deployment pipelines would be my pick." — Alexey, BI COE working session, August 2026. "Start small — use deployment pipelines first, then grow into code-first options as your needs get more complex." — Anton, BI COE working session, August 2026.

### 5.3 Prepare the Release

1. Develop in an isolated environment — a feature branch and workspace, or a fixed personal workspace switched to a feature branch — never directly against a shared Dev branch or workspace.
2. Open a pull request to merge completed work back into the shared branch that triggers the team's release pipeline.
3. Ensure the change has passed applicable development testing (APC-AP-300, Section 5.7) before the pull request is opened.

![Diagram showing how the development process works.](https://learn.microsoft.com/en-us/fabric/cicd/media/manage-deployment/development-process.png)

*Diagram source: Microsoft Learn — [Manage the Fabric deployment lifecycle](https://learn.microsoft.com/en-us/fabric/cicd/manage-deployment).*

### 5.4 Promote Through Environments (Dev → Test → Prod)

1. Promote the merged change through Dev, Test, and Prod using the mechanism defined by the selected pattern (Section 6): Fabric Git APIs, the Fabric Items APIs / fabric-cicd, or the Fabric Deployment Pipelines API/UI.
2. Do not skip the Test stage. Validate in Test before promoting to Prod, even for patterns that technically allow a direct Dev-to-Prod promotion.
3. For Gitflow-style patterns, obtain a change from Dev to Test/Prod on its own timeline by cherry-picking the relevant commits; confirm no dependent change is left behind. Where a team regularly needs to merge backward from Prod to Dev just to keep branches in sync, treat that as a signal the pattern may not fit the team's release cadence and revisit Section 5.2.

### 5.5 Manage Item References and Connections Across Stages

1. Identify every connection, lakehouse reference, and workspace ID embedded in the item definitions being promoted.
2. Re-bind or parameterize each reference for the target stage before or during deployment, using deployment rules (Fabric Deployment Pipelines), build-environment transformation scripts (Items APIs / fabric-cicd), or environment-specific Git branches (Git Integration), as appropriate to the selected pattern.
3. Maintain and grow the dependency-mapping logic as new item types are added; this is an ongoing cost of code-first patterns (Options 2 and 4), not a one-time setup task.

### 5.6 Move Reference and Lookup Data

1. Identify reference and lookup tables required by the deployed items that are not created by the deployment itself (for example, mapping or configuration tables).
2. Re-push required reference data into the target environment as part of the deployment, using the team's established data movement process. Confirm this step explicitly for every deployment — unlike application code, reference data does not deploy itself.

### 5.7 Secure Production Deployment Credentials

1. Configure production deployments — whether triggered via CI/CD pipeline or API — to run under a service principal, not a personal user account.
2. Where a deployment currently runs under a personal account, raise this as a remediation item; a credential tied to one person breaks production when that person changes their password or leaves the company.
3. Where deployment is triggered via the Fabric Deployment Pipelines API rather than the UI, confirm the deploying identity has the intended scope — API-triggered deployment promotes the entire workspace and cannot be scoped to individual items the way a manual UI deployment can.

### 5.8 Validate the Production Deployment

1. Confirm the deployment completed successfully in the target workspace (pipeline run status, deployment history, or API response).
2. Hand off to APC-SOP-042 (Production Validation Procedure) to perform functional, data, and access validation of the deployed asset in Production.

### 5.9 Close and Document the Deployment

1. Record the deployment (pattern used, items promoted, date, and deploying identity) per APC-TMP-020, Deployment Plan Template.
2. Confirm operational ownership transition per APC-SOP-045 before closing the deployment record.

## 6. Fabric CI/CD Deployment Patterns

Microsoft Fabric supports four deployment patterns. Most organizations combine more than one in a hybrid approach. Patterns 1–3 are documented by Microsoft as the primary options; Pattern 4 is a variant of Pattern 2 for multi-tenant (ISV/SaaS) scenarios. Diagrams are reproduced from Microsoft Learn — [Manage the Fabric deployment lifecycle](https://learn.microsoft.com/en-us/fabric/cicd/manage-deployment); refer to that page for the current, canonical versions.

#### Pattern 1 — Git Integration (Definition-Based Deployment)

Git is the single source of truth. A dedicated Git branch exists per stage (Gitflow — dev, test, main/prod); the Fabric Git API syncs each branch straight into its own workspace. Developers branch out into a feature workspace (or a fixed personal workspace switched to a feature branch) and open a pull request to merge back.

![Diagram showing how the Git based deployment works.](https://learn.microsoft.com/en-us/fabric/cicd/media/manage-deployment/git-based-deployment.png)

*Diagram source: Microsoft Learn — Manage the Fabric deployment lifecycle.*

- **Source of truth:** Git repository
- **Branching model:** Gitflow (dedicated branch per stage)
- **Best for:** teams that want Git as the definitive source of truth and already follow a Gitflow-style branching strategy.
- **Watch out for:** getting a change from Dev to Test/Prod on its own timeline usually means cherry-picking commits, which risks missing a dependency; merging backward from Prod to Dev to keep branches in sync gets tedious; item/connection ID references often need custom logic to stay correct across branches.

#### Pattern 2 — Fabric Items APIs (Code-First Automation)

A single Main branch (trunk-based). A build pipeline spins up a build environment, runs tests, and rewrites connection IDs, lakehouse IDs, and parameters for the target stage. A release pipeline then uploads the transformed items to Dev, Test, and Prod using the Fabric Items APIs. The `fabric-cicd` Python library wraps this in configurable, YAML-driven deployments; the Bulk Import Item Definitions API handles dependency ordering.

![Diagram showing the flow of Git based deployment using build environments.](https://learn.microsoft.com/en-us/fabric/cicd/media/manage-deployment/git-build.png)

*Diagram source: Microsoft Learn — Manage the Fabric deployment lifecycle.*

- **Source of truth:** Git (single Main branch)
- **Branching model:** Trunk-based
- **Best for:** teams with strong Git/DevOps skills, greenfield projects, or work needing custom environment-specific transformations that deployment pipelines cannot express.
- **Watch out for:** requires standing up real build environments and scripting; the team owns dependency-mapping logic that grows with every new item type; deploys should run as a service principal, not a personal account (Section 5.7).

#### Pattern 3 — Fabric Deployment Pipelines (Native, Low-Code)

Fabric's native UI moves items directly between linked Dev, Test, and Prod workspaces with deployment rules and automatic dependency binding. Deployment can also be triggered from Azure DevOps or GitHub Actions via the Deployment Pipelines API once manual clicking no longer scales.

![Diagram showing the flow of Git based deployment using deployment pipelines.](https://learn.microsoft.com/en-us/fabric/cicd/media/manage-deployment/deployment-pipelines.png)

*Diagram source: Microsoft Learn — Manage the Fabric deployment lifecycle.*

- **Source of truth:** Fabric workspace (Git connects only through the Dev stage, if used at all)
- **Branching model:** Trunk-based
- **Best for:** Power BI–heavy workspaces (semantic models, reports), teams without deep Git/DevOps skills yet, and anyone who wants deployment history visible in the Fabric UI. This is the recommended starting pattern for most BI teams.
- **Watch out for:** UI-triggered deploys run under personal credentials by default and should be moved to a service principal for Production; API-triggered deployment promotes the entire workspace rather than a selective set of items; the linear, workspace-to-workspace structure is less flexible than code-first transformation.

#### Pattern 4 — ISV Multi-Tenant CI/CD (Fan-Out Deployment)

The same trunk-based, Items APIs mechanism as Pattern 2, scoped to a multi-tenant architecture: one workspace per customer. Development and testing are centralized; release then fans out in parallel to each customer's Production workspace with customer-specific parameters and configuration.

![Diagram showing the flow of Git based deployment for ISVs.](https://learn.microsoft.com/en-us/fabric/cicd/media/manage-deployment/software-vendors.png)

*Diagram source: Microsoft Learn — Manage the Fabric deployment lifecycle.*

- **Source of truth:** Git (single Main branch)
- **Branching model:** Trunk-based
- **Best for:** ISVs and SaaS builders shipping the same Fabric solution to many customers, each in an isolated workspace.
- **Watch out for:** workspace overhead multiplies quickly with true multi-tenancy; per-customer parameter management becomes its own discipline; requires the same ID/reference-mapping rigor as Pattern 2, at greater scale.

#### Comparison at a Glance

| | 1 · Git Integration | 2 · Items APIs | 3 · Deployment Pipelines | 4 · ISV Multi-Tenant |
| --- | --- | --- | --- | --- |
| Source of truth | Git repository | Git (Main) | Fabric workspace | Git (Main) |
| Branching model | Gitflow (per-stage branches) | Trunk-based | Trunk-based | Trunk-based |
| Deployment mechanism | Fabric Git APIs | fabric-cicd / Bulk Import API | Deployment Pipelines API | Item APIs (per customer) |
| Config per stage | Separate branches | Build-env scripts | Rules & auto-binding | Per-customer parameters |
| Best for | Gitflow teams, Git-first shops | Complex, custom transformations | Low-code, Fabric-native teams | ISV / SaaS, many tenants |

## 7. Inputs

The following inputs may initiate this procedure:

- Deployment Authorization
- Business Sign-Off and Test Sign-Off
- Approved Solution Components (items ready for promotion)
- Selected CI/CD Deployment Pattern
- Reference/Lookup Data required by the target environment

## 8. Outputs

This procedure may produce:

- Promoted Fabric Items in Production
- Deployment Record (pattern, items, date, deploying identity)
- Updated Connection/Parameter Bindings per stage
- Deploy Authorization for APC-SOP-042 (Production Validation)

## 9. Related Procedures

| Procedure ID | Procedure Name |
| --- | --- |
| APC-SOP-040 | Release Management Procedure |
| APC-SOP-042 | Production Validation Procedure |
| APC-SOP-043 | Release Communication Procedure |
| APC-SOP-044 | Hypercare Procedure |
| APC-SOP-045 | Operational Handoff Procedure |

## 10. Related Standards

| Standard ID | Standard Name |
| --- | --- |
| APC-STD-002 | Documentation Standards |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-007 | Report Certification Standard |
| APC-STD-008 | Security & Access Standard |

## 11. Related Templates

| Template ID | Template Name |
| --- | --- |
| APC-TMP-020 | Deployment Plan Template |
| APC-TMP-021 | Production Validation Template |

## 12. Related Checklists

| Checklist ID | Checklist Name |
| --- | --- |
| APC-CHK-020 | Deployment Readiness Checklist |
| APC-CHK-021 | Production Validation Checklist |
| APC-CHK-023 | Deploy Phase Exit Checklist |

## 13. Open APC Decisions

The following unresolved APC decisions may impact execution of this procedure.

#### APC-OD-002: CI/CD Strategy (carried from APC-AP-500)

A formal, APC-ratified CI/CD strategy and deployment governance model has not yet been approved. This procedure documents the four patterns available in Fabric and the COE BI team's working recommendations (Section 6) as an interim reference pending formal ratification.

#### APC-OD-001: Environment Management Strategy (carried from APC-AP-500)

Standards governing DEV, TEST, and PROD environments and workspace strategy have not yet been finalized; this affects how deployment pipelines and stage branches are provisioned under every pattern in Section 6.

#### APC-SOP-041-OD-001: Service Principal Provisioning Standard

A standard process for provisioning, scoping, and rotating the service principals referenced in Section 5.7 has not yet been established.

## Revisions

| Issue Date | Rev | Change | Written / Revised by |
| --- | --- | --- | --- |
| 2026-08-17 | 0 | Initial Release — authored from the BI Center of Excellence's "CI/CD in Microsoft Fabric" working session (August 2026) and Microsoft Learn: Manage the Fabric deployment lifecycle. |  |
|  |  |  |  |

Remove the yellow highlight from previous versions of the document when making changes. Then highlight all new document changes in yellow for quick reference. An original issue document will have no highlights.
