---
name: ownership-and-size
description: "Establish who actually owns each surviving company from filings and registers, run the four-part sponsor screen that catches companies already bought but still marketing themselves as family owned, produce labeled revenue and EBITDA ranges for companies that publish nothing, and decide the platform or add-on role against named platforms. Triggers on: who owns this company, ownership research, sponsor screen, is this PE owned, estimate revenue, size these companies, EBITDA estimate, platform or add-on, depth 2."
---

# Ownership and Size

Depth 2. The expensive pass, and the one the whole ranking depends on.

Four questions per row: **who owns it, how big is it, platform or add-on, and is
it already somebody else's.** Every answer gets used by a rubric that cannot tell
the difference between a sourced fact and a confident guess, so the discipline
here is not thoroughness. It is honesty about what is known.

**Read first:** `references/evidence-rules.md`, `references/estimation-rules.md`,
`references/ranking-rubric.md` (hard rules 1, 2, 3 and 7), and the segment map's
economics and consolidator sections.

---

## Step 0 — Preconditions

1. Only rows at `depth` = `1` with `screen_result` = `carry` are in scope
2. **The segment map has economics.** If revenue per head and typical margin are
   both `Not found`, run the ownership half and **stop the sizing half**, saying
   so plainly. An invented benchmark makes every row wrong in the same direction
3. The depth 2 cap from `run/state.json`. Stop when you reach it and report what
   is researched and what is waiting
4. The consolidator list from the map

---

## Step 1 — Ownership before size, always

Estimating revenue for a company a sponsor bought two years ago is wasted
research, and at 800 rows that waste is the budget.

Establish `ownership_type` from evidence, in this order of source quality:

1. **The register.** Officers, shareholders, share allocations, transfers,
   formation date. Tier 1
2. **Filings that name a parent or a security holder.** UCC filings, charges,
   bond filings. Tier 1
3. **The company or the owner on the record.** An interview, a press release,
   their own anniversary page with a date on it. Tier 2
4. **A dated third-party report naming its source.** Tier 3

Write `ownership_type`, `ownership_evidence` (what it is, which tier, with a
date) and `evidence_tier`.

**`Not found` is a legitimate outcome.** It caps the row at WATCH and it never
drops it. Do not fill it with the most likely answer: a letter that guesses who
owns the company announces itself in the first sentence.

---

## Step 2 — The sponsor screen, on every row

Including the ones that look obviously founder-owned. Especially those.

Four checks, all four, every row:

1. **The consolidator list** from the segment map, by name
2. **Trade press, back 36 months**, for an acquisition announcement
3. **UCC filings or equivalent security registrations** naming a fund entity,
   an SPV, or a lender syndicate of the kind used in sponsor deals
4. **The register, followed one level up.** A corporate shareholder is followed
   until it resolves to people, a fund, or a dead end that gets recorded

`sponsor_screen` records what was checked and what was found, not just the
conclusion:

```
clear - screened against the 4 sponsor platforms named in the map, no trade
press 36mo, no UCC filings naming a fund entity, register resolves to two
named individuals
```

**Sponsor-owned is always a drop.** `screen_result` = `drop`, `excluded_by` =
`ownership`, however good the fit looks otherwise.

### The report that earns the whole skill

Keep a separate list: **companies a sponsor already owns that still describe
themselves as family owned or independent on their own website.**

In the sample run there were 37 of them. Each one is a letter that does not get
written to an owner who sold two years ago, and that letter is the kind that gets
forwarded to the new owner with a comment. This list is the most valuable single
output of depth 2 and it goes in the gate report by name.

---

## Step 3 — Size

Follow `references/estimation-rules.md`. The short version:

- **Free Tier 1 inputs first, for the whole batch.** Award floors, licence class
  bands, bonding capacity, filed accounts where they exist. In the sample run 188
  rows already carried a verified award floor out of depth 1
- **Then two methods minimum**, or `financial_confidence` is `low`
- Report the **spread**, not a point. Where two methods disagree by more than
  about 40%, widen the range and drop the confidence rather than picking the one
  that suits the thesis
- **Stop at the first `verified` figure.** A company with filed accounts does not
  need three estimates
- **The label travels with the number**, in the same cell, always

| Situation | Result |
|---|---|
| Verified figure outside the box | **Drop.** `excluded_by` = `economics` |
| Estimate outside the box, at any confidence | **Carry, capped at WATCH.** Say how far outside and at what confidence |
| `Not found` | **Carry, capped at WATCH** |

