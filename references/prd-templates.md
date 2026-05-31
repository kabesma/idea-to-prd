# PRD File Templates

These are the exact templates for each of the 8 PRD output files. Fill in all placeholders based on the discovery conversation.

**Context-aware guidance:** Remove or mark N/A any section that genuinely does not apply. Do not include a section just because the template has it. The goal is a useful document, not a complete template. When in doubt: less is more.

---

## 00-overview.md

```markdown
# [Product Name] — Overview

> **Version:** 1.0 | **Date:** [YYYY-MM-DD] | **Status:** Draft

## Problem Statement

[2–3 sentences: What pain does this solve? Who experiences it? How significant is the problem?]

## Solution Summary

[2–3 sentences: What are we building? How does it solve the problem?]

## Goals

| Goal | Metric | Target | Timeline |
|------|--------|--------|----------|
| [Goal 1] | [How measured] | [Target value] | [By when] |
| [Goal 2] | [How measured] | [Target value] | [By when] |

## Non-Goals

What this product explicitly will NOT do:
- [Non-goal 1]
- [Non-goal 2]

## Assumptions

- [Assumption 1]
- [Assumption 2]

## Stakeholders

<!--
For team projects, list each role with the person or team responsible.
For solo or open source projects, simplify: list just yourself as owner and remove rows that don't apply.
Example for solo project:
| Role | Responsibility |
|------|----------------|
| Owner | [Your name] — all decisions |
-->

| Role | Name/Team | Responsibility |
|------|-----------|----------------|
| Product Owner | [Name] | Final decisions on scope |
| Engineering Lead | [Name/TBD or N/A] | Technical feasibility |
| Design | [Name/TBD or N/A — e.g., "N/A — CLI tool"] | UX/UI |

## Related Documents

- [01-personas.md](01-personas.md)
- [02-features.md](02-features.md)
- [03-user-stories.md](03-user-stories.md)
- [04-technical.md](04-technical.md)
- [05-metrics.md](05-metrics.md)
- [06-timeline.md](06-timeline.md)
- [07-risks.md](07-risks.md)
```

---

## 01-personas.md

```markdown
# [Product Name] — User Personas

## Persona Overview

| Persona | Role | Primary Goal | Key Pain Point |
|---------|------|-------------|----------------|
| [Name] | [Role] | [What they want] | [What frustrates them today] |

---

## Persona 1: [Persona Name]

**Role:** [Job title / user type]
**Demographics:** [Age range, tech savvy level, context of use]

**Goals:**
- [Primary goal]
- [Secondary goal]

**Pain Points:**
- [Pain 1 — what they struggle with today]
- [Pain 2]

**Jobs to Be Done:**
> When [situation], I want to [action] so that [outcome].

**Typical Workflow Today:**
1. [Step 1 of current workflow]
2. [Step 2 — where friction exists]
3. [Step 3]

**How This Product Helps:**
[1–2 sentences on how the product resolves their pain]

---

## Persona 2: [Persona Name]

[Repeat structure above]

---

## Primary Persona

**[Persona Name]** is the primary user. All P0 features must serve this persona first.
```

---

## 02-features.md

```markdown
# [Product Name] — Features & Scope

## Priority Definitions

| Label | Meaning |
|-------|---------|
| **P0** | Launch blocker — product cannot ship without this |
| **P1** | High value — ship in V1 if time allows |
| **P2** | Nice-to-have — V2 or later |
| **Out** | Explicitly out of scope |

---

## Feature Priority Matrix

| # | Feature | Priority | Persona | Rationale |
|---|---------|----------|---------|-----------|
| F1 | [Feature name] | P0 | [Persona] | [Why this priority — links to a user need] |
| F2 | [Feature name] | P0 | [Persona] | |
| F3 | [Feature name] | P1 | [Persona] | |
| F4 | [Feature name] | P2 | [Persona] | |
| F5 | [Feature name] | Out | — | [Why excluded] |

---

## Feature Details

### F1: [Feature Name] — P0

**Description:** [What does this feature do?]

**User Need:** [Which persona, which pain point from 01-personas.md]

**Key Behavior:**
- [Behavior 1]
- [Behavior 2]

**Dependencies:** [Other features or systems this depends on]

---

### F2: [Feature Name] — P0

[Repeat structure]
```

