# Manufacturing Operations with Microsoft Fabric: build plan

**Status:** Phase 1 only. Review this plan before starting Phase 2. No workshop files, datasets, or Fabric items have been created.

## Workshop design

Participants act as a manufacturing operations team preparing a morning risk review for three fictional plants. They answer one question: **Which production orders need attention, and what should the plant team check next?** Material shortages drive the at-risk KPI. Supplier deliveries, repeated machine faults, and quality rejections provide separate context, not proof of what caused an order to be at risk.

The flow is **CSV files → OneLake and Lakehouse → production-risk analysis → Eventhouse or report-based event analysis → semantic model → Power BI report → Fabric Data Agent if available → optional Foundry demonstration → PoC next steps.** Day 1 introduces the agent with a prepared baseline model and report; Day 2 shows how to improve the model and build the report. The Day 1 agent is a preview, not a dependency for Day 2.

Use the Fabric web interface throughout. GitHub is for reading or downloading files. No participant needs to write code, install VS Code or Power BI Desktop, use GitHub Copilot, run a notebook, or access Microsoft Foundry. Where a lab uses KQL or DAX, supply the whole snippet, explain it, show where to paste it, and offer a prepared path if participants cannot run it. Do not introduce CLI, APIs, MCP, CI/CD, or deployment pipelines.

## Complete repository structure

The private repository is `fabric-manufacturing-workshop`. Paths below are relative to its root. The source prompt is an input, not a workshop deliverable; this plan does not create another copy. Browser-created Fabric items stay in Fabric, not in the repository.

| Phase | File | Purpose |
|---|---|---|
| 1 | `BUILD-PLAN.md` | Record the design, file inventory, phase gates, tenant checks, manual setup, and fallbacks. |
| 2 | `README.md` | Introduce the workshop and direct participants and facilitators to the right starting points. |
| 2 | `workshop.md` | Provide the private MOAW entry point and navigation for all workshop sections. |
| 2 | `LICENSE` | State the approved reuse terms; confirm the license and rights holder before adding it. |
| 2 | `SECURITY.md` | Explain how to report security issues privately and prohibit real data, credentials, and tenant details in the repository. |
| 2 | `SUPPORT.md` | Describe access and workshop help, with placeholders for approved support contacts. |
| 2 | `CONTRIBUTING.md` | Cover phase gates, simple English, source attribution, browser step checks, and screenshot redaction. |
| 2 | `docs/references.md` | List official product documentation and workshop sources, what each is used for, and when click paths were checked. |
| 3 | `data/plants.csv` | Provide fictional plant names and locations, at least 3 rows. |
| 3 | `data/materials.csv` | Provide material categories, safety stock, and units, at least 15 rows. |
| 3 | `data/suppliers.csv` | Provide invented suppliers, regions, and target lead times, at least 6 rows. |
| 3 | `data/purchase_orders.csv` | Provide supplier delivery dates, quantities, and statuses, at least 80 rows. |
| 3 | `data/production_orders.csv` | Provide plant, product, required material and quantity, schedule, and status, at least 80 rows. |
| 3 | `data/inventory.csv` | Provide dated plant/material snapshots with available and reserved quantities, at least 150 rows. |
| 3 | `data/quality_inspections.csv` | Provide inspection totals, rejects, results, and defect categories, at least 100 rows. |
| 3 | `data/machine_events.csv` | Provide machine, plant, timestamp, event type, severity, temperature, and duration, at least 500 rows. |
| 3 | `data/validation-summary.md` | Record per-file counts, key relationships, deliberate findings, example records, and confirmation that all data is synthetic. |
| 4 | `docs/00-prerequisites.md` | Use the supplied wording for browser, sign-in, permissions, optional features, and access escalation. |
| 4 | `docs/01-business-scenario.md` | Introduce the morning risk review, the fictional plants, business terms, and the decision teams must make. |
| 4 | `docs/day-1/README.md` | Lay out the agenda, welcome, brief Fabric/Ignite updates relevant to this scenario, Fabric item map, and checkpoint. |
| 4 | `docs/day-1/01-onelake-lakehouse.md` | Create `ManufacturingOperationsLH_<TeamName>`, upload the files, load tables in the browser, and check columns and row counts. |
| 4 | `docs/day-1/02-eventhouse.md` | Load machine events, inspect repeated faults and high severity, and add an optional dashboard tile; include the Lakehouse/Power BI path. |
| 4 | `docs/day-1/03-data-agent.md` | Use one approved source, select relevant model tables, add instructions and five questions, diagnose one weak answer, and retest; include the no-agent activity. |
| 4 | `docs/business-questions.md` | Provide five shared questions, a manual answer-checking worksheet, and spaces for filters, evidence, and metadata improvements. Reuse on both days. |
| 5 | `docs/day-2/README.md` | Provide the agenda, Day 1 recap, team use-case checkpoint, and end-of-day checks. |
| 5 | `docs/day-2/01-semantic-model.md` | Review the starter model, relationships, display names, descriptions, hidden IDs, and the five required measures. |
| 5 | `docs/day-2/02-business-definitions.md` | Make definitions and questions precise; compare answers before and after the changes, with or without the agent. |
| 5 | `docs/day-2/03-power-bi-report.md` | Build the KPI card, plant risk bar chart, supplier late-delivery bar chart, fault trend, and production risk table. Give each visual its fields, filters, title, and expected output. |
| 5 | `docs/day-2/04-team-challenge.md` | Offer production risk, supplier performance, machine faults, or quality. Improve one visual on the existing report, add two questions, name one limitation, and prepare a three-minute demo. |
| 6 | `docs/day-3/README.md` | Run the 09:30–14:00 facilitation agenda, use-case conversations, and action review. |
| 6 | `docs/day-3/01-optional-foundry-demo.md` | Outline a facilitator-only demonstration using authorized synthetic data, with a Fabric-only walkthrough if omitted. |
| 6 | `docs/day-3/02-poc-planning.md` | Capture priority use case, current status, blocker, required support, scope, architecture, data, security, dependencies, owners, success criteria, and next actions. |
| 6 | `docs/troubleshooting.md` | Give symptom-based recovery paths for access, missing options, import, modeling, reporting, and agent issues. |
| 6 | `facilitator/README.md` | Cover group size, pacing, checkpoints, common errors, alternate paths, and recovery during delivery. |
| 6 | `facilitator/environment-setup.md` | List one-week and one-day tasks, roles, capacity/settings, readiness evidence, manual item creation and resets, and the screenshot list. |
| 6 | `facilitator/answer-key.md` | Record the fixed dates and filters, demo questions, verified answers, and matching outcomes across the main and fallback paths. |
| 7 | `QUALITY-REPORT.md` | Record files, link checks, assumptions, tenant dependencies, screenshot needs, manual items, and open issues. |

