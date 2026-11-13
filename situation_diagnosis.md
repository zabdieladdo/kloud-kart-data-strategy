# Kloud Kart: Situation Diagnosis

**Prepared for:** Nana Adjei, Head of Operations
**Consultant:** Zabdiel Yidjiemo Addo
**Date:** 13 November 2026

## 1. Summary

There are four root causes identified from the brief, namely:

- **Root Cause 1: Reads for reporting are taken from the live database.** The Monday export runs on the same box as the website, and a full pull of a few hundred thousand rows competes for resources with shoppers.This has a visible and direct cash and brand cost each time it happens, and it hits customers. The damage it leads to is already bounded, and there is a pre-approved and cheap solution.
- **Root Cause 2: There is no agreed written definition of "sales".** The Head of Operations and Finance each apply their own rules and definitions across the business. Each figure is correct by its owner's rules. It is a silent issue that affects most decisions about stock, revenue and anything pertaining to "sales". It also undermines board conversations and discussions, and leads to disagreement between departments and figures nobody can vouch for.
- **Root Cause 3: The reports are rebuilt weekly by hand.** Nana's logic and spreadsheet handle this, and it is not documented, repeatable or audited. It is only vital when Nana is away or unavailable, in which case no Monday figures and reports are built or replicated.
- **Root Cause 4: Nobody tracks copies of personal data or owns the data.** Exports are made with no record of who took them, where they went and when records are deleted. A customer record deletion only affects MySQL.
It has a hard deadline set by an outsider (a 90-day clock; I assume 90 days remain, A13); up to 300,000 people in each untracked copy; an unknown number of copies; and finding one customer in every copy takes an unbounded amount of time. It has legal and reputational consequences. Fines are small (150–250 penalty units), but the Commission can order processing to stop. As such it takes the highest precedence and risk.



## 2. How this diagnosis is built

- Causes are ranked by risk to the board conversation, not by cost or by how irritating they are.
- Costs are given in orders, hours, days and people. Cedis appear only where an assumption supports them.
- Assumptions are numbered (A01…) and listed in Appendix A, because Nana couldn't be asked.

## 3. Symptoms to causes

| What Kloud Kart sees | What produces it | Cause |
|---|---|---|
| Website becomes slow on Monday | Analytical data extraction competes with live transactions for production resources | RC1 |
| Finance and Nana disagree | No agreed revenue definition or ownership of business rules | RC2 |
| Customer deletion is difficult | Personal data is distributed across untracked exports and other copies | RC4 |
| Nana rebuilds the Monday numbers by hand every week | The report's logic lives only in her spreadsheet, so it is rebuilt each time and can't run without her | RC3 |

## 4. Root causes, in rank order

### RC4: Nobody tracks copies of personal data or owns the data

**What it costs:**

- A deadline set by an outsider: 90 days (A13).
- Up to 300,000 people in each untracked copy, with the number of copies unknown.
- Finding one customer has no time limit today, because nobody knows where to look.
- Fines of 150–250 penalty units for the relevant offences, about GHS 1,800–3,000 (A18).
- The Commission can order processing to stop, which for an online shop means stopping trade, and customers can claim compensation.

**Why it ranks here:** It is the only cause that has already happened (the complaint exists), has an outsider's deadline, and can't be undone. It also gets worse under our own plan: the replica adds one more copy of every customer, and a warehouse adds another.

**Objection noted:** "You have no penalty figure and no days remaining." The ranking rests on things that are certain: the deadline, the irreversibility, and the fact that it has already happened.

**What would move it:** The complaint concerns only the MySQL record (no copies involved), and most of the 90 days are left.

### RC2: No agreed written definition of "sales"

**What it costs:** Finance spends 1–2 hours a week reconciling against Nana's figure (A11). Over 48 working weeks (A09), that is **48–96 hours a year**. The larger cost is the share of sales nobody can vouch for: every decision about stock, advertising and hiring starts from a disputed number. Nana's rebuilding time is counted under RC3, not here.

**Why it ranks here:** The board's first question, what did we sell, gets two answers, and every decision about stock, advertising and hiring starts from that number. It also blocks the plan: anything built before the definition exists produces two figures faster.

