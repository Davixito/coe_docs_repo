# Architecture Design Procedure

**Procedure ID:** APC-SOP-203 | **Document Type:** SOP | **Lifecycle Phase:** Phase 2 – Design (APC-PHASE-002)

> ## ⚠️ DRAFT — NOT YET ISSUED
>


[← Back to documentation index](../index.md)

---

## Document Control

| Field | Value | Field | Value |
| --- | --- | --- | --- |
| Document ID | APC-SOP-203 | Revision | 0 |
| Document Title | Architecture Design Procedure | Status | **Draft** |
| Document Type | SOP | Issue Date | *[YYYY-MM-DD]* |
| Document Owner | *[Name], Data Engineering Lead* | Next Review | *[YYYY-MM-DD]* |
| Approver | *[Name], Analytics Leadership]* | Review Cycle | Annual |
| Applies To | Data Engineering Team; BI Analytics Team designing architecture for APC-governed initiatives | Classification | Internal |

## 1. Purpose

The purpose of this procedure is to define how solution and data architecture — most centrally, the medallion lakehouse architecture used across APC-governed initiatives — is designed, documented, and approved during the Design phase, before development begins.

Architecture decisions made here determine how source data is landed, validated, cleansed, conformed, historized, and curated long before a semantic model or dashboard is ever built. A change made after Develop is underway is materially more expensive than the same decision made at Design, because it can require reprocessing already-built Bronze, Silver, and Gold assets. This procedure exists to make those decisions explicit, reviewed, and recorded before that cost is incurred.

This procedure is owned and executed by the Data Engineering Team, in coordination with the BI Analytics Team, who consume the Gold layer this procedure produces the design for.

## 2. Scope

This procedure applies to:

- Design of the source-to-Gold data architecture for new APC-governed initiatives, including the Bronze, Silver, and Gold layers of the medallion lakehouse
- Selection of ingestion mechanism per source system (physical copy vs. virtual/zero-copy shortcut, CDC, full load vs. incremental)
- Design of the Silver layer refresh strategy, including incremental / Change Data Feed (CDF) processing
- Design of historization (SCD) requirements at the Silver layer
- Design of the Gold layer curation pattern (OBT vs. Mart, business rule placement)
- Production of the Architecture Design output (APC-TMP-203) submitted for Design phase exit

This procedure applies to activities involving:

- Data Engineering Team (DE) — process owner
- BI Analytics Team (BI) — Gold layer consumer
- APC Representatives
- Business Stakeholders
- Analytics Leadership

**Exclusions**

- Semantic model design and development on top of Gold layer curated data — covered by APC-SOP-205 (Semantic Model Design Procedure, Design phase) and APC-SOP-303 (Semantic Model Development Procedure, Develop phase).
- Physical build of pipelines, transformations, and Delta tables against an approved architecture — covered by APC-SOP-301 (Data Pipeline Development Procedure).
- Data validation testing of pipeline output — covered by APC-SOP-302 (Data Validation Procedure).
- Dimensional/data modeling of Gold layer facts and dimensions — covered by APC-SOP-204 (Data Modeling Procedure).

## 3. Roles & Responsibilities

#### Data Engineering Team (DE) — Process Owner

Responsible for:

- Designing the source-to-Gold architecture for each new initiative, including layer design, ingestion mechanism selection, and refresh strategy
- Documenting the architecture using APC-TMP-203 (Architecture Design Template)
- Selecting and justifying the ingestion mechanism per source system (shortcut, zero-copy, CDC, mirroring, export)
- Designing the Silver layer incremental / CDF refresh strategy and historization (SCD) requirements
- Designing the Gold layer curation pattern and business-rule placement
- Presenting the architecture for review and carrying open items through to resolution

#### BI Analytics Team (BI)

Responsible for:

- Confirming that the proposed Gold layer design (OBTs and Marts) satisfies downstream semantic modeling and reporting needs
- Flagging gaps between the proposed architecture and known consumption requirements before approval

#### Business Stakeholder

Responsible for:

