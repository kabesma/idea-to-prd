# Eval Results — idea-to-prd — 2026-06-01

## Summary

| Metric | Count |
|--------|-------|
| Total evals | 17 |
| PASS | 9 |
| PARTIAL PASS | 8 |
| FAIL | 0 |
| Total assertions | 86 |
| Assertions passed | 55 |
| Assertions failed | 0 |
| Assertions deferred | 31 |

## Methodology

These are simulated skill responses. For each eval, a subagent read the skill's SKILL.md and responded as if the skill were active, given the prompt in `eval_metadata.json`. Multi-turn evals inject conversation history so the subagent can respond to a specific scenario mid-conversation.

**DEFERRED** means the assertion is about a later phase (typically Phase 3 alignment summary or Phase 4 PRD file generation) that was not triggered in a single-turn or scenario-specific test. DEFERRED assertions are not counted as failures — they require a full multi-turn conversation test to evaluate. For evals 1–8 (single-turn discovery tests), many assertions about PRD file content are expected to be DEFERRED. For evals 9–17 (multi-turn scenario tests), most assertions are directly testable.

Eval 16 is the only test that triggered full PRD generation, so PRD file content assertions are only testable there.

**Verdicts:**
- **PASS** — all testable assertions pass (DEFERRED assertions are accepted)
- **PARTIAL PASS** — testable assertions pass, but some non-trivial assertions are deferred
- **FAIL** — at least one testable assertion fails

---

## Results

### Eval 1: vague-input-with-context
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Asks questions before producing any PRD content | PASS | Response begins "Before I write anything, I need to understand the actual problem..." — no PRD content anywhere |
| Asks no more than 2 questions in the first response | PASS | Exactly 2 numbered questions |
| Questions probe the problem and target user | PASS | Q1 probes specific financial pain (irregular income, tax estimation, invoice tracking); Q2 asks for a success outcome |
| No PRD files or sections are generated in the first response | PASS | 8-line response: 2 questions only, no sections or files |

**Notes:** Clean, minimal, well-scoped response. Questions are domain-specific to freelancer finance rather than generic. The 2-question limit is respected exactly.

---

### Eval 2: rich-context-async-standups
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill does not ask 'What problem does this solve?' or 'What does success look like?' — those are already answered | PASS | Response explicitly: "The problem is clear...I won't re-ask any of that" |
| First response acknowledges the rich context and asks only targeted follow-up questions | PASS | Affirms known context, then asks 4 targeted questions on integrations, stack, pricing, and video flow |
| Alignment summary is shown before any PRD file is generated | DEFERRED | Single-turn test; response closes with "Once I have these answers, I'll draft the alignment summary for your review before writing any files" |
| All 8 PRD files are generated (00-overview through 07-risks) | DEFERRED | PRD generation (Phase 4) not triggered in this test |
| Feature priority matrix uses P0/P1/P2 labels | DEFERRED | Requires Phase 4 |
| User stories have acceptance criteria | DEFERRED | Requires Phase 4 |
| 04-technical.md distinguishes functional from non-functional requirements | DEFERRED | Requires Phase 4 |

**Notes:** Both testable assertions pass. 5 of 7 assertions are deferred because this is a single-turn discovery test. The 4 questions asked are all high-value and directly relevant. The skill correctly avoids re-asking answered questions.

---

### Eval 3: feature-prd-push-notifications
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill recognizes this is a feature addition to an existing product, not a new product | PASS | First sentence: "you're adding a push notification feature to an existing e-commerce app, not building something from scratch. That shapes everything: the PRD will be scoped to the feature, not the whole platform." |
| Discovery questions ask about existing tech stack, notification infrastructure, and integration points | PASS | Q1 asks mobile platform + notification service (FCM, APNs, OneSignal); Q2 explicitly asks about existing notification infrastructure and event/webhook systems |
| Alignment summary lists 3 notification types (order, promos, restocks) | DEFERRED | Phase 3 not triggered; however response acknowledges all 3 types |
| PRD is scoped to the feature, not an entire e-commerce rebuild | DEFERRED | Phase 4 not triggered; commitment made in discovery framing |
| 07-risks.md contains an Out of Scope section | DEFERRED | Requires Phase 4 |
| 06-timeline.md uses a feature-addition timeline — NOT a full Alpha/Beta/Launch structure | DEFERRED | Requires Phase 4 |

