# idea-to-prd

A Claude Code skill that turns a raw software idea into a complete, multi-file PRD through structured discovery — and reasons critically about whether the idea holds up, instead of just documenting it.

## What it does

Acts as a **principal-level Product Manager** who:

- **Adapts its lens to the product's class.** A viral consumer app and an internal accounting module are different jobs. Go-to-market, moat, and CAC/LTV apply to a market-facing product and are *actively wrong* for an internal tool, an infra migration, or a research spike — the skill turns those lenses off.
- **Critiques by reasoning, not by script.** It reconstructs the user's numbers, names the load-bearing assumption, attacks the weakest one — even when that assumption isn't on any checklist — corrects false premises, and concedes when the user rebuts it with valid evidence.
- **Handles real complexity.** For large multi-module systems (ERP-class), it maps modules and their dependencies first, then discovers module-by-module, tracking state in a file rather than a leaky mental checklist.
- **Tells you when to stop.** If the honest read is "this shouldn't be built as framed," it says so before writing a single file.

Specialized for **software engineering contexts**: web apps, APIs, mobile apps, SaaS, CLIs, developer tools, internal/enterprise systems, regulated platforms, and large multi-module systems.

## Two axes set before any questions

| Axis | What it decides |
|------|-----------------|
| **Product class** | Which lenses apply. Market-facing / Internal tool / Regulated / Infrastructure-or-migration / Research-or-experimental — each has its own discovery bank, its own "minimum to proceed" gate, and its own success definition. |
| **Size & complexity** | Cadence and structure. Simple → lightweight. Standard → persisted state artifact. Complex/multi-module → decomposition mode (map modules + dependency graph before diving). |

Full per-class playbooks live in `references/product-classes.md`.

## How it works

The phases are a **state machine, not a one-way script** — any later phase can loop back to discovery when it exposes an earlier gap.

| Phase | What happens |
|-------|-------------|
| **0a — Classify** | Determine product class → set which lenses are ON/OFF |
| **0b — Size** | Simple / standard / complex → decide cadence, state artifact, decomposition |
| **1 — Idea Intake** | Scan for already-answered context; ask only what's missing (max 2) |
| **2 — Discovery** | Dimension-driven; class-specific + domain-specific questions; generative critique of claims; context-triggered pivots |
| **2.5 — Viability** | Class-appropriate adversarial challenges; flags surfaced in the summary header, not footnotes |
| **3 — Alignment** | Challenge weak metrics/scope, then a one-page summary; explicit preserve-vs-challenge rule; waits for confirmation |
| **4 — Generation** | Files scaled to class and scope (GTM only for market-facing; module-structured output for complex systems) |
| **4.5 — Consistency** | Traceability sweep across files (P0 ↔ story ↔ FR ↔ timeline; decision-log consequences honored) |
| **5 — Critical Path** | Before-Engineering-Kickoff checklist: riskiest assumptions, spikes, decision gates, stop criteria |

## Mechanisms (not slogans)

- **State artifact** — `prd/_discovery.md` with a **decision → downstream-consequence log**. "Offline-first" is recorded as forcing "sync-conflict resolution = P0" and "no last-write-wins data model," and that constraint is carried into generation and verified in the consistency pass. This is how a trade-off survives 12 modules and 15 rounds.
- **Generative critique** — a procedure: reconstruct the claim → name the load-bearing assumption → attack the weakest → correct facts → concede to valid rebuttals. The scripted challenges are *worked examples of the technique*, not the whole set.
- **Decomposition mode** — module map + dependency graph + per-module sub-PRDs, so an ERP isn't flattened into 9 shapeless files. Output is stable per-module structure that downstream schema/blueprint tooling can consume.
- **Cross-file consistency pass** — an actual verification step, so "cross-referenced" means something.

## Output

**Market-facing product (standard):** nine files

