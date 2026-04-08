# Flywheel Plugin — Implementation Strategy

**Type:** Strategy
**Status:** Draft
**Created:** 2026-04-05
**Origin:** plans/brainstorm-flywheel-plugin.md

---

## Strategic Intent

This is a product bet. The hypothesis: founders doing positioning and growth work with AI get generic output because the tools optimize for ease, not rigor. If we encode the friction of expert frameworks (Dunford, Lerner) into a structured tool, the output will be meaningfully better — and compounding knowledge stores will make each session faster without sacrificing specificity.

**What success looks like beyond "the plugin works":** Flywheel becomes the default way the author and at least 3 other founders run positioning and growth workflows. The compounding loop demonstrably reduces rework — decisions made in session 1 hold through session 5 without being relitigated.

**Why build a plugin instead of just doing the work directly?** The live case (Hundredweight) needs positioning work regardless. Building the tool *while* doing the work means the first real engagement validates the plugin simultaneously. If the tool doesn't improve the output vs. freeform Claude, kill it and keep the positioning canvas.

**Core hypothesis (falsifiable):** If we enforce Dunford's step sequence with redirect-warn-reveal enforcement, users who complete the full sequence will produce canvases that are measurably more specific than freeform positioning conversations with Claude. Test during Phase 1 dogfood: run the live case through both `/fw:position` and a freeform Claude conversation, compare specificity of outputs.

## Recommendation

Build Flywheel as a standalone Claude Code plugin with four skills (`/fw:position`, `/fw:copy`, `/fw:grow`, `/fw:compound`) that encode April Dunford's positioning framework and Matt Lerner's growth framework into compounding workflows. Start with `/fw:position`, dogfood it against a live case (likely Hundredweight), and only build the downstream skills once the positioning canvas reliably produces uncomfortably specific output.

The plugin should use firm-but-non-blocking enforcement: redirect users to the right step with framework reasoning, warn if they skip, but never hard-block. Three separate knowledge stores reflect the genuinely different schemas of positioning decisions, copy tests, and growth experiments.

## Current State (as of 2026-04-05)

- The `flywheel` repo is greenfield — only `plans/` exists
- Two installed plugins provide the structural template: Compound Knowledge (`~/.claude/plugins/cache/compound-knowledge-plugin/`) and Compound Engineering (`~/.claude/plugins/cache/every-marketplace/compound-engineering/`)
- A live positioning case exists for immediate dogfooding: Hundredweight freemium tier positioning (see `~/Documents/code/hundredweight/plans/brainstorm-freemium-and-data-expansion.md`)
- No prior knowledge base entries — the compounding loop hasn't started

## Architecture

### Plugin Structure

Fork the Compound Knowledge plugin structure. Follow Compound Engineering's skill compliance checklist.

```
flywheel/
  .claude-plugin/
    plugin.json              ← Plugin manifest (name, version, skills, agents)
  CLAUDE.md                  ← Shim pointing to AGENTS.md
  AGENTS.md                  ← Dev conventions + skill compliance rules
  skills/
    fw-position/
      SKILL.md               ← Dunford's 5-step positioning sequence
      references/
        positioning-canvas-template.md
        enforcement-prompts.md
    fw-copy/
      SKILL.md               ← Positioning → copy artifact translation
      references/
        artifact-templates.md
        drift-detector-rules.md
    fw-grow/
      SKILL.md               ← Lerner's behavior-change → experiment sequence
      references/
        experiment-card-template.md
    fw-compound/
      SKILL.md               ← Save learnings to the three stores
      references/
        frontmatter-schema.md
  agents/
    research/
      positioning-researcher.md    ← Searches docs/positioning/ for prior decisions
      copy-researcher.md           ← Searches docs/copy-tests/ for past performance
      growth-researcher.md         ← Searches docs/growth-experiments/ for past experiments
```

### Three Knowledge Stores

Each store has a different schema and lifecycle. Separate directories, not one store with typed frontmatter.

