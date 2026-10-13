---
name: segment-mapping
description: "Map the segment a mandate implies before enumerating a single company: the boundary, the population and fragmentation, the segment economics every later estimate depends on, the typical owner, who is already consolidating it, where these companies are actually findable, and a verdict that is sometimes do not source this segment. Triggers on: map the market, market map, segment map, how fragmented is this sector, who is consolidating, revenue per head, segment economics, is this segment worth sourcing, where are these companies listed."
---

# Segment Mapping

Sourcing without a map pulls from whichever source is easiest and inherits its
bias invisibly. Every later step depends on four things this skill produces and
nothing else does:

1. **The segment boundary**, which decides what depth 1 drops
2. **The segment economics** — revenue per head and typical margin — which every
   revenue and EBITDA estimate in the run rests on
3. **The consolidator list**, which the sponsor screen runs against
4. **The source list**, which decides whether two thousand rows are reachable at
   all

It also produces a verdict, and the verdict is sometimes worth more than a list.

**Read first:** `MANDATE.md` sections 2, 3, 4, 5 and 7;
`references/sourcing-directories.md`; `references/estimation-rules.md`.

---

## Step 1 — Define the boundary, in and out

Write it so a researcher could sort a thousand companies with it and get the same
answer you would.

```
IN      Companies holding their own state electrical contractor licence,
        serving commercial and light industrial end customers, with a
        maintenance or service agreement base alongside project work

OUT     Residential-only service
        Solar EPC
        Utility transmission and substation line work
        Labour-only subcontract and staffing
        Electrical supply and distribution (wholesale, not contracting)
        Facilities management companies that subcontract all electrical work

EDGE    Building systems integrators with no electrical licence — in scope
        for the Pembury add-on case only, because that platform holds the
        licence. Flag them rather than dropping them.
```

The EDGE block matters more than the other two. It is where the false negatives
live, and writing it down is what lets the audit catch them later.

---

## Step 2 — Population and fragmentation

| What to establish | Why it matters |
|---|---|
| How many companies exist inside the boundary, in this geography | Decides whether the enumeration target is real |
| How many are plausibly inside the size box | A segment with four hundred operators and nine inside the box is not a sourceable segment |
| The size distribution shape | Tells you whether the mandate is fishing at the top, the middle or the tail |
| Who the ten largest are, and who owns them | The top of a consolidating segment is usually already sponsor-owned |
| How many have changed hands in 36 months | The rate of consolidation, which is the clock on the thesis |

Source every number and date it. Where the number can only be estimated, say so
and say from what: a licence roster count is a fact, an industry association
membership total is a fact about membership, and a market research headline is
Tier 4.

---

## Step 3 — Segment economics

**This is the part the rest of the run cannot work without.**

| Figure | What to find | Minimum standard |
|---|---|---|
| Revenue per head | A range, for this segment, in this geography | Two independent sourced data points, dated |
| Typical EBITDA margin | A range for independent operators at this size | Sourced and dated. Not a public company margin pasted onto a private one |
| Revenue per physical unit, where the segment has one | Fleet, bay, line, route, chair | Where it exists, it is the best cross-check available |
| Working capital and capex shape | Why margins differ between two similar companies | Qualitative, but say it |

Where industry benchmarks come from, in order: trade association financial
surveys, state or federal industry statistics, filed accounts of comparable
independents, and interviews or trade press where an operator states a figure.

**If revenue per head and typical margin both come back `Not found`, say so
plainly and stop the sizing half of the run.** The downstream skills are built to
handle that: they will report `Not found` on size rather than invent a benchmark.
An invented benchmark makes every row on the list wrong in the same direction,
which is the hardest kind of wrong to notice and the easiest to act on.

---

## Step 4 — The typical owner

What the ownership structure of this segment usually looks like, and therefore
what the sponsor screen is up against.

- The common structure: founder, family, partner group, ESOP
- Typical company age, and therefore where the segment is in its generational
  cycle
- Whether ownership is publicly establishable in this geography at all
- The language these companies use about themselves, and how long after a sale
  they keep using it

That last point is the one that earns its keep. In segments where "family owned
since 1974" stays on the website for a decade after the family sold, the sponsor
screen has to be run on every row, including the obvious ones.

---

## Step 5 — Who is already consolidating