- Confirming data latency, historization, and auditability requirements that inform Silver/Gold design decisions
- Confirming source system access and any constraints on ingestion mechanism (e.g., licensing limits on CDC or mirroring)

#### APC Representatives

Responsible for:

- Reviewing the proposed architecture against APC-STD-005 (Medallion Architecture Standard) and APC-STD-006 (Fabric Architecture Standard)
- Reviewing and tracking open architecture decisions raised during design
- Approving architecture exceptions (e.g., deviations from the standard layer pattern)

#### Analytics Leadership

Responsible for:

- Approving this procedure and any revision to it
- Resolving escalated architecture decisions that cannot be settled at the team level

## 4. Definitions

| Term | Definition |
| --- | --- |
| Medallion Architecture | A layered lakehouse design pattern — Bronze, Silver, Gold — that progressively filters, cleans, and curates data from raw source form to consumption-ready form. |
| Bronze Layer | The raw-copy layer. Source data is landed with minimal transformation, subject to technical integrity, completeness, lineage, and schema-drift checks. |
| Silver Layer | The cleansed and conformed layer. Bronze data is filtered, standardized, validated, and (lightly) enriched, and — where required — historized. |
| Gold Layer | The consumption-ready layer. Silver tables are joined, harmonized, and denormalized into curated, application-specific data (OBTs and Marts). |
| Landing Zone | An intermediate storage location (e.g., blob file store) where source extracts are deposited before Bronze ingestion, used where a source cannot be shortcut directly. |
| Raw Shortcut | A virtual, zero-copy reference to source data (e.g., Parquet, Excel, CSV) that avoids physically duplicating the data into Bronze storage. |
| Zero-Copy / Virtual Flow | A data flow that references source data in place rather than physically copying it, shown as a dashed line on the architecture diagram. |
| Validated Delta Table | The Bronze-layer Delta Lake table produced after technical integrity, completeness, lineage, schema-drift, and ingestion audit checks are applied to a raw ingest. |
| CDC (Change Data Capture) | A mechanism that captures and propagates only inserted, updated, or deleted source records rather than requiring a full reload. |
| Mirrored Database | A continuously synchronized, read-only copy of a source database (e.g., via database mirroring) used as an alternative to CDC-based extraction. |
| Cleaned Table | A Silver-layer table with irrelevant, invalid, or duplicate data removed; missing values handled; formatting and errors corrected. |
| Conformed Table | A Silver-layer table standardized against enterprise terminology, units, data types, and cross-source validation rules, so equivalent concepts from different sources align. |
| Historized Table (SCD) | A Silver-layer table that preserves attribute history using a Slowly Changing Dimension (SCD) pattern, typically Type 2. |
| Curated Data | Gold-layer output produced by joining, harmonizing, and denormalizing Silver tables into application-specific data assets. |
| OBT (One Big Table) | A flattened, denormalized Gold-layer table designed for simple, fast, single-purpose reporting. |
| Mart | A subject/domain-scoped, dimensionally modeled grouping of facts and conformed dimensions for a specific business function. |
| Change Data Feed (CDF) | The Delta Lake feature that exposes row-level changes (inserts, updates, deletes) between two table versions, used to drive incremental Silver processing. |
| Incremental Processing | Processing only the data affected by a change — identifying what changed, determining everything that change affects, and recomputing only that scope — rather than reprocessing a full table on every run. |
| Business Key | The natural, source-system identifier for an entity (as distinct from a surrogate key), used to determine which downstream records are affected by an incoming change. |

## 5. Procedure

### 5.1 Confirm Design Readiness

1. Confirm Discovery/Define phase outputs are available: approved project charter, high-level requirements, and known source systems for the initiative.
2. Identify every source system in scope and confirm access (connectivity, credentials, licensing) for each.
3. Confirm known data latency, historization, and auditability requirements with the business stakeholder before layer design begins.

### 5.2 Define Source Systems and Landing Strategy

