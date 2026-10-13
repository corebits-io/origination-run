---
name: owner-contact-routing
description: "Find the person who can actually sell each PRIORITY company and a route that reaches them - warm introduction, published or verified email, posted letter, or a senior LinkedIn note - recording confidence honestly and never guessing an address from a pattern. Triggers on: find the owner, who do I contact, decision maker, contact details, find emails, verify emails, route to the owner, contact routing, depth 5."
---

# Owner Contact Routing

Depth 5. The first step whose output is about a named human being rather than a
company, which changes both the care and the law. Read
`references/compliance.md` section 2 before this skill runs for the first time.

A perfect target list pointed at a plant manager is a wasted campaign. So is a
technically plausible address that bounces and takes a sending domain with it.

---

## Step 0 — Scope, and why the scope is narrow

**Only PRIORITY rows.** Not WATCH, not PASS.

That is a data protection decision as much as an efficiency one. The run
enumerated two thousand companies; building a file of two thousand named
individuals with their contact details, for companies nobody will ever write to,
creates an obligation with no corresponding benefit. Personal data gets collected
for the rows that are actually going to be contacted.

If the user wants the top of the WATCH pile routed as well, that is a deliberate
choice and the `priority_route_cap` in the state file is where it is recorded.

Report the count in scope and confirm before starting.

---

## Step 1 — The right person, before any address

Order matters. Find the correct human first; an address for the wrong person is
worth less than nothing, because the first touch is spent and the owner now has
the gatekeeper's framing.

Use `ownership_type` to know who can actually say yes:

| Ownership | Who can sell |
|---|---|
| Founder-owned | The founder. Usually owner, president or managing member |
| Family-owned | The majority shareholder. Check which generation holds the shares, not who holds the title |
| Management-owned | The majority holder, or the managing partner. Note that every shareholder has to want the same thing |
| Partner-owned | The named partners, per the partnership filing |
| ESOP | **Nobody you should cold-write to.** The trustee is not a seller in the ordinary sense. Route through counsel or mark unroutable |
| Sponsor-owned | Dropped at depth 2. Not here |
| `Not found` | **Do not route.** A letter that guesses who owns the company announces itself. Back to depth 2 for ownership, or leave it unrouted |

**A hired CEO cannot sell a family business.** Writing to one wastes the touch
and frequently gets your name to the owner with somebody else's framing on it.

**Where to look**, in order: the company's own site (about, team, history), the
state registry or Companies House (officers and agents are public and reliable),
the licence record (often names the qualifying individual, who is frequently the
owner), LinkedIn, trade association listings, and local press.

A second-generation name on an "our story" page is also a succession note. Record
it in `notes`, not as a signal unless it is dated.

**One contact per company.** Small companies talk. Writing to the owner and the
owner's son in the same week reads as a mail merge to both.

---

## Step 2 — A route to them

In order of what actually works with this audience.

### Warm path

If the row carries a warm path — including the `cold-only` scope rows from
`suppression.csv`, which exist precisely for this — **stop here.** Do not look
for an email. An introduction through a shared advisor, lender or peer converts
many times better than the best cold message anybody will ever write.

`route_status` = `warm-path`. The row leaves the cold queue entirely and goes to
the user as an introduction to make personally.

A warm path exists only when the person who would make the introduction has
agreed to be named. An assumed warm path is a fabricated one.

### Email

Only a real one.

| Acceptable | Not acceptable |
|---|---|
| Published on the company's own site | Guessed from a pattern, ever |
| In a registry, licence or official filing | Inferred because `info@` exists so the owner "probably" does too |
| In a trade or association listing the owner controls | Taken from a purchased list without independent verification |
| Returned by a verification service with a confidence score | A variant tried after a bounce |

> Pattern-guessing is the fastest way to destroy a sending domain. A high bounce
> rate on a young domain can end the ability to send email at all, for every
> campaign, for months. One guessed address is not worth that, and at volume it
> is not one guessed address, it is thirty.

### Posted letter

Where there is a contact form or a published phone number but no email, the
route is **paper**. A one-page letter to the owner of a licensed trade business
is the least regulated channel in most jurisdictions, is almost never sent by
anybody else, and outperforms cold email with offline owners more often than
people expect.

