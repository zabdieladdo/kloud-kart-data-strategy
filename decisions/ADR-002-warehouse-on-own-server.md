# ADR-002: Build a warehouse-shaped store on the pre-approved server, not a cloud warehouse, lake or lakehouse

- **Status:** Pending
- **Date:** 2026-11-13
- **Decision owner:** Nana Adjei, Head of Operations (proposed by Zabdiel Addo, consultant)

## Context

All of Kloud Kart's data is about 40 GB of relational tables in one MySQL database. Nana's and Finance's sales figures never match, because nothing holds one agreed definition of a sale. The company has one developer (PHP/MySQL); nobody has run a warehouse or written Python professionally. The developer wants to "just buy Snowflake or BigQuery"; Finance flinched at the cost. The board has budgeted two data hires, a second server is pre-approved, and the plan must be defensible under Act 843 with a deletion complaint open.

## Decision

We build a second relational database on the pre-approved server, with its table structure fixed before data is loaded, holding one agreed definition of a sale. Reports, including Nana's Monday report, read only from it.

## Alternatives considered

### Alternative A: managed cloud warehouse (Snowflake or BigQuery)

- **How it would work:** data is copied from the read replica into a vendor-run warehouse; the same SQL definitions and reports run there; the vendor runs the servers, storage and scaling.
- **Why it is attractive:** no server for the hires to patch or back up, fast to set up, cheap storage at 40 GB, scales without effort, and the developer already wants it.
- **Why rejected:** it bills by use, which Finance has already flinched at, and a badly written refresh repeats the charge; customer data would sit on a vendor's servers, possibly outside Ghana, which brings s.30(4) duties and a safeguards case; it is one more copy of every customer that each deletion must reach inside the 90 days; and it is a new tool for a team where nobody has run a warehouse.

### Alternative B: data lake or lakehouse

- **How it would work:** raw files from MySQL are kept in cheap storage; structure is applied when each report reads them (lake), or a table layer adds database-style guarantees on top (lakehouse).
- **Why it is attractive:** cheapest storage for any kind of data, raw history kept for later, and a path open to machine learning, which the wish list mentions.
- **Why rejected:** there is no non-relational data to store; when structure is applied at reading time, each reader decides what a sale is, which rebuilds the Nana-Finance disagreement; removing one customer from raw files means rewriting files; and a lakehouse adds the most moving parts for two hires, for a forecast nobody can build until sales figures are agreed.

## Consequences

- **What this buys:** one place where a sale is defined once; SQL on tools close to what the developer already knows; a near-fixed cost on a server already approved; customer data stays on servers Kloud Kart controls.
- **What this costs:** the hires must run, secure and back up the server; every new data source needs design work before it can be reported on; no machine learning in year one.
- **What it costs the client if I am wrong:** if running the server consumes more of the hires' time than expected, moving to a cloud warehouse later costs a few weeks of the data engineer's time; at about 40 GB in standard SQL, the move is small.
- **What would make me revisit this:** running the server takes more than one working day a week (8 hours) of the hires' combined time for 4 weeks in a row; a non-relational data source is added (product images, click records, supplier files); or stored data passes about 500 GB.

## What this survives

- Growth at 15 to 20% a year: about 100 GB in five years, well inside one server.
- The Nigeria pilot grows: Nigerian orders are a country column and a filter before loading, not a new platform.
- The board insists on real-time: a stream can be added in front for stock; this store does not change.
- One hire leaves: the tools are SQL and MySQL, which the developer can keep running until a replacement starts.
