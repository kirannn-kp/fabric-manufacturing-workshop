# Workshop quality report

**Status:** Local workshop package complete. Fabric tenant rehearsal is pending. No remote repository, cloud workspace, data agent, or Foundry resource was created by this build.

## Files and navigation

- Entry points: [README](README.md) and the private [MOAW workshop](workshop.md).
- Governance: [license](LICENSE), [security](SECURITY.md), [support](SUPPORT.md), and [contributing](CONTRIBUTING.md).
- Participant material: [prerequisites](docs/00-prerequisites.md), [business scenario](docs/01-business-scenario.md), [Day 1](docs/day-1/README.md), [Day 2](docs/day-2/README.md), [Day 3](docs/day-3/README.md), [question sheet](docs/business-questions.md), [troubleshooting](docs/troubleshooting.md), and [references](docs/references.md).
- Data: the [data inventory](data/validation-summary.md) links to the seven source CSVs and the separate [facilitator risk snapshot](facilitator/production_risk.csv).
- Facilitator material: [guide](facilitator/README.md), [setup](facilitator/environment-setup.md), and [answer key](facilitator/answer-key.md).
- The original [build plan](BUILD-PLAN.md) is included for traceability. The user's go-ahead superseded the phase pauses. The sole extra data file is the derived facilitator snapshot so the participant experience stays browser-based.

## Validation

| Check | Result |
|---|---|
| Markdown navigation | All 112 relative links, including linked heading anchors, passed local validation. External product click paths were compared with the relevant Microsoft Learn articles; private workshop links are not embedded. |
| CSVs and expected outcomes | Checked headers, types in source, row counts, uniqueness, joins, and the derived risk snapshot against the source. Independently reproduced risk, supplier, machine, and quality figures in the answer key. |
| Browser exercise design | Required tasks have observable checks and recovery. No participant CLI, SDK, VS Code, GitHub Copilot, Power BI Desktop, notebook, or Foundry is required. |
| KQL and DAX | The snippets are complete, include definitions, and use the supplied table and column names. The business calculations were independently checked from the CSVs. The KQL and DAX engines were not run in a Fabric tenant. |
| Pacing | Core days run 09:30–16:00; Day 3 ends at 14:00. No hands-on slot exceeds 75 minutes. Kept the requested `duration_minutes: 720` as MOAW metadata; the posted core agendas total 780 minutes with breaks or 630 without. |
| Privacy | All files created from invented data or original instructions. No secrets, private tenant links, real operational data, generated UI images, or fabricated Fabric binaries. The repository is intended for private use. |

## Tenant gates and remaining setup

- **Core:** Confirm capacity and browser authoring for the workshop group. Test role, Build access where required, Lakehouse type inference, web model edits, and report creation with an ordinary participant identity.
- **Eventhouse and dashboard:** Check ingestion, queryset permissions and optional tile separately. If blocked, use the prepared Lakehouse-backed **Machine events** page. Verify it returns the same machine counts and high-severity events.
- **Data Agent:** Verify eligible capacity, supported region, required tenant settings, source access, and agent responses. The report and question sheet are the fallback. Foundry is demonstration-only and may be skipped.
- **Manual items:** Prepare the private baseline and team workspaces, loaded Lakehouse, baseline/team semantic models, and completed reference/team backup reports. Prepare KQL and agent backups only where the features are enabled. See the [build and readiness checklist](facilitator/environment-setup.md).
- **Screenshots:** Five text placeholders identify authentic captures to make during rehearsal. Their filenames, screens, size and redaction rules are in [environment setup](facilitator/environment-setup.md#screenshot-capture-list).
- **Open items for the organizer:** Complete the participant-account rehearsal; choose which optional branches to run; share private links and support contacts; check whether the organizer wants to replace the private-use notice with a separately approved license.