---

## 03-user-stories.md

```markdown
# [Product Name] — User Stories

## Format

> As a [persona], I want to [action] so that [outcome].

---

## Epic 1: [Epic Name — e.g., Authentication]

### Story 1.1: [Story Title]

**Story:**
> As a [persona], I want to [action] so that [outcome].

**Priority:** P0

**Acceptance Criteria:**
- [ ] [Criterion 1 — testable, observable behavior]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

<!-- Edge Cases and Out of Scope are optional.
     Include them for complex stories where failure modes matter.
     Omit them for straightforward CRUD operations to keep the document lean. -->

**Edge Cases** *(include only for non-trivial stories):*
- [Edge case 1 — what happens when...]
- [Edge case 2]

**Out of Scope for this Story** *(include only when the boundary is non-obvious):*
- [What this story does NOT cover]

---

### Story 1.2: [Story Title]

[Repeat structure]

---

## Epic 2: [Epic Name]

[Repeat structure]
```

---

## 04-technical.md

```markdown
# [Product Name] — Technical Requirements

## Platform & Environment

| Attribute | Value |
|-----------|-------|
| Platform | [Web / iOS / Android / Desktop / CLI / API] |
| Supported browsers/OS | [e.g., Chrome 100+, Safari 15+, iOS 15+] |
| Deployment | [Cloud provider / self-hosted / TBD] |
| Tech stack | [Frontend / Backend / DB — or TBD if not decided] |

---

## Functional Requirements

These are behaviors the system must perform.

| ID | Requirement | Priority | Source |
|----|-------------|----------|--------|
| FR1 | [System must do X] | P0 | [Links to story or feature] |
| FR2 | [System must do Y] | P1 | |

---

## Non-Functional Requirements

These are quality attributes the system must have.

<!--
Only include NFRs that are genuinely relevant to this context:
- WCAG accessibility: relevant for web and mobile apps used by the public; skip for CLI tools, server-side APIs, and internal developer tools
- 99.9% uptime: relevant for consumer-facing products and critical infrastructure; may be overkill for internal tools with <500 users
- OWASP Top 10: relevant for any product handling user auth, payment, or sensitive data; less relevant for read-only public tools
- Scalability targets: base on actual usage projections, not generic maximums
Remove rows that don't apply — a half-relevant NFR is worse than no NFR.
-->

| ID | Attribute | Requirement | Rationale |
|----|-----------|-------------|-----------|
| NFR1 | Performance | [e.g., page load < 2s on 4G] | [Why this matters for this product] |
| NFR2 | Availability | [e.g., 99.5% uptime — calibrate to actual user expectations] | |
| NFR3 | Security | [e.g., OWASP Top 10 — if handling auth/payments/PII] | |
| NFR4 | Scalability | [e.g., support N concurrent users — based on realistic projections] | |
| NFR5 | Accessibility | [e.g., WCAG 2.1 AA — for public-facing web/mobile; N/A for CLI] | |

---

## Integrations

| System | Direction | Purpose | Auth Method |
|--------|-----------|---------|-------------|
| [System name] | Inbound / Outbound | [What data flows] | [API key / OAuth / etc.] |

---

## Data Requirements

- **Data stored:** [What user data is persisted?]
- **Data sensitivity:** [PII? Payment data? Health data?]
- **Retention policy:** [How long is data kept?]
- **Compliance:** [GDPR, HIPAA, SOC2, etc. — if applicable; omit if not relevant]

---

## Technical Assumptions & Open Questions

- [ ] **[Open question 1]** — [What needs to be decided before engineering starts]
- [ ] **[Open question 2]**
```

---

## 05-metrics.md

