---
name: fit-ranking
description: "Build a ranking rubric from the mandate, get it approved before ranking a single row, rank every row in the list identically into PRIORITY, WATCH or PASS with the rule that produced each verdict written next to it, then run the five-part audit that verifies signals at source and hunts false negatives among the cheap drops. Triggers on: rank the list, score the targets, buy box fit, which companies are priority, build the rubric, audit the ranking, re-rank, why is this a pass, depth 4."
---

# Fit Ranking

Depth 4. Research becomes decisions.

Two thousand rows arrive here in three states: dropped cheaply at depth 1,
dropped after research at depth 2, or carried and researched in full. All of them
get a verdict, because a row with no verdict gets rediscovered and re-researched
next quarter.

**Read first:** `references/ranking-rubric.md` in full. It is the rules. This
skill is the procedure.

---

## Step 1 — Build the rubric from the mandate

Not from the rows. A rubric built after looking at the list is a rubric built to
produce that list.

One row per criterion: the criterion, the mandate section it came from, the exact
test, and what it does to the bucket.

```
RUBRIC — SE-ELEC-Q4                                      2026-10-09

EXCLUSIONS (any one of these is a PASS, checked in this order)
  1  Suppression        suppression.csv, any scope              §8
  2  Geography          licensed address outside GA/TN/AL/SC    §5  HARD
  3  Segment            outside the map boundary                §4
  4  Live process       retained banker running a process       §8
  5  Ownership          sponsor-owned, public, out-of-scope
                        corporate                               §7
  6  Economics          VERIFIED figure outside $8-60M /
                        $1.2-6M EBITDA                          §3
  7  Must-have 1        licence inactive, or issued under
                        10 years ago                            §6

CAPS AT WATCH (the row carries, but cannot be PRIORITY)
  8   Estimated size outside the box, any confidence            §3
  9   ownership_type = Not found                                §7
  10  Must-have 2 unknown: no named second-tier manager found   §6
  11  Must-have 3 unknown: service mix not establishable        §6
  12  fit_role = Not found                                      §2
  13  ESOP ownership                                            §7
  14  signal_strength low, expired or Not found                 §9

PRIORITY REQUIRES ALL OF
  - Clean on every exclusion
  - ownership_type in the actionable list, Tier 1 or 2 evidence
  - Size inside the box, or an estimate inside at medium or better
  - All testable must-haves met
  - fit_role decided, and for an add-on, the platform named
  - signal_strength high or medium, inside its family window

TIE-BREAK WITHIN PRIORITY, in order
  1  Signal family rank from §9: leadership, financing, growth, hiring
  2  Signal strength
  3  Ownership evidence tier
  4  Role: platform before add-on, per §10 (one platform wanted this year)
  5  Size: closer to the middle of the box ranks higher than the edges
```

### 🚧 HARD GATE — the rubric, before a single row is ranked

Show the rubric in full and get it approved. Then save it as
`rubric-[run]-[date].md` next to the CSV, and record the approval in the state
file.

This gate exists because a rubric approved after the ranking is just a
description of what happened.

---

## Step 2 — Rank every row in the fixed order

The order in `references/ranking-rubric.md`, applied identically to every row, so
two rows with the same facts always get the same verdict.

For each row write:

- `verdict` — PRIORITY, WATCH or PASS
- `fit_reason` — the rules that fired, in plain language, so the verdict can be
  argued with in March
- `excluded_by` — for a PASS only: `suppression`, `geography`, `segment`,
  `process`, `ownership`, `economics`, `licence`, `strategic`, `defunct`
- `depth` = `4`

The depth 1 and depth 2 drops already carry their reason. Convert each into a
PASS with the same reason rather than re-deriving it.

**Write `fit_reason` as a sentence, not a code.** "Clean on exclusions;
founder-owned at Tier 1; estimate midpoint inside the box; add-on to Pembury on
licence coverage; all three testable must-haves met; high-strength leadership
signal four months old" is a reason. "Score 8.4" is not.

---

## Step 3 — Check the distribution before reporting it

| Measure | Healthy | If it is off |
|---|---|---|
| PRIORITY as a share of **researched** rows | 4-8% | Above 25%: the rubric is flattering the user, or `low` signals are being read as `high`. Below 1%: usually the signals pass has not run, or there are too many must-haves |
| WATCH as a share of researched rows | 60-80% | This is meant to be the big bucket |
| Rows with no signal | 50-70% | Below 30% means signals are being invented |
| Ownership PASS within depth 2 | 15-30% | Above 40% means the segment is consolidated |

Name which way it is off. Do not adjust the rubric until the shape looks right:
that is the one move that makes the whole exercise worthless.

---

## Step 4 — The audit

Runs every time, reported whether or not it is clean. An audit that finds nothing
on a two-thousand-row list has usually not run.