**Objection noted:** *"48–96 hours a year is trivial, and one meeting could fix it."* The cost is the decisions and time spent disagreeing built on the number, not the hours.

**What would move it:** If one week's line-by-line comparison traces most of the gap to a single rule (the cut-off time), a meeting settles it and RC2 drops in rank.

### RC1: Reporting reads compete with shoppers for the live database

**What it costs:**

1. 4,000 orders a day (brief).
2. Orders spread over 16 trading hours: 4,000 ÷ 16 = 250 orders an hour (A01).
3. A slowdown lasts 60 minutes, so 250 orders are affected (A05).
4. 25% of those are lost: 250 × 0.25 = 62.5 orders lost per slowdown (A06).
5. Two a month (brief) × 12 = 24 a year, assuming the rate continues (A07).
6. 62.5 × 24 = **1,500 orders lost a year**.

Other calculated ranges: 30 minutes at 10% gives 12.5 × 24 = 300 a year; 120 minutes at 50% gives 250 × 24 = 6,000 a year (Appendix B).

**Why it ranks here:** It is the largest costed loss, but it is the lowest risk to the board conversation. The fix is pre-approved, and the board can be shown it is solved within weeks.

**Objection noted:** "It's the only cause with a measured loss, and it hits customers." True, which is why it is fixed first. The ranking measures what remains after the cheap fix, and here little does.

**What would move it:** If the overnight stopgap isn't possible (A08), the second server shares hardware with the live box (A25), or the developer has no hours for the copy (A27).

### RC3: The reports are rebuilt weekly by hand

**What it costs:** Nana's 2–3 hours of rebuilding a week (A10): 96–144 hours a year, about 12–18 working days. No Monday figures when Nana is away.

**Why it ranks here:** It is mostly a result of RC1 and RC2. Once the copy and the definition exist, it goes away.

**Objection noted:** "Nana is a single point of failure." The fix is already in the plan, so the risk ends when RC1 and RC2 are fixed.

**What would move it:** Nana leaves, or her logic turns out to be undocumented and impossible to rebuild.

## 5. My Rankings
| Rank by risk | Cause | Cost | The board question it leaves unanswered | Rank by cost |
|---|---|---|---|---|
| 1 | RC4 | 90-day clock; up to 300,000 people per copy; search time unbounded; 150–250 penalty units | "Are we compliant, and can we prove it?" | Not costable |
| 2 | RC2 | 48–96 h a year; share of sales nobody can vouch for | "What did we sell last quarter?" | 3 |
| 3 | RC1 | ~1,500 orders a year (300–6,000) | "Why does reporting slow the shop?" | 1 |
| 4 | RC3 | 96–144 h a year; no figures when Nana is away | "What happens when Nana is away?" | 2 |

## 6. Risks outside the ranking

- **The Nigeria pilot:** whether its data is in the same database and which rules apply (A19; s.18(2)).
- **Asks that start from tools, not decisions (context):** the wish list names products rather than decisions; the recommendation answers it under "What we are saying no to".
- **Overselling (risk):** stock wrong at the moment of sale; how often and why are unknown (A22). The recommendation addresses it at checkout (ADR-003).

## 7. The questions I would have asked Nana

Nana was unavailable, so each question is paired with the assumption I recorded instead, in the order I would ask them.

