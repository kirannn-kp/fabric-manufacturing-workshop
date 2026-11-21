# Environment setup and rehearsal

## Full onsite workshop: delivery setup

Use the [onsite schedule](../docs/onsite-workshop.md). Monday and Tuesday each have 315 activity minutes; Wednesday has 210 and ends at 14:00. Keep the same workspace and item names across both Fabric days. Cap setup troubleshooting at 10 minutes before using a fallback.

| Before the block | Facilitator action | Switch if blocked |
|---|---|---|
| Monday concepts and demo | Show a file, Lakehouse table, and KQL query. Explain the two copies of telemetry. | Use the item diagram and evidence card. |
| Monday data labs | Stage a fallback Lakehouse with `plants` and `machine_events`, plus a KQL database with the 500 events. | Use prepared tables, then CSV checks if necessary. |
| Monday SQL and dashboard | The SQL check and both dashboard results were verified live. Both tiles rendered after reopening, but their custom titles did not persist in rehearsal. Identify the tiles by their columns. | Use the prepared endpoint or CSV for SQL checks; keep KQL results in two named tabs if dashboard creation is unavailable. |
| Tuesday model, Data Agent, and ontology | Open the prepared two-table model and KQL database. Use the verified DAX query in Viewing mode. Only offer relationship editing or live ontology if separately verified. | Use the read-only model, KQL evidence, and the ontology diagram. |
| Tuesday Operations Agent | Open the saved, stopped playbook. Leave actions unconfigured; use the reference KQL for the threshold replay. | Review the rule and replay from the evidence card. |
| Wednesday Foundry and PoC | Bring a diagram and the Day 2 answers. Use a live read-only demo only if already prepared and verified. Close by recording PoC scope, owner, success criteria, and a dated next step. | Deliver the same walkthrough without Foundry. No participant account is needed. |

