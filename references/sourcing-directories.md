# Where Two Thousand Companies Actually Come From

A list pulled from an M&A database covers the companies that have been written
about, which is the same population every other fund is calling. The companies
that appear on a state licence roster and in no aggregator are, in their large
majority, the ones nobody has phoned.

This file is about where to get volume without getting the wrong volume.

**The discipline that matters more than the source list:** pull the whole
population, then filter. Never search a roster for the names you recognize.
Searching biases the list toward the well-marketed, which is the exact opposite
of the point.

---

## Source tiers

| Tier | What it is | Why it ranks here |
|---|---|---|
| **1** | Statutory and regulatory: licence rosters, state and national registries, permit and inspection records, procurement award databases, bond and security filings | Complete by law, dated, and almost never in an aggregator. This is the spine |
| **2** | Industry infrastructure: trade association member directories, certification bodies, manufacturer dealer and installer locators, union and apprenticeship program rosters, trade show exhibitor lists | Membership implies a real operating business. Over-represents larger and more growth-minded firms, which is a bias worth naming |
| **3** | Commercial and local: chamber of commerce rosters, local business journal top-N lists, industry buyer guides, insurance and bonding broker listings | Useful for cross-finding. Rarely complete |
| **4** | Aggregators: company databases, map listings, review platforms, scraped B2B lists | Use as a **pointer** to find a Tier 1-3 record, never as a row on its own. Heavy duplication, stale entities, branch offices as companies |

A row whose only source is Tier 4 is a lead, not a company. Confirm it against a
Tier 1 or 2 record before it carries forward.

---

## Getting to two thousand

The order to work in, and roughly what each contributes in a four-state
single-segment run:

1. **The state or national licence roster, per state, complete pull.** Usually
   50-70% of the final population. If the segment is licensed, this is the run
2. **The registry, filtered by industry classification code and status active.**
   Catches the holding and operating structures the roster misses
3. **Two to four trade association member directories.** 10-20%, heavily
   overlapping with the roster, which is what makes them a good cross-find
4. **Manufacturer dealer and installer locators.** The most underused source
   there is. A manufacturer knows exactly who installs its equipment and
   publishes the list to help customers find them
5. **Trade show exhibitor lists, last three years.** Dated, which is useful. An
   exhibitor list is also a growth signal source later
6. **Procurement and contract award records.** Gives you a revenue floor you can
   verify, which is worth more than any estimate
7. **The user's own existing list or database export.** Loaded last and used as
   a cross-find, not as the spine, so its bias does not become the run's bias

If the total is far short of the enumeration target after all seven, the honest
conclusions are: the segment is smaller than the mandate assumes, the geography
is too narrow, or the segment is not licensed and has no registry handle. Say
which. Do not make the number up with Tier 4 rows.

---

## By geography

**United States.** Licensing is at state level and the rosters are usually
public and downloadable: contractors, electrical, mechanical, plumbing, HVAC,
pest, waste, medical and dental facilities, pharmacies, child care, security and
alarm, liquor, transport authorities. Secretary of State registries give entity
status, formation date and officers. UCC filings give secured lenders. Municipal
and state procurement portals give award history. Federal award data covers
anybody selling to the government.

**United Kingdom.** Easier than the US in one important way: Companies House
publishes filed accounts, officer histories and share allocations for free,
which means more `verified` revenue figures and more Tier 1 ownership evidence
than any US run will produce. Trade body registers are strong. Licence rosters
are sector-specific and sit with the relevant regulator.

**EU.** Varies sharply by country. Some national registers publish accounts,
some publish nothing useful without a paid lookup. The market map step decides
whether ownership and size are publicly establishable in a given country
*before* the run commits to it. If they are not, the honest verdict is to source
a different geography.

**Everywhere.** Trade press archives, local business journals, and the
association that runs the segment's annual conference are the three sources
people forget and they are frequently the best.

---

## Recording a source so it can be re-run

Every row carries a `source` string. The test: could somebody else reproduce
this pull from the string alone?

```
Good:  Georgia electrical contractor licence roster, EC and EU classes,
       Fulton + DeKalb + Cobb + Gwinnett counties, complete pull
       2026-10-02; cross-found in IEC Atlanta member directory and
       2026 NECA exhibitor list

Bad:   licence roster
Bad:   web search
Bad:   Google
```

And every pull gets a row in `source-ledger.csv`, before the rows are written:
what population it covers, how it was filtered, what it returned, and **whether
it capped**.

---

## The cap problem

This is the most common silent failure in sourcing, and a truncated pull looks
exactly like a complete one.

Portals cap results: 500 rows per query, 20 pages of 25, a result set that
quietly stops at the alphabet's halfway point. The fix is to split the query
until no slice returns exactly the cap number: by county, by licence class, by
first letter, by issue year.

If a slice still returns exactly the cap, it is incomplete. Record it in the
ledger, estimate what is missing, and put it in `known_gaps` in the state file.
Six weeks later, nobody remembers.

---

## Deduplication

Private company lists duplicate heavily and the duplicates are not obvious.

Merge on **domain** first, then **registry or licence number**, then **normalized
name plus postcode**.

Watch for:

- Trading name versus registered name
- Holding company and operating subsidiary listed separately
- Branch offices appearing as separate companies in maps and directories
- Entity suffix noise: Ltd, Limited, LLC, Inc, Inc., Corp, Co, and the
  hand-typed registry spelling variants
- The same company licensed in three states, which is one company

Keep the merged row, put the other names in `notes`, and **keep every source
string**. The cross-find is what makes a row credible and a dedupe that drops a
source string destroys that evidence. Report the dedupe count: 2,417 collapsing
to 2,140 is normal and worth seeing.

---

## What not to do

- **No scraping behind a login that forbids it.** LinkedIn's terms restrict
  automated collection. Reading a profile is fine; harvesting profiles is not
- **No paywalled content without a licence**
- **No pretexting.** No posing as a customer to get a dealer list, no calling
  reception under a false name to find out who owns the company. If a fact is
  only obtainable by deception, the fact is `Not found`
- **Read the terms of the directories you pull.** Many prohibit bulk
  extraction. Where they do, work manually and at human pace, or use a different
  source
- **No buying a list and treating it as the spine.** Load it as a cross-find and
  flag every address on it as `inferred-DO-NOT-USE` until independently verified

---

## The coverage log

Written at the sourcing gate, kept for the life of the run. It is the part that
makes the list honest, and it has three sections.

**Sources worked** — every pull, what it returned, and the cap detail.

**Known gaps** — what is missing and roughly how much of it. Truncated pulls,
unlicensed adjacent operators who appear on no roster, companies with no web
presence and no membership of anything.

**Bias statement** — one plain paragraph naming which way this list leans. A
roster-led list leans toward licensed operators, which is usually the segment
definition. An association-led list leans toward larger and more outward-facing
firms. The thirty-year-old company that joined nothing and advertises nowhere
appears only in the rosters, which is exactly why the rosters go first.
