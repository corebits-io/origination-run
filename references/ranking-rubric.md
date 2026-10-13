# The Ranking Rubric — Three Verdicts, Eight Hard Rules, One Audit

Any system can return two thousand ranked rows. The rules below decide whether
the ranking means anything.

---

## Three verdicts, not a score

**PRIORITY** — strong mandate fit, and a dated reason to engage now
**WATCH** — fits the thesis, needs a better trigger or a missing fact
**PASS** — wrong ownership, economics, geography, or strategic fit

A score out of 100 invites an argument about whether a 71 beats a 68 and tells
nobody what to do on Monday. Each of these three tells you exactly what happens
next: PRIORITY gets a letter, WATCH gets re-read next quarter, PASS gets left
alone with the reason written next to it.

Every row on the list gets a verdict, including the fourteen hundred dropped at
depth 1. A drop carries its `excluded_by` reason into a PASS, so the same company
is not rediscovered and re-researched in six months.

---

## The rubric is built from the mandate, and approved before anything is ranked

Before a single row is ranked, write the rubric out in full and get it approved.
One row per criterion:

| Criterion | Mandate section | The test | Effect |
|---|---|---|---|
| Geography | 5 | Licensed address inside the four states | Outside a **hard** constraint: PASS. Outside a preference: no promotion |
| Segment | 4 | Holds its own electrical contractor licence, commercial end customers | Outside: PASS |
| Ownership actionable | 7 | `ownership_type` in the actionable list | Sponsor-owned: PASS. `Not found`: cap at WATCH |
| Size | 3 | Revenue and EBITDA against the box | Verified outside: PASS. Estimated outside: WATCH |
| Must-have 1 | 6 | Licence active, issued 10+ years ago | Fails: PASS. Unknown: cap at WATCH |
| Must-have 2 | 6 | A named second-tier manager, not family | Fails: cap at WATCH. Unknown: cap at WATCH |
| Role decided | 2 | Platform, or add-on with a named receiving platform | `Not found`: cap at WATCH |
| Timing signal | 9 | A dated, sourced, in-window signal | `high` or `medium`: eligible for PRIORITY. `low` or `Not found`: WATCH |

The approved rubric is saved as `rubric-[run]-[date].md` next to the CSV. It is
the thing an argument in March gets settled against.

**Write the rubric from the mandate, never from the rows.** A rubric built after
looking at the list is a rubric that was built to produce a list.

---

## The fixed ranking order

Every row is ranked in the same order, so two rows with the same facts always get
the same verdict.

```
1. Suppression        on the list → PASS, excluded_by = suppression. Stop.
2. Geography          outside a hard constraint → PASS. Stop.
3. Segment            outside the boundary → PASS. Stop.
4. Live process       retained banker, mandate says do not go around → PASS. Stop.
5. Ownership          sponsor-owned, public, out-of-scope corporate → PASS. Stop.
6. Economics          verified figure outside the box → PASS. Stop.
                      estimate outside the box → carry, cap at WATCH.
7. Must-haves         a failed testable must-have → PASS. Stop.
                      an unknown must-have → carry, cap at WATCH.
8. Role               platform, or add-on with a named platform.
                      Not decidable → carry, cap at WATCH.
9. Signal             high or medium, in window → PRIORITY eligible.
                      low, expired or Not found → WATCH.
10. Caps applied      any cap from 6, 7 or 8 holds. WATCH.
```

Order matters for cost as much as for consistency: the free exclusions run
first, so no expensive test is ever applied to a row that was already out.

---

## The eight hard rules

**1. Unknown is not failed.** `Not found` revenue is not a failed size test.
`Not found` ownership is not a failed ownership test. Ranking gaps as negatives
systematically deletes the least-marketed companies from the list, which is to
say the proprietary ones.

**2. Only a verified figure excludes on economics.** A labeled estimate outside
the box is WATCH. See `estimation-rules.md`.

**3. Sponsor-owned is always PASS.** The screen runs on every row, including the
ones that look obviously founder-owned, because companies keep the family-owned
language for years after a sale.

**4. A thin website is not a negative signal.** Neither is no website, no
LinkedIn page, no reviews and no marketing. The companies with no marketing
budget are the ones no banker has called.

**5. Fit and timing stay separate.** A loud signal never promotes an
out-of-mandate company. A missing signal never drops an in-mandate one.

**6. Signals are quoted verbatim or they do not exist.**

**7. `Not found` ownership can never be PRIORITY.** Flag it rather than filling
it with the most likely answer.

**8. Nothing is deleted.** A PASS carries the rule that excluded it.

---

## Distribution bands

After ranking, check the shape before reporting it.

| Measure | Healthy | If it is off |
|---|---|---|
| PRIORITY, as a share of **researched** rows | 4-8% | Above 25%: the rubric is flattering you, or `low` signals are being read as `high`. Below 1%: the signals pass has not run, or there are too many must-haves |
| WATCH, as a share of researched rows | 60-80% | This is meant to be the big bucket. Most honestly researched companies fit and have no trigger yet |
| Rows with no signal | 50-70% | Below 30% means signals are being invented or over-rated |
| PASS on ownership, within depth 2 | 15-30% | Above 40% means the segment is consolidated and the market map should have said so |

Report the distribution against these bands every time, and name which way it is
off rather than quietly adjusting the rubric until it looks right.

---

## The audit

Runs every time, on every run, and gets reported whether or not it is clean. An
audit that catches nothing on a two-thousand-row list has usually not run.

**Part 1 — Verify PRIORITY signals at source.** Open the URL for at least ten
PRIORITY rows, or all of them if there are fewer. Confirm the quote is on the
page and the date is right. Pages get rewritten. A signal that cannot be
re-confirmed is downgraded to `Not found` and the row moves to WATCH.

**Part 2 — Hunt false negatives among the depth 1 drops.** This part is specific
to running at volume and it is the most valuable half hour in the whole run.
Pull **thirty random rows** that were dropped at depth 1 and re-check the drop
reason against the actual source. The failure modes it catches:

- A licensed address that is a registered agent, with the operations in-state
- A company classified out-of-segment on a website that undersells what it does
- A licence recorded as inactive because it was renewed under a new entity name
- A name matched to the suppression list that is a different company

**Part 3 — Hunt false negatives among the depth 2 and 3 drops.** Twenty random
PASS rows from the researched pile. The usual catch is rule 2: a row excluded on
an estimate that should have been WATCH.

**Part 4 — Re-screen the keep pile against sponsors.** Every PRIORITY and WATCH
row, re-checked for a transaction announced since capture. On a six-day run, two
or three will have been bought.

**Part 5 — Distribution.** Against the bands above.

Report every correction with the row name and the reason, and give the net
figures before and after. Three corrections on a two-thousand-row list is a
normal result and it is the evidence the audit ran.

---

## What the user can change

The mandate is theirs. Change it and the list re-ranks.

The criteria table, the weights, the bands: all editable. Be careful with four
of the hard rules, because each one protects against a failure that is invisible
when it happens:

- **Unknown is not failed** (rule 1)
- **Estimates never produce an exclusion on their own** (rule 2)
- **A thin website is not a negative signal** (rule 4)
- **Signals are quoted verbatim** (rule 6)

Break the first three and the list quietly becomes the same list a database would
have sold you. Break the fourth and a fabricated quote eventually reaches an
owner.
