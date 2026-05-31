# Product Classes — Lenses, Question Banks & Gates

The **product class** is the primary axis of this skill (set in Step 0a of `SKILL.md`). It decides which lenses are ON and which are actively wrong to apply. A consumer app and an internal accounting module are different jobs. Read the relevant section once the class is clear; do not run a market-facing playbook on a non-market product.

A product may carry a **secondary** lens (an externally-sold regulated fintech is *market-facing + regulated* → both sets ON). The **domain add-ons** (marketplace, AI-native, gaming, etc.) in `SKILL.md` are orthogonal and stack on top of any class.

---

## 1. Market-facing

**Definition:** sold or distributed to users outside the building organization — consumer apps, B2B SaaS, marketplaces, paid developer tools, mobile apps.

**Lenses ON:** go-to-market, competitive moat, CAC/LTV and unit economics, acquisition funnel, retention, external validation, kill criteria.

**Discovery question bank (add the relevant ones):**
- What do users use today to solve this? Why would they switch — specifically, what does the incumbent lack?
- Direct/indirect competitors? Sustainable advantage over the one with the strongest distribution or network effect?
- Validated with real users (interviews, waitlist, beta)? Or is the problem still an internal belief?
- Business model / sustainability — if free/OSS, who funds the ongoing cost?
- At what point would you kill or pivot? What signal says it's not working?

**Pressure-tests (Phase 2.5), pick the 1–2 sharpest:**
- "If [the obvious incumbent] ships this tomorrow, what changes and what doesn't?"
- "Your top 3 reasons this fails — the most pessimistic honest version."
- "Who holds the strongest network effect/distribution here, and what's your specific path past them?"
- *(AI-native)* "Is 'AI-powered' a capability or a positioning claim? If a frontier model makes it free tomorrow, what's left?"
- *(stated conversion/revenue)* "That conversion number — benchmark, competitor data, or your own research?"

**Gate to leave Phase 2:** universal floor + kill criteria known/flagged + ≥2 pressure-tests covered, of which **competitive context OR external validation must be one** (business model alone is insufficient).

**PRD files:** full nine — includes `08-gtm.md`.

---

## 2. Internal tool

**Definition:** used by employees of the building org; replaces a manual / Slack / spreadsheet workflow; there is no external market and no "customer" to acquire.

**Lenses ON:** adoption vs. the current workaround, build-vs-buy, maintenance ownership, internal rollout/change-management, integration with internal systems (SSO, HR system, data warehouse).
**Lenses OFF — do not ask these:** competitive moat, CAC/LTV, go-to-market, acquisition funnels, "who are your competitors," market kill-criteria.

**Discovery question bank:**
- What's the current workaround, and what *exactly* breaks at the current scale? (the real "competitor" is the spreadsheet)
- Why build vs. buy an off-the-shelf tool? What makes the off-the-shelf option not fit?
- Who maintains this after the original builder moves on? Is there an owning team?
- What's the rollout plan — mandated, opt-in, phased by team? What drives people to actually switch off the old way?
- Which internal systems must it integrate with (identity, HR, finance, data)?
- What's the cost of *not* building it (hours wasted, errors, compliance exposure)?

**Pressure-tests (Phase 2.5):**
- "What stops the team from reverting to the spreadsheet in month 2?"
- "Why build this instead of buying [obvious option] — honestly?"
- "Who owns this in 18 months when it breaks and the builder is on another team?"

**Gate to leave Phase 2:** universal floor + adoption-vs-current-workaround addressed + build-vs-buy considered + maintenance owner known/flagged.

**PRD files:** 00–07 as relevant, **omit `08-gtm.md`.** Put adoption/rollout in `06-timeline.md` and `07-risks.md`. Success metric = adoption / time saved / error reduction, not acquisition.

---

## 3. Regulated / compliance-driven

**Definition:** health, finance, legal, government, identity, payments, or services to minors; or anywhere "compliance/legal said…" is a hard input. May *also* be market-facing.

**Lenses ON:** applicable regulatory framework, liability ownership, audit trail, data governance, certification/legal-review timeline, **privacy by design**. (Add market lenses only if also externally sold.)

