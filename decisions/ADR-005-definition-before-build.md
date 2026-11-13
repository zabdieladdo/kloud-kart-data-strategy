# ADR-005: Build no sales report until Nana and Finance sign one definition of a sale

- **Status:** Pending
- **Date:** 2026-11-13
- **Decision owner:** Zabdiel Addo; pending acceptance by Nana Adjei and the Finance lead

## Context

Nana's and Finance's sales figures never match. Each is correct by its owner's own rules, so neither is wrong and no data cleaning settles which to use. Nobody owns the definition of a sale, and nobody has the authority to settle a dispute between the two. A faster pipeline built now would deliver both figures sooner. The board is funding two salaries partly to get one trusted number.

## Decision

Nana and Finance sign a one-page definition of a sale (which orders count, at what point, refunds in or out, cut-off time and time zone) by the end of month 2. The analytics engineer builds the sales report from that definition only. If it is not signed by the end of month 2, the dispute goes to the board for a decision before the report is built.

## Alternatives considered

### Alternative A: build first and settle the definition inside the warehouse

- **How it would work:** the hires build the reporting database and the report from month 2, computing both figures side by side, and use the data to show where they differ and agree a definition along the way.
- **Why it is attractive:** no waiting; the hires are productive from day one; and the data itself may reveal the cause of the gap faster than a meeting.
- **Why rejected:** without anyone holding the authority to decide, the build produces two figures more neatly, and two salaries are spent hosting the disagreement; the definition is a business decision that a hire cannot make for Finance.

## Consequences

- **What this buys:** the first report is the one number the board asked for; the hires build against a fixed target; the signed page outlives staff changes.
- **What this costs:** the report waits on two busy people agreeing; the board may be handed a decision it does not want; the analytics engineer spends the first weeks on preparation rather than building.
- **What it costs the client if I am wrong:** if the gap would have been obvious from the data, up to a month of the analytics engineer's time is spent waiting.
- **What would make me revisit this:** the definition is not signed by the end of month 2; or a line-by-line comparison of one week in month 1 traces 90% or more of the gap to a single rule, such as the cut-off time, in which case sign that rule in a week and build at once.

## What this survives

- A hire starts late: signing is business work and does not need either hire.
- A change of Finance staff: the signed page stays and binds the next person.
- The board pushes for speed: the comparison test above offers a fast path when the gap is simple.
