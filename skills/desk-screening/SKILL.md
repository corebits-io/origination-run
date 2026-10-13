---
name: desk-screening
description: "The cheap pass over every enumerated row that decides which companies earn expensive research: drops only on free facts that are verified - hard geography, segment boundary, missing or inactive licence, public company, dissolved entity, suppression - and never on a missing website, an absent headcount or an estimate. Triggers on: screen the list, desk screen, depth 1, which rows carry forward, cut the list down, filter two thousand rows, drop reasons, carry rate."
---

# Desk Screening

Depth 1. The pass that makes volume affordable.

Two thousand rows cannot all have their ownership established, their revenue
estimated and their signals researched. Nor should they: most of them are
residential, or out of state, or not licensed, or already public, and every one
of those facts is free to check.

The whole skill rests on one distinction, and getting it wrong is the most
expensive mistake available in this package:

> **A row is dropped by a fact that is false. A row is never dropped by a fact
> that is absent.**

A company outside the state line is false against the mandate. A company with no
website is absent. The first is a drop. The second is the proprietary end of the
list, and deleting it here is both silent and permanent, because nothing
downstream ever looks at a depth 1 drop again except the audit.

---

## Step 0 — Preconditions

1. Sourcing is complete and approved, and every row is at `depth` = `0`
2. `suppression.csv` is loaded
3. The segment map's boundary — including the EDGE block — is in front of you
4. Mandate section 5 says whether geography is **hard** or a **preference**

That last one decides whether geography drops rows at all. A preference never
drops anything; it moves a row down the ranking later. **Check it rather than
assuming.** Treating a preference as hard is the second most common way a real
target leaves the list.

---

## Step 1 — The six checks, in cost order

Run them in this order and stop at the first drop. Each is free, each is binary,
each produces a recorded reason.

| # | Check | Drops when | `screen_reason` |
|---|---|---|---|
| 1 | **Suppression** | Company, domain or owner is on `suppression.csv` in any scope | `suppression` |
| 2 | **Not a company** | Supply house, trade school, association, dissolved shell with no licence and no operations | `not-an-operator` |
| 3 | **Geography** | Registered or licensed address outside a **hard** constraint | `geography-hard` |
| 4 | **Segment** | Clearly outside the boundary: residential-only, wholesale, staffing, out-of-scope specialty | `segment` |
| 5 | **Licence** | A licence the mandate requires is absent, inactive, revoked, or issued too recently, **confirmed on the roster** | `licence` |
| 6 | **Public or listed** | The company or its parent is publicly listed | `public` |

Everything else carries. `screen_result` = `carry`, `depth` = `1`.

### What each check may and may not use

**Geography.** The licensed or registered address. Not a mailing address, not a
PO box, not a registered agent's address — that last one is a known false
positive and the audit specifically hunts for it. Where a company is licensed in
two states and one is in scope, it carries.

**Segment.** The boundary from the map, and the EDGE block. A company whose
website is one page and says "electrical contractor" is **not** out of segment;
it is a company with one page. Where the website undersells what the company
does, the licence class is better evidence than the marketing. When in doubt,
carry it: a wrong carry costs twenty minutes at depth 2, a wrong drop costs the
company.

**Licence.** Only from the roster, and only where the mandate makes it a
must-have. A licence recorded as inactive because it was renewed under a new
entity name is a false positive, so check the entity name against the row before
dropping.

**Public.** A free check and a real one. Public companies are out of scope by
design, and learning material non-public information about one during research is
a problem nobody wants.

---

## Step 2 — What never drops a row at depth 1

Write this list into the batch report every time, because the pressure to break
it is constant and it comes from wanting a shorter list.

- No website, a one-page website, an ugly website, no SSL certificate
- No LinkedIn page, no reviews, no social presence, no marketing of any kind
- No headcount recorded anywhere
- No founding year recorded
- An **estimated** revenue outside the size box. Estimates never drop a row, at
  any depth. See `references/estimation-rules.md`
- A headcount proxy below the size floor
- Ownership that looks wrong but has not been established
- A company that "looks too small" or "looks like a one-man operation"
- A name that resembles something on the suppression list without matching it

