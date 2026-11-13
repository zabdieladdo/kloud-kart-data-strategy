# ADR-001: Reports read from a copy of the database on the second server

- **Status:** Pending
- **Date:** 2026-11-13
- **Decision owner:** Nana Adjei, Head of Operations (proposed by Zabdiel Addo, consultant)

## Context

Orders, stock and customer accounts live in one MySQL database (about 40 GB) on the same box as the live website. Nana's Monday export (a few hundred thousand rows) slowed the site to a crawl twice last month. Base case: about 62 orders lost per slowdown and about 1,500 a year (diagnosis assumptions A1 to A4: 250 orders an hour, 60-minute slowdown, 25% of orders lost, 24 slowdowns a year). A second server is pre-approved. The site must stay up.

## Decision

We move all reporting reads to a copy of the live database on the pre-approved second server, kept in step with the live database continuously, and stop running exports against the live box. Until the copy is live, the export runs overnight.

## Alternatives considered

### Alternative A: nightly export at 02:00 into a separate database

- **How it would work:** the same export, scheduled for 02:00, loaded into a database on the second server that reports read from.
- **Why it is attractive:** nothing new to keep in sync, no setup beyond a schedule, and almost no shoppers at 02:00.
- **Why rejected:** it still loads the live box every night, so it moves the load rather than removing it; a customer deleted on the live database stays in the copy until the next full reload, which matters with a complaint on a 90-day clock; and it fails if Nana's Monday figures need Monday-morning orders.

## Consequences

- **What this buys:** the shop's speed no longer depends on reporting; deletions on the live database reach the copy automatically.
- **What this costs:** one more copy of every customer to list in the register and include in each deletion; a delay between the live database and the copy that someone must watch; the developer's hours to set it up while he also keeps the shop up.
- **What it costs the client if I am wrong:** if the second server shares disk or hardware with the live box (unconfirmed), the slowdowns continue at about 62 orders per slowdown in the base case until the copy is moved to separate hardware.
- **What would make me revisit this:** the copy falls more than 5 minutes behind the live database during the Monday report hour on two Mondays in a row; or the developer confirms the second server shares hardware with the live box.

## What this survives

- Orders double: the copy handles 80 GB as easily as 40 GB.
- The Commission escalates: deletions carry through to the copy, and the register lists it.
- The developer leaves: this is standard MySQL work that any replacement knows.
- The board insists on real-time: unaffected; any stream would be added alongside the copy, not instead of it.