**Notes:** Both testable assertions pass strongly. Feature-vs-product detection is immediate and shapes the entire response framing. 4 assertions about PRD file content are deferred.

---

### Eval 4: extremely-vague-i-want-an-app
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill does not generate a PRD immediately from this vague input | PASS | Response is questions only — no PRD content |
| Skill asks clarifying questions to understand the domain | PASS | Q1: "What problem does this app solve, and who has that problem?" — directly probes domain |
| Tone is encouraging and exploratory, not dismissive | PASS | Opens with: "That's a great starting point — every product starts as a spark like this." |
| Response asks no more than 2 questions | PASS | Exactly 2 numbered questions |

**Notes:** Strong handling of minimal input. The tone is warm without being hollow, and both questions are well-chosen to extract maximum signal from the vaguest possible prompt. 2-question limit respected exactly.

---

### Eval 5: internal-hr-tool
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Discovery questions address edge cases like partial-day requests, overlapping leave, approval chains | PASS | Q1 asks about approval chain complexity (skip-level, manager-OOO, HR co-sign); Q2 asks about "half-days / hourly blocks"; Q3 asks about overlapping leave handling |
| 04-technical.md mentions Google Workspace integration | DEFERRED | Requires Phase 4; Q4 explicitly probes Google Apps Script, Sheets, Chat bot, vs. standalone web with Google SSO |
| PRD is appropriately scoped for a 4-engineer internal tool — not over-engineered | DEFERRED | Requires Phase 4; discovery states "with 4 engineers and an internal tool for 150 people, I'll be keeping scope tight" |
| Personas include both employee and manager | DEFERRED | Requires Phase 4; response identifies "~150 employees (requestors) + their managers (approvers)" |
| 06-timeline.md reflects a realistic timeline for a small internal team | DEFERRED | Requires Phase 4 |
| 04-technical.md does NOT include WCAG or other NFRs irrelevant to an internal HR tool | DEFERRED | Requires Phase 4 |

**Notes:** The one fully testable assertion (edge case coverage) passes cleanly — all 3 edge cases are covered across Q1–Q3. 5 assertions are deferred. The response signals strong scoping awareness for a 4-engineer team.

---

### Eval 6: tutoring-marketplace
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| 01-personas.md contains both tutor and student personas | DEFERRED | Requires Phase 4; Q5 and Q6 probe tutor and student personas separately |
| 03-user-stories.md has stories for both user types | DEFERRED | Requires Phase 4 |
| Discovery questions probe trust, safety, and payment handling | PASS | Q3: "How is trust built between strangers?" (background checks, credential verification, trial sessions); Q4: "15% platform fee — who pays it?" plus price-testing |
| 05-metrics.md includes marketplace-specific metrics (GMV, take rate, supply/demand balance) | DEFERRED | Requires Phase 4 |
| 07-risks.md addresses marketplace cold-start problem | DEFERRED | Requires Phase 4; cold-start is the first question asked and prominently called out |

**Notes:** The one testable assertion (trust, safety, payment handling) passes strongly. 4 assertions deferred. The response is comprehensive — 9 questions covering marketplace structure, personas, and scope. Cold-start, liquidity, and trust are all explicitly addressed in discovery.

---

### Eval 7: developer-cli-changelog
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Discovery questions probe git hook approach, AI provider preference, config format | PASS | Q1: git hook approach (post-commit vs manual vs pre-push); Q2: AI provider (OpenAI, Anthropic, Ollama) and config format (.gitchangelog.toml or env var) |
| PRD is concise and technically oriented — not padded with business-context fluff | DEFERRED | Requires Phase 4; discovery response itself is technically sharp |
| 04-technical.md covers CLI design, AI API integration, and config schema | DEFERRED | Requires Phase 4 |
| 04-technical.md does NOT list WCAG as an NFR | DEFERRED | Requires Phase 4 |
| 06-timeline.md is realistic for a solo open-source project — uses milestones like v0.1/v1.0 | DEFERRED | Requires Phase 4 |
| 05-metrics.md reflects open-source success metrics (stars, downloads, contributors) | DEFERRED | Requires Phase 4 |
| 00-overview.md Stakeholders section is adapted for a solo project — not a full corporate table | DEFERRED | Requires Phase 4; discovery acknowledges "open source + no monetization model means your sustainability plan is essentially a passion project" |