`route_status` = `form-or-phone`, and `contact_route` records the postal address
as published by the company.

### LinkedIn

Real but weaker for this audience, and only from a senior sender. Many owners of
very good private companies have a bare profile or none at all. Record the URL
where it exists. **Absence is not a negative signal** and it correlates with
exactly the companies nobody has called.

### Published phone

A real fallback, and a human job. Record it only if the company publishes it.
Never look up a personal number.

---

## Step 3 — Record confidence honestly

| `route_status` | Meaning |
|---|---|
| `warm-path` | An introduction is available and the introducer has agreed |
| `verified` | Confirmed deliverable by a verification service, with the date |
| `published` | On the company's own site or an official filing, with the URL |
| `form-or-phone` | No email. Letter or manual contact only |
| `linkedin-only` | A profile exists, nothing else does |
| `inferred-DO-NOT-USE` | From an imported list, pattern-derived. **Never sent to.** Exists only so a bought list can be flagged |
| `not-found` | No route located. An honest and common outcome |

Only `warm-path`, `verified`, `published` and `form-or-phone` can be drafted for.
`outreach-queue` enforces it.

Fill `owner_name`, `owner_title`, `owner_evidence` (what establishes that this
person can sell, with its tier and date), `contact_route`, `route_status`, and
`depth` = `5`.

---

## Step 4 — Flags that go back upstream

Routing is where research errors surface, because it is the first time anybody
looks hard at one company.

Report, and send back:

- **Actually sponsor-owned** — a transaction found during routing. Back to depth
  2, then PASS
- **Owner has died or exited** — check the register date. The conversation is
  with somebody else now, or not at all
- **Ownership turned out to be different** from what depth 2 established
- **A retained banker is running a process** — mandate section 8 decides whether
  this becomes a letter to the banker or a drop
- **The company has been sold since capture** — it happens on a six-day run

---

## Step 5 — The gate

### 🚧 HARD GATE — before writing

Show:

- Rows about to be updated, with the breakdown by `route_status`
- **Ten rows in full**, including every `not-found`
- Any company where no owner could be identified at all
- Every row whose ownership turned out to be different from the research
- Confirmation that **no** row carries a guessed address

Get approval. Then write, and update the state file.

---

## Step 6 — Report

```
CONTACT ROUTING COMPLETE — 2026-10-11
31 PRIORITY rows in scope

Flagged out during routing   3
  Severn Electrical              sold since capture, announced 2026-10-06.
                                 To PASS.
  Kessler Electric               owner died 2026-04, register confirms.
                                 Row closed, note added.
  Trevose Electrical             retained banker running a process. Mandate
                                 section 8 says do not go around. No cold
                                 draft. Letter to the banker offered instead.

Live rows                   28
  owner identified          26
  no owner identified        2   ← registry-only entities, no named officer,
                                   no team page, no licence qualifier named

Routes, of the 28
  warm-path                  3   ← operating partner knows all three.
                                   Off the cold queue, introductions to make
  published email           12
  verified email             5
  form-or-phone              6   ← letters. Three of these are the oldest
                                   companies on the list
  linkedin-only              0   ← one profile found, no other route; the
                                   senior sender declined the channel
  inferred-DO-NOT-USE        0   ← by design. Nothing is guessed
  not-found                  2   ← the two with no owner identified

Draftable now               26   (3 introductions + 17 email + 6 letters)

Other flags
  hired CEO, owner found
  via the register           4

Next: owner-outreach-drafting on the 23 cold rows. The 3 warm paths go to
the user as introductions, not drafts.
```

---

## Notes

- **Never invent an email.** Not once, not for the best row on the list, not
  because the pattern is obvious. `not-found` is the correct output and it is a
  real answer
- **Verify before any send.** Even published addresses go stale, and a batch
  check before the first send is cheap insurance for the domain
- **Professional footprint only.** No personal addresses, no personal numbers, no
  pretexting a receptionist. See `references/compliance.md`
- **This data is personal data.** It stays in the gitignored workspace and it is
  not collected for rows nobody will contact
- **Re-check before a second campaign.** Owners retire, sell, hand over and die.
  A contact file is stale faster than anybody expects