| # | Question | Cause | Choice its answer changes | Assumption recorded |
|---|---|---|---|---|
| 1 | "Walk me through last Monday from the moment you sat down: what did you open, what did you copy, what did you decide from it, and what went wrong?" | RC3, RC2 | What the first thin slice is, and the report's shape | She rebuilds a weekly sales and stock summary for reorder and promotion decisions |
| 2 | "When the complaint arrived, what did the customer say we still held, where was it found, and when did the letter arrive?" | RC4 | Whether privacy work takes the developer's time ahead of the replica (the ~35-day cut-off) | The data was in a copy outside MySQL (A14); 90 days remain (A13) |
| 3 | "Who has taken a customer list out of the system in the past year, and where did each copy go?" | RC4 | How large the copy search is, and the scope of the register | Marketing, Operations and Finance, plus at least one outside platform |
| 4 | "Take one order placed Sunday night, paid Monday and partly refunded Wednesday: which week and what amount does it count as for you, and for Finance?" | RC2 | Whether the fix is a signed definition or a build, and which hire comes first | **Marked assumption:** the gap is a few rules you can name (A20) |
| 5 | "When your figure and Finance's differ, who decides which one goes to the board?" | RC2 | Who signs the definition, and whether the month-2 gate can actually stop a build | Nobody has that authority today, so the board must name someone (A21) |
| 6 | "Tell me about the last time an item showed as available and wasn't: how did you find out, how long was it wrong, what happened to the order?" | Overselling (risk) | A live check at checkout versus a five-minute copy, and the streaming position | A few a month; the system count was wrong, not the shelf (A22) |
| 7 | "On the two Mondays the site slowed, what time did you start the export, how long until it recovered, and did customers complain?" | RC1 | Cost inputs, and whether moving the export to a quiet hour works as a stopgap | Monday morning, about an hour (A05) |
| 8 | "Do your Monday figures need Monday morning's orders, or would orders up to Sunday midnight do?" | RC1, RC3 | Whether an overnight copy and a daily refresh are enough | Up to Sunday midnight is enough (A08) |
| 9 | "When the investors asked about real-time analytics, what were they looking at or worried about?" | Context | Whether "real-time" means seconds, or current and trusted figures | Current and trusted figures (A31) |
| 10 | "Where do Nigerian customers' orders and details end up: in the same system and report as Ghana's, or somewhere else?" | Risk (Nigeria) | One store, a filter before loading, or a separate store; s.18(2) of Act 843 | Same database, with a country field (A19) |

## 8. What I could not verify

- Days left on the complaint (assumed 90, tested at 30; A13).
- Order value (A02).
- Slowdown length and the share of orders lost (A05, A06).
- How often overselling happens and why (A22).
- Whether the second server is separate hardware (A25).
- Salaries (A28) and the penalty unit value (A18).

---

## Appendix A: Assumptions register

Every figure marked as an assumption is a judgement, not a sourced fact. The same numbers are used across the diagnosis, recommendation, roadmap and decision records.

### Business volume

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A01 | Orders are spread over 16 trading hours: 4,000 / 16 = 250 an hour | Brief gives 4,000 a day; 16 hours is a judgement (24 hours gives 167 an hour) | Over 24 hours, lost orders fall by a third |
| A02 | Average order value is GHS 400 | Jumia physical-goods average about USD 35–37 (2025 earnings calls) × GHS 11.64 per USD (Bank of Ghana rate, 9 Nov 2026); Jumia is multi-country and may differ | Halving it to GHS 200 still leaves RC1 costing more than its fix |
| A03 | Gross margin is 20% | Judgement; only needed if lost profit, not lost sales, is shown | Changes the profit figure in proportion |
| A04 | Data grows with orders, 15–20% a year | Brief gives order growth; data growth assumed to follow | Faster growth brings the 500 GB trigger closer |

### The slowdowns

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A05 | Each slowdown lasts 60 minutes (range 30–120) | Judgement; brief says only "slowed to a crawl" | Range shown: 300–6,000 orders a year |
| A06 | 25% of orders during a slowdown are lost for good (range 10–50%) | Judgement | Range shown |
| A07 | Two slowdowns a month continue: 24 a year | Brief: "twice last month" | Fewer slowdowns lower the cost in proportion |
| A08 | Nana's Monday figures can be built from orders up to Sunday midnight | Judgement; makes the overnight export a workable stopgap | If not, the stopgap fails and the copy is needed sooner |

### Staff time

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A09 | 48 working weeks a year | 52 weeks minus leave and holidays | Small effect |
| A10 | Nana spends 2–3 hours a week rebuilding the Monday report | Judgement | Changes RC3's cost in proportion |
| A11 | Finance spends 1–2 hours a week reconciling against Nana's figure | Judgement | Changes RC2's labour figure only |
| A12 | Loaded staff cost GHS 100 an hour | Guess; used only if labour is shown in cedis | Hours are shown instead |