1. For each source system, determine whether it can be connected to directly (e.g., via a native shortcut or mirroring capability) or whether it requires an intermediate landing zone (e.g., a blob file store) before Bronze ingestion.
2. Select the ingestion mechanism per source using the decision guidance in Section 6.2. Document the choice and its justification for each source.
3. Where a zero-copy / virtual shortcut is selected, explicitly evaluate whether the data should nonetheless be persisted into Bronze storage rather than only referenced, for performance reasons — see Open Decision in Section 14.

### 5.3 Design the Bronze Layer

1. Design the raw-copy ingestion for each source, producing a Validated Delta table per source.
2. Define the metadata and quality checks applied at ingestion: technical integrity, completeness, lineage, schema-drift, and ingestion audit checks.
3. Determine whether each source is ingested incrementally or as a full load, defaulting to incremental wherever the source supports it.
4. For sources requiring historical snapshots for auditability or historization (e.g., mirrored databases), define the snapshot capture approach at the Bronze layer.

> **Best practice:** Default to incremental ingestion. A full load should be a deliberate, documented exception (e.g., a small reference/mapping source), not the default path.

### 5.4 Design the Silver Layer and Refresh Strategy

1. Design the Cleaned, Conformed, and — where required — Historized (SCD) stages for each Bronze source, per the transformations in Section 6.3.
2. Select and document the Silver refresh strategy. The APC-preferred pattern is incremental processing via Change Data Feed (CDF), applying the six steps below rather than a full Silver rebuild on every run:
   1. Read new / changed Bronze records.
   2. Identify affected business keys or partitions.
   3. Pull enough related data to correctly recalculate those keys.
   4. Run all Silver transformations on that subset.
   5. MERGE the results into the existing Silver table.
   6. Save the processed Bronze version / batch.
3. For each table requiring historization, confirm the SCD type (Type 2, by default) and document what triggers a new historical row.
4. Confirm the intended relationship between the Silver and Bronze layers — see Open Decision in Section 14; the source guidance for this step was incomplete at time of drafting and needs process-owner confirmation before this step is finalized.

> **Best practice:** Recompute only the scope affected by a change — reprocessing an entire Silver table for a small incoming Bronze delta wastes compute and extends refresh windows unnecessarily.

### 5.5 Design the Gold Layer

1. Design the join, harmonization, and denormalization logic required to produce curated data from Silver, including business rules, calculations, enrichments, corrections, and aggregations.
2. Determine the target consumption pattern(s) for the curated data — OBTs, Marts, or both — per the criteria in APC-SOP-303 Section 5.1 (OBT vs. Mart decision), coordinating with the BI Analytics Team.
3. Confirm the curated data is application-specific (i.e., shaped for its consuming semantic layer) rather than a generic restatement of Silver.

### 5.6 Produce the Architecture Design Document

1. Document the completed architecture — source systems, landing zone, ingestion mechanism per source, Bronze/Silver/Gold design, and refresh strategy — using APC-TMP-203 (Architecture Design Template).
2. Include an architecture diagram consistent with the reference pattern in Section 6.
3. Log every open item or unconfirmed decision explicitly rather than leaving it implicit in the diagram or document.

### 5.7 Architecture Review and Approval

1. Submit the Architecture Design Document for review against APC-STD-005 (Medallion Architecture Standard) and APC-STD-006 (Fabric Architecture Standard).
2. Resolve or formally log every open item raised during design as an APC Open Decision (Section 14) if it cannot be resolved before review.
3. Obtain sign-off per APC-CHK-203 (Architecture Validation Checklist).

### 5.8 Transition to Develop Phase

1. Confirm the approved architecture, with no unresolved blocking open items, is available to the Develop phase team.
2. Hand off to APC-SOP-301 (Data Pipeline Development Procedure) for build against the approved design.

## 6. Medallion Lakehouse Reference Architecture

This section documents the APC reference pattern for the medallion lakehouse architecture — Source systems → Bronze (raw) → Silver (cleansed & conformed) → Gold (curated) — referenced throughout Section 5. It reflects the architecture diagram supplied for this update, redesigned for readability from an earlier working sketch; content is preserved from that sketch and two items remain open pending confirmation (Section 14).

