---
published: false
type: workshop
title: Manufacturing Operations with Microsoft Fabric
short_title: Fabric Manufacturing Workshop
description: Investigate one manufacturing incident in Microsoft Fabric, explain the evidence, and plan a human-reviewed maintenance pilot.
level: beginner
authors:
  - Kiran Panchal
contacts:
  - Kiran Panchal
duration_minutes: 720
tags: microsoft-fabric, manufacturing, onelake, lakehouse, real-time-intelligence, power-bi, data-agent
---

# Start here

- [Three-day manufacturing incident lab](docs/incident-lab.md) — the main route through Lakehouse, Eventhouse, Data Agent, semantic models, ontology, and Operations Agent. No Power BI report authoring is required.
- [Synthetic data and validation](data/validation-summary.md)

---

# Day 1: Find and verify the incident

- [Open Day 1](docs/incident-lab.md#day-1--find-and-verify-the-incident): load the plant lookup, query fault records, and compare the Data Agent's answers to KQL.

---

# Day 2: Give the evidence business context

- [Open Day 2](docs/incident-lab.md#day-2--give-the-evidence-business-context): run read-only DAX, draw an ontology, and choose a first maintenance review.

---

# Day 3: Review an Operations Agent rule and design a pilot

- [Open Day 3](docs/incident-lab.md#day-3--review-an-operations-agent-rule-and-design-a-pilot): inspect a stopped playbook, replay its threshold against historical data, and write a pilot handoff.

---

# Help and references

- [Troubleshooting](docs/troubleshooting.md)
- [Facilitator guide](facilitator/README.md)
- [References](docs/references.md)
- [Optional report authoring](docs/day-2/03-power-bi-report.md) and [optional Foundry demonstration](docs/day-3/01-optional-foundry-demo.md) belong to the extended agenda, not the main route.
