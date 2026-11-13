# Kloud Kart Data Strategy Engagement

DE01 Data Foundations, graded lab. Consultant: Zabdiel Yidjiemo Addo. November 2026.

Kloud Kart is a three-year-old e-commerce company in Accra shipping about 4,000 orders a day, with orders, stock and customer accounts in one 40 GB MySQL database on the same machine as the live website. This repository holds the diagnosis, recommendation, roadmap, decision records, board deck and one improvement beyond the brief.

## The recommendation in three sentences

Move all reporting onto a copy of the shop's database on the server already approved, and build one reporting database there that holds a single agreed rule for what counts as a sale. Keep customer names and contacts out of that database, and list every copy of customer data so a deletion can be shown to reach all of them. In exchange, Kloud Kart accepts figures updated once a day rather than live, and no forecasting this year.

## Deliverables

| Brief deliverable | File |
|---|---|
| 1. Situation diagnosis (root causes, costed, ranked by risk; discovery questions) | [`situation_diagnosis.md`](situation_diagnosis.md) |
| 2. Recommendation (two pages) | [`recommendation.md`](recommendation.md) |
| 2. Roadmap (one page, quarterly, outcomes Nana can check) | [`roadmap.md`](roadmap.md) |
| 3. Decision records (3–6 ADRs, shared template) | [`decisions/`](decisions/) |
| 4. Board presentation | [`deck/Kloud-Kart-Board-Deck.pptx`](deck/Kloud-Kart-Board-Deck.pptx) |
| 5. One improvement beyond the brief | [`improvement.md`](improvement.md) and the thing built: [`customer_data_register.md`](customer_data_register.md) (spreadsheet version in [`assets/`](assets/)) |
| Supporting material (assumptions A01–A31, cost arithmetic, penalties, timeline test, operating load, sources) | [`appendix.md`](appendix.md) |

## Decision records

| ADR | Decision | Main rejected alternative |
|---|---|---|
| [ADR-001](decisions/ADR-001-read-replica.md) | Reports read from a copy of the database on the second server | Nightly export at 02:00 |
| [ADR-002](decisions/ADR-002-warehouse-on-own-server.md) | Warehouse-shaped store on the pre-approved server | Managed cloud warehouse; lake or lakehouse |
| [ADR-003](decisions/ADR-003-daily-batch-stock-at-checkout.md) | Daily refresh, stock fixed at checkout, no streaming platform | Managed stream for stock events |
| [ADR-004](decisions/ADR-004-personal-fields-before-load.md) | Personal fields removed or keyed before loading; register of every copy | Load raw data and clean it inside the store |
| [ADR-005](decisions/ADR-005-definition-before-build.md) | No sales report until Nana and Finance sign one definition of a sale | Build first and settle the definition inside the warehouse |
| [ADR-006](decisions/ADR-006-two-hires.md) | Data engineer and analytics engineer, both starting in month 2 | Data engineer and data analyst; hiring one at a time |

## Suggested reading order

1. `situation_diagnosis.md`: what is wrong, what it costs, and the ranking by risk.
2. `recommendation.md`: what to build, what not to build, and what it costs.
3. `roadmap.md`: what Nana can check each quarter.
4. `decisions/`: why each choice beat its alternative.
5. `improvement.md` and `customer_data_register.md`.
6. `appendix`: every assumption and calculation behind the figures.

## Repository layout

```
kloud-kart-data-strategy/
├── README.md
├── situation_diagnosis.md
├── recommendation.md
├── roadmap.md
├── improvement.md
├── decisions/
│   ├── ADR-001-read-replica.md
│   ├── ADR-002-warehouse-on-own-server.md
│   ├── ADR-003-daily-batch-stock-at-checkout.md
│   ├── ADR-004-personal-fields-before-load.md
│   ├── ADR-005-definition-before-build.md
│   └── ADR-006-two-hires.md
├── deck/
│   └── Kloud-Kart-Board-Deck.pptx
├── glossary.md
```

## Notes on the figures

Nana Adjei was unavailable for questions, so every gap in the brief is filled by a numbered assumption (A01–A31 in `appendix`) and cited by number wherever it is used. The assumption that would most change the recommendation if wrong is A20: that the gap between Operations' and Finance's sales figures comes from a few rules that can be named.

Section references to Ghana's Data Protection Act, 2012 (Act 843) are for planning only and are not legal advice.