Use these folders as shown. If authentic screenshots are available and approved later, keep them under `assets/screenshots/` using filenames from the facilitator's capture list. Until then use inline text placeholders, not broken image links. Each capture entry names the filename, Fabric page, expected visible content, details to redact, and recommended screen size. No generated UI images or dummy binary files.

## Build order and review gates

1. **Plan:** Create only this file. Confirm review before continuing.
2. **Skeleton:** Create the folders, root documents, reference navigation, and private MOAW entry point. Use the workshop title, short title, description, author/contact, tags, `type: workshop`, `level: beginner`, `published: false`, and `duration_minutes: 720` as valid YAML. Verify the tag format against the MOAW template and parser. Use existing section anchors for navigation to modules not yet written, clearly mark them as planned, and switch to file links as content lands. Check all active links. Do not create exercises or data. Do not submit to public MOAW.
3. **Data:** Create the seven CSVs with the exact source schemas and minimum counts. Fix a single workshop dataset and reporting period; validate encoding, headers, dates, types, key uniqueness, lookup matches, and expected results. Prove at least 10 production shortages, at least 2 suppliers with repeated late deliveries, at least 2 machines with repeated faults, and at least 1 product with a high rejection rate. Use explicit thresholds and example records. Record the results and stop.
4. **Day 1:** Add prerequisites, the story, OneLake/Lakehouse, Eventhouse, Data Agent, and the shared question sheet. Write and rehearse both fallbacks. Link only files that exist. Stop.
5. **Day 2:** Add semantic model, business definitions, report, team challenge, and checkpoints. For the team use-case checkpoint, capture priority use case, PoC status, blocker, and support needed. Stop.
6. **Day 3 and facilitator:** Add optional Foundry, PoC, facilitator content, setup/reset details, the answer key, and troubleshooting. Stop.
7. **Quality:** Check all files and links; compare browser steps to current Microsoft Learn and rehearse with a participant account in the workshop tenant. Check core and fallback results against the answer key. Confirm synthetic data only, no secrets, complete and explained DAX/KQL, expected results and recovery for key tasks, and no required Foundry, Copilot, VS Code, notebooks, or coding. Report any feature or click path that could not be verified and write `QUALITY-REPORT.md`.