```markdown
# [Product Name] — Success Metrics

## North Star Metric

> **[Single most important metric]**
> [Why this is the north star — what user behavior it reflects]

---

## OKRs

### Objective: [High-level goal]

| Key Result | Baseline | Target | Timeline |
|------------|----------|--------|----------|
| [KR1] | [Current state] | [Goal] | [Date] |
| [KR2] | | | |

---

## Metrics by Phase

### Phase 1 — Launch (0–30 days)
Measure adoption and first-run success.

| Metric | Definition | Target | Source |
|--------|------------|--------|--------|
| [Activation rate] | [% users who complete first key action] | [X%] | [Analytics tool] |
| [Day-7 retention] | [% users who return within 7 days] | | |

### Phase 2 — Growth (30–90 days)
Measure engagement and value delivery.

| Metric | Definition | Target | Source |
|--------|------------|--------|--------|
| [DAU/MAU ratio] | [Stickiness] | | |

### Phase 3 — Scale (90+ days)
Measure business impact.

| Metric | Definition | Target | Source |
|--------|------------|--------|--------|
| [Revenue / conversion] | | | |

---

## Anti-Metrics (what we're NOT optimizing for)

- [Anti-metric 1 — e.g., "We do not optimize for raw pageviews"]
- [Anti-metric 2]

---

## Analytics Implementation

| Event | Properties | Trigger |
|-------|------------|---------|
| [event_name] | [key: value] | [When does this fire?] |
```

---

## 06-timeline.md

```markdown
# [Product Name] — Timeline & Milestones

<!--
Choose the timeline structure that fits your context:

A) New product (default): Discovery → Alpha → Beta → Launch
B) Feature addition to an existing product: Scoping → Build → Release
C) Improvement/redesign of an existing flow: Audit → Design → Build → Measure
D) Open source / solo project: Prototype → v0.1 → v1.0

Replace the structure below with whichever fits. "Alpha" and "Beta" are meaningful
only when there are distinct internal and external testing stages — skip them for
feature additions, small teams, or open source projects without a traditional beta.
-->

## Overview

<!-- Example for a new product (adapt for other contexts): -->
| Phase | Description | Duration | Target Date |
|-------|-------------|----------|-------------|
| Discovery | Requirements finalized, designs started | [X weeks] | [Date] |
| Alpha | Core P0 features built, internal testing | [X weeks] | [Date] |
| Beta | All P1 features, limited external users | [X weeks] | [Date] |
| Launch | Public release | — | [Date] |

<!-- Example for a feature addition:
| Phase | Description | Duration | Target Date |
|-------|-------------|----------|-------------|
| Scoping | Requirements and design finalized | [X weeks] | [Date] |
| Build | Feature implemented and tested | [X weeks] | [Date] |
| Release | Staged rollout to production | [X weeks] | [Date] |
-->

---

## Phase 1: [Phase Name]

**Goal:** [What this phase must accomplish]

**Deliverables:**
- [ ] [Deliverable 1]
- [ ] [Deliverable 2]

---

## Phase 2: [Phase Name]

**Goal:** [What this phase must accomplish]

**Deliverables:**
- [ ] [Feature or milestone 1]
- [ ] [Feature or milestone 2]

---

## Phase 3: [Phase Name] *(if applicable)*

**Goal:** [What this phase must accomplish]

**Deliverables:**
- [ ] [Deliverable 1]

---

## Open Items

- [ ] [Decision needed: X] — Owner: [Name/TBD] — Due: [Date]
```

---

## 07-risks.md

```markdown
# [Product Name] — Risks, Assumptions & Out of Scope

## Risk Register

| # | Risk | Likelihood | Impact | Mitigation |
|---|------|-----------|--------|------------|
| R1 | [Risk description] | High / Med / Low | High / Med / Low | [How to reduce or respond] |
| R2 | | | | |

---

## Key Assumptions

These are things we believe to be true but have not fully validated. Each assumption is a risk if wrong.

| # | Assumption | Validation Plan |
|---|-----------|----------------|
| A1 | [We assume that users will X] | [User interviews / A-B test / survey] |
| A2 | [We assume the tech stack can handle Y] | [Spike / proof of concept] |

---

## Dependencies

| Dependency | Owner | Risk if Blocked |
|-----------|-------|----------------|
| [External API / team / decision] | [Who owns it] | [What breaks if this is delayed] |

---

## Out of Scope

These items were explicitly excluded from V1. They may be revisited in future versions.

| Item | Reason for Exclusion | Future Version? |
|------|---------------------|----------------|
| [Feature/capability] | [Too complex / low priority / separate product] | V2 / TBD / No |

---

## Open Questions

These must be answered before engineering begins.

- [ ] **[Question 1]** — Owner: [Name/TBD] — Due: [Date]
- [ ] **[Question 2]** — Owner: [Name/TBD] — Due: [Date]
```
