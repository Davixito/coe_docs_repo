# Publishing the 9 Administrative Procedures

This folder contains the 9 Administrative Procedure documents (from the "COE SOP" project)
converted from .docx to clean GitHub-flavored Markdown, ready to drop into `docs/administrative-procedures/`
in the `apc-docs-repo` repository.

## What's included

| File | Procedure ID | Title |
| --- | --- | --- |
| `apc-ap-001-project-lifecycle-handbook.md` | APC-AP-001 | APC Project Lifecycle Handbook |
| `apc-ap-100-discovery-define-phase-procedure.md` | APC-AP-100 | Discovery / Define Phase Procedure |
| `apc-ap-200-design-phase-procedure.md` | APC-AP-200 | Design Phase Procedure |
| `apc-ap-300-develop-phase-procedure.md` | APC-AP-300 | Develop Phase Procedure |
| `apc-ap-400-deliver-phase-procedure.md` | APC-AP-400 | Deliver Phase Procedure |
| `apc-ap-500-deploy-phase-procedure.md` | APC-AP-500 | Deploy Phase Procedure |
| `apc-ap-600-operate-phase-procedure.md` | APC-AP-600 | Operate Phase Procedure |
| `apc-ap-700-enhance-phase-procedure.md` | APC-AP-700 | Enhance Phase Procedure |
| `apc-ap-800-retire-phase-procedure.md` | APC-AP-800 | Retire Phase Procedure |

Each file has an H1 title, a procedure-ID line, a "back to index" link (`../index.md`, assuming the
file lives at `docs/administrative-procedures/*.md` and the index lives at `docs/index.md`), then the
full procedure body converted to headings/lists/tables (Purpose, Scope, Roles & Responsibilities,
Definitions, Procedure steps, Inputs, Outputs, Related Procedures/Standards/Templates/Checklists,
Open APC Decisions where present, and Revisions).

**Important — check the filenames against your index.md:** I generated these filenames myself
(kebab-case from the ID + title) since I could only see your index.md rendered in a screenshot, not
its actual link targets. Before committing, open `docs/index.md` in your editor and confirm the
`APC-AP-xxx` links point at these exact filenames — rename either the links or the files so they match.

## Steps to publish

1. Copy the `docs/administrative-procedures/*.md` files from this package into your local clone of
   `apc-docs-repo`, replacing/filling in that folder.
2. Confirm/update the links in `docs/index.md` (see note above) and update its "Content status" line
   if you want it to reflect that these are now committed.
3. Commit and push:

   ```bash
   git checkout main
   git pull
   cp /path/to/this-package/docs/administrative-procedures/*.md docs/administrative-procedures/
   cp -r /path/to/this-package/docs/sops docs/
   cp /path/to/this-package/docs/index.md docs/index.md
   git add docs/administrative-procedures/*.md docs/sops docs/index.md
   git commit -m "Publish Administrative Procedures, 3 SOPs, and convert index to tables"
   git push
   ```

## docs/index.md — now table-based

`docs/index.md` in this package is rewritten with every section (Administrative Procedures, SOPs,
Standards, Templates, Checklists) as a Markdown table instead of a bullet list, with the 9
Administrative Procedure rows linked to their published files.

I reconstructed the SOP/Standard/Template/Checklist rows from the "Related Procedures / Standards /
Templates / Checklists" tables inside the 9 source .docx files, because I only had a screenshot of
your live index.md (which cut off partway through the Design SOPs) rather than its raw source. Please
diff this against your actual `docs/index.md` before overwriting it — in particular:

- **Inconsistent numbering blocks:** the Discovery/Define, Design, and Develop phases use SOP/Template/
  Checklist IDs matching their AP block (100s/200s/300s), but Deliver, Deploy, Operate, Enhance, and
  Retire use low double-digit IDs (e.g. `APC-SOP-030`–`075`) instead of 400–800. That's what's in the
  source docs as written — I didn't renumber anything, just flagging it in case your tracker expects
  the higher numbers.
- **Duplicate names with different IDs:** "UAT Readiness Checklist" appears as both `APC-CHK-012` and
  `APC-CHK-303`; "Prioritization Worksheet" as both `APC-TMP-105` and `APC-TMP-043`; "UAT Scenario
  Template" as both `APC-TMP-014` and `APC-TMP-305`. Worth reconciling in the tracker if these are
  meant to be the same artifact.

If your real index.md has content past what I could see (extra columns, descriptions, a different
grouping scheme), tell me what's there and I'll adjust the table to match instead of replace it.

## Three SOPs now published (docs/sops/)

You uploaded four source .docx files for SOPs; three are now converted and included here, one is held back:

| File | Procedure ID | Status |
| --- | --- | --- |
| `apc-sop-303-semantic-model-development-procedure.md` | APC-SOP-303 | Content-complete, but the source doc's own metadata says "Status: Draft — Rev 0" — carried forward as a note at the top of the file. |
| `apc-sop-304-dashboard-development-procedure.md` | APC-SOP-304 | The source is explicitly a "brainstorm draft, not issued" with ~32 `[bracketed]` placeholders and an open-decisions list. Published as requested, with a prominent "DRAFT — NOT YET ISSUED" banner at the top so nobody mistakes it for ratified guidance. |
| `apc-sop-306-documentation-procedure-in-report.md` | APC-SOP-306 | Complete, "Initial Release." Note: the uploaded filename said "304" but the document itself is titled and numbered APC-SOP-306 — I went with what's in the document body, not the filename. Includes 3 wireframe images, copied to `docs/sops/assets/apc-sop-306/`. |

**Held back — "Dashboard Validation & UAT Procedure":** this fourth upload is complete content but its
own header literally reads `APC-SOP-[PENDING]` — no ID has been assigned — and it functionally overlaps
both APC-SOP-031 (Dashboard Validation) and APC-SOP-033 (UAT Execution) in the tracker. Per your
instruction I did not convert or publish it; once you confirm the correct APC-SOP number I'll convert
and add it.

**APC-SOP-307 (UAT Scenario Development Procedure)** — referenced throughout the other documents but
never uploaded — is still a placeholder in the index.

`docs/index.md` in this package reflects all of the above: APC-SOP-303 and 306 rows link to the
published files and read "Published"; APC-SOP-304 reads "Draft — not yet issued" and links to the
draft; everything else is still marked Placeholder.

## Not included in this pass

Per your scoping choice, the remaining SOPs (including APC-SOP-307), Templates, Checklists, and
Standards referenced throughout these procedures (e.g. APC-STD-001, APC-TMP-101, APC-CHK-101) are
still placeholders — only their IDs/names exist in the tracker. Source content for those wasn't
available in this project, so they weren't drafted here.