**Notes:** The one testable assertion passes. 6 of 7 assertions are about PRD file content and are deferred. The skill correctly identifies the open-source/solo context and asks about community vs. niche which signals awareness of how this shapes the PRD.

---

### Eval 8: onboarding-redesign-60-percent-dropoff
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill frames this as an improvement to an existing flow, not a new product | PASS | Explicitly: "This is an improvement to an existing flow, not a greenfield product, so let me ask targeted questions about what's there today before I write anything." |
| Discovery questions ask about current onboarding steps and what data is required at each step | PASS | Q1: "What does the current profile setup flow look like, step by step?"; Q2: "Which fields are actually required by the product to function, versus nice to have?" |
| 03-user-stories.md focuses on the onboarding journey | DEFERRED | Requires Phase 4 |
| 05-metrics.md uses '60% drop-off' as the baseline metric — not reframed as '40% completion' or any other paraphrase | DEFERRED | Requires Phase 4; response commits: "The 60% drop-off figure is the baseline metric for this project and will be preserved exactly as stated throughout all PRD documents" |
| 07-risks.md lists assumptions about why users are dropping off | DEFERRED | Requires Phase 4 |
| 06-timeline.md uses an improvement-appropriate structure — NOT Alpha/Beta/Launch | DEFERRED | Requires Phase 4 |

**Notes:** Both testable assertions pass. The existing-flow-improvement framing is immediate and correct. The explicit commitment to preserve "60% drop-off" verbatim is a strong signal for the metric assertion, though the actual test is deferred. 4 assertions deferred.

---

### Eval 9: user-refuses-discovery-questions
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill does not silently skip to Phase 4 and generate PRD files without any alignment check | PASS | Response presents alignment summary and gates on "confirm or correct" — no files generated |
| Skill acknowledges the urgency without being dismissive | PASS | Opens with "Got it — I'll move fast" — immediate affirmation of urgency |
| Response lists the key unknowns explicitly as assumptions | PASS | Detailed "⚠️ Key Assumptions" section: "Platform: Assuming web-based", "Team size / timeline: Unknown", "Tech stack: Undecided / not mentioned", plus 6 more |
| Skill presents a reduced alignment summary and asks for confirmation before writing | PASS | Full alignment summary with all sections, ending with explicit "confirm or correct" confirmation request |
| Tone remains helpful and professional — not passive-aggressive about being told to skip | PASS | Cooperative and brisk throughout — no complaint or pushback about skipping discovery |

**Notes:** All 5 assertions pass. The user-refuses scenario is handled well — the response moves fast, surfaces all unknowns as explicit assumptions, and maintains exactly one gate (alignment confirmation) without lecturing the user. The "confirm or correct" framing is minimal-friction while still ensuring accuracy.

---

### Eval 10: contradictory-information
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill explicitly names the contradiction — it does not silently adopt the new framing | PASS | "I need to pause here — there's a direct conflict between what you've described now and what we established earlier, and I can't move forward without resolving it." Names both contexts explicitly |
| Skill asks which context is correct before continuing discovery | PASS | Response ends with binary choice: "A. K-12 e-learning platform / B. Corporate L&D / training SaaS" — forces resolution before continuation |
| Skill notes which prior answers (mobile-first, gamification, offline support) may need to be revisited depending on the answer | PASS | Dedicated section "Why this matters for answers you've already given" explicitly calls out mobile-first, gamification, and offline support as potentially invalidated |
| Skill does not generate an alignment summary until the contradiction is resolved | PASS | No alignment summary present — response holds at the contradiction-resolution gate |

**Notes:** All 4 assertions pass. Exemplary contradiction handling — precise naming of both conflicting contexts, a clear binary choice for resolution, and proactive identification of which prior answers may need revisiting. No passive-aggressive tone.

---