**Part 1 — Verify PRIORITY signals at source.** Open the URL on at least ten
PRIORITY rows, all of them if there are fewer than ten. Confirm the quote is on
the page and the date is right. A signal that cannot be re-confirmed is
downgraded to `Not found` and the row moves to WATCH.

**Part 2 — Thirty random depth 1 drops, re-checked against the source.** The most
valuable half hour in the run, and the part specific to working at volume. Hunt
for:

- A licensed address that is a registered agent, with the operations in-state
- A company classified out-of-segment on a website that undersells it
- A licence recorded inactive because it was renewed under a new entity name
- A suppression match that is a different company with a similar name

**Part 3 — Twenty random PASS rows from the researched pile.** The usual catch is
hard rule 2: a row excluded on an estimate that should have been WATCH.

**Part 4 — Re-screen the keep pile against sponsors.** Every PRIORITY and WATCH
row, re-checked for a transaction announced since capture. On a six-day run, two
or three will have been bought.

**Part 5 — Distribution**, against the bands above.

Report every correction by name with its reason, and give the net figures before
and after.

---

## Step 5 — The PRIORITY rows, in full

Each PRIORITY row gets summarized for the user with:

- Company, HQ, segment, size estimate with its confidence
- Ownership and its evidence tier
- Role, and for an add-on, the named platform and the gap it fills
- The signal, quoted, with its date and strength
- A **`NOT KNOWN`** block: the material things that are still unknown

The `NOT KNOWN` block is not a disclaimer. It is the difference between a brief
and a sales pitch to yourself, and it is what stops a labeled estimate becoming
a fact on the second page of a memo.

```
NOT KNOWN   Margin is a sector benchmark, not theirs. No accounts filed.
            Customer concentration unknown. Whether the named GM would
            stay post-transaction is unknown and material to the platform
            case.
```

---

## Step 6 — The gate and the report

### 🚧 HARD GATE

Show the distribution, the PRIORITY rows in full with their `NOT KNOWN` blocks,
the WATCH reasons grouped, the PASS reasons grouped, and the audit with every
correction. Get approval, then write.

```
RANKING COMPLETE — 2026-10-10
Rubric: rubric-SE-ELEC-Q4-2026-10-09.md (approved before ranking)

Before the audit     PRIORITY 34   WATCH 490   PASS 1,616
After the audit      PRIORITY 31   WATCH 494   PASS 1,615

PRIORITY as a share of researched rows   5.9%   inside the 4-8% band
Rows with no signal                      63%    inside band

WATCH — 494
  fits, no signal found                  268
  fits, signal below the window           31
  fits, signal strength low               72
  ownership Not found                     35
  size Not found                          25
  estimate outside the box                44
  role not decidable                      19

PASS — 1,615
  segment            611
  licence            389
  geography          216
  sponsor-owned      162   ← 37 still market themselves as family owned
  defunct            109
  economics           61   verified figures only
  corporate           28
  public              24
  suppression          9
  process              6   retained banker, per mandate section 8

AUDIT
  1. PRIORITY signals verified        10 of 31 checked
       confirmed at URL                 9
       page no longer says it           1  ← Marchmont Electric. Downgraded
                                           to Not found, row to WATCH.
  2. Depth 1 drops re-checked         30 random rows
       correctly dropped               28
       wrong                            2  ← Dunbar Systems (licence address
                                           is a registered agent, operations
                                           in Chattanooga - restored, now
                                           WATCH). Trenholm Building Systems
                                           (dropped on segment, is a licensed
                                           integrator inside the EDGE block -
                                           restored, now WATCH).
  3. Researched PASS re-checked       20 random rows
       correctly excluded              19
       wrong                            1  ← Verity Power, excluded on a low
                                           confidence estimate $7.4M against
                                           an $8M floor. Hard rule 2 says
                                           WATCH. Corrected.
  4. Keep pile re-screened            525 rows
       new sponsor hits                 2  ← Calderwood Systems and Pike
                                           Electrical, both announced after
                                           our capture. Both to PASS.
  5. Distribution                     inside band

  Net: 6 corrections. Every one in the direction the rubric requires.
```

---

## Notes

- **The rubric is approved before ranking, every time.** No exceptions
- **Every row gets a verdict, including the 1,348 dropped at depth 1.** Nothing
  is deleted
- **Unknown is not failed.** A cap is not a drop
- **Say the distribution out loud.** A user with 34 PRIORITY rows out of 2,140
  has a usable week. A user with 300 has a list that will be abandoned by
  Thursday
- **Report the audit even when it is clean**, and especially when it is not. Six
  corrections on a two-thousand-row list is the evidence that the audit ran
- **Re-ranking is cheap.** If the user widens the size box or changes a
  must-have, re-run this skill on the existing research rather than re-sourcing.
  That is what the stored rubric and the `fit_reason` column are for
