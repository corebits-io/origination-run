---
name: population-sourcing
description: "Enumerate the whole population inside a mapped segment at volume - two thousand rows or more - from licence rosters, registries, association directories, installer locators, exhibitor lists and award records, with a source ledger per pull, honest cap reporting, deduplication at scale, and a coverage log that names what the pull missed. Triggers on: enumerate the population, find the companies, build the target list, source two thousand companies, pull the licence roster, who are the operators in this segment, source ledger, coverage log."
---

# Population Sourcing

This is the step that decides whether the list is proprietary. Everything after
it is processing.

The job is not to find good companies. It is to enumerate **all** the companies
inside the boundary, including the ones that look unpromising, because at depth 0
you cannot tell the difference between a company with no website and a company
with no marketing budget, and the second one is the whole point.

**Read first:** `segment-map-[run]-[date].md` — specifically the source list and
the boundary; `references/sourcing-directories.md`; `MANDATE.md` sections 4, 5
and 8.

---

## Step 0 — Preconditions

1. **A segment map exists, and its verdict is not DO NOT SOURCE IT.** If there
   is no map, stop and run `segment-mapping`
2. `targets.csv` exists with the 40 columns from `templates/targets.csv`
3. `source-ledger.csv` exists
4. `suppression.csv` is loaded with everything from mandate section 8
5. The enumeration target and the depth 2 cap are in `run/state.json`

---

## Step 1 — Work the sources in tier order, one at a time

Start with Tier 1. The spine of the list should be statutory or regulatory.

**Pull the whole population, then filter. Never search and cherry-pick.**
Searching a roster for the names you recognize biases the list toward the
well-marketed, which is the exact opposite of the point.

Before each pull, write the ledger row: what population the source covers, how
you filtered it, the date. After it: what it returned, whether it capped, how
many rows were new, how many were duplicates.

One source per batch. Report, write, then the next one. A single pass that works
eleven sources and reports at the end is a pass whose first mistake repeats
eleven times.

---

## Step 2 — One row per company, with its source

At depth 0, fill only these fields:

`company`, `domain`, `hq_location`, `country`, `sector`, `segment`, `source`,
`source_count`, `year_founded`, `employee_count`, `date_added`, `depth` = `0`

Leave everything else blank. Ownership, size, signals, verdicts and contacts are
later depths with their own rules, and a half-guessed ownership field written
here is worse than an empty one, because it looks like research.

The `source` string must be specific enough that somebody else could re-run the
pull:

```
Good:  Georgia electrical contractor licence roster, EC and EU classes,
       Fulton + DeKalb + Cobb + Gwinnett counties, complete pull 2026-10-02;
       cross-found in IEC Atlanta member directory and 2026 NECA exhibitor list

Bad:   licence roster
Bad:   web search
```

**Never fabricate a domain.** If a company has no website, `domain` is blank and
that is a fact about the company, not a gap in the research.

---

## Step 3 — Cross-find, and count it

A company appearing in three independent sources is a real company. One appearing
in a single aggregator may be a duplicate, a dissolved entity, or a holding shell
with no operations.

Append each additional source to the `source` string rather than overwriting it,
and keep `source_count` current. Rows whose only source is Tier 4 do not carry
forward until they are confirmed against a Tier 1 or 2 record.

Report the cross-find distribution at the gate. In the sample run, 48% of rows
were cross-found in two or more sources and 94 of the single-source rows were
roster-only — which is the proprietary end of the list, not the weak end.

---

## Step 4 — Deduplicate

At two thousand rows the duplicates are not visible by eye. Merge on **domain**
first, then **licence or registry number**, then **normalized name plus
postcode**.

Watch for trading name versus registered name, holding and operating entities
listed separately, branch offices appearing as companies, entity suffix noise,
hand-typed registry spelling variants, and the same company licensed in three
states.

Keep the merged row, put the other names in `notes`, and **keep every source
string**. A dedupe that silently drops a source string destroys the cross-find
evidence that made the row credible.

Report the count. In the sample run 2,417 collapsed to 2,140: 183 name variants,
61 branches, 33 holding and operating pairs.

---

## Step 5 — The one filter that runs here

