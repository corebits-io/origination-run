# Mandate

> This is the only file you have to fill in. Every skill in the package reads it.
> Ten to fifteen minutes here decides whether a 2,000-row run returns a dozen
> real conversations or a thousand plausible-looking rows nobody will call.
>
> **Three rules while filling it in**
>
> 1. If something does not apply, write `N/A`
> 2. If you do not know yet, write `TBD`. The run will ask rather than invent
> 3. Answer section 1 properly. It decides whether the run starts at all
>
> Sections 4, 9 and 10 get better after your first run. Come back and update
> them. Stuck on the level of detail? `MANDATE-example.md` is a complete worked
> one.

---

## 1. Who we are

| Field | Your answer |
|---|---|
| Buyer entity | |
| Entity type | *fund / family office / search fund / independent sponsor / holdco / corporate development / other* |
| **Are you buying for your own account?** | *yes / no* |
| **Do you earn transaction-based compensation for arranging a purchase somebody else makes?** | *yes / no* |
| Capital status, stated honestly | *committed fund / pledge / deal-by-deal / balance sheet / seeking backing* |
| What we may truthfully say about our capital in a message to an owner | |
| Operating history we can point to | |
| Website | |

> **The principal-buyer gate.** If you earn a fee for arranging a transaction
> you are not a party to, the intake skill stops the run and tells you to talk
> to securities counsel about broker-dealer registration before anybody
> researches or writes to a company on your behalf. That gate has no override,
> and saying it is fine does not change the answer. See
> `references/compliance.md`.

---

## 2. What we are buying

| Field | Your answer |
|---|---|
| Platform, add-on, or both | |
| If add-ons: the existing platforms they would attach to | |
| For each platform: HQ, what it does, what it is missing | |
| Hold period | |
| Control or minority | |
| Will you back the existing management, or replace it | |

> **Name the platforms if you want add-ons.** Without a named receiving
> platform, "add-on" is a label with no test behind it and every add-on verdict
> on your list is a guess. Give the geography and the capability gap for each
> one.

---

## 3. Size box

| Field | Floor | Ceiling |
|---|---|---|
| Revenue | | |
| EBITDA | | |
| Headcount, if you use it | | |
| Enterprise value you can write | | |

| Field | Your answer |
|---|---|
| Which of the above is the real constraint | |
| Will you look below the floor for an add-on | *yes / no, and how far* |
| Minimum EBITDA margin, if any | |

> A labeled estimate outside this box makes a row WATCH, never a drop. Only a
> verified figure excludes on economics. That rule is not adjustable and the
> reason is in `references/estimation-rules.md`.

---

## 4. Sectors and segments

| Field | Your answer |
|---|---|
| Sectors in scope | |
| The specific segment inside each sector | |
| What makes a good one, in your words | |
| Business models you will not buy | |
| Revenue mix you require | *contract / recurring / project / mixed* |
| Sectors you have looked at and ruled out, and why | |

> Be narrow. "Business services" enumerates forty thousand companies and screens
> badly. "Commercial contract-recurring mechanical service, eleven counties"
> enumerates two thousand and screens well. The segment boundary is what makes
> the volume useful.

---

## 5. Geography

| Field | Your answer |
|---|---|
| Countries | |
| States, regions or metros | |
| Hard geographic constraint, or a preference | *hard / preference* |
| Radius around an existing platform, for add-ons | |
| Geographies you will not go to, and why | |

> Mark it hard or preference honestly. A hard constraint drops rows at depth 1,
> for free, before any expensive research. A preference only moves a row down
> the ranking. Marking a preference as hard is the most common way a real target
> leaves the list silently.

---

## 6. Must-haves

Three to five. Testable. Each one must be checkable from a public source or it
will be rewritten at intake.

| # | Must-have | How a researcher would test it |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |
| 5 | | |