### Teaching and pacing

Each exercise will state its goal, starting item and role, time, numbered clicks using the labels seen in the tenant, an observable **Check**, and an **If you don't see it** recovery or fallback. Use short sentences and define each Fabric term on first use.

- **Day 1, 09:30–16:00:** Keep the supplied agenda and break/lunch times. Split 11:05–12:30 into 65 minutes of Lakehouse work and a 20-minute verification/debrief. Use 65 minutes of Eventhouse or fallback practice in the 13:15–14:35 slot, plus 15 minutes for briefing and comparison. Keep 14:50–15:50 for agent or manual answer checking.
- **Day 2, 09:30–16:00:** Keep the supplied agenda. Split 09:50–11:15 into 70 minutes of semantic model work and 15 minutes of review. Split 13:25–14:45 into 70 minutes of report building and 10 minutes of share-back. Preserve the 15:40–15:50 team use-case checkpoint and 15:50–16:00 close.
- **Day 3, 09:30–14:00:** Use a short optional facilitator demo, team discussions, a break, PoC scoping, and action review. No required Foundry lab. Keep any working block at or below 75 minutes.
- Keep the requested `720` minutes as MOAW metadata pending review. It does not equal the two core days' 780 scheduled minutes including breaks, or 630 excluding breaks. Publish the agenda times separately and confirm what the metadata is intended to count.

### Data and model rules to lock before authoring labs

- Use a fixed review date and forecast window, not today's date. For open orders in that window, take the latest inventory snapshot at or before the review date for each plant/material. Document whether `AvailableQuantity` is gross of reservations; plan for net usable stock to be gross available less reserved, floored at zero. Flag missing snapshots as unknown rather than silently treating them as zero.
- For the beginner exercise, design the target data so eligible orders do not compete for the same plant/material stock snapshot; document that this is a per-order check, not an inventory allocation engine. Define shortage as required minus usable stock, floored at zero. Keep safety stock contextual, and only sum shortage quantities in comparable units. Count distinct orders with a positive shortage.
- The raw production order has no supplier key. Do not join the purchase and production facts in the report. Prepare a one-row-per-order risk table or equivalent modeled fields, with an explicit, deterministic supplier-context rule for eligible purchase orders of the same plant/material as of the review date. Keep unmapped cases as unknown, and label the display field as supplier context, not an assigned or causal supplier. Keep the shortage reason separate.
- Plan one-to-many lookup relationships, with explicit snapshot and date grains. Calculate late-delivery percentage from delivered purchase orders where actual date exceeds promised date, excluding pending orders from that denominator. Count only fault events for the fault measure, group repeated faults by plant and machine, and use the same event time zone in both paths. Calculate quality rejection rate as total rejected divided by total inspected, with no rate for a zero denominator. Define the repeated-fault, repeated-late, high-severity, and high-rejection thresholds in the validation summary.
- Reconcile the five business measures and the report table against the validated data and answer key. For Day 1, provide a saved baseline report with the fault visuals and risk evidence already in place; do not make a Day 1 fallback wait for Day 2.

## Tenant gates and facilitator's manual setup

Check one week before the workshop and retest one day before using an ordinary participant account. Record **Check | Owner | Due date | Status | Evidence** with placeholder names and dates in the setup guide. Check item creation and item/data permissions separately. Don't enable features or cross-region processing without the tenant owner's approval.