![Medallion Lakehouse Architecture: source systems (SAP Datasphere current and BDC, SAP HANA, Oracle DB, SharePoint Mappings) flow through a landing zone and Bronze layer (ingestion mechanism, Validated Delta table) into a Silver layer (Cleaned, Conformed, Historized/SCD tables) and a Gold layer (Curated data feeding OBTs and Marts). A callout at top describes the six-step CDF incremental refresh strategy for Silver.](assets/apc-sop-203/medallion-lakehouse-architecture.png)

### 6.1 Layer Overview

| Layer | Purpose |
| --- | --- |
| Bronze — raw copies | Metadata and quality checks for technical integrity, completeness, lineage, schema drift, and ingestion audit checks. Data is ingested incrementally where possible, otherwise as a full load. |
| Silver — filtered, clean, augmented | Cleanse, standardize, and (slightly) enrich source data: remove irrelevant/invalid/duplicate data, handle missing values, trim spaces and correct errors, standardize formats/terminology/units/data types, validate ranges/uniqueness/parent-child relationships, detect anomalies and outliers, mask sensitive data, apply master data management, conform data across source systems, and cross-validate SharePoint mapping data, among other checks. |
| Gold — modeled for consumption | Incorporates numerous complex business rules and extensive post-processing: calculations, enrichments, application-specific optimizations, corrections, transformations, aggregations, and more. Sources are joined, harmonized, and denormalized where required. Data is application-specific — i.e., semantic layers. |

### 6.2 Source Systems and Ingestion Mechanisms

| Source System | Landing Zone | Ingestion Mechanism | Flow Type | Bronze Output |
| --- | --- | --- | --- | --- |
| SAP Datasphere (current) | Blob file store | Raw shortcut (Parquet) | Physical | Validated Delta table |
| SAP Datasphere (BDC) | — | Zero-copy shortcut | Virtual / zero-copy ¹ | Validated Delta table |
| SAP HANA | — | Raw export (Parquet) | Physical | Validated Delta table |
| Oracle DB | — | Mirrored Oracle Database (via CDC) ² | Physical | Validated Delta table |
| SharePoint Mappings | — | Raw shortcut (Excel, CSV, …) ² | Virtual / zero-copy | Validated Delta table |

¹ **Open item — under consideration:** always persisting this data (rather than only referencing it) for greater performance, even on the zero-copy path. See Section 14.
² Historical snapshots are captured where required for auditability / historization.

### 6.3 Silver Layer Refresh Strategy — Change Data Feed (CDF)

Incremental processing = identify changes + determine everything affected + recompute only that affected scope.

1. Read new / changed Bronze records.
2. Identify affected business keys or partitions.
3. Pull enough related data to correctly recalculate those keys.
4. Run all Silver transformations on that subset.
5. MERGE the results into the existing Silver table.
6. Save the processed Bronze version / batch.

### 6.4 Gold Layer Consumption

Curated Gold data branches into two consumption forms, consistent with the OBT vs. Mart guidance in APC-SOP-303 Section 5.1:

- **OBTs** — flattened, single-purpose tables for simple, fast reporting.
- **Marts** — dimensionally modeled, subject-scoped groupings of facts and conformed dimensions for reuse across a business domain.

### 6.5 Diagram Legend

| Symbol | Meaning |
| --- | --- |
| Solid line | Physical data flow |
| Dashed line | Virtual / shortcut flow (no data duplication) |
| Orange marker | Bronze — raw |
| Blue/grey marker | Silver — cleansed |
| Yellow marker | Gold — curated |
| Red numbered marker | Footnote — see layer notes above |
| Purple "i" marker | Open item — needs confirmation |

## 7. Inputs

- Approved Discovery / Define Phase Outputs (project charter, high-level requirements)
- Confirmed source system inventory and access
- Business latency, historization, and auditability requirements
- APC-STD-005 Medallion Architecture Standard *(not yet authored — see Section 14)*
- APC-STD-006 Fabric Architecture Standard

## 8. Outputs

