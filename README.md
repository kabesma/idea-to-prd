# idea-to-prd

A Claude Code skill that transforms any raw software idea into a complete, multi-file PRD through structured discovery questioning.

## What it does

Acts as a **Senior Product Manager** who asks the right questions first, achieves alignment, then generates a production-ready PRD split across 8 focused files — so engineering teams get exactly what they need without under- or over-engineering.

Specialized for **software engineering contexts**: web apps, APIs, mobile apps, SaaS platforms, CLIs, and internal tools.

## How it works

The skill follows 4 phases before writing a single line of PRD:

| Phase | What happens |
|-------|-------------|
| **1 — Idea Intake** | 2 high-level questions: what problem, what success looks like |
| **2 — Discovery** | 2–4 rounds of 3–4 targeted questions covering users, features, tech, metrics, risks |
| **3 — Alignment Check** | Presents a one-page summary and asks for confirmation before writing |
| **4 — PRD Generation** | Generates 8 structured files only after alignment is confirmed |

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
└── 07-risks.md          # Risks, assumptions, dependencies, out of scope
```

## Benchmark

Evaluated across 8 software engineering scenarios (freelancer finance app, async standup SaaS, push notification feature, vague input, internal HR tool, two-sided marketplace, developer CLI tool, onboarding redesign):

| | Pass Rate |
|--|-----------|
| **With skill** | **97.5%** ± 7% |
| Without skill | 76% ± 22% |
| **Delta** | **+21%** |

Key wins over baseline:
- Enforces alignment check before writing — baseline skips this
- Always splits output into 8 files — baseline produces a monolith
- Caps questions at 3–4 per round — baseline fires 5+ at once
- Consistently includes acceptance criteria, out-of-scope section, and FR/NFR distinction

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

## Language support

The skill itself is written in English, but **automatically adapts to the user's language** at runtime. Write in Indonesian and the entire conversation and PRD output will be in Indonesian.

## File structure

```
idea-to-prd/
├── SKILL.md                     # Skill instructions
├── references/
│   └── prd-templates.md         # Templates for all 8 PRD files
└── evals/
    └── evals.json               # 8 benchmark test cases
```
