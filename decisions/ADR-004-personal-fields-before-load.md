# ADR-004: Remove or key personal fields before loading, and keep a register of every copy of customer data

- **Status:** Pending
- **Date:** 2026-11-13
- **Decision owner:** Nana Adjei, Head of Operations (proposed by Zabdiel Addo, consultant)


## Context

Kloud Kart has a Data Protection Commission complaint about a deleted customer's data, with 90 days to respond. Marketing exports a customer list of about 300,000 people with no record of how many copies exist. Every copy of customer data is a place each deletion must reach. The plan adds two new stores (the read replica and the reporting database), and must be defensible under Act 843. The definition of a sale is still being agreed and will change.

## Decision

We remove names, phone numbers and email addresses, or replace them with a key, before data enters the reporting database; the key table is held separately with restricted access. Business rules, including the definition of a sale, run after loading, in SQL. From day one we keep a register listing every copy of customer data, with its owner, purpose and how a deletion reaches it, and we test it monthly by finding one customer in every copy.

## Alternatives considered

### Alternative A: load raw data and clean it inside the store

- **How it would work:** full tables, personal fields included, are loaded into the reporting database as they are; all cleaning and business rules run afterwards inside it, and the raw tables are kept.
- **Why it is attractive:** the standard modern pattern, simpler to build, and any question can be rerun from the raw data later without going back to the live system.
- **Why rejected:** the kept raw tables are a full copy of every customer that each deletion must reach, along with every table built from them, any snapshots and the backups, inside the 90 days; and the reports need no names, phone numbers or emails to answer any question in the brief.

### Alternative B: totals only, with no customer-level rows

- **How it would work:** the reporting database holds only totals (sales by week, by category, by country); no row refers to a single customer.
- **Why it is attractive:** nothing personal exists in the store, so it needs no deletion at all.
- **Why rejected:** it permanently loses questions about customers as a group, such as how many buy again, which the business is likely to ask within the year; adding customer rows later means rebuilding the store.

## Consequences

- **What this buys:** deletions are mostly done at the source; a leak from the reporting database exposes no names or contacts; the register answers a "what do you hold on me" request (s.32), lists whose data was affected in a breach (s.31), and gives the evidence for the open complaint.
- **What this costs:** questions about named customers need the restricted key table; the key table is one more place every deletion must reach; a field that was dropped has to be pulled again from the live system; and keeping the register is a monthly duty for someone.
- **What it costs the client if I am wrong:** if keyed data still counts as personal data under the Act, each deletion has one more place to reach; that is hours per request, not a redesign.
- **What would make me revisit this:** the monthly one-customer search fails to find the customer in a listed copy, or finds them in an unlisted one; or the board approves an analysis that needs named customers.

## What this survives

- A second complaint or a "what do you hold on me" request: the register lists every copy, and the search target is one working day, falling to one hour by Q4.
- A breach: the register shows whose data was where.
- The definition of a sale changes: business rules run after loading, so they are rerun inside the store without touching the live system.
- One hire leaves: the register is a written list with a named fallback owner in Operations.