**`docs/positioning/`**
- `current.md` — The active positioning canvas. Read by `/fw:copy` and `/fw:grow` automatically.
- `archive/` — Previous versions, dated. Triggered when the user explicitly says "we're repositioning" or when competitive alternatives change fundamentally. Editing in place is the default; archiving is the exception.

**`docs/copy-tests/`**
- One file per copy attempt: `{artifact-type}-{slug}.md`
- Schema: artifact type, target reader, positioning claims used, draft, outcome notes (even qualitative)
- Lifecycle: accumulates. Old entries stay — they're the learning record.

**`docs/growth-experiments/`**
- One file per experiment: `{experiment-slug}.md`
- Schema: behavior, barrier, hypothesis, test design, success criteria, result, next bet
- Lifecycle: accumulates. Completed experiments get a `result:` field added.

**Shared frontmatter:**
```yaml
---
type: positioning-decision | copy-test | growth-experiment
tags: [icp, differentiation, landing-page, ...]
confidence: high | medium | low
created: 2026-04-05
source: [session description]
---
```

### Enforcement Model: Firm but Non-Blocking

Three levels of enforcement, applied consistently across all skills:

1. **Redirect with reasoning** (first attempt to skip) — "Dunford's framework starts with competitive alternatives because without them, differentiation claims have no anchor. Let's name the real alternatives first."

2. **Warn and flag** (second attempt to skip) — "Proceeding without competitive alternatives. Flagging this gap in the canvas — `/fw:copy` will note that differentiation claims aren't grounded." Add a `⚠️ skipped: competitive-alternatives` flag to the canvas.

3. **Let the output speak** (downstream consequence) — `/fw:copy` checks for skip flags and surfaces them: "This headline claims differentiation, but the positioning canvas skipped competitive alternatives. The claim may not land."

This avoids hard-blocking while making the cost of skipping visible. Founders who skip once and get generic output won't skip again.

**Specificity enforcement** works the same way:
- `/fw:position`: "Nothing like us on the market" gets redirected → "Name 3 specific things your customer would do instead. Include 'do nothing' if that's real."
- `/fw:grow`: "Increase signups" gets redirected → "That's a metric, not a behavior. What specific action would a person take? e.g., 'clicks Start free trial within 60 seconds of landing'"

## Proposed Approach

### Phase 1: `/fw:position` + Dogfood (build first, validate immediately)

**Estimated effort:** 2–4 days build + 1 day dogfood. Full-time.

**Build:**
- Plugin scaffolding (manifest, CLAUDE.md, AGENTS.md)
- `/fw:position` skill with full Dunford 5-step sequence
- Positioning canvas template with frontmatter schema
- Enforcement prompts (redirect text for each step)
- `docs/positioning/` directory only — no researcher agent yet, no other stores. Keep Phase 1 minimal to test the core hypothesis.

**Dogfood (hypothesis test):**
- Run `/fw:position` against Hundredweight freemium positioning
- Also run a freeform Claude conversation on the same positioning problem (no framework enforcement)
- Compare both outputs for specificity: number of named alternatives, segment precision, falsifiable differentiation claims
- Note what enforcement worked, what felt annoying, what gaps appeared

**Success gate:**
- The enforced canvas is measurably more specific than the freeform output (more named alternatives, narrower segments, claims tied to concrete attributes)
- Someone unfamiliar with Hundredweight could explain who it's for and why it wins, just from reading `current.md`
- If the enforced path is NOT more specific: revisit whether the enforcement model adds value, or whether the framework sequence alone (without enforcement) is sufficient

### Phase 2: `/fw:copy` + `/fw:compound` + Knowledge Stores (make the loop work)

**Estimated effort:** 3–5 days build + 1–2 days dogfood. Full-time.

**Build:**
- `/fw:copy` skill — reads `current.md`, asks for artifact type + reader, drafts with positioning logic visible
- Generic drift detector — mechanically: for each claim in the draft, check whether it traces back to a specific unique attribute or value statement in the canvas. Flag any claim that doesn't map. Implementation: the skill reads the canvas, extracts claims list, then audits each draft sentence against that list.
- `/fw:compound` skill — saves positioning decisions, copy attempts, and experiment results to the three stores. Uses overlap detection pattern from `ce:compound` to avoid duplicates.
- Split out `docs/copy-tests/` and `docs/growth-experiments/` stores (Phase 1 only had `docs/positioning/`)
- Positioning researcher agent + copy researcher agent (searches prior decisions and copy attempts)