Check the mandate's sub-floor add-on rule before applying the floor at all. The
smallest companies on the list are frequently the cleanest tuck-ins, and the
radius test is free.

**Never estimate a valuation or a multiple.** Not in the CSV, not in a brief,
not ever.

---

## Step 4 — Platform or add-on

`fit_role` is `platform`, `add-on`, or `Not found`. And an add-on verdict needs
the **named receiving platform** in `fit_role_reason`, from mandate section 2.

| Role | What has to be true |
|---|---|
| `platform` | In the upper part of the size box, and second-tier management evidenced by name. A company where the owner is the only person who can price a job is not a platform, whatever its revenue |
| `add-on` | Inside the radius or the capability gap of a **named** platform, and the gap is stated: geography, capability, licence coverage, customer access |
| `Not found` | Neither is establishable. Caps the row at WATCH |

"Add-on" with no receiving platform and no stated gap is not an answer. If
mandate section 2 names no platforms, every add-on verdict in the run is
`Not found` and the user was told that at intake.

---

## Step 5 — Batches of 20 to 30

Report between every batch. A two-hundred-row pass with one report at the end is
a pass nobody can correct mid-flight, and at depth 2 a systematic error is
expensive in a way the earlier depths are not.

Each batch report:

- Ownership distribution with evidence tiers
- **Every sponsor hit by name**, and which of them still market themselves as
  family owned
- Verified versus estimated split, and the benchmark provenance
- Every row whose estimate lands outside the size box, and by how much
- Every material method disagreement
- Role distribution, with the `Not found` count stated plainly

Write to `targets.csv` and `run/state.json` after every batch. Set `depth` = `2`
on every row touched.

---

## Step 6 — The gate

### 🚧 HARD GATE — at the end of the depth, and at every batch boundary

The batch reports are reports. The depth gate is an approval. Show:

- The full ownership distribution and the tier mix
- The sponsor-owned count against what the segment map predicted
- The family-owned-language list, by name
- The size picture: verified, high, medium, low, `Not found`
- The role split
- The drops with reasons, and the rows capped at WATCH with which cap fired
- Ten rows in full, chosen to include two `Not found` ownership rows and two
  `Not found` size rows

Get approval before signals.

---

## Step 7 — Report

```
OWNERSHIP AND SIZE COMPLETE — 2026-10-08
792 rows researched in 32 batches. Depth 2 cap 800, not reached.

Carried forward        524

Dropped                268
  sponsor-owned        161   ← 37 of these still describe themselves as
                               family owned or independent on their own site
  corporate subsidiary  28
  verified outside box   61   filed accounts or disclosed awards only
  public parent           6
  defunct discovered     12

Ownership of the 524
  founder-owned        243   Tier 1: 198, Tier 2: 45
  family-owned         171   Tier 1: 121, Tier 2: 50
  management/partner    61
  ESOP                  14   ← capped at WATCH per mandate section 7
  Not found             35   ← capped at WATCH, never dropped

Sponsor rate           161 of 792 = 20%
                       The map predicted 20-25%. Consistent.

Size of the 524
  verified              58   filed accounts, disclosed figures, award totals
  estimate high        149
  estimate medium      221
  estimate low          71
  Not found             25
  Benchmark             NECA 2025 southeast survey, $165-210k per head,
                        7-12% margin. Every estimate rests on it.

  Outside the box on an estimate   44   ← all WATCH, none dropped
  Inside on a verified floor       31   ← award history did this for free

Role
  platform              87
  add-on               298   all with a named platform: Calder 171,
                             Pembury 127
  Not found            139   ← capped at WATCH

Next: signal-detection on the 524.
```

---

## Notes

- **Sponsor-owned is always a drop.** No exceptions, no "but the fit is perfect"
- **`Not found` ownership can never be PRIORITY.** Flag it instead of filling it
- **A company calling itself family owned is Tier 3 evidence at best.** Check the
  register. In this segment the language survives a sale by five years or more
- **Unknown is not failed**, on ownership, on size, on role
- **Never write a number without its basis.** A stripped estimate becomes a fact
  the moment somebody pastes it into a second document
- **You do not write `verdict` for a surviving row.** You write drops for the
  ownership and economics gates you own. The bucket belongs to `fit-ranking`,
  under an approved rubric, so the decision stays inspectable
- **If almost nothing is verified, lead with that.** The whole size gate is then
  resting on one benchmark and the user needs to know it before they trust the
  list
