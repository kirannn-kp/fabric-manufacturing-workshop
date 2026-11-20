# Facilitator answer key

Clear visual selections before verifying. The production snapshot is 10 November 2026 for open orders starting 11–17 November. The supplier, machine, and quality analysis windows are 1–10 November 2026; machine time is UTC.

| Question | Correct result | Evidence or explanation |
|---|---|---|
| 1. At-risk production orders? | **12**, four in each of Plant North, South, and East. | Risk card and plant bar. These are distinct orders with a positive shortage, not all open orders. |
| 2. PR001 shortage and reason? | **35 Each**, material shortage. | P01/M01: required 100, gross 75, reserved 10, usable 65. The supplier context is Supplier D, from PO046. It is not the reason. |
| 3. Highest late-delivery percentage? | **Supplier A: 8/12 = 66.7%**. B: 6/12 = 50.0%; C–F: 0/12. | Only delivered orders with actual delivery dates in the window count. Totals: 14/72 = 19.4%; 12 open orders excluded. |
| 4. Which machines repeatedly fault? | **P01 / MC-N01: 8** and **P02 / MC-S01: 8**. | Machine page or KQL. Repeated means at least three. Total faults: 16. |
| 5. Highest rejection rate? | **Drive Unit A: 525/3,500 = 15.0%**. | Quality page. Pump Unit B: 3.0%; Valve Unit C: 1.0%. |

Eventhouse ingest count: 500. The six High events are all on `MC-N01`; first is `2026-11-01T00:00:00Z`. The Lakehouse-backed page should show the same six, whether or not a KQL tile was created. Risk detail: 45 eligible orders, 12 shortage rows, 420 total short units. Check these under no cross-filters. [Data validation](../data/validation-summary.md) lists full counts and rules.

For the weak-answer exercise, give one point each for the right result, date/filter, and denominator or evidence. Mark correct at 3/3, incomplete if the number is right but context is missing, and wrong if the number is wrong. On a causal question, accept “the data does not establish cause”; don't accept speculation presented as fact.