**Fast teams only:** Offer the Day 1 Copy pipeline or Day 2 dashboard plant selector after the core handoff. The [reserve labs](../docs/onsite-workshop.md#optional-fabric-reserve-labs) offer a OneLake shortcut, a Spark notebook, and a facilitator-led Eventstream preview. Check each optional feature in the delivery workspace before offering it live; the optional portal workflows were not part of the core rehearsal. Keep practice outputs separate, pipelines unscheduled, and sample streaming data out of the workshop Eventhouse. If capacity or access is constrained, use the verified fault-rate KQL stretch instead.

## Short technical rehearsal: core checks

- **Day 1:** Prepare fallback items with both Lakehouse tables and the 500-row KQL copy. Confirm both copies are available for the Day 2 labs.
- **Day 2:** Prepare a Direct Lake semantic model with `plants` and `machine_events` from the workshop Lakehouse. Test that attendees can run the exact DAX in the [incident lab](../docs/incident-lab.md), including in Viewing mode. If access fails, use the KQL results and plant lookup. Only show the plant relationship and saved measure after testing them. For the live ontology extension, ask a Fabric admin to verify that **Users can create ontology (preview) items** applies to the intended group, and verify a prepared ontology before class. Otherwise use the diagram exercise.
- **Days 2–3:** For Tuesday, check the saved playbook and reference replay (two groups at 3+ and 8+, none at 9+). For Wednesday, use the evidence card to rehearse a short pilot handoff with a named human owner and dated checkpoint.

The remaining setup below is for the extended report-based agenda only. No baseline Power BI report or Foundry resource is required for the incident lab.

## One week before

1. Ask the Fabric tenant and capacity admins to verify Fabric creation for the workshop group, capacity region/state, browser semantic-model editing, and author/reader licensing. Check guest policies if applicable. Give facilitators the workspace management rights they need; use **Contributor** for team authors where sufficient. Give reference viewers only the Read rights needed and authorize Build for report authors where required.
2. Create a private baseline workspace and one private editable workspace per team if possible. Verify attendees are in the correct tenant. Keep the baseline read-only for attendees, and store private links in the event invite. Assign an authorized participant per team who can create and edit items.
3. Build the baseline and team items below. Check optional capabilities separately: Eventhouse/KQL ingestion, optional dashboard, and Data Agent. Current Learn guidance for Data Agent calls for paid F2+ or enabled P1+ capacity; review region alignment and applicable cross-geo AI processing/storage settings. Do not enable them without tenant-owner approval. Use the optional Foundry path only if already authorized.
4. Use only the workshop CSVs. Do not enable public sharing. Record the assigned workspace, team item names, and chosen branches in private facilitator notes.

## Build the baseline items manually

1. Create `ManufacturingOperationsLH_Baseline`. Load the seven files per the [Day 1 Lakehouse instructions](../docs/day-1/01-onelake-lakehouse.md). Also load [production_risk.csv](production_risk.csv) as `production_risk`, with a header. Verify the source and risk row counts. Confirm amounts/counts are numeric; confirm `EventTime` and delivery/inspection dates work with date filters. Check `EventTime` is interpreted as UTC. If Load to tables infers a type that breaks the lab, correct it with a supported browser data-preparation path, such as a browser import model with Power Query type changes, before advertising readiness. Recheck connection/permissions and lab steps on that model; don't rely on the Lakehouse load dialog for a custom schema.
2. From the baseline Lakehouse select **SQL analytics endpoint** > **New semantic model** (or **New Power BI semantic model** in the Lakehouse). Enter `Manufacturing Operations - Baseline`. Select exactly `plants`, `suppliers`, `production_risk`, `purchase_orders`, `machine_events`, and `quality_inspections`. Confirm and open the model. In **Editing**, use **Manage relationships** to create the five active single-direction relationships from the [model lab](../docs/day-2/01-semantic-model.md), all one-to-many from the named lookups. Remove any conflicting auto-detected relationships before testing. Do not connect supplier context to `suppliers`. The other raw tables remain available for the Lakehouse lab.
3. Add the seven DAX formulas and formats from the model lab. Keep readable columns visible. In the baseline, you can leave `DefectCategory` unchanged for the team exercise. Verify all numbers against the [answer key](answer-key.md). Create an editable `Manufacturing Operations - <TeamName>` in each team workspace using the same browser build steps, pointing to baseline data where permissions support it. If that path is blocked, load the same tables in a separate facilitator-prepared team Lakehouse and build the model there. Give teams access to the model/source as needed; validate changes persist and cannot affect the baseline model.
4. In the baseline model select **New report**. Build and save `Manufacturing Operations - Reference`, starting with **Risk review** and the five visuals in the [report recipe](../docs/day-2/03-power-bi-report.md). Add the following evidence pages:

   | Page and visual | Setup |
   |---|---|
   | **Machine events** > Repeated faults | Table: `plants[PlantName]`, `machine_events[MachineId]`, and `Machine fault count`. Filter the visual by `Machine fault count` greater than or equal to 3. |
   | **Machine events** > High severity events | Table: raw `EventTime`, `machine_events[PlantId]`, `MachineId`, `EventType`, `TemperatureC`, `DurationMinutes`; raw numeric fields use **Don't summarize**. Set a visual filter `Severity = High`; do not apply a Fault filter here. |
   | **Machine events** > Date filter | Add raw `EventTime` as a page filter from 1 Nov inclusive to 11 Nov exclusive UTC. Save with no plant selection. |
   | **Quality** > Product rejection | Table: `quality_inspections[ProductName]`, `Quality rejection rate`, and `InspectedQuantity` summarized as Sum. Set `InspectionDate` to 1–10 Nov inclusive. |

5. If enabled, build `ManufacturingEvents_Baseline`, its KQL database, a preloaded `machine_events` table, and a saved query set using the three snippets in the [Eventhouse lab](../docs/day-1/02-eventhouse.md). Optionally save the repeated-fault tile. Verify the report matches the KQL results using the same dates.
6. If enabled, create `ManufacturingRiskAgent_Baseline` against the approved model. Test the five [sample questions](../docs/business-questions.md), end-user access, tested metadata, and the no-agent report path. Prepare the reference report and worksheet even if the agent works. No agent needs to be shared publicly. If Foundry is in the agenda, rehearse only the already approved [demonstration](../docs/day-3/01-optional-foundry-demo.md).
7. Prepare a private team working report for groups who reach the challenge without saving their own, or preassign access to a facilitator-led working report. Keep it separate from the reference. Download the workshop ZIP before the event; share the unmodified participant data through an approved private channel if GitHub access fails.

## One day before: readiness

Use a regular test participant, not only an administrator. Check team models and report creation from the browser, the fallback links, and all answer-key counts. Write launch-day branch decisions beside the readiness rows.

| Check | Owner | Due date | Status | Evidence |
|---|---|---|---|---|
| Tenant/capacity/guest permissions | `<tenant admin>` | `<one week before>` | Pending | `<private record>` |
| Source CSV loads, exact counts, and type checks | `<data facilitator>` | `<one day before>` | Pending | `<counts and types>` |
| Team model editing and report creation | `<participant tester>` | `<one day before>` | Pending | `<tested workspace and result>` |
| Reference report and both fallbacks | `<facilitator>` | `<one day before>` | Pending | `<verified results>` |
| Eventhouse, query access and optional dashboard | `<facilitator>` | `<one day before>` | Pending/skip | `<enabled or fallback>` |
| Data Agent permissions, setup and retest | `<facilitator>` | `<one day before>` | Pending/skip | `<enabled or fallback>` |
| Optional Foundry rehearsal | `<facilitator>` | `<one day before>` | Pending/skip | `<rehearsed or Fabric-only>` |

## Reset between sessions

Confirm which workspace and team items are safe to reset. For a failed team import, use a fresh team Lakehouse name, point the exercise to the clean backup, and check counts instead of appending. Restore measures and metadata from the starter instructions or recreate the team's model/report in its own workspace. Use a fresh KQL table for a second import and retest the query name. Clear agent test chat and restore baseline instructions before another class. Delete only confirmed training items with the organizer's approval; never remove a shared baseline or source. Release temporary roles and capacity per organizer policy after the workshop.

## Screenshot capture list

Capture only a synthetic demo workspace. Hide browser URLs if they contain item IDs, profile names, emails, tenant/capacity identifiers, private workspace names, and any sensitive settings. Add approved files under `assets/screenshots/`; leave the inline text placeholder until then.

| Filename | Fabric page | What should be visible | Hide | Screen size |
|---|---|---|---|---|
| `01-lakehouse-files.png` | Lakehouse Explorer | Files and Tables; synthetic inventory preview | Workspace URL, profile | 1440 × 900 minimum |
| `02-eventhouse-query.png` | KQL Queryset | Repeated-fault KQL and two result rows | Database URLs, capacity | 1440 × 900 minimum |
| `03-agent-test.png` | Fabric Data Agent | Synthetic question, answer and source pane | Private source links, account | 1440 × 900 minimum |
| `04-model-relationships.png` | Semantic model | Relationship diagram and Properties | Workspace IDs, account | 1600 × 900 minimum |
| `05-risk-report.png` | Power BI report | Five visuals and the 12-order card | Sharing link, workspace, profile | 1600 × 900 minimum |