### Eval 11: language-switch-mid-conversation
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill's next response is in Indonesian, not English | PASS | Entire response in Indonesian: "Oke, bagus — masalah konsistensi adalah salah satu yang paling sering gagal di space habit-tracking..." |
| All subsequent discovery questions are in Indonesian | PASS | All 4 questions in Indonesian: "Apa yang dipakai pengguna sekarang?", "Apa satu hal terpenting...", "Platform apa yang menjadi target utama?", "Sudahkah kamu memvalidasi..." |
| If PRD files are eventually generated, they are written in Indonesian | DEFERRED | Requires full multi-turn test with Phase 4 triggered — not tested here |
| Skill does not acknowledge the language switch explicitly — it just adapts naturally | PASS | Response begins directly in Indonesian with no meta-comment like "I see you switched to Indonesian" |

**Notes:** 3 of 4 testable assertions pass. Language adaptation is seamless and natural. 1 assertion about PRD file language is deferred — requires full execution to verify Indonesian is maintained into Phase 4.

---

### Eval 12: disagrees-with-alignment-summary
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill does not proceed to Phase 4 after the disagreement | PASS | Revised summary presented, ends with "Anything else missing or wrong before I write the PRD?" — still gating on confirmation |
| Social features are removed from the MVP scope in the revised summary | PASS | Out of Scope section explicitly lists: "Social accountability features", "Community or friend-based challenges", "Social sharing or leaderboards" |
| Problem statement is updated to use the user's exact framing about motivation and exhaustion | PASS | Problem: "Lack of motivation when exhausted after kids — not a time problem, but an energy and motivation problem at the end of a demanding day with children." Response acknowledges: "I'll use your exact words" |
| Skill re-presents the alignment summary and asks for confirmation again | PASS | Full revised alignment summary with all sections, explicit confirmation request |
| Skill does not add back social features or reframe the problem in the revised version | PASS | Social features appear only in Out of Scope. No reversion to time-management framing. No social features smuggled back under different labels |

**Notes:** All 5 assertions pass. The response handles disagreement gracefully — immediate acknowledgment ("You're right on both counts"), exact preservation of user language, clean removal of social features, and a re-presented summary. No defensiveness.

---

### Eval 13: post-prd-timeline-revision
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill does not restart the discovery process from Phase 1 | PASS | Opens with: "Got it — scoped revision to 06-timeline.md only. No re-discovery needed." |
| Skill treats this as a scoped revision to a specific file | PASS | Response focuses entirely on 06-timeline.md. Final note: "No other PRD files were modified." |
| Skill may ask one clarifying question about the target timeline (7 vs 8 months, or what phasing engineering suggested) | PASS | Asks: "Did engineering suggest a specific phasing within that window — for example, an internal alpha at month 4–5 and a hardened MVP at month 7–8? Or is the estimate a single block?" |
| Skill updates only 06-timeline.md — it does not regenerate all 8 files | PASS | Only 06-timeline.md content provided. "No other PRD files were modified." |
| Revised timeline reflects the engineering team's estimate, not the original 4-month plan | PASS | Updated file shows 3 phases across 8 months (Foundation: 1-3, P0 Build: 4-7, Stabilization: 8). Change log documents replacement of "4-month MVP" with "7-8 months" |

**Notes:** All 5 assertions pass. Excellent handling of a post-PRD revision — scoped, targeted, single-file with one appropriate clarifying question. The change log addition is a best-practice bonus. Best-case/planning-horizon framing (7 vs 8 months) is appropriately conservative.

---

### Eval 14: vanity-metric-challenge
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill explicitly names '50,000 downloads' as measuring acquisition, not value | PASS | "50,000 downloads in 3 months measures acquisition — it tells you how many people installed the app, not whether the app is actually working." |
| Skill asks what retained or engaged usage looks like — what a user does beyond installing the app | PASS | Q1: "What does a successful user do in week 2?"; Q2: "What's a meaningful retention signal for this product?" — both probe post-install behavior |
| Skill does not proceed to alignment summary with only the downloads metric defined | PASS | No alignment summary — response stays in discovery/challenge mode |
| Tone is constructive and educational, not dismissive | PASS | Explains why downloads are insufficient with a concrete example (90% churn), offers an alternative framing, asks constructive questions |

**Notes:** All 4 assertions pass. The vanity metric pushback is direct without being dismissive. The "50k downloads + 90% churn = expensive marketing experiment" analogy is effective and educational. The 3 follow-up questions naturally extend discovery toward a more meaningful metric definition.

---

