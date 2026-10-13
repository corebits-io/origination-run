# Estimation Rules — Sizing Companies That Publish Nothing

Most of the companies worth buying publish no numbers at all. That is not an
obstacle to be worked around with a confident guess. It is the condition of the
whole exercise, and it has a method.

Two rules carry the rest of this file:

> **1. Every number carries its basis, and the basis travels with the number.**
>
> **2. A labeled estimate outside the size box makes a row WATCH, never a drop.
> Only a verified figure excludes on economics.**

Rule 2 is the expensive one to break. Excluding a real target because a headcount
proxy landed fifteen percent under the floor is the most common silent error in
origination, and the company it deletes is usually the one nobody else has
called either.

---

## The methods, best first

### 1. Filed accounts or a disclosed figure

A filed set of accounts, a disclosed turnover, a figure the owner stated on the
record. This is `verified`, and it is the only thing that excludes on economics.

In the UK, Companies House makes this the normal case. In the US it is the
exception, and it usually arrives via an award notice, a bond filing or an
interview.

### 2. Procurement and contract award history

Add up the disclosed awards over a period. This gives a **floor**, not a figure:
public work is rarely all the work. A floor is genuinely useful, because it can
only move a row up the size box, never down.

### 3. Revenue per head

Headcount multiplied by the sector-typical revenue per head from the market
map's segment economics, expressed as a range.

This needs a sourced benchmark. **If the market map came back with no revenue
per head and no typical margin, stop the sizing pass and say so.** Inventing a
benchmark makes every row on the list wrong in the same direction, which is the
hardest kind of wrong to notice.

Headcount itself needs a source and a date. A LinkedIn follower-page number is
weak, a LinkedIn employee count is medium, a stated figure in a trade piece is
better, and two independent sources agreeing is the standard worth having.

### 4. Physical capacity

Fleet size, bays, lines, licensed vehicles, square footage, machine count, beds,
chairs, routes. Where the segment has a well-understood revenue per unit, this
cross-checks method 3 well, and it works on companies with no web presence at
all.

### 5. Licence class and bonding capacity

In licensed trades, the licence class or the bonding capacity frequently implies
a revenue band. Tier 1, free, and almost never used by anybody.

### 6. Customer and footprint inference

Named customer logos, service areas, branch count. Weak on its own, useful as a
third opinion.

---

## The two-method rule

**Two independent methods minimum, or `financial_confidence` is `low`.**

Report the spread, not a point. Where two methods disagree by more than about
forty percent, **widen the range and drop the confidence** rather than picking
the one that suits the thesis.

| `financial_confidence` | Test |
|---|---|
| `verified` | Filed accounts, a disclosed figure, or an owner statement on the record |
| `high` | Two or more methods agreeing within about 15%, with a sourced benchmark and a dated headcount |
| `medium` | Two methods, wider spread, or one strong method with a firm input |
| `low` | One method, or a soft input, or a benchmark with no clear provenance |
| `Not found` | No defensible basis at all. Leave the field blank and say so |

---

## EBITDA

Apply the segment-typical margin range from the market map to the revenue range.
That is all. Both ranges are estimates and the output inherits the uncertainty of
both inputs, so a wide revenue range and a wide margin range produce an EBITDA
range wide enough to be nearly useless, and saying that plainly is better than
narrowing it to look decisive.

Never adjust a margin for a company-specific factor you have inferred rather
than read. "They look efficient" is not a margin adjustment.

**Never estimate a valuation or a multiple.** Not in the CSV, not in a brief,
and never in a message. A number in a first message is either a fabrication or
an anchor, and the owner knows which.

---

## The label format

The estimate and its basis live in the same cell, so the label cannot be
separated from the number by somebody pasting it into a second document.

```
$18-23M (estimate: 142 staff x $130-165k sector-typical revenue per head,
MCAA 2025 regional benchmark; headcount from LinkedIn 2026-09, cross-checked
against 138 stated in a 2026-06 trade piece. Cross-check: $16.1M floor
implied by disclosed 2024-25 state and municipal awards.)
```

```
$2.9-4.1M (estimate: 16-18% sector-typical margin from map segment economics
applied to the revenue range; both ranges unverified)
```

Three things are present in both: the word **estimate**, the **method**, and the
**source and date of every input**. A cell missing any of the three is not
finished.

---

## How size interacts with the box

| Situation | Result |
|---|---|
| Verified figure inside the box | Economics clear |
| Verified figure outside the box | **Drop**, `excluded_by` = `economics` |
| Estimate midpoint inside the box | Economics clear, confidence recorded |
| Estimate range straddling a boundary | **WATCH**, never a drop |
| Estimate entirely outside the box | **WATCH**, never a drop. Say how far outside and at what confidence |
| `Not found` | **WATCH.** A gap is a gap, not a negative |

Where the mandate allows a sub-floor add-on inside a radius of a named platform,
check the radius before applying the floor at all. That rule exists because the
smallest companies on the list are frequently the cleanest tuck-ins.

---

## At 2,000 rows

Sizing is the most expensive research in the run, which is why depth 2 only ever
sees the rows that survived depth 1, and why the mandate carries a depth 2 cap.

Two further efficiencies, both safe:

- **Do the free Tier 1 inputs for the whole batch first** — licence class,
  award history, registry formation date, employee count where the roster
  carries it — then estimate. A surprising number of rows get a floor out of
  the free pass alone
- **Stop at the first `verified` figure.** A company with filed accounts does not
  need three estimation methods

And one false efficiency to avoid: never carry a benchmark across segments
because the segments look similar. Commercial electrical and building systems
integration have different revenue per head, and a benchmark borrowed from the
wrong one is wrong on every row it touches.