**Dogfood:**
- Write a landing page or pitch from the Hundredweight positioning canvas
- Run `/fw:compound` to save the positioning decisions and copy attempt
- Run `/fw:position` again — verify that prior decisions surface before new ones are made

**Success gate:** `/fw:copy` produces a draft where every claim traces to the canvas. The drift detector catches at least one generic insertion. `/fw:compound` saves a positioning decision that surfaces in a subsequent `/fw:position` session.

### Phase 3: `/fw:grow` (complete the loop)

**Estimated effort:** 2–3 days build + 1 day dogfood. Full-time.

**Build:**
- `/fw:grow` skill — Lerner's full sequence: behavior → barrier → hypothesis → experiment → success criteria
- Growth researcher agent (searches `docs/growth-experiments/`)
- Experiment card template

**Dogfood:**
- Design a growth experiment for Hundredweight
- Run `/fw:compound` to save it
- Hand the experiment card to someone uninvolved and ask: "Could you run this?" If they need clarification, the card failed.

**Success gate:** The experiment card names a specific behavior (not a metric), a specific barrier, and a test that could run in under a week. A non-author can understand and execute it without follow-up questions.

### Phase 4: Polish + Publish

**Estimated effort:** 1–2 days. Full-time.

- README and install instructions
- Pipeline mode for all skills (skip prompts, use defaults, structured output)
- Edge case handling: what if no positioning canvas exists when `/fw:copy` is run? (Redirect to `/fw:position` with explanation)
- Archive workflow: explicit "reposition" trigger vs. edit-in-place default
- Distribution: revisit whether plugin marketplace is the right channel based on dogfood learnings. May be direct install or GitHub-only initially.

### Phase 5 (Future): `/fw:review` — Cross-Store Consistency

**Rationale:** Each skill already has review logic built into its enforcement (redirect → warn → flag). But no single skill can catch *cross-store* inconsistencies — where positioning, copy, and growth diverge over time.

**What `/fw:review` would check:**
- **Positioning ↔ Copy alignment** — "Your canvas says the ICP is early-stage SaaS founders, but your last three copy tests targeted enterprise marketing teams."
- **Positioning ↔ Growth alignment** — "Your growth experiments target a behavior that doesn't map to any value claim in the canvas."
- **Copy ↔ Growth alignment** — "Your best-performing copy angle emphasizes speed, but your growth experiments are testing trust-building interventions."
- **Staleness detection** — "The positioning canvas hasn't been updated in 3 months but 6 copy tests have been run since. Are the positioning decisions still current?"

**Design principle:** This is a compounding-level insight tool, not a quality gate. It surfaces drift between stores that accumulates silently over multiple sessions. Only useful once all three stores have meaningful content — not before Phase 3 is complete.

**Build when:** After multiple real sessions have populated all three stores and cross-store drift has had time to emerge.

## Design Decisions Log

| Decision | Choice | Reasoning |
|----------|--------|-----------|
| Namespace | `fw:` (renamed from `mk:` in brainstorm) | Matches `kw:`, `ce:` convention. "Flywheel" is the product name. `mk:` could collide with "make" conventions. |
| Knowledge stores | 3 separate directories | Different schemas, different lifecycles. One store with typed frontmatter would fight the data shape. |
| Enforcement | Firm but non-blocking | Founders are self-directed. Redirect with reasoning, warn on skip, let downstream output reveal the cost. |
| Build order | position → copy+compound → grow → polish | Position is load-bearing. Copy+compound prove the loop. Grow extends it. |
| Canvas versioning | Edit in place by default, archive on explicit reposition | Most changes are refinements, not pivots. Archiving every edit creates noise. |
| Drift detector | Claim-to-canvas tracing | Each draft claim must map to a specific canvas attribute or value. Ungrounded claims get flagged. |
| Plugin relationship | Standalone, not an extension of Compound Knowledge | Different artifact, schema, user context. Can coexist. |

