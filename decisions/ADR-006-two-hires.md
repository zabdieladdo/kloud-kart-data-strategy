# ADR-006: Hire a data engineer and an analytics engineer together, both starting in month 2

- **Status:** Pending
- **Date:** 2026-11-13
- **Decision owner:** Kloud Kart board and Nana Adjei, Head of Operations (proposed by Zabdiel Addo, consultant)

## Context

The board has budgeted two data hires this year, not three. Four problems need an owner: the live box slowed by reporting, two figures for sales, the Monday report rebuilt by hand, and untracked copies of customer data under a 90-day complaint. Nobody owns data today. The one developer (PHP/MySQL) also keeps the shop up, and nobody has run a warehouse or written Python professionally. The wish list asks for forecasting "eventually".

## Decision

We hire a data engineer and an analytics engineer at the same time, both starting at the beginning of month 2. The data engineer owns the copy, the nightly loads, failure alerts, the register of copies and the monthly deletion test. The analytics engineer owns the agreed definition in tested SQL, the Monday report and the check that it matches Finance's figure and some analytics. Explaining why numbers moved, and heavy forecasting, are not staffed this year.

## Alternatives considered

### Alternative A: data engineer and data analyst

- **How it would work:** the data engineer builds the copy and loads; the analyst answers Nana's and the board's questions and builds dashboards.
- **Why it is attractive:** someone whose job is explaining the numbers, which is what Nana and the board most want to hear; easier to sell to investors as "insight".
- **Why rejected:** nobody builds and owns the agreed tables, so the definition of a sale would live in the analyst's own tool and become a third version; the analyst would rebuild Nana's Monday spreadsheet in a nicer tool.

### Alternative B: hire one now and the second later in the year

- **How it would work:** hire the data engineer first; hire the second role once the copy and loads are running and the first hire can help choose.
- **Why it is attractive:** spreads the salary cost, and the first hire's experience sharpens the second job description.
- **Why rejected:** the 90-day complaint and the definition work run at the same time; with one hire, one of them waits, and the open complaint cannot.

## Consequences

- **What this buys:** work runs in parallel from month 2; each hire can cover the other's basic duties from early on; every problem has a named owner.
- **What this costs:** both salaries from month 2 (GHS 250,000 to 500,000 a year on the salary ranges used; to be confirmed against a named source); nobody whose job is explaining why numbers moved; forecasting waits a year; month 1 has no hires, so the developer, Nana, Finance and an Operations owner carry it; two people are harder to recruit at once.
- **What it costs the client if I am wrong:** if the analyst was the better second hire, months of one salary are spent on the wrong role, and Nana keeps explaining the numbers herself.
- **What would make me revisit this:** questions from Nana and Finance take more than one working day a week (8 hours) of the analytics engineer's time for 4 weeks in a row by month 6, which makes the case for a third hire, an analyst, next year; or either hire leaves.

## What this survives

- One hire leaves: the tools are SQL and MySQL; every part has a one-page runbook and the SQL is in versioned files; each hire can run the other's parts at a basic level by month 3; failure alerts go to both; the developer keeps the copy and nightly load running, and the Operations owner runs the monthly deletion test, until a replacement starts.
- A hire starts late: Q1 needs neither hire; if the data engineer is late, the developer keeps the copy running; if the analytics engineer is late, the "one number" outcome slips by the length of the delay.
- The board asks for forecasting early: stock history is collected from Q2, so forecasting can be revisited at the Q4 board review.