- Architecture Design Document (APC-TMP-203)
- Architecture diagram, per the reference pattern in Section 6
- Documented ingestion mechanism decision per source system
- Documented Silver refresh strategy and historization (SCD) requirements
- Logged open architecture decisions (Section 14 and/or new APC-OD entries)
- Signed APC-CHK-203 (Architecture Validation Checklist)

## 9. Entry & Exit Criteria

| | Criteria |
| --- | --- |
| Entry Criteria | Discovery/Define phase outputs approved. Source systems identified and access confirmed. Business latency, historization, and auditability requirements gathered. |
| Exit Criteria | Architecture Design Document (APC-TMP-203) complete, covering source-to-Gold design for every in-scope source. Ingestion mechanism justified per source. Silver refresh strategy and historization approach documented. Architecture reviewed against APC-STD-005 and APC-STD-006. No unresolved *blocking* open items; non-blocking items logged as APC Open Decisions. APC-CHK-203 signed. |
| Approval Authority | Data Engineering Lead, with APC Representative concurrence. |

## 10. Related Procedures

| Procedure ID | Procedure Name |
| --- | --- |
| APC-SOP-201 | Business Requirements Development Procedure |
| APC-SOP-202 | Technical Specification Procedure |
| APC-SOP-204 | Data Modeling Procedure |
| APC-SOP-205 | Semantic Model Design Procedure |
| APC-SOP-301 | Data Pipeline Development Procedure |
| APC-SOP-303 | Semantic Model Development Procedure |

## 11. Related Standards

| Standard ID | Standard Name |
| --- | --- |
| APC-STD-001 | Naming Standards |
| APC-STD-002 | Documentation Standards |
| APC-STD-004 | Data Modeling Standard |
| APC-STD-005 | Medallion Architecture Standard *(not yet authored)* |
| APC-STD-006 | Fabric Architecture Standard |
| APC-STD-008 | Security & Access Standard |

## 12. Related Templates

| Template ID | Template Name |
| --- | --- |
| APC-TMP-203 | Architecture Design Template |

## 13. Related Checklists

| Checklist ID | Checklist Name |
| --- | --- |
| APC-CHK-203 | Architecture Validation Checklist |

## 14. Open APC Decisions

| Decision ID | Decision | Impact on This Document | Owner | Target Date |
| --- | --- | --- | --- | --- |
| `[APC-OD-###]` | Persist vs. reference on the zero-copy path | Section 6.2, footnote 1: whether SAP Datasphere (BDC) data ingested via zero-copy shortcut should always be persisted into Bronze storage rather than only referenced, for greater performance. Currently "under consideration" per the source diagram, unresolved. | Data Engineering Lead | *[YYYY-MM]* |
| `[APC-OD-###]` | Intended Silver/Bronze relationship wording | Section 5.4, step 4: the source diagram's note on this point was cut off mid-sentence after "It's common for the Silver and Bronze layers to…" — the intended content is unknown and needs to be supplied by a process owner before this step can be finalized. | Data Engineering Lead | *[YYYY-MM]* |
| `[APC-OD-###]` | APC-STD-005 Medallion Architecture Standard authorship | This SOP references APC-STD-005 as the standard governing the reference architecture in Section 6, but that standard has not yet been authored. Confirm whether Section 6 should be extracted into APC-STD-005 once written, with this SOP reduced to a reference. | APC Representatives | *[YYYY-MM]* |
| `[APC-OD-###]` | Roles, Definitions, and Entry/Exit Criteria review | Sections 3, 4, and 9 have no source material of their own and were drafted from the conventions used in APC-SOP-303/304. A process owner needs to confirm they accurately reflect how architecture design is actually performed. | Data Engineering Lead | *[YYYY-MM]* |

## Revision History

| Issue Date | Rev | Change Description | Written / Revised By | Approved By |
| --- | --- | --- | --- | --- |
| 2026-08-17 | 0 | Initial draft, authored from the Medallion Lakehouse Architecture diagram provided for this update. Not issued. | | *[Pending]* |

Remove the yellow highlight from previous versions of the document when making changes. Then highlight all new document changes in yellow for quick reference. An original issue document will have no highlights.
