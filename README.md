# idea-to-prd

A Claude Code skill that transforms any raw software idea into a complete, multi-file PRD through structured discovery questioning.

## What it does

Acts as a **Senior Product Manager** who asks the right questions first, achieves alignment, then generates a production-ready PRD split across 8 focused files — so engineering teams get exactly what they need without under- or over-engineering.

Specialized for **software engineering contexts**: web apps, APIs, mobile apps, SaaS platforms, CLIs, and internal tools.

## How it works

The skill follows 5 phases before and after writing a PRD:

| Phase | What happens |
|-------|-------------|
| **1 — Idea Intake** | Scans for already-answered context; asks only what's missing (max 2 questions) |
| **2 — Discovery** | Dimension-driven questioning — covers users, features, tech, metrics, competitive context, and validation in any order; adapts based on what's already known; detects product domain and auto-adds domain-specific questions |
| **3 — Alignment Check** | Challenges weak metrics and over-scoped MVPs before presenting a one-page summary; waits for explicit confirmation |
| **4 — PRD Generation** | Generates structured files scaled to scope — fewer for feature additions, all 8 for new products, more for complex products |
| **5 — Post-PRD Critical Path** | Presents a Before Engineering Kickoff checklist: riskiest assumptions, suggested review chain, and what changes if assumptions are wrong |

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

## Evals

17 test cases covering:

- **Happy path** (evals 1–8): vague input, rich context, feature addition, internal tool, two-sided marketplace, developer CLI, onboarding redesign
- **Adversarial — conversation dynamics** (evals 9–13): user refuses to answer questions, contradictory information across turns, mid-conversation language switch, disagreement with alignment summary, post-PRD revision from engineering feedback
- **Adversarial — output quality** (evals 14–17): vanity metric challenge, two-sided marketplace domain detection, post-PRD critical path output, scope/team/timeline mismatch

These evals measure **structural correctness and substantive quality** — whether the skill follows its phases, challenges weak assumptions, adapts to domain context, and produces output that survives engineering review. They do not measure latency or token cost.

Key behaviors validated over baseline:

- Skips Phase 1 questions when the user's initial message already answers them
- Never re-asks questions the user already answered
- Preserves the user's exact metric framing (does not reframe "60% drop-off" as "40% completion")
- Enforces alignment check before writing — baseline skips this
- Scales file count to scope — feature additions use 4–5 files, new products use all 8
- Caps questions at 3–4 per round — baseline fires 5+ at once
- Consistently includes acceptance criteria (Given/When/Then format), out-of-scope section, and FR/NFR distinction
- Adapts templates to context: removes WCAG for CLI tools, adapts timeline structure for feature additions
- Challenges vanity metrics before accepting them into the PRD
- Detects product domain (marketplace, AI-native, developer tool, regulated) and auto-adds domain-specific questions
- Flags scope/team/timeline mismatches explicitly instead of silently accepting an unshippable MVP
- Presents a Before Engineering Kickoff checklist after PRD generation

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

The skill itself is written in English, but **automatically adapts to the user's language** at runtime. Write in Indonesian and the entire conversation and PRD output will be in Indonesian. Language can switch mid-conversation and the skill will follow.

## File structure

```
idea-to-prd/
├── SKILL.md                     # Skill instructions
├── references/
│   └── prd-templates.md         # Templates for all 8 PRD files
└── evals/
    └── evals.json               # 17 test cases (8 happy path + 9 adversarial)
```