The last two are judgment dressed as a fact. At depth 1 there is no judgment,
only the six checks.

---

## Step 3 — Free enrichment while you are there

Some facts are free because the sourcing pull already contains them, and having
them before depth 2 makes the expensive pass cheaper. Fill them where they come
at no extra cost:

- Licence number, class and original issue date, from the roster
- Entity status and formation date, from the registry
- Officer names as recorded, **without** interpreting them as ownership
- Award history totals, where the procurement pull covered the row. This is a
  verified revenue **floor** and it is the single most useful free fact available

Record them in the relevant columns and in `notes`. Do not infer ownership from
an officer list here: that is depth 2, with its own evidence rules.

---

## Step 4 — Batches of 100 to 200

Report between batches. Each report shows the drop counts by reason, the running
carry rate, and **ten carries and ten drops in full**, so a systematic error
shows up at row two hundred rather than row two thousand.

Write to `targets.csv` and the state file after every batch.

---

## Step 5 — Watch the carry rate

| Carry rate | What it means | What to do |
|---|---|---|
| 30-45% | Normal for a tight segment | Proceed |
| Below 15% | The population is wrong, not the companies. Sourcing pulled from the wrong classes or the wrong geography | **Stop.** Re-aim sourcing before spending depth 2 |
| Above 70% | The segment boundary is loose and the screen is not screening | **Stop.** Tighten the boundary with the user |

Also watch the **shape** of the drops. If one reason accounts for most of them,
say so and check it is right. Six hundred segment drops out of two thousand is
plausible for a roster that includes residential. Six hundred geography drops is
usually a sourcing error, because the rosters were pulled by state.

---

## Step 6 — The gate

### 🚧 HARD GATE

Show:

- Total carried and dropped, with drop counts by reason
- The carry rate against the band above
- **Ten carried rows in full**, including at least three with no website and
  three with no headcount
- **Ten dropped rows in full**, with the exact evidence for each drop
- Every row where the drop was arguable, listed separately with the reason it
  was arguable. These are the rows the audit will come back to
- The free enrichment coverage: how many rows now carry a licence date, an
  entity status, an award floor

Get approval. Then write, update `run/state.json`, append to `run/log.md`.

---

## Step 7 — Report

```
DESK SCREEN COMPLETE — 2026-10-04
2,140 rows screened in 14 batches

Carried forward      792   (37%)   ← inside the 30-45% band

Dropped            1,348
  segment            611   residential-led 402, wholesale 94, staffing 61,
                           out-of-scope specialty 54
  licence            389   no licence found 214, inactive or revoked 98,
                           issued under 10 years ago 77
  geography          218   outside the four states
  defunct             97   dissolved, licence expired, no operations
  public              24   listed, or subsidiary of a listed parent
  suppression          9   2 opt-outs, 4 Calder subcontractors,
                           3 cold-only relationships

Arguable drops        17   listed in notes. 11 are licence-address-is-a-
                           registered-agent cases, flagged for the audit

Free enrichment on the 792 carried
  licence issue date   792 / 792
  entity status        764 / 792
  award floor          188 / 792   ← 188 rows now have a VERIFIED revenue
                                     floor before any estimate was made

Never dropped at this depth
  no website           198 of the 792 carried
  no headcount         402 of the 792 carried

Next: ownership-and-size on the 792, 32 batches of 25.
Depth 2 cap is 800. The whole carried set fits inside it.
```

---

## Notes

- **The 198 carried rows with no website are not a problem to be cleaned up.**
  They are the reason this list is worth more than a database export
- **Every drop carries its reason into the ranking** as a PASS with
  `excluded_by`, so the row is never rediscovered and re-researched
- **The audit samples thirty depth 1 drops** and re-checks them against the
  source. Expect it to find one or two, and expect them to be registered-agent
  addresses or a company whose website undersells it. That is the system working,
  not failing
- **When the carry rate and the user's expectation disagree, say the number.** A
  user who wanted eight hundred rows and got three hundred has a sourcing
  problem, and padding the screen is the one response that guarantees it goes
  unnoticed
