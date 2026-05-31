# idea-to-prd

A Claude Code skill that transforms any raw software idea into a complete, multi-file PRD through structured discovery questioning.

## What it does

Acts as a **Senior Product Manager** who asks the right questions first, achieves alignment, then generates a production-ready PRD split across focused files — so engineering teams get exactly what they need without under- or over-engineering.

Specialized for **software engineering contexts**: web apps, APIs, mobile apps, SaaS platforms, CLIs, and internal tools.

## How it works

The skill follows 6 phases before and after writing a PRD:

| Phase | What happens |
|-------|-------------|
| **1 — Idea Intake** | Scans for already-answered context; asks only what's missing (max 2 questions) |
| **2 — Discovery** | Dimension-driven questioning — covers users, features, tech, metrics, competitive context, and validation; adapts based on context-triggered pivots; detects product domain and auto-adds domain-specific questions; challenges weak assumptions directly |
| **2.5 — Pre-Alignment Viability Check** | Mandatory gate before writing anything: surfaces kill criteria, competitive differentiation gaps, and unvalidated assumptions; fires adversarial challenges not yet covered in discovery |
| **3 — Alignment Check** | Challenges weak metrics and over-scoped MVPs before presenting a one-page summary; waits for explicit confirmation |
| **4 — PRD Generation** | Generates structured files scaled to scope — fewer for feature additions, 9 files (including GTM) for new products |
| **5 — Post-PRD Critical Path** | Presents a Before Engineering Kickoff checklist: riskiest assumptions, technical spikes needed, decision gates, kill criteria, and suggested review chain |

## Output

```
prd/
├── 00-overview.md       # Executive summary, problem, goals
├── 01-personas.md       # User personas, jobs-to-be-done
├── 02-features.md       # Feature matrix with P0/P1/P2 priority
├── 03-user-stories.md   # Stories with acceptance criteria
├── 04-technical.md      # Functional vs non-functional requirements
├── 05-metrics.md        # KPIs, north star metric, analytics events
├── 06-timeline.md       # Phases, milestones, deliverables
├── 07-risks.md          # Risks, assumptions, dependencies, out of scope
└── 08-gtm.md            # Go-to-market: segment, positioning, distribution, pricing, moat
```

`08-gtm.md` is generated for all new products. Feature additions and internal tools use a smaller subset.

## Domain Detection

The skill detects product type and auto-adds domain-specific discovery questions:

| Domain | Detected by |
|--------|-------------|
| Two-sided marketplace | Supply/demand split, platform fee model |
| AI-native product | Model/provider references, AI as value prop |
| Developer tool | CLI, SDK, API, IDE extension context |
| Regulated industry | Health, finance, legal, education for minors |
| B2B Enterprise SaaS | Enterprise buyers, SSO/procurement requirements |
| IoT / Hardware + Software | Device lifecycle, offline behavior, connectivity |
| Gaming | Core loop, retention, monetization model |
| Content / Media Platform | Creator economics, content moderation |
| B2C Mobile App | App store distribution, push notification flow |

## Evals

20 test cases covering:

- **Happy path** (evals 1–8): vague input, rich context, feature addition, internal tool, two-sided marketplace, developer CLI, onboarding redesign
- **Adversarial — conversation dynamics** (evals 9–13): user refuses to answer questions, contradictory information, mid-conversation language switch, disagreement with alignment summary, post-PRD revision from engineering feedback
- **Adversarial — output quality** (evals 14–17): vanity metric challenge, marketplace domain detection, post-PRD critical path output, scope/team/timeline mismatch
- **New behaviors** (evals 18–20): B2B Enterprise domain detection, kill criteria gate, AI-native premise challenge

Key behaviors validated over baseline:

- Skips Phase 1 questions when the user's initial message already answers them
- Never re-asks questions the user already answered
- Preserves the user's exact metric framing (does not reframe "60% drop-off" as "40% completion")
- Enforces Phase 2.5 viability check — kill criteria must be answered or flagged before alignment summary
- Challenges weak competitive moats, AI-as-differentiator claims, and assumed conversion rates
- Responds to context-triggered pivots (paying customers, fundraising, named competitors, hard deadlines)
- Enforces alignment check before writing — baseline skips this
- Scales file count to scope — feature additions use 4–5 files, new products use all 9
- Caps questions at 3–4 per round — baseline fires 5+ at once
- Consistently includes acceptance criteria (Given/When/Then), out-of-scope section, and FR/NFR distinction
- Adapts templates to context: removes WCAG for CLI tools, adapts timeline for feature additions
- Challenges vanity metrics before accepting them into the PRD
- Flags scope/team/timeline mismatches explicitly
- Generates 08-gtm.md for all new products

## Installation

Install via Claude Code:

```bash
/install-skill https://github.com/kabesma/idea-to-prd
```

Or place the `SKILL.md` file in your Claude skills directory (`~/.claude/skills/idea-to-prd/`).

## Triggering the skill

Say any of the following:

- `"I want to build [something]"`
- `"Write a PRD for [feature/product]"`
- `"Help me write a PRD"`
- `"I have an idea for an app"`
- `"We need a feature for X"`

**Does not trigger for:** architecture discussions, critiquing an existing PRD, implementation requests, or narrow technical questions.

## Language support

The skill itself is written in English, but **automatically adapts to the user's language** at runtime. Write in Indonesian and the entire conversation and PRD output will be in Indonesian. Language can switch mid-conversation and the skill will follow. Code-switching messages follow the dominant language; technical terms (API, SDK, P0) may stay in English regardless of conversation language.

## File structure

```
idea-to-prd/
├── SKILL.md                     # Skill instructions
├── references/
│   └── prd-templates.md         # Templates for all 9 PRD files (including 08-gtm.md)
└── evals/
    ├── evals.json               # 20 test cases (8 happy path + 12 adversarial)
    └── eval-results-2026-06-01.md
```
