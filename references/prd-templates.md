# PRD File Templates

These are the exact templates for each of the 8 PRD output files. Fill in all placeholders based on the discovery conversation. Remove sections that genuinely don't apply — but only if they truly don't apply, not because the information is unknown.

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

| Role | Name/Team | Responsibility |
|------|-----------|----------------|
| Product Owner | [Name] | Final decisions on scope |
| Engineering Lead | [Name/TBD] | Technical feasibility |
| Design | [Name/TBD] | UX/UI |

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

**Edge Cases:**
- [Edge case 1 — what happens when...]
- [Edge case 2]

**Out of Scope for this Story:**
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
| Platform | [Web / iOS / Android / Desktop / API] |
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

| ID | Attribute | Requirement | Rationale |
|----|-----------|-------------|-----------|
| NFR1 | Performance | [e.g., page load < 2s on 4G] | [Why this matters] |
| NFR2 | Availability | [e.g., 99.9% uptime] | |
| NFR3 | Security | [e.g., OWASP Top 10 compliance] | |
| NFR4 | Scalability | [e.g., support 10k concurrent users] | |
| NFR5 | Accessibility | [e.g., WCAG 2.1 AA] | |

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
- **Compliance:** [GDPR, HIPAA, SOC2, etc. — if applicable]

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

## Overview

| Phase | Description | Duration | Target Date |
|-------|-------------|----------|-------------|
| Discovery | Requirements finalized, designs started | [X weeks] | [Date] |
| Alpha | Core P0 features built, internal testing | [X weeks] | [Date] |
| Beta | All P1 features, limited external users | [X weeks] | [Date] |
| Launch | Public release | — | [Date] |

---

## Phase 1: Discovery & Design

**Goal:** Finalize requirements and produce design mockups for all P0 features.

**Deliverables:**
- [ ] PRD signed off by stakeholders
- [ ] Wireframes for all P0 flows
- [ ] Tech stack decided
- [ ] Database schema designed

---

## Phase 2: Alpha (Internal)

**Goal:** Working product with all P0 features for internal testing.

**Deliverables:**
- [ ] [Feature F1] built and tested
- [ ] [Feature F2] built and tested
- [ ] Basic error handling and logging

---

## Phase 3: Beta (Limited External)

**Goal:** P0 + P1 features, with real users providing feedback.

**Deliverables:**
- [ ] [Feature F3] built and tested
- [ ] Analytics instrumented
- [ ] Performance targets met

---

## Phase 4: Launch

**Goal:** Public release with monitoring in place.

**Deliverables:**
- [ ] All P0 and prioritized P1 features shipped
- [ ] Documentation published
- [ ] On-call runbook created
- [ ] Launch announcement ready

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