```
prd/
├── 00-overview.md     ├── 03-user-stories.md   ├── 06-timeline.md
├── 01-personas.md     ├── 04-technical.md      ├── 07-risks.md
├── 02-features.md     ├── 05-metrics.md        └── 08-gtm.md   ← market-facing only
```

**Internal / infra / research product:** `00`–`07` as relevant, **no `08-gtm.md`**.

**Complex / multi-module system:** `00-overview.md`, `dependency-map.md`, `07-risks.md`, plus `prd/modules/<module>/` sub-PRDs.

`04-technical.md` includes a **Privacy by Design** section (data minimization, consent, retention/DSAR, access control) whenever the product stores personal data.

## Product classes

| Class | Lenses ON | Lenses OFF |
|-------|-----------|------------|
| Market-facing | GTM, moat, CAC/LTV, acquisition, kill criteria, validation | — |
| Internal tool | adoption vs. workaround, build-vs-buy, maintenance owner | GTM, moat, CAC/LTV, competitors |
| Regulated | framework, liability, audit, data governance, privacy | GTM/moat unless also sold |
| Infra / migration | reliability/SLO, cutover/rollback, blast radius | GTM, moat, retention |
| Research / experimental | hypothesis, cheapest experiment, decision informed | GTM, moat, timeline-to-launch, revenue |

## Domain detection (orthogonal to class)

Two-sided marketplace · AI-native · developer tool · B2B Enterprise SaaS · IoT/Hardware · gaming · content/media · B2C mobile — each auto-adds specialized questions, stacking on top of any class.

## Evals

30 cases (`evals/evals.json`), 9 of them **fail-capable** (they define a specific wrong behavior that counts as a failure). Coverage:

- **Discovery & domain (1–8, 14–20):** scoping, rich context, feature additions, marketplace/B2B/AI detection, vanity-metric and scope-mismatch challenges
- **Conversation dynamics (9–13):** refusal, contradiction, language switch, alignment disagreement, post-PRD revision
- **Hard set (21–30):** internal/infra/research classes with market lenses off, multi-module decomposition, generative critique of an unlisted claim, factual correction, conceding to a valid rebuttal, the "don't build this" recommendation, the consistency pass, and state-artifact usage

**Run record (2026-06-01):** the 9 fail-capable evals (21–29) passed once each under an **independent-grader** setup (responder reads the skill files; a separate grader reads only the transcript + fail-conditions). The four reasoning evals — **23 generative critique, 24 factual correction, 25 concede-to-rebuttal, 26 shelf recommendation** — were then **variance-tested 5× each (20 runs) and held at 20/20 PASS, 0 fail-condition triggered**, with the grader's soft-spot notes kept visible rather than tuned away.

See `evals/eval-status.md` for the full run record, the methodology, and **why the previous "0 failures" result was discarded** (circular self-grading, no failure possible, deferred-as-pass inflation). A suite where nothing can fail proves nothing.

## Installation

Place the skill directory at `~/.claude/skills/idea-to-prd/`, or install via Claude Code:

```bash
/install-skill https://github.com/kabesma/idea-to-prd
```

## Triggering

Say things like: `"I want to build [something]"`, `"write a PRD for [feature/product]"`, `"help me write a PRD"`, `"I have an idea for an app"`, `"we need a feature for X"`.

**Does not trigger for:** architecture discussions without a deliverable, critiquing an existing PRD, implementation requests, or narrow technical questions.

## Language support

Written in English, but **adapts to the user's language at runtime** — conversation, PRD files, and the state artifact. Switches mid-conversation if the user does. Code-switching follows the dominant language; technical terms (API, SDK, P0, FR/NFR) may stay in English.

## File structure

```
idea-to-prd/
├── SKILL.md                       # Skill instructions
├── references/
│   ├── prd-templates.md           # Templates for all files + multi-module output
│   └── product-classes.md         # Per-class lenses, question banks, gates
└── evals/
    ├── evals.json                 # 30 test cases (9 fail-capable)
    └── eval-status.md             # Honest methodology + run status
```
