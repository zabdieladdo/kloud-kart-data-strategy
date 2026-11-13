# Kloud Kart: Data Recommendation

**Prepared for:** Nana Adjei, Head of Operations
**Consultant:** Zabdiel Yidjiemo Addo
**Date:** 13 November 2026

## The recommendation

My recommendation is to have a copy of the shop's database that all reporting is done from. This will be on the server you have already approved, together with one reporting system that holds the agreed rules for everything about "sales". Customer names and contacts stay out of that database, and every copy of customer data is listed, so a deletion can be shown to reach all of them. In exchange, you accept figures updated once a day rather than live, and no forecasting this year.

## Why it fits Kloud Kart

Kloud Kart's data is about 40 GB of ordinary tables in one database; one server holds that many times over, and at 15–20% growth it reaches about 100 GB in five years (A04). The site slows because reporting and shoppers share one machine, so the fix is to move reporting off it, not to buy a bigger platform. The two sales figures disagree because no rule defines a sale; a faster system would deliver both figures sooner, so the rule comes before the build. Two hires can run a database copy and SQL; they cannot also run several new platforms nobody at Kloud Kart has used. With a complaint on a 90-day clock, every new copy of customer data is one more place a deletion must reach, so the design adds as few as possible.

## What we build

| Part | What it does | Fixes | Decision record |
|---|---|---|---|
| Copy of the database on the second server | All reports read from it; the shop no longer slows | RC1 | ADR-001 |
| Reporting database on the same server | One place every report comes from, updated nightly | RC2, RC3 | ADR-002 |
| One signed rule for a sale | Nana and Finance read the same figure | RC2 | ADR-005 |
| Names and contacts removed before loading; a register of every copy | Deletions can be proven; requests can be answered | RC4 | ADR-004 |
| Stock reserved at checkout | The shop cannot sell what the system shows as gone | Overselling (risk) | ADR-003 |

## Where we do not use live streaming, and why

Overselling happens on the live database at the moment of sale. A streaming system would only make a reporting copy faster, and no customer buys from the reporting copy. So checkout reserves stock in the same step as the order, the reporting copy of stock refreshes every five minutes, and every figure shows the time it was last updated. A streaming platform would take an estimated 12–20 hours a week to run (estimate), most of the hires' spare capacity, for a need the checkout fix already meets. Nothing else in the brief is decided faster than daily: Nana reviews weekly and Finance closes monthly.

## The two hires and their roles

Hiring both at once lets the copy and the sales rule proceed in parallel; month 1 needs neither (A29). Not staffed this year: explaining why figures move, which Nana and Finance continue to cover, and forecasting.

| Role | Owns | First 90 days |
|---|---|---|
| Data engineer | The copy, nightly loads, failure alerts, the register and the monthly deletion test | Finishes the copy; runs the nightly load and alerts; completes the register; starts daily stock records |
| Analytics engineer | The sales rule in tested form, the Monday report, the check against Finance's figure, analytics | Builds the agreed sales figure; delivers the Monday report by 08:00; matches it to Finance's figure |

## What it costs

Doing nothing loses about 1,500 orders a year to slowdowns (A01, A05–A07), leaves the complaint without evidence that every copy was cleared, and keeps every decision about stock, advertising and hiring resting on two figures.

| Item | Cost |
|---|---|
| Two salaries | About GHS 250,000–500,000 a year (A28; source to be named) |
| Second server | Already approved; close to a fixed cost |
| Developer time | Setting up the copy and the checkout change, alongside keeping the shop up (A27) |
| Running the system | About 16.5 hours a week of the hires' 80 (estimate); nothing in it needs anyone woken at night |

## What we are saying no to

| Request | Answer |
|---|---|
| "A data warehouse, or maybe a lakehouse" | A reporting database, yes. A lakehouse adds storage for machine learning that no decision in the brief needs. |
| "Real-time dashboards" | Stock is correct at checkout, and every figure shows its update time. Reports can refresh hourly later if a decision needs it. |
| "ML for demand forecasting" | Not this year. A forecast needs an agreed sales figure and stock history; stock history starts in Q2. |
| "Just buy Snowflake or BigQuery" | Not now: billed by use, holds customer data on a vendor's servers, and nobody here has run it. Revisit if running our own server takes more than a day a week (ADR-002). |

## Build order

Stop the damage first, then fix what we would most regret getting wrong. In month 1, with no hires yet, the export moves overnight, registration is confirmed, the search for every copy of the complaining customer starts, and Nana and Finance begin drafting the sales rule. The first piece built end to end is last week's sales, from copy to report, in Q2: it tests every part against one number Nana already knows.

## Customer data and the law

The reporting database holds no names, phone numbers or emails; they are replaced with a key held separately. The register lists every copy with an owner and how a deletion reaches it, and is tested monthly by finding one customer everywhere. Registration with the Data Protection Commission is checked in month 1, since processing without it is an offence (s.56). I assume the notice customers saw covers internal reporting (A17); this is also checked in month 1.

## What this survives, and what would change it

- **The board insists on real-time:** stock at checkout and hourly refresh first; a stream for stock only if still required, added without changing the rest.
- **One hire leaves:** the tools are SQL and MySQL, every part has a one-page runbook, and the developer keeps the copy running until a replacement starts.
- **Orders double, or a second complaint arrives:** 80 GB fits the same server; the register shows every copy.

I would change this recommendation if the copy falls more than 5 minutes behind during the Monday report on two Mondays running (ADR-001); the sales rule is not signed by the end of month 2 (ADR-005); or cancellations caused by a wrong system count stay above one a week at the end of Q2 (ADR-003).

## What I could not verify

Days left on the complaint (assumed 90, tested at 30), order value, slowdown length, how often overselling happens and why, whether the second server is separate hardware, salaries and the penalty unit value. Each is listed with its basis in the diagnosis, Appendix A (A01–A31).
