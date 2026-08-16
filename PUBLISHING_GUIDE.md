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
   cp -r /path/to/this-package/docs/standards docs/
   cp -r /path/to/this-package/docs/templates docs/
   cp -r /path/to/this-package/docs/checklists docs/
   cp /path/to/this-package/docs/index.md docs/index.md
   git add docs/administrative-procedures docs/sops docs/standards docs/templates docs/checklists docs/index.md
   git commit -m "Publish Administrative Procedures + 3 SOPs; fill remaining tracker with generic placeholders"
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

## Everything else — 121 auto-generated skeleton documents

You asked for basic content on the rest of the tracker rather than leaving it empty, and to make the
auto-generated ones distinguishable from the 4 docs you actually shared. That's now done:

- **121 files generated**: 44 SOPs (including APC-SOP-307), all 8 Standards, all 37 Templates, all 32
  Checklists — in `docs/standards/`, `docs/templates/`, and `docs/checklists/` (new folders), plus
  alongside the real SOPs in `docs/sops/`.
- Every auto-generated file opens with a **🧩 DRAFT — auto-generated, not reviewed** banner explaining
  it's a skeleton to replace, not approved guidance.
- Each follows a consistent skeleton for its type (SOP: Purpose/Scope/Roles/4-step generic
  procedure/Inputs/Outputs/Related; Standard: Purpose/Scope/Requirements/Enforcement/Related; Template:
  Purpose/When to Use/Suggested Fields table; Checklist: Purpose/checkbox list) with `*[bracketed
  prompts]*` marking exactly what a process owner needs to fill in.
- Each links back to its lifecycle phase's Administrative Procedure, and SOPs also cross-link to the
  other SOPs in the same phase block.

`docs/index.md` now has a **Status legend** at the top and every single row — all 133 documents —
carries one of these statuses: **Published**, **Published (Draft status in doc metadata)**, **Draft —
not yet issued**, or plain **Draft** for the 121 auto-generated skeletons. That's the distinction you
asked for: scan the Status column to immediately tell real content (Admin Procedures + APC-SOP-303/304/306)
apart from the 121 auto-generated skeletons — note "Draft" (skeleton, unreviewed) and "Draft — not yet
issued" (real content from your upload, just formally unissued) are deliberately different exact strings
so they don't collide, even though both use the word "Draft."

**Still not included:** the "Dashboard Validation & UAT Procedure" you uploaded — still held back
pending you assigning it a real APC-SOP number, per your last instruction. Everything else from the
tracker now has at least a skeleton.