Name them. This list is what the sponsor screen checks against for the rest of
the run, so a missing consolidator is a sponsor-owned company that reaches the
PRIORITY pile and then a letter.

For each: the platform name, the sponsor behind it, its geography, roughly how
many add-ons it has done, and when it started. Then say what it means: a segment
with three active consolidators and a four-year head start on you is a different
mandate from a segment with none.

---

## Step 6 — Findability

For the geography in the mandate, write the actual source list the run will pull
from, in tier order, with what each is expected to contribute. See
`references/sourcing-directories.md`.

Then answer the question the enumeration target depends on: **can this segment be
enumerated to the target from Tier 1 and 2 sources?** If the answer is no, the
options are a wider geography, an adjacent segment, or a smaller target. Guess
which one the user would rather hear, then tell them the true one.

---

## Step 7 — The verdict

One of four, with the reason:

| Verdict | When |
|---|---|
| **SOURCE IT** | Enough operators inside the box, ownership establishable, sources exist, consolidation not terminal |
| **SOURCE A DIFFERENT SLICE** | The segment is right but the geography or the size band is wrong. Say which slice |
| **SOURCE IT WITH A CAVEAT** | Workable, but with a named problem: no margin benchmark, a capped roster, three active consolidators. The caveat travels into the run |
| **DO NOT SOURCE IT** | Too few operators inside the box, mostly sponsor-owned already, ownership not publicly establishable, or no source enumerates the population |

A DO NOT SOURCE verdict is a successful outcome of this skill. It costs a day and
saves a quarter, and the user is free to overrule it as long as it is recorded.

### 🚧 HARD GATE

Show the map and the verdict. Get approval before sourcing anything. Write
`segment-map-[run]-[date].md`, and update the state file.

---

## Step 8 — The map file

```
SEGMENT MAP — commercial electrical + building systems, GA/TN/AL/SC
2026-10-03

BOUNDARY            in / out / edge, as above

POPULATION          ~3,900 licensed commercial electrical contractors in the
                    four states (roster counts, 2026-10)
                    ~2,400 plausibly commercial rather than residential-led
                    ~430 plausibly inside the $8-60M revenue band
                    Size shape: long tail. Around 85% under $8M

ECONOMICS           Revenue per head  $165-210k   (NECA 2025 financial survey,
                                                   southeast region, n=; plus
                                                   3 filed comparables)
                    EBITDA margin     7-12%       (same survey, independents
                                                   under $50M revenue)
                    Service-heavy mix runs 3-5 points above project-led
                    Cross-check unit: licensed vehicles, ~$280-340k per van
                    for service-led firms

TYPICAL OWNER       Founder or second generation, company age 25-45 years,
                    single state licence, owner still prices large jobs.
                    Ownership establishable: yes, state filings name officers.
                    Language risk: HIGH. "Family owned since 1981" commonly
                    survives a sale by 5+ years on the website

CONSOLIDATORS       4 named, 2 active in-geography, the earliest started 2019,
                    between them ~60 add-ons in the four states
                    → sponsor screen runs on every row, no exceptions

FINDABILITY         4 state licence rosters (Tier 1, the spine, ~2,400 in
                    scope after category filtering)
                    2 registries for entity and officer data
                    3 association directories (Tier 2)
                    5 manufacturer installer locators (Tier 2)
                    NECA exhibitor lists 2024-2026 (Tier 2)
                    2 state procurement award portals (Tier 1, revenue floors)
                    Enumeration target of 2,000: reachable

VERDICT             SOURCE IT WITH A CAVEAT
                    Two active consolidators with a six-year head start means
                    the top of the size box is thin and the add-on end is
                    where this mandate wins. Expect a high sponsor-owned rate
                    at depth 2: 20-25% rather than the usual 15%.
```

---

## Notes

- **The map is written before any company is enumerated, every time.** A map
  written after the list is a description of the list
- **Date every figure.** Segment economics go stale and so does a consolidator
  list
- **Do not borrow a benchmark across segments because they look similar.**
  Commercial electrical and building systems integration have different revenue
  per head, and a borrowed benchmark is wrong on every row it touches
- **A thin segment is a finding.** "There are nine companies in your box" is the
  most valuable sentence this skill can produce, and it is always unwelcome
- **Record the sponsor-owned expectation.** If depth 2 comes back at double the
  rate the map predicted, either the map was wrong or the screen is catching
  something real. Both are worth knowing before the ranking