### The complaint and Act 843

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A13 | 90 days remain on the complaint, tested at 30 | Brief: "90 days to respond", read literally | Below about 35 days, privacy work takes the developer ahead of the copy |
| A14 | The deleted customer's data was found in a copy outside the live database | Most likely reading; brief does not say | If only in the live database, the complaint is quicker to answer, but the register is still needed |
| A15 | The privacy work's critical path is 18–30 days | Task durations estimated by judgement | Longer tasks move the cut-off above 35 days |
| A16 | Registration with the Commission is unknown; checked in month 1 | Brief silent; s.56 makes processing without registration an offence | If lapsed, registration becomes the first task |
| A17 | The privacy notice customers saw covers using their order data for internal reporting | Brief silent; Act 843 s.25 (further processing must fit the original purpose) | If not, the notice must change before the reporting database holds customer-level data |
| A18 | A penalty unit is GHS 12 | DLA Piper Ghana guide (2023); current value to be verified | Fine figures scale in proportion; the ranking does not rest on them |
| A19 | Nigerian orders are in the same database, with a country field | Brief silent | If separate, a second source to copy; s.18(2) handling may need a filter before loading |

### The definition of a sale

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| **A20 (marked)** | **The gap between Nana's and Finance's figures comes from a few rules that can be named (cut-off, refunds, status changes)** | **Judgement; the brief says only that they never match. This is the assumption whose being wrong would most change the recommendation.** | **If many differences, the definition work becomes the first build and takes longer; if one rule, a meeting settles it** |
| A21 | Nobody has the authority to settle a dispute between the two figures; the board names someone | Judgement | If someone already has it, the month-2 gate is easier to enforce |

### Stock

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A22 | Overselling is caused mainly by checkout not reserving stock in the same step as the order; how often is unknown | Brief: "that's how the company oversells"; cause not stated | If mainly shelf miscounts, the fix is stock counting, not checkout |
| A23 | Cancelled orders can be identified from order status or customer-service records | Judgement | If not, the count is done by hand or needs a cancellation reason added |
| A24 | The payment provider screens payments for fraud | Judgement | If Kloud Kart screens fraud itself, a second flow needs seconds-level speed |

### Technical

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A25 | The pre-approved second server is separate hardware from the live box | Brief says pre-approved; separation not stated | If shared, the slowdowns continue until it is moved |
| A26 | Deletions on the live database carry through to the copy; backups expire on a set schedule | Usual behaviour of a database copy; backup schedule unknown | If backups are kept indefinitely, they must be listed and handled in the register |
| A27 | The developer has hours for the copy and the checkout change alongside keeping the shop up | Brief silent | If not, the copy and the stock fix slip |

### People and money

| # | Assumption | Basis | If wrong |
|---|---|---|---|
| A28 | Monthly salary: data engineer GHS 7,000–25,000; analytics engineer GHS 11,100–18,000; two hires about GHS 250,000–500,000 a year | (Employsome, 2026) | Changes the cost line |
| A29 | Both hires are recruited in month 1 and start at the beginning of month 2 | Judgement | If later, Q2 outcomes slip by the delay |
| A30 | Each hire owes 0–4 hours a week to keeping the shop up | Brief silent | At more than 4, building time shrinks |
| A31 | By "real-time analytics" the investors meant current, trusted figures, not seconds-old data | Inference from the brief's problems | If they meant seconds, stock and site monitoring weigh more |

## Appendix B: RC1 cost across assumptions

Annual orders lost = 250 orders an hour (A01) × (minutes ÷ 60) × share lost × 24 slowdowns (A07).

| Slowdown length | 10% lost | 25% lost | 50% lost |
|---|---|---|---|
| 30 minutes | 300 | 750 | 1,500 |
| 60 minutes | 600 | **1,500 (base)** | 3,000 |
| 120 minutes | 1,200 | 3,000 | 6,000 |

At GHS 400 an order (A02), the base case is about GHS 600,000 a year in lost sales, or about GHS 120,000 in lost profit at a 20% margin (A03).