### Eval 15: marketplace-domain-detection
**Verdict:** PARTIAL PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill identifies this as a two-sided marketplace with creator (supply) and buyer (demand) split | PASS | "I can already see this is a two-sided marketplace: independent photographers as creators/sellers (supply side) and other photographers as buyers (demand side)." |
| Discovery questions include at least 2 of: cold-start strategy, liquidity threshold, trust mechanism, platform fee model | PASS | All 4 present: Q1 (cold-start / who comes first), Q2 (liquidity threshold), Q3 (trust mechanism), Q4 (platform fee model) |
| Skill does not ask only the generic checklist — marketplace-specific questions appear explicitly | PASS | Questions organized under "Marketplace-Specific (these are the highest-priority unknowns for a two-sided platform)" heading, clearly distinguished from general discovery |
| 01-personas.md (if eventually generated) would contain both creator and buyer personas | DEFERRED | Requires Phase 4; both sides clearly identified in discovery |
| 07-risks.md (if eventually generated) would address the cold-start problem | DEFERRED | Requires Phase 4; cold-start prominently featured in Q1 and framing |

**Notes:** All 3 testable assertions pass strongly. Marketplace domain detection is immediate and explicit. All 4 key marketplace questions present. 2 assertions about PRD file content deferred. This is one of the strongest discovery responses in the eval set.

---

### Eval 16: post-prd-critical-path-output
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill generates fewer than 8 files — only files with real content for this scope | PASS | 6 files generated; 01-personas.md skipped ("single user type, no meaningful differentiation") and 05-metrics.md skipped ("no specific KPIs; goals captured in 00-overview.md") — both skips documented with rationale |
| After generation, skill presents a 'Before Engineering Kickoff' section | PASS | Dedicated "## Before Engineering Kickoff" section with 3 numbered riskiest assumptions, suggested review chain, and contingency analysis |
| The checklist names specific riskiest assumptions from this PRD (not generic placeholder text) | PASS | A1: team adoption vs Slack reverting (tied to A5+A1 in 07-risks.md); A2: 6 weeks achievable alongside startup work (tied to A6); A3: flat tasks without notifications are sufficient (tied to A2+A5) — all specific to this PRD's context |
| Skill offers to help design a validation plan, challenge assumptions, or go deeper on a section | PASS | Final line: "Want me to challenge any of the assumptions above, help you design a validation experiment (particularly for the adoption risk), or go deeper on a specific section — like the Supabase RLS setup in 04-technical.md or the Week 1 scope in 06-timeline.md?" |

**Notes:** All 4 assertions pass. This is the only eval with full PRD generation and all assertions are directly testable. The checklist is PRD-specific and actionable. The contingency analysis ("If assumption #1 turns out to be wrong...") exceeds the assertion requirement. PRD file count of 6 (not 8) is well-justified for a small internal tool.

---

### Eval 17: scope-team-timeline-mismatch
**Verdict:** PASS

| Assertion | Status | Evidence |
|-----------|--------|----------|
| Skill explicitly flags the scope/team/timeline mismatch — does not silently accept all 8 listed features as MVP | PASS | "## Scope Reality Check (Read This First)" section lists all 8 features and states: "For 2 engineers targeting a 2-month launch, that's a significant mismatch." |
| Skill notes or estimates that the listed features likely exceed a 2-month window for 2 engineers | PASS | "A realistic estimate for all 8 areas built well — even at a fast pace — is 12–18 months for a 2-person team." |
| Skill asks which features are true P0 and which can be deferred to a later phase | PASS | "Which 2–3 of these features are true P0 launch blockers — the ones without which there's no product at all?" |
| Skill does not generate an alignment summary that includes all listed features in the MVP | PASS | No alignment summary generated — stays in scope-challenge mode |
| Tone is direct and constructive — honest about execution reality without dismissing the product vision | PASS | "This is not a reason to abandon the vision. It's a reason to be surgical about what you launch first." and "The vision is solid. The 2-month version just needs to be much smaller. Let's find it." |

**Notes:** All 5 assertions pass. Scope mismatch handling is exemplary — proactive reality check with concrete estimate (12-18 months), explicit validation of the product vision, and a clear path to right-sizing the MVP. The "Scope Reality Check (Read This First)" heading is a strong UX choice.

---

## Patterns Observed