> "Strong management team" is not a test. "A named second-tier manager who is
> not the owner and not a family member" is. Twelve aspirations means nothing
> survives the rubric. Three real requirements means the survivors mean
> something.

---

## 7. Actionable ownership types

Which owners can actually sell you the company, in your order of preference.

| Ownership type | In scope? | Notes |
|---|---|---|
| Founder-owned | | |
| Family-owned, second generation or later | | |
| Management-owned or partner-owned | | |
| ESOP | | |
| Sponsor-owned | *usually no* | |
| Corporate subsidiary or carve-out | | |
| Publicly listed | *no* | Out of scope by design |

| Field | Your answer |
|---|---|
| Will you buy from another sponsor | |
| Will you do a carve-out | |
| Minimum ownership stake the person you write to must hold | |

---

## 8. Exclusions, conflicts and suppression

| Field | Your answer |
|---|---|
| Portfolio conflicts: companies or segments you cannot approach | |
| Companies already worked, and the outcome | |
| Anybody who has asked not to be contacted | |
| Intermediaries you will not go around | |
| Hard nos: regulatory, reputational, ESG, customer concentration | |
| Existing relationships you want routed as warm, not cold | |

> Put every name you already know into `suppression.csv` before the run starts.
> An opt-out is permanent on every channel. The run reads that file at depth 1
> and again before anything is queued, and it has no way to override it.

---

## 9. Timing signals we care about most

Rank the four families for your thesis. The run reads this to decide what
promotes a row.

| Family | Rank 1-4 | What specifically, for you |
|---|---|---|
| Leadership and succession | | |
| Financing | | |
| Growth | | |
| Hiring | | |

| Field | Your answer |
|---|---|
| A signal that would make you call this week | |
| A signal you consider noise | |
| Do you want rows with no signal at all kept in the ranking | *yes, as WATCH / no* |

---

## 10. This run

| Field | Your answer |
|---|---|
| Run name | |
| Segment and geography for this run | |
| **Enumeration target** | *e.g. 2,000 companies* |
| How many companies you can research deeply this month | |
| How many owner conversations you can actually hold at once | |
| How many first touches per week, per sender | |
| Your deal target for the year | |
| What you already have: an existing list, a database export, nothing | |

> **The volume numbers are the budget, not an ambition.** Enumeration is cheap
> and wide on purpose. Deep research is expensive, so it is earned. Outreach is
> the narrowest number in the file, because the market you are sourcing in is
> one where owners know each other and talk. Intake does this arithmetic with
> you before it sources a single company. See `references/run-protocol.md`.

---

## 11. Senders and what each may truthfully claim

One row per person whose name will appear on a message.

| Sender | Role | Title as they would sign it | What is true about them that an owner would care about | Sending address | Weekly capacity |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |

| Field | Your answer |
|---|---|
| Who signs the first touch to an owner | |
| Anybody who may **not** be named in copy | |
| Named third parties cleared to be referenced, with their consent recorded | |

> The message carries a real person's name and every claim in it must be true
> about that person. An associate cold-writing to a founder about selling their
> life's work reads as low priority, because it is.

---

## 12. Channels, jurisdictions and counsel

| Field | Your answer |
|---|---|
| Channels in scope | *email / LinkedIn / posted letter / phone / introduction only* |
| Recipient jurisdictions this run will reach | |
| Postal address that goes in the footer of an email | |
| Counsel who has reviewed your outreach | |
| Has counsel confirmed your principal status | *yes / no / TBD* |
| Opt-out wording you want used | |

> The rules that bind you are the ones where the **recipient** sits, not where
> you sit. `references/compliance.md` sketches CAN-SPAM, CASL, UK GDPR and PECR
> and the EU position. It is a sketch, not a map, and it is not legal advice.

---

## 13. Notes

Anything else the run should know. Previous attempts and what went wrong, a
sector you keep nearly buying in, a lender who sees everything, a trade show
that matters, the reason the last process fell over.