**Discovery question bank:**
- Which framework applies (HIPAA, SOC2, PCI-DSS, GDPR, FERPA, KYC/AML, etc.)?
- Who owns liability if something goes wrong? Where does it sit legally?
- What must be auditable — who did what, when, with what data? Retention requirements?
- Data: what PII/PHI/financial data is touched? Minimization, consent/lawful basis, residency, deletion/erasure (DSAR)?
- What's the legal/certification review timeline, and is it on the critical path?

**Pressure-tests (Phase 2.5):**
- "Which single control here is the one an auditor or regulator fails you on if it's wrong?"
- "Is the compliance timeline on the critical path — and have you sequenced for it?"

**Gate to leave Phase 2:** universal floor + applicable framework identified + highest-liability control surfaced + any open compliance question flagged as **blocking** (not a footnote).

**PRD files:** include `04-technical.md` with a full privacy-by-design section and consider a dedicated `10-security.md` / `09-data-governance.md`. GTM only if externally sold.

---

## 4. Infrastructure / platform / migration

**Definition:** internal platform, shared service, data pipeline, dev-infra, or a legacy migration/cutover. The consumers are other systems or internal teams, not a market.

**Lenses ON:** reliability/SLO, backward compatibility, migration & cutover safety, rollback, internal adoption by consuming teams, blast radius / failure isolation.
**Lenses OFF:** GTM, moat, CAC/LTV, app-store/retention metrics.

**Discovery question bank:**
- Who/what consumes this — which teams or systems, and what's their hard dependency?
- Reliability target (SLO/SLA)? What's the cost of an outage to the consumers?
- Migration: what's the cutover strategy — big-bang, strangler-fig, dual-run? Rollback plan?
- Backward compatibility — what existing contracts/clients must keep working?
- Blast radius — if this fails, what else fails with it? How is that contained?
- Adoption — are consuming teams mandated onto it, or do they choose? What's the migration cost *for them*?

**Pressure-tests (Phase 2.5):**
- "What's the blast radius if the cutover goes wrong, and what's the rollback?"
- "Which consuming team is most likely to refuse to migrate, and why?"

**Gate to leave Phase 2:** universal floor + reliability/SLO expectation + migration/cutover-and-rollback plan known/flagged + blast radius understood.

**PRD files:** 00–07 as relevant, **omit `08-gtm.md`.** Emphasize `04-technical.md` (compatibility, SLO, cutover) and `07-risks.md` (rollback, blast radius). Success metric = reliability + consumer adoption, not market metrics.

---

## 5. Research / experimental

**Definition:** a prototype or spike whose purpose is to *learn* whether something is true — "we want to find out whether…", a POC, a throwaway.

**Lenses ON:** the learning goal, a falsifiable hypothesis, what *decision* the result will inform, throwaway-vs-keep.
**Lenses OFF:** GTM, moat, timeline-to-launch, retention, revenue, polish.

**Discovery question bank:**
- What's the hypothesis, stated so it can be proven false?
- What decision does the result inform — what do you do differently if it's true vs. false?
- What's the *cheapest* experiment that answers it? (Is a PRD even the right artifact, or a one-week spike?)
- What's the success threshold — what result counts as "validated"?
- Throwaway or foundation — does this code/design survive if the hypothesis holds?

**Pressure-tests (Phase 2.5):**
- "Is this the cheapest experiment that answers the question, or are you over-building the test?"
- "If the result is negative, will you actually stop — or is this validation theater?"

**Gate to leave Phase 2:** universal floor + falsifiable hypothesis stated + decision-the-result-informs named + cheapest-experiment sanity check.

**PRD files:** lean — often just `00-overview.md` (with hypothesis + success threshold), `04-technical.md` (the spike plan), and `07-risks.md`. No GTM, no metrics-funnel file, no Alpha/Beta timeline.

---

## Quick reference — gate + GTM by class

| Class | Extra gate beyond universal floor | `08-gtm.md`? | Kill/stop criteria framed as |
|-------|-----------------------------------|--------------|------------------------------|
| Market-facing | competitive context OR validation + kill criteria | **Yes** | market kill signal |
| Internal tool | adoption + build-vs-buy + maintenance owner | No | cancel-or-buy-instead |
| Regulated | framework + top liability control + blocking compliance Qs | only if sold | compliance gate failure |
| Infra / migration | SLO + cutover/rollback + blast radius | No | cutover failure / rollback trigger |
| Research | hypothesis + decision-informed + cheapest-experiment | No | negative result ends it |
