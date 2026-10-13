# Compliance, Ethics and Two Thousand Named Strangers

**This is not legal advice.** Nobody who wrote this is your lawyer. Securities
rules, marketing rules and data protection rules are jurisdiction specific, fact
specific and unforgiving. Talk to qualified counsel before you send a single
message.

What this file is: the guardrails the skills enforce by default, so the run does
not casually produce something that creates a problem for you. They are
deliberately conservative. Your counsel may loosen them. They should not need to
tighten them.

---

## 1. The first question: principal or intermediary

This decides whether the run starts at all.

**Buying as a principal.** You, your fund, your search vehicle or your holdco
intend to acquire the company for your own account. Writing to owners about
buying their business is the ordinary activity of a principal buyer. This is the
model the whole package assumes.

**Acting as an intermediary.** If you source for somebody else and expect
transaction-based compensation — a success fee, a percentage, a finder's fee —
you may be acting as an unregistered broker-dealer under US federal and state
law. The consequences are serious: rescission rights, fee disgorgement, and
worse. The M&A broker exemptions are narrow and conditional.

> Mandate section 1 records the answer. If it says yes to
> transaction-based compensation for somebody else's acquisition, **the intake
> skill stops the run** and tells you to talk to securities counsel. That gate
> has no override and the package provides no way around it. If it says `TBD`,
> the run stops and asks.

**Private targets only.** This package targets private companies. If a target is
public, or you acquire material non-public information about a public company
during research, you are in insider trading territory and nothing here covers
you. Public companies are dropped at depth 1 by design.

---

## 2. Two thousand rows is a data protection fact

This is the part that is different from a hundred-row list, and it is the part
people do not think about until somebody asks.

At the end of a run you hold a file containing the names of hundreds of
individuals, their employers, their roles, in some cases their contact details,
and notes about their businesses and their intentions. In the UK and EU that is
personal data about identifiable people, processed for your commercial purposes,
and it carries obligations whether or not you ever contact them: a lawful basis,
transparency, accuracy, retention limits, and the right of the person to see what
you hold and have it erased.

What the package does about it:

| Rule | Where it lives |
|---|---|
| **Research the company at depth 2, the person only at depth 5** | So personal data is collected for the thirty-one rows you will actually contact, not the two thousand you enumerated |
| **Professional footprint only** | Roles, tenure, licences, filings, public statements. Never health, family, finances, divorce, estates, or anything about private life, even where technically public |
| **Notes are factual** | Assume every note could be read back to the person in it, because in some jurisdictions they have the legal right to ask |
| **Minimum retained** | A row you will never contact does not need an owner name on it |
| **Delete on request** | Remove the data, and keep only what is needed to honour the do-not-contact state itself |
| **The workspace is never committed** | The `.gitignore` blocks it. Do not override it |

---

## 3. Email rules follow the recipient

The rules that bind a message are the ones where the **recipient** sits, not
where you sit. This is a sketch, not a map.

- **US, CAN-SPAM.** Truthful headers, no deceptive subject line, a working
  opt-out honoured promptly, and a physical postal address in the message. No
  prior consent required, but every other rule here still applies
- **Canada, CASL.** Materially stricter. Commercial electronic messages
  generally require consent, express or implied, with narrow exemptions, and the
  penalties are large. Do not email Canadian owners before you understand it
- **UK, UK GDPR and PECR.** PECR governs electronic marketing. Corporate
  subscriber addresses are treated differently from individual ones, but sole
  traders and partnerships often count as individuals, which describes a great
  many small business owners. UK GDPR applies to your file regardless
- **EU, GDPR and the ePrivacy rules.** Similar shape to the UK, implemented
  differently in each member state. B2B cold email that is lawful in one member
  state is not lawful in another
- **A posted letter** is the least regulated channel in most jurisdictions and
  frequently the most effective with offline owners. Where the email position is
  unclear, the queue prefers paper

**Opt-outs are permanent, everywhere.** They go in `suppression.csv` with scope
`all`, and the queue refuses to stage to them. There is no legitimate reason to
override that, so there is no way to.

---

## 4. No misrepresentation, ever

- **No fake committed capital.** "Funded" means committed capital exists and
  mandate section 1 permits saying so. Searchers and independent sponsors
  describe their model honestly, which is also the version owners respect
- **No invented offers, LOIs or valuations.** Nothing implies a price you have
  not underwritten
- **No fake urgency or scarcity.** A manufactured deadline is misrepresentation
  with a clock on it
- **No fabricated warm paths or endorsements.** Nobody is named without recorded
  consent
- **No pretexting in research.** No posing as a customer, a job applicant, a
  student or a survey. No calling reception under a false name to find out who
  owns the company. If a fact is only obtainable by deception, the fact is
  `Not found`
- **Respect the sites you use.** Read the terms. Many directories prohibit bulk
  extraction and several platforms restrict automated collection. Manual reading
  at human pace is almost always fine; harvesting frequently is not

---

## 5. Confidentiality once somebody engages

The moment an owner replies properly, they start telling you things they have
told nobody else.

- Treat everything an owner shares as confidential from the first call, NDA or
  not. Reputation in a small segment is your sourcing channel
- Get the NDA signed before financials change hands, and track `nda_status`
- Never leak one owner's information to another, **including by implication**.
  "We are also talking to someone else in your market" is a leak
- What an owner said is not the same as what has been verified. Keep the
  distinction in the notes, in the quotes, and in any memo

---

## 6. The approval gate

No message leaves this system without a human reading it first. The run drafts,
checks and stages. Sending is a separate, explicit, human action.

---

## 7. Before any batch goes out

- [ ] Counsel has confirmed principal status, or the intermediary question is
      resolved
- [ ] Mandate section 12 records the recipient jurisdictions and counsel
- [ ] Recipient jurisdictions checked against the rules above
- [ ] An opt-out path exists in every email and works
- [ ] `suppression.csv` applied to the staged queue, re-checked at queue time
- [ ] No message implies capital, an offer or a valuation that does not exist
- [ ] Every named third party is cleared to be named
- [ ] No target in the batch is a public company
- [ ] A named human has approved every message in the batch
- [ ] The workspace is gitignored and not sitting in a shared drive by accident

This file is a floor, not a ceiling, and it is not legal advice. Where anything
here conflicts with what your counsel tells you, your counsel wins.