## Open Questions

- **[Phase 1]** How much inline framework reasoning per step? Enough for a founder to understand *why* this step matters, but not so much it reads like a textbook. Calibrate during dogfood.
- **[Phase 2]** Should `/fw:copy` support custom artifact types beyond the five listed, or is the fixed list part of the enforcement?
- **[Phase 2]** How does `/fw:compound` handle disagreements with past decisions? (e.g., "we said X last month but now I think Y") — probably surface the prior decision and ask explicitly whether to update or archive.
- **[Phase 5]** Should the plugin auto-detect when `current.md` is stale relative to recent copy tests or growth experiments? (Now addressed by `/fw:review` staleness detection.)

## Success Metrics

| Metric | Current Baseline | Target | How to Measure | Phase |
|--------|-----------------|--------|----------------|-------|
| Enforcement value | N/A | Enforced canvas is more specific than freeform on same problem | A/B comparison: run Hundredweight through `/fw:position` AND freeform Claude. Count named alternatives, segment specificity, falsifiable claims in each. | 1 |
| Positioning canvas specificity | N/A | ≥3 named real alternatives, ≥2 specific customer segments, all differentiation claims tied to concrete attributes | Checklist review of `docs/positioning/current.md` against these three criteria. Pass = all three met. | 1 |
| Copy grounding rate | N/A | 100% of claims trace to canvas (0 ungrounded flags) | Drift detector output — automated. | 2 |
| Experiment runnability | N/A | A non-author can execute the experiment card without follow-up questions | Hand the card to one person. If they ask clarifying questions, it failed. | 3 |
| Compounding signal | N/A | Researcher agent returns a prior decision that the user did not explicitly remember | Observe during session 2+: did the surfaced decision change or confirm the user's approach? | 2 |
| External adoption | 0 users | ≥3 founders outside the author's network using Flywheel | Track installs or direct outreach. Revisit after Phase 4. | 4+ |

## References

- Origin brainstorm: `plans/brainstorm-flywheel-plugin.md`
- Architectural template: Compound Knowledge plugin (`kw:` skills, `docs/knowledge/` store, same loop philosophy)
- Skill compliance: Compound Engineering AGENTS.md (frontmatter, AskUserQuestion, TaskCreate conventions)
- Compounding pattern: `ce:compound` skill (parallel research > assembly > overlap detection)
- Likely dogfood case: Hundredweight freemium positioning (`/Users/wonderchook/Documents/code/hundredweight/plans/brainstorm-freemium-and-data-expansion.md`)
- Real marketing output example: Obscure Audio marketing strategy (`/Users/wonderchook/Documents/code/obscure-audio/research/10_marketing-strategy.md`)

## Execution Log

### 2026-04-05 — Phase 1, Batch 1: Plugin Scaffolding + Reference Files
- Plugin manifest ✅ — `.claude-plugin/plugin.json` (v0.1.0)
- CLAUDE.md ✅ — Shim pointing to AGENTS.md
- AGENTS.md ✅ — Dev conventions, knowledge store schemas, enforcement model, design principles
- Positioning canvas template ✅ — `skills/fw-position/references/positioning-canvas-template.md` (Dunford's 5 components, frontmatter schema, field notes)
- Enforcement prompts ✅ — `skills/fw-position/references/enforcement-prompts.md` (3 enforcement levels, all 5 steps + sequence enforcement)

### 2026-04-05 — Phase 1, Batch 2: Skill + Knowledge Store
- `/fw:position` SKILL.md ✅ — `skills/fw-position/SKILL.md` (full 5-step sequence, enforcement hooks, existing canvas detection, pipeline mode)
- `docs/positioning/` ✅ — Directory created with `archive/` subdirectory and `.gitkeep` files
- Notes: Phase 1 build complete. Ready for dogfood against Hundredweight.