| Capability | What to verify | What the facilitator manually prepares |
|---|---|---|
| Fabric workspace, OneLake, and Lakehouse | Fabric is enabled for the relevant users; the assigned capacity is running and supports the items; team members can create or edit and can read the tables. Test guest identities if used. | Ask the tenant/capacity admin for access and capacity. Create the private workspace(s) and team assignments. Give at least one member per group edit access, ideally all hands-on users. Use Contributor where sufficient; keep workspace Admin duties with the facilitator/admin. Create and load a backup Lakehouse with all seven tables, check schemas and counts, and verify team naming and file-to-table clicks. |
| Eventhouse and optional dashboard | Verify Eventhouse and KQL database creation, local CSV ingestion, query permissions, and dashboard/tile availability independently. | If enabled, create a backup Eventhouse, KQL database, typed machine events table, and saved KQL query set; create the completed dashboard only if supported. Validate the same date and severity filters in the fallback report. |
| Web semantic modeling and Power BI | Verify the tenant allows web model editing, that the chosen model/storage mode supports the required edits, and that participants have the relevant edit and source permissions, including report creation and Build where needed. Check capacity and Power BI licensing for authors and viewers. | In Fabric, prepare model-ready tables and a starter semantic model accessible on Day 1; create team-editable copies or isolate team workspaces. Prepare the five baseline measures and a completed reference model/report. Confirm that a participant can create, edit, and save a browser report. If authoring is blocked on the day, use the completed report for guided analysis and record that the authoring goal was not met. |
| Fabric Data Agent | Verify current eligible capacity, supported region, tenant switches for agent creation and required AI processing/storage, source compatibility and permissions, and the intended participant's access. Check region alignment for agent and source capacities. Test the actual model/table selection and question flow; visibility alone is not readiness. | If enabled, create a backup Data Agent using the approved synthetic semantic model, test all five questions under the intended role, and reserve a team-safe copy or naming scheme. Regardless of availability, prepare the report, question sheet, and expected answers. |
| Optional Microsoft Foundry | Validate access and integration only for the facilitator if the demo is approved; it is not a readiness gate for Days 1 and 2. | Use an approved demo environment only, or skip the integration and show the same use case in the Fabric report. Do not ask participants to provision or sign in to Foundry. |

Prefer teams of 3–4 as a starting point. Keep baseline items separate from team edits. Record which items use shared data and which are team-owned, and rehearse restoring from the baseline without overwriting shared items or other teams' work.

## Fallback paths

**No Eventhouse, KQL ingestion, or query access:** Open the facilitator's Lakehouse-backed Power BI report with `machine_events.csv` already loaded as a table. Use the same plant, dates, fault type, and high-severity filters as the Eventhouse path. Find the same two or more repeated-fault machines and review the same high-severity examples. Check against the same answer key. If only the tile is unavailable, keep the query path and view its results without creating a tile. Explain that the CSV is a fixed sample, not a live stream.

**No Fabric Data Agent or usable source access:** Open the prepared Power BI report and business-question sheet. For each of the five questions, record the filters used, the evidence visual, and the answer. Pick one ambiguous question, such as “Which supplier is late?” Clarify the date range and denominator, improve one label or definition in the model where edits are permitted (otherwise on the worksheet), and answer again against the report. Check both attempts against the same answer key used for the agent. This teaches the value of metadata without claiming that the manual activity tested an agent.

## Sources to adapt

| Upstream source | Adapt | Leave out |
|---|---|---|
| [Microsoft MOAW repository](https://github.com/microsoft/moaw) and [workshop template](https://github.com/microsoft/moaw/blob/main/template/workshop/workshop.md) | Front matter, section-based navigation, and reusable Markdown structure. Test private GitHub rendering without relying on a public renderer to read private files. | Public submission, hosting infrastructure, and unrelated example content. |
| [Microsoft Fabric Data Agent Workshop](https://github.com/microsoft/fabric-data-agent-workshop) | From Lab 1, use the pattern of baseline answer → inspect one weak answer → improve model metadata or instructions → retest. Use business names, definitions, and example questions. Mention the multi-source pattern as optional facilitator context only. Replace automated evaluation with a five-question human answer check. | Notebooks, catalog/SDK setup, managed example artifacts, multi-source build, LLM judge, and MLflow. Write new instructions and use only the workshop's invented dataset. |
| [Microsoft Skills for Fabric](https://github.com/microsoft/skills-for-fabric) | Builder reference only for terminology and pointers to official documentation. | Participant setup, coding tool skills, CLI, APIs, and MCP instructions. |

Use Microsoft Learn as the click-path and requirements reference, especially [Fabric Data Agent creation](https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent) and [semantic model editing in the Power BI service](https://learn.microsoft.com/en-us/power-bi/transform-model/service-edit-data-models). Record the verified UI labels, dates, and any tenant-specific differences in the build. Do not copy upstream workshop prose or screenshots.

## Phase 1 review

Review the file structure, the Day 1 starter model/report, the fallback paths, the shortage and supplier-context rules, and the pacing. Confirm the license and rights holder before Phase 2, and decide whether to retain or revise the requested MOAW duration value. After approval, **Phase 2 only** is next.