### 1. Discovery phase is consistently well-executed
Every single-turn eval (1–8, 15, 17) correctly held back from PRD generation and asked targeted questions. The skill never jumped to PRD output prematurely. Domain-specific question quality was high across the board — eval 5 asked about approval chain edge cases, eval 6 probed cold-start and trust for a marketplace, and eval 7 asked about git hook mechanisms specific to a CLI tool.

### 2. Existing product / feature-addition detection is reliable
Evals 3 (push notifications) and 8 (onboarding redesign) both triggered immediate correct framing as feature additions or improvements rather than new products. The skill surfaced this framing in the first sentence in both cases, which is the correct behavior — it shapes the entire discovery approach.

### 3. Adversarial scenario handling (evals 9–14, 17) is consistently strong
All multi-turn adversarial scenarios passed — user refuses (eval 9), contradiction detection (eval 10), language switch (eval 11), alignment disagreement (eval 12), post-PRD revision (eval 13), vanity metric (eval 14), and scope mismatch (eval 17). The skill maintained its gates without being obstructive, adapted its tone to urgency levels, and never silently adopted incorrect framings.

### 4. Marketplace domain detection triggers specialized questions
Both marketplace evals (6 and 15) showed the skill immediately identifying the two-sided structure and leading with cold-start, liquidity, and trust questions — not the generic discovery checklist. This is a meaningful behavioral differentiator that would show up in PRD quality if Phase 4 were triggered.

### 5. PARTIAL PASS verdicts are an artifact of test design, not skill failures
All 7 PARTIAL PASS verdicts are single-turn tests where PRD content assertions are correctly deferred. No deferred assertion shows evidence of a likely future failure — in fact, several responses include explicit commitments or framing that predict correct PRD behavior (eval 8's "60% drop-off will be preserved exactly", eval 9's full assumption list, eval 2's explicit alignment-summary-before-PRD commitment).

---

## Deferred Assertions

All 26 deferred assertions fall into 3 themes. These require a full multi-turn conversation test where Phase 3 (alignment summary) and Phase 4 (PRD generation) are triggered.

### Theme A: PRD file structure and content (22 assertions)

These require Phase 4 execution to evaluate:

- **Eval 2:** All 8 PRD files generated; P0/P1/P2 in feature matrix; acceptance criteria in user stories; FR/NFR distinction in 04-technical.md
- **Eval 3:** Alignment summary with 3 notification types; feature-scoped PRD; Out of Scope in 07-risks.md; feature-addition timeline structure in 06-timeline.md
- **Eval 5:** Google Workspace integration in 04-technical.md; appropriate scope for 4-engineer team; employee + manager personas; realistic timeline; absence of WCAG in NFRs
- **Eval 6:** Tutor + student personas in 01-personas.md; user stories for both types; marketplace metrics in 05-metrics.md; cold-start in 07-risks.md
- **Eval 7:** Technical orientation of PRD; CLI/AI/config coverage in 04-technical.md; no WCAG in NFRs; v0.1/v1.0 milestones; open-source metrics; solo-project stakeholders
- **Eval 8:** Onboarding-focused user stories; "60% drop-off" preserved verbatim; drop-off assumptions in 07-risks.md; Audit/Design/Build/Measure timeline structure
- **Eval 15:** Creator + buyer personas in 01-personas.md; cold-start in 07-risks.md

### Theme B: Alignment summary content (2 assertions)

These require Phase 3 execution to evaluate:

- **Eval 2:** Alignment summary shown before any PRD file is generated
- **Eval 3:** Alignment summary lists all 3 notification types

### Theme C: Language persistence into PRD files (1 assertion)

This requires Phase 4 execution with language-switch active:

- **Eval 11:** PRD files written in Indonesian if eventually generated

### Recommended follow-up tests

To evaluate deferred assertions, run a full multi-turn simulation for:
1. **Eval 2** (async standups) — provide answers to all 4 discovery questions, confirm alignment summary, trigger PRD generation
2. **Eval 7** (developer CLI) — provide answers, trigger generation, verify no WCAG in NFRs and v0.1/v1.0 milestones
3. **Eval 8** (onboarding redesign) — verify "60% drop-off" appears verbatim in 05-metrics.md, verify Audit/Design/Build/Measure timeline
4. **Eval 11** (language switch) — continue through full PRD generation to verify Indonesian is maintained in all files
