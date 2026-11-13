# ADR-003: Refresh reports daily, fix stock at checkout, and run no streaming platform

- **Status:** Pending
- **Date:** 2026-11-13
- **Decision owner:** Nana Adjei, Head of Operations (proposed by Zabdiel Addo, consultant)

## Context

The brief sets the freshness rule: stock counts cannot go stale, because that is how the company oversells; everything else can refresh daily. Investors asked about "real-time analytics" and a board member wants "real-time dashboards". Nana reviews figures weekly and Finance closes monthly. The company has two data hires and one developer who also keeps the shop up.

## Decision

We refresh all reporting once a day. Checkout reserves stock in the same step that records the order, on the live database, so the shop cannot sell what the system shows it does not have. The reporting copy of stock is overwritten every 5 minutes from the read replica and shows the time it was last updated. We run no streaming platform.

## Alternatives considered

### Alternative A: managed stream for stock events

- **How it would work:** checkout sends a message for each stock change to a vendor-run service; a small program of ours reads the messages and updates the reporting copy of stock within seconds.
- **Why it is attractive:** stock figures seconds old, a vendor runs the service, and the investors get the real-time they asked about.
- **Why rejected:** overselling likely happens at checkout on the live database, and a stream only makes the reporting copy faster; nobody buys from the reporting copy. It adds a change to checkout code, a vendor service with a monthly bill, a reader program to write and run, and an on-call duty for "the reader is down" (copy shows too much stock) and "a message arrived twice" (copy shows too little, permanently), taken from two hires with a 90-day deletion clock running.

### Alternative B: hourly refresh for all reports

- **How it would work:** the same loads as the daily refresh, run every hour, so dashboards are never more than an hour old.
- **Why it is attractive:** fresher figures with no new parts; the most likely compromise if the board pushes back on daily.
- **Why rejected:** no decision in the brief is made hourly (Nana reviews weekly, Finance closes monthly), so the extra runs buy nothing anyone acts on; a full reload every hour puts 24 loads a day on the copy, and the lighter option, loading only changed rows, needs a reliable "last changed" time on every table and misses deleted rows, which works against the deletion complaint; and 24 runs a day means 24 chances a day to fail and be watched.

## Consequences

- **What this buys:** the stock harm is fixed where it happens; one simple refresh to run and rerun; no extra vendor, bill or on-call duty.
- **What this costs:** no "real-time" label for the investors; report figures up to a day old; a change to checkout code that the developer must make while keeping the shop up.
- **What it costs the client if I am wrong:** overselling happens and rampant: the weekly count of orders cancelled for lack of stock, times the cost of each cancellation (refund handling and a customer let down; not priced).
- **What would make me revisit this:** orders cancelled because the system showed stock that did not exist stay above 1 a week at the end of Q2, after the checkout fix; Kloud Kart starts screening payments for fraud itself rather than through its payment provider; or orders reach 40,000 a day (10 times today).

## What this survives

- The board insists on real-time: first, stock is correct at checkout and every figure shows when it was updated. If the board still insists, a new ADR supersedes this one and adds a managed stream for stock only, with a named owner, the hosting question answered and the bill accepted; the daily core does not change.
- Orders double: a daily refresh of 80 GB still fits overnight.
- One hire leaves: one daily job is simple to hand over.