Only one, and only when it is free and certain: **a row that is not a company**.
A supply house listed as a contractor, a trade school, a trade association
itself, a dissolved shell with no licence and no operations.

Everything else waits for `desk-screening`. Geography, segment, licence status
and suppression all run at depth 1 in one pass, where the drop reasons get
recorded consistently.

Resist the temptation to pre-filter as you pull. It feels efficient and it
produces a list whose exclusions nobody can audit.

---

## Step 6 — The coverage log

Written at the gate, kept in the run file and in `known_gaps` in the state file.

```
COVERAGE LOG — 2026-10-04

Sources worked
  Georgia licence roster        complete pull, 1,840 rows, filtered to
                                EC/EU classes → 612 in scope
  Tennessee licence roster      complete pull → 441
  Alabama licence roster        CAPPED at 500 per query. Pulled per county;
                                2 counties still returned exactly 500 and
                                are incomplete. ~180 rows estimated missing
  South Carolina roster         complete pull → 305
  2 state registries            officer and status data on 1,790 rows,
                                41 new companies
  3 association directories     488 members, 206 in scope, 37 new
  5 installer locators          264 in geography, 61 new
  NECA exhibitor 2024-26        212 contractors, 74 in geography, 18 new
  2 procurement award portals   award history on 341 rows, 9 new companies
  User database export 2025     190 rows, 171 already present, 19 new,
                                all 19 flagged for Tier 1 confirmation

Known gaps
  - Alabama cap above. Rerun by licence issue year to close it
  - Building systems integrators with no electrical licence appear on no
    roster. 34 found via installer locators, certainly incomplete
  - Companies with no website and no association membership exist only in
    the rosters, so the Alabama gap is concentrated exactly there

Bias statement
  This list leans toward licensed operators, which is the segment
  definition, and toward association members and exhibitors, which
  over-represents larger and more outward-facing firms. The 40-year-old
  company that joined nothing and advertises nowhere appears only via the
  rosters, which is why the rosters went first and why the Alabama cap is
  the most important line in this log.
```

---

## Step 7 — Volume check against the target

| Result | What it means |
|---|---|
| Within 20% of the enumeration target | Normal. Proceed |
| Far under | The geography is too narrow, a source capped, or the map's population estimate was wrong. Name which. Do not pad with Tier 4 rows |
| Far over | The boundary is loose. Tighten it before depth 2, because every extra row either costs research or dilutes the screen |

### 🚧 HARD GATE — before writing

Show:

- Row count by source, before and after dedupe, with the merge breakdown
- The cross-find distribution
- The full coverage log, every cap, and the bias statement
- **15 sample rows**, including at least 3 with a blank `domain` and 3 with a
  blank `employee_count`, so the user sees what a thin row looks like before
  deciding it is a bad row
- Any row that looks like a duplicate you chose not to merge, and why

Get approval, then write to `targets.csv` and `source-ledger.csv`, update
`run/state.json`, and append to `run/log.md`.

---

## Step 8 — Report

```
SOURCING COMPLETE — 2026-10-04

Enumerated          2,417 rows from 11 sources
After dedupe        2,140   (277 merges: 183 name variants, 61 branches,
                             33 holding/operating pairs)
Cross-found in 2+   1,027   (48%)
Single source         1,113  ← 94 roster-only, the proprietary end

Field completeness
  domain            1,604 / 2,140   (536 have no website at all)
  employee_count      912 / 2,140
  year_founded      1,881 / 2,140

Coverage gaps       Alabama roster capped, ~180 rows likely missing.
                    Unlicensed integrators under-covered.

Against target      2,000 target, 2,140 enumerated. Proceed.

Next: desk-screening on all 2,140.
```

---

## Notes

- **536 companies with no website is a feature.** Hard rule 4 in the ranking
  rubric exists because those rows are frequently the best ones on the list
- **Report every cap, every time.** A truncated pull is the most common silent
  failure in sourcing and it looks exactly like a complete one
- **Never invent a headcount or a founding year.** Blank beats a guess, and the
  sizing skill is built to handle blanks honestly
- **Rows are never deleted.** Everything enumerated stays on the list and gets a
  verdict eventually, so the same company is not rediscovered next quarter
- **Write after every source.** A two-thousand-row pull that dies at source nine
  with nothing on disk is a day gone
