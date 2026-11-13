# Glossary

Abbreviations and terms used across this repository, grouped by type. Each document also ends with the terms it uses.

## Root causes and risks

| Term | Meaning |
|---|---|
| RC1 | Root cause 1: reporting reads run on the same live database and machine as the shop, so the Monday export slows the website. |
| RC2 | Root cause 2: no agreed written definition of a sale, so Operations and Finance report different figures. |
| RC3 | Root cause 3: the Monday report is rebuilt by hand from exports, and only Nana can do it. |
| RC4 | Root cause 4: nobody tracks copies of customer data or owns the data, so a deletion cannot be shown to reach every copy. |
| Overselling (risk) | Selling stock the shop does not have; tracked as a risk outside the ranking because its frequency and cause are unknown (A22). |

## Time

| Term | Meaning |
|---|---|
| Q1–Q4 | The four quarters of the 12-month plan: Q1 = months 1–3, Q2 = months 4–6, Q3 = months 7–9, Q4 = months 10–12. |
| Month 1, month 2, day 60 | Months and days count from the month the plan is approved (month 1). Day 60 is 60 days from that start. |
| Month-2 gate | The deadline for Nana and Finance to sign one definition of a sale; if it is not signed by the end of month 2, the dispute goes to the board before the report is built (ADR-005). |

## References

| Term | Meaning |
|---|---|
| A01–A31 | Numbered assumptions, listed with their basis in appendix.md, section A. Used because Nana could not be asked. |
| A20 (marked assumption) | The assumption that would most change the recommendation if wrong: the gap between the two sales figures comes from a few rules that can be named. |
| ADR | Architecture Decision Record: a short file recording one decision, the alternatives rejected and why, in the shared template. Six are in decisions/. |
| Appendix A–G, B1–B4, F1–F2 | Sections of appendix.md: A assumptions, B cost arithmetic (B1 RC1, B2 RC2, B3 RC3, B4 RC4), C penalties, D complaint timeline, E operating load, F salaries (F1) and growth (F2), G sources. |
| P1–P7 | The seven tasks for answering the data protection complaint, in appendix.md, section D. |
| C01–C11, R001 | Row IDs in the customer data register: C = a copy of customer data, R = a request (R001 is the open complaint). |

## Plan terms

| Term | Meaning |
|---|---|
| Copy of the database (read replica) | A second database on the approved server that receives every change from the live database, so reports read from it instead of the live shop (ADR-001). |
| Reporting database | One database on the approved server where the agreed definition of a sale is held and every report comes from; "warehouse-shaped" means its structure is fixed before data is loaded (ADR-002). |
| Key / key table | Names, phones and emails are replaced with a code (the key) before loading; the key table links codes back to customers and is held separately with restricted access (ADR-004). |
| Register | The list of every copy of customer data, with its owner, purpose and how a deletion reaches it (customer_data_register.md). |
| One-customer search | The monthly test: find one customer in every copy on the register and record the time taken. |
| Overnight export (stopgap) | Running the Monday export at night, when few people shop, until the copy of the database is ready. |
| "As of" time | The time printed on a report showing when its figures were last updated. |
| Revisit trigger | A number, event or date, written down in advance, that would make us reopen a decision. |
| Operating load | The weekly hours the hires spend keeping the system running, about 16.5 hours (appendix.md, section E). |
| Base case | The central estimate, using the middle value of each assumption; ranges show the lowest and highest cases. |

## Law and money

| Term | Meaning |
|---|---|
| Act 843 | Ghana's Data Protection Act, 2012. "s." means section, e.g. s.32 is section 32. References are for planning, not legal advice. |
| The Commission | Ghana's Data Protection Commission, which received the complaint and enforces Act 843. |
| Penalty unit | The unit fines are set in under Ghanaian law; taken as GHS 12 (A18, to be verified). |
| GHS | Ghana cedi. |

## People

| Term | Meaning |
|---|---|
| Data engineer | Hire 1: runs the copy, the nightly load, failure alerts, the register and the monthly deletion test. |
| Analytics engineer | Hire 2: turns the agreed definition of a sale into the one figure everyone reads, and builds the Monday report. |
| The developer | Kloud Kart's one existing PHP/MySQL developer, who also keeps the shop running. |
| Operations owner | The person in Operations named to own customer data work until the data engineer starts (an assumption; not named in the brief). |
