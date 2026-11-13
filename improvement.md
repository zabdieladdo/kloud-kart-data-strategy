# Improvement beyond the brief: Customer data register and monthly one-customer search

## The problem it solves

Nobody at Kloud Kart can say where customer data is kept. Marketing exports a list of about 300,000 people with no record of how many copies exist, Nana's Monday exports and both spreadsheets sit outside the database, and the backups and outside platforms are not listed anywhere. As a result:

- no deletion can be shown to be complete, which is the subject of the open Data Protection Commission complaint;
- a customer's "what do you hold on me" request (Act 843, s.32) cannot be answered;
- after a breach, nobody could say whose data was where (s.31).

The brief asks for an answer to this complaint. It does not ask for a way to answer the next one, or to stop untracked copies being made again. That is the gap this closes.

It differs from ADR-004. ADR-004 decides that a register should exist and that the data engineer runs it from month 2. This improvement delivers a working first version now, before either hire starts, filled from what the brief already tells us, and usable on day one for the open complaint.

## What to build

An excel file with a workbook`, with five tabs:

- **Read me:** purpose, legend, the three settings (start date, days left on the complaint, search interval), the six-step monthly search procedure and the rule for new copies.
- **Register:** 11 copies of customer data, each with where it is, which personal fields it holds, about how many people, owner, purpose, how a deletion reaches it, and whether the row comes from the brief, an assumption or the plan. Two formulas per row show days since the copy was last searched and whether a search is due.
  - From the brief: the live database, Marketing's list exports, Nana's exports, Nana's spreadsheet, Finance's spreadsheet.
  - Assumed: backups, lists uploaded to advertising or email platforms, courier delivery lists.
  - Planned in the recommendation: the database copy, the reporting database and the key table.
- **Search log:** one row per copy searched for one customer: found, deleted, evidence, who, minutes taken. Three grey example rows show the format.
- **Request log:** every deletion request, "what do you hold" request, complaint or breach, with due date, days left and copies searched calculated. Row 1 is the open complaint, due on the engagement start date plus the days left (A13).
- **Summary:** copies by status, copies due a search, open requests, days left on the complaint and total search time, all calculated.

## What it is worth to Nana

- **The complaint response becomes evidence.** Instead of "we deleted the customer from the system", she can show every listed copy, who searched it, what was found and what was done, with dates.
- **Finding one customer has a known cost.** Today the search has no end, because nobody knows where to look. With the register, the target is one working day from Q3 and one hour by Q4, and the Summary tab shows the time actually taken.
- **The next request does not start from nothing.** A deletion or "what do you hold" request follows the same procedure and lands in the same log.
- **A breach can be traced.** The register shows which copies held which fields for which people, which is what a notification to the Commission and to customers needs.
- **New untracked copies stop.** The rule for new copies (a row before any export) keeps the register true without a fresh search each time.

## What it cost

- **To build:** about 3 to 4 hours (assumption).
- **To run:** about 2 hours a month for the monthly search, plus about a working day per request (assumption), carried by the Operations owner in month 1 and the data engineer from month 2. This is already counted in the operating load (about 0.5 hours a week for the search and 2 hours a week for requests).
- **What it does not cost:** no new tool, no new server and no new copy of customer data; the register holds descriptions of copies, not the customer data itself.
- **What it does not do:** it does not delete anything by itself, and outside parties (platforms, couriers) confirm deletions on their own timetable. Section references are from Act 843 and are not legal advice.
